# Vertex Buffers

## What we have

Right now, we're creating a VBO, assigning it a layout, and creating an IBO. In this guide, we'll just be focusing on the VBOs and IBOs.

Currently, the generation and setting the data is really all we need to abstract. The buffers can be rebound through a different method later, or just simply bound using their IDs before drawing.

## Abstracting

First, we'll make a "VertexBuffer" `.cpp` and `.hpp` file. Then, after including our `.hpp` in the main `.cpp` file, we can start writing our `VertexBuffer` class in the `.hpp`. This class should have:

+ An `unsigned int m_RendererID`;
+ A constructor with a `const void* data`, and an `unsigned int size`.
+ A destructor
+ A `void bind()` function
+ An `void unbind()` function

We know for every OpenGL object, there has to be some kind of ID that identifies that specific buffer or object. Other APIs also work on a similar system, so giving our new object an ID keeps things consistent. If we're using OpenGL as our renderer, this will be the ID that it uses. Later, we may have an engine-side ID to keep track of things.

We should also probably modify the `bind` and `unbind` methods to be `const`.

After we declare these in our `.hpp` file, we'll implement them individually in our `.cpp` file.

## Implementation

> Note: For debugging, `#include "Renderer.h"`

### Constructor

Our constructor should include the code to generate, bind, and set the data of our buffer. We can copy the code from our main application, but we need to remember our new instance variables and arguments to pass to the OpenGL functions.

+ ID &rightarrow; `m_RendererID`
+ Size &rightarrow; `size`
+ Data / array &rightarrow; `data`

After passing these in, our constructor should be complete.

### Binding and Unbinding

To bind and unbind our vertex buffer, we'll use `glBindBuffer()` with the `GL_ARRAY_BUFFER` slot selected.

For binding, use the `m_RendererID` member variable.

For unbinding, simply rebind to `0` instead of any ID.

### Destructor

Here we can use the `glDeleteBuffers()` function the same way we use `glGenBuffers()`, specifying the count and ID pointer for the buffer(s) we want to delete.

Then we're done with VBOs!

# Index Buffers

*Here, we'll follow a similar method to our vertex buffer class. In fact, we can duplicate our files and just modify them to use index buffers*

## Abstracting

Besides changing the class name and other obvious changes, we need to: 

+ Add an `unsigned int m_Count` member variable
+ Change our constructor to use a `const unsigned int*` for the type of `data`
+ Changing our `size` to `count` to represent a change from # of bytes to # of indices

## Implementation

> Again, for debugging, include the renderer header
> 
> We also need to remember to change any "VertexBuffer" instances to "IndexBuffer"

Besides changing the constructor header, we need to change the `size` in our buffer data assignment to our `count` multiplied by the size of its type, in this case the `sizeof(unsigned int)`. We also need to remember to replace any instances of `GL_ARRAY_BUFFER` with `GL_ELEMENT_ARRAY_BUFFER`.

We also need to initialize our `count`, which can be done in an initializer list, as well as a getter for the count which can be done as follows:

```c++
inline unsigned int getCount() const { return m_Count; }
```

Notice the `inline` keyword due to definition of a function in a header file.

