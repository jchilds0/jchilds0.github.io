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
Currently this collections consists of [Chroma Viz](https://github.com/jchilds0/chroma-viz), [Chroma Engine](https://github.com/jchilds0/chroma-engine), [Chroma Hub](https://github.com/jchilds0/chroma-viz), and [Chroma Artist](https://github.com/jchilds0/chroma-viz), with the source code for each available on GitHub.

<video width="720" controls>
    <source src="/assets/chroma-graphics/demo.mp4">
</video>

### **Chroma Viz**

Chroma Viz is the front end for Chroma Engine.
It provides a UI to view the templates contained in Chroma Hub.
On startup, Chroma Viz requests the templates from Chroma Hub over a tcp socket.
Chroma Hub collects the template IDs of all templates in the hub and sends an array of the template IDs to Chroma Viz.

<img src="/assets/chroma-graphics/templates.png" alt="Templates">

Pages can then be created from templates, which expose a number of attributes that can be changed using the editor page.
To create a page, Chroma Viz requests the template from Chroma Hub using the template ID.
Templates are encoded using a json-like format, specified below.
Pages form shows, which can be imported or exported to a text file.
Internally we use the `encoding/json` Golang package for simplicity to write and read a json format of the pages or shows to a file.

<img src="/assets/chroma-graphics/show.png" alt="Templates">

Chroma Viz can connect to any number of Chroma Engine instances over a tcp socket, with the connection having either Engine or Preview type.
When the user opens a page to edit by double clicking on the page, or by saving changes made to the page with the save button, the page is sent to all connections with the preview type.
By default Chroma Viz starts with a Chroma Engine instance as a preview window using the Preview type.
The actions at the top of the editor panel, $ \texttt{Take On, Continue} $ and $ \texttt{Take Off} $, send pages to connected Chroma Engine instances with the Engine type.

- Take On animates a page onto the screen using the animation specified or no animation.
- Continue is used for page update operations such as updating the time on a clock geometry.
- Take Off animates a page off, usually in the reverse of the take on animation.

Chroma Viz encodes the attributes changed by the user into a string and sends it to Chroma Engine.
Chroma Engine parses this string and combines the data with the template from the graphics hub to display the graphic.

<img src="/assets/chroma-graphics/chroma-viz.png" alt="Chroma Viz">

### **Chroma Engine**

Chroma Engine renders graphics requests from Chroma Viz.
Chroma Engine has two modes: engine and preview.
In engine mode, Chroma Engine launches a standalone gtk window to render graphics.
This is a placeholder for what would be a process that communicates with a graphics card to output graphics.
In preview mode, Chroma Engine recieves an xorg window id and uses gtk plugs to embed a window with Chroma Viz while still running as a standalone instance.
This allows the operator to view graphics in a preview window within Chroma Viz.

On startup, Chroma Engine connects to the Chroma Hub specified and requests all templates in the Hub.
This is done so Chroma Engine can build its own database containing each template that could be received from Chroma Viz.
This has the added cost of needing to allocate resources for each template, but the benefit is we don't need to allocate memory at run time when we receive a graphics request.
A middle ground between these two options would be allowing the user to load a subset of templates currently in use, and requesting any new templates on the fly from Chroma Hub as needed.

Chroma Engine renders graphics using OpenGL.
To render a graphic, first Chroma Engine recieves a string of data from a Chroma Viz instance.
A simple name-attribute format `name=attr#` is sufficient for our purposes.
The string contains a header with the format version, layer, template id, and action.
Then each geometry, specified by an integer, followed by a list of attributes for the geometry.
As we parse the string, we set the values for each geometry of the target template.

Image assets are also contained in Chroma Hub, so before we can render an image we request it from Chroma Hub.
Chroma Hub first send 4 bytes with the length of the image, followed by the image as a raw PNG file.
Then we store this data for later use, as well as decoding the png to extract the pixel data using libpng.
In later render calls, if the image id matches the currently stored image id, we reuse this file instead of requesting the image again from Chroma Hub.

<img src="/assets/chroma-graphics/chroma-engine.png" alt="Chroma Engine">

### **Chroma Hub**

The purpose of Chroma Hub is to synchronize the graphic templates used by Chroma Viz and Chroma Engine instances.
Chroma Hub also stores any assets needed by the templates such as images, currently only in png format.
It also provides a single point to update or add a template.
Chroma Hub is implemented in Golang and contains a database of templates and their geometries.
Internally we use the `encoding/json` Golang package for simplicity to write and read a json format of the database to a file.
Chroma Hub communicates with Chroma Engine and Chroma Viz instances over tcp socket connections.
Chroma Hub listens to port 9000 by default (or as specified) for connections and then responds to a command as needed.
For example

$$ \texttt{ver 0 1 tempid 5;} $$

is a command using version 0.1 and requesting template 5.
Chroma Viz and Chroma Engine can set the Chroma Hub address individually and connect on startup, reading and parsing the data sent by Chroma Hub.

Chroma Hub encodes the templates using a json-like format, which is restricted to simplify implementation on the Chroma Engine/Chroma Viz side.
The format is described by the following Context Free Grammar (see Quaternion Calculator for a description of CFGs).

$$ \begin{align}
S &\to \{ \texttt{N, 'templates': [$T$]} \} \\
T &\to \{ \texttt{N, 'geometry': [$G$]} \} \mid T, T \\
G &\to \{ \texttt{N, 'attr': [$A$]} \} \mid G, G \\
A &\to \{ \texttt{N} \} \mid A, A \\
N &\to \texttt{'string1'}: \texttt{'string2'} \mid \texttt{'string1'}: \texttt{num} \mid N, N
\end{align}$$

where $ \texttt{string1} $ and $ \texttt{string2} $ are strings and $ \texttt{num} $ is an integer or float.
The non-terminals $ T, G, A $ represent a templates, geometries, and attributes respectively.
The list of attributes for each non terminal is generated by the non terminal $ N $.
Both Chroma Viz and Chroma Engine contain custom parsers for this grammar.

On the Chroma Engine/Viz side we begin by tokenizing the string recieved.
We have strings which begin with an ', integers and the special characters {, }, [, ], : and ,.
While the grammar specified above is left-recursive and ambiguous, it is relatively simple to parse.
Consider the following example production, which has the same form as $ T, G, A $ as above,

$$ A \to \beta \mid A, A $$.

To eliminate left recursion and the amibiguity of this production, we replace this production with

$$ A \to \beta, A \mid \beta $$.

This new production is unambiguous and not left recursive.
For simplicity in specifying the grammar we use the former.
Now the grammar is unambiguous and not left-recursive, we can use a type of recursive-descent parsing known as predictive parsing.
In Chroma Engine, this parser is contained in `/src/parser/parser_recieve_hub.c`, in Chroma Viz it is contained in `/viz/parser.go`.

Chroma Hub also contains a simple CLI interface for importing and exporting assets, archive and templates.

### **Chroma Artist**

Chroma Artist provides a front end to design and export templates which can be imported to Chroma Hub.
The key difference between Chroma Viz and Chroma Artist is in Chroma Artist we are free to manipulate the geometry heirachy of a page, and any attribute of a geometry.
In the discussion of Chroma Engine, we omitted the discussion of relative coordinates.
To enable easier manipulation of graphics, each geometry has a parent geometry.
This gives the geometries a tree structure, and coordinates of a geometry are relative to the position of the parent geometry.
Chroma Artist gives an easy interface to specify this tree structure, which Chroma Engine rebuilds to calculate the absolute positions.

Chroma Artist shows all attributes of a geometry to the designer.
The designer is then free to set these values.
They can also set which attributes will be visible when the template is imported into Chroma Viz.
By default all values set in Chroma Artist are stored with the template.
Once loaded into Chroma Hub, these values will be sent to Chroma Engine and stored as the defaults, aswell as shown by default in Chroma Viz.

An example of this functionality is a simple lower frame super, which contains say a rectangle for the background, and two text geometries parented to the rectangle.
The designer could set the default position, width and height of the background rectangle, aswell as the position of the text.
The position of the text does not need to be changed since it is parented to the rectangle, so these can be hidden, with the text left visible for the user to update in Chroma Viz.
The color, rounding and height of the rectangle could also be hidden, with the width remaining visible to accommodate longer text entries.

<img src="/assets/chroma-graphics/chroma-artist.png" alt="Chroma Artist">
