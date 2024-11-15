---
title: Chalkboard
date: 2024-10-01 00:00
categories: [Software Developement, Distributed Systems]
tags: [distributed systems, peer to peer, golang]     # TAG names should always be lowercase
math: true
comments: false
---

### **Introduction**

Chalkboard is a peer-to-peer, distributed whiteboard.
Users can create and discover rooms, each with their own whiteboard.

![Chalkboard](/assets/chalkboard/example.png)

Source is available at [Chalkboard](https://github.com/jchilds0/chalkboard).

### **Implementation**

The core communication stack is built on [libp2p](https://libp2p.io).
The clients use [mDNS](https://docs.libp2p.io/concepts/discovery-routing/mdns/) to discover other clients on the network without configuration from the user.
mDNS uses IP multicast to discover other clients on the local network, which removes the need for a central directory service to store clients, or the user specifying other clients.

For communication we use a combination of tcp sockets and libp2p [pubsub](https://docs.libp2p.io/concepts/pubsub/overview/).
Each line is represented using the following struct,

```go
type Point struct {
    X float64
    Y float64
}

type Line struct {
    Index  int
    Pencil Pencil
    Points []Point
}
```

where `Pencil` contains information about the line style.
As the user draws the line, we update the `Points` array and redraw the canvas containing all lines.
To synchronize the lines between the client drawing the line and all other clients we make use of pubsub.

A Publisher/Subscriber (pubsub) system consists of clients, also known as peers, and a collection of topics.
Pubsub is a form of indirect communication in distributed systems.
Publishers can publish messages to a given topic, while subscribers can subscribe to a topic, indicating they wish to receive messages for the topic.
This removes the requirement for publishers and subscribers to know each other, instead communicating through topics.
In our case, we create a topic for each room with the format `<host_name>-<room_name>` to reduce room name clashes.
When a user joins a room, they are subscribed to the relevant topic.
The messages published to a topic are simply the `Line` struct given above in `json` format, as the peer draws the line.

This reduces the complexity of managing the clients in a room, since pubsub handles passing messages from a publisher out to all subscribers.
The caveat is pubsub is time coupled, peers only receive a message if they are subscribed when the message is published.
Additionally, each client must know the rooms made by other clients since pubsub does not include any topic discovery mechanism.
A client could be listening to all rooms at all times but they would still miss messages created before the client program is started.
To solve this issue, we create a mini server service on each peer for serving rooms.

We have a special topic `/client` which active clients periodically publish their name, a list of rooms, ip address and port.
If a client wants to join a room, they first send a request to the IP Address and Port of the room host, requesting the room.

```go
type Request struct {
    Type int
    Name string
}
```

The peer responds with a canvas containing all lines in the room.

```go
type Canvas struct {
    OwnerName string
    RoomName  string
    Lines     map[string]Line
}
```

Then the client subscribes to the room topic to receive any future drawing.
This reduces the time coupling problem to each client maintaining the state of each room they create.
