---
title: Chroma Graphics
date: 2024-02-08 13:00
categories: [Software Development, Broadcast Graphics]
tags: [opengl, golang, chroma viz]     # TAG names should always be lowercase
math: true
comments: false
---

### **Introduction**

The aim of this project is to develop a collection of applications which can render custom graphics.
Inspiration is taken from the VizRT suite of applications.
Currently this collections consists of Chroma Viz, Hub, Engine and Artist.
Chroma Viz, Hub and Artist are built in Golang and are contained in the [Chroma Viz](https://github.com/jchilds0/chroma-viz) repo on github.
They share a common base library with a separate package for each application and a single main file to launch any of the applications.
Chroma Engine is built in C and is contained in the [Chroma Engine](https://github.com/jchilds0/chroma-engine) repo.

<video width="720" controls>
    <source src="https://github.com/jchilds0/chroma-viz/raw/main/data/demo.mp4">
</video>

### **Chroma Viz**

Chroma Viz is the front end for Chroma Engine.
It provides a UI to view the templates contained in Chroma Hub.
On startup, Chroma Viz requests the templates from Chroma Hub over a tcp socket.
Chroma Hub collects the template IDs of all templates in the hub and sends this list to Chroma Viz.

<img src="/assets/chroma-graphics/templates.png" alt="Templates">

Pages can be created from templates, by double clicking on the template in the Templates tab.
Pages are independent of each other, while partially compatible with future updated templates.
To create a page, Chroma Viz requests the template from Chroma Hub using tcp sockets.
For example, if we wanted template 10, we would write

$$ \texttt{ver 0 1 temp 10;} $$

to the Chroma Hub socket.
Templates are encoded using a json-like format, described in the Chroma Hub section.
Pages form shows, which can be imported or exported to disk.
Internally we use the `encoding/json` Golang package for simplicity to read and write a
json format of the pages or shows to a file.

<img src="/assets/chroma-graphics/show.png" alt="Templates">

Chroma Viz can connect to any number of Chroma Engine instances over a tcp socket, with
the connection having either Engine or Preview type.
When the user opens a page to edit by double clicking on the page, or by saving changes
made to the page with the save button, the page is sent to all connections with the preview type.
By default Chroma Viz starts with a Chroma Engine instance as a preview window using the Preview type.
The actions at the top of the editor panel, $ \texttt{Take On, Continue} $ and
$ \texttt{Take Off} $, send pages to connected Chroma Engine instances with the Engine type.

- Take On runs the keyframes until the first pause point
- Continue runs keyframes from the last pause point to the next pause point.
- Take Off runs keyframes from the final pause point until the end.

Chroma Viz encodes the attributes changed by the user into a string and sends it to Chroma Engine.
Chroma Engine parses this string and combines the data with the template from the graphics
hub to display the graphic.

<img src="/assets/chroma-graphics/chroma-viz.png" alt="Chroma Viz">

### **Chroma Engine**

Chroma Engine renders graphics requests from Chroma Viz.
Chroma Engine has two modes: engine and preview.
In engine mode, Chroma Engine launches a standalone gtk window to render graphics.
This is a placeholder for what would be a process that communicates with a graphics card to output graphics.
In preview mode, Chroma Engine recieves an xorg window id and uses gtk plugs to
embed a window with Chroma Viz while still running as a standalone instance.
This allows the operator to view graphics in a preview window within Chroma Viz.

On startup, Chroma Engine connects to Chroma Hub and requests all templates in the Hub.
This is done so Chroma Engine can build its own database containing each template that could be received from Chroma Viz.
This has the added cost of needing to allocate resources for each template, but the benefit
is we don't need to allocate memory at run time when we receive a graphics request.
A middle ground between these two options would be allowing the user to load a subset of
templates currently in use, and requesting any new templates on the fly from Chroma Hub as needed.

Chroma Engine renders graphics using OpenGL.
To render a graphic, first Chroma Engine recieves a string of data from a Chroma Viz instance.
A simple name-attribute format `name=attr#` is sufficient for our purposes.
The string contains a header with the format version, layer, template id, and action.
Then each geometry, specified by an integer, followed by a list of attributes for the geometry.
As we parse the string, we set the values for each geometry of the target template.

Image assets are also contained in Chroma Hub, so before we can render an image we request it from Chroma Hub.
Chroma Hub first send 4 bytes with the length of the image, followed by the image as a raw PNG file.
Then we store this data for later use, as well as decoding the png to extract the pixel data using libpng.
In later render calls, if the image id matches the currently stored image id, we reuse
this file instead of requesting the image again from Chroma Hub.

After receiving the graphics request and any image assets, Chroma Engine calculates the absolute
position of each geometry in the page using the parent tree and relative positions.
Next the animations are calculated.
Currently this is a simple black rectangle which is the same size as the background
rectangle and is resized to create the animation effect.
For smooth animations, we use a bezier curve to control the animation timing.
Finally each geometry in the page is rendered to the screen using OpenGL.

<img src="/assets/chroma-graphics/chroma-engine.png" alt="Chroma Engine">

### **Chroma Hub**

The purpose of Chroma Hub is to synchronize the graphic templates used by Chroma Viz and Chroma Engine instances.
Chroma Hub also stores any assets needed by the templates such as images, currently only in png format.
Chroma Hub wraps a SQL database, which currently needs to be setup with the schema in `hub/chroma_hub.sql`.
Internally we use the `encoding/json` Golang package for simplicity to write and read a json format of the database to a file.

Chroma Hub communicates with Chroma Engine and Chroma Viz instances over tcp socket connections.
Chroma Artist uses Chroma Hub directly to updates templates in the current hub.
Chroma Hub listens to port 9000 by default (or as specified) for connections and then responds to a command as needed.
For example

$$ \texttt{ver 0 1 tempid 5;} $$

is a command using version 0.1 and requesting template 5.
Chroma Viz and Chroma Engine can set the Chroma Hub address individually and connect on startup, reading and parsing the data sent by Chroma Hub.
Chroma Hub encodes the templates using a json-like format, which is restricted to simplify implementation on the Chroma Engine/Chroma Viz side.
The format is described by the following Context Free Grammar (see Quaternion Calculator for a description of CFGs).

$$ \begin{align*}
S &\to \{ \texttt{N, 'templates': [$T$]} \} \\
T &\to \{ \texttt{N, 'geometry': [$G$]} \} \mid T, T \\
G &\to \{ \texttt{N, 'attr': [$A$]} \} \mid G, G \\
A &\to \{ \texttt{N} \} \mid A, A \\
N &\to \texttt{'string1'}: \texttt{'string2'} \mid \texttt{'string1'}: \texttt{num} \mid N, N
\end{align*}$$

where $ \texttt{string1} $ and $ \texttt{string2} $ are strings and $ \texttt{num} $ is an integer or float.
The non-terminals $ T, G, A $ represent a templates, geometries, and attributes respectively.
The list of attributes for each non terminal is generated by the non terminal $ N $.
Both Chroma Viz and Chroma Engine contain custom parsers for this grammar.

On the Chroma Engine/Viz side we begin by tokenizing the string recieved.
We have strings which begin with an ', integers and the special characters {, }, [, ], : and ,.
While the grammar specified above is left-recursive and ambiguous, it is relatively simple to parse.
Consider the following example production, which has the same form as $ T, G, A $ as above,

$$ A \to \beta \mid A, A $$

To eliminate left recursion and the amibiguity of this production, we replace this production with

$$ A \to \beta, A \mid \beta $$

This new production is unambiguous and not left recursive.
For simplicity in specifying the grammar we use the former.
Now the grammar is unambiguous and not left-recursive, we can use a type of recursive-descent parsing known as predictive parsing.
In Chroma Engine, this parser is contained in `/src/parser/parser_recieve_hub.c`, in Chroma Viz it is contained in `/viz/parser.go`.

Chroma Hub also contains a simple CLI interface for importing and exporting assets, archive and templates.

### **Chroma Artist**

Chroma Artist provides a front end to design and export templates which can be imported to Chroma Hub.
The key difference between Chroma Viz and Chroma Artist is in Chroma Artist we are free to manipulate the geometry hierarchy of a template, and any attribute of a geometry.
In the discussion of Chroma Engine, we omitted the discussion of relative coordinates.
To enable easier manipulation of graphics, each geometry has a parent geometry.
This gives the geometries a tree structure, and position of a geometry are relative to the position of the parent geometry.
Chroma Artist gives an easy interface to specify this tree structure, which Chroma Engine rebuilds to calculate the absolute positions.

Chroma Artist shows all attributes of a geometry to the designer.
The designer is then free to set these values.
They can also set which attributes will be visible when the template is imported into Chroma Viz.
By default all values set in Chroma Artist are stored with the template.
Once loaded into Chroma Hub, these values will be sent to Chroma Engine and stored as the defaults, as well as shown by default in Chroma Viz.

An example of this functionality is a simple lower frame super, which contains a rectangle for the background, two text geometries parented to the rectangle, and a circle as a logo placeholder also parented to the rectangle.
The designer could set the default position, width and height of the background rectangle, aswell as the position of the text.
Since the text geometries and circle are parented to the rectangle, to move the graphic we only need to change the rectangle position.
In Chroma Artist, the following image shows an example of this graphic.

![keyframe](/assets/chroma-graphics/keyframe_artist.png)

Currently the rectangle is static and the width of the rectangle needs to be updated when the text changes.
Keyframing allows us to animate the graphic and have the width of the rectangle be linked to the text width.
The keyframing system is based on a directed acyclic graph.
We begin with the simplest case of no keyframes which is used to calculate the absolute positions from relative position.
This will be extended to construct keyframes.

Consider the following table which represents some attributes of the graphic we described above,

![keyframe](/assets/chroma-graphics/keyframe_img.svg){: width="700"}

The x position of geometry 4 depends on the x position of geometry 1 (it's parent) and its own relative x position.
We indicate this dependency with an arrow from the x position of geometry 4 to the x position of geometry 1 and the relative x position of geometry 4.
Continuing for all geometries we form the following graph, which is a directed acyclic graph.

![keyframe](/assets/chroma-graphics/keyframe_start.svg){: width="700"}

At each node of this graph, we want to compute the value of the node by combining the values of the dependencies in some way.
To do this we store a function at each node, in the case of relative positions this function evaluates the sum of the value for each child node of the current node.
But we need to evaluate each node only once each child node has been evaluated.
This problem is known as topological sorting.
This excellent video by William Fiset describes topological sorting of directed acyclic graphs ([Topological Sort](https://youtu.be/eL-KzMXSXXI?si=mG9_kixJYgjSUAU_)).

We can make the rectangle width dynamic by adding the following dependencies, and adding a function to the rectangle node which evaluates the maximum of the value of each child node.

![keyframe](/assets/chroma-graphics/keyframe_expand.svg){: width="700"}

Keyframing consists of a set of frames an index 1, 2, ... up to some fixed number $ n $.
For each index, we create the table of attributes for each geometry show above.
Then a keyframe is simply a way to add dependencies and evaluation functions to the graph.
When animated, the values are interpolated linearly between the frames.
Current types of keyframes are

- Set Frame: Set the value of an attribute of a geometry in a specific keyframe. In the graph this updates the value of a node and doesn't add any dependencies.
- User Frame: Similar to set frame, except the value from the template or page when the graphic is animated on is used. This adds an edge which points to the attribute values set by the user, and is the default for non keyframed attributes.
- Bind Frame: Use a value computed in a keyframe. This adds an edge to another node in the graph, and the current node simply takes the value of the single child node.

The only restrictions on keyframes is they cannot create cycles in the graph.
Doing so makes evaluating them ambiguous, so Chroma Engine terminates if it receives a template with a cycle in the keyframe graph.

<img src="/assets/chroma-graphics/chroma-artist.png" alt="Chroma Artist">
