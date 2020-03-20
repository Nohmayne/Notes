# Vertex Arrays

## Reasoning

### We need to:

+ Tie together vertex buffers with some kind of data
    + Layout, content, etc.
+ *Possibly* add in an index buffer
+ Store the data on the CPU
    + Useful for debugging
    + Useful for reading / manipulation of shape data

### Ideal workflow:

1. Create an object
1. Give it a layout
1. Give it a buffer
1. Later call `vao.bind()`

&mdash;OR&mdash;

1. Create a vertex array
    + Series of buffers
1. Tell it what the layout is
1. Later call `vao.bind()`

## Abstraction

In the actual code, we'll need 2 objects.

+ Vertex Array
    + Constructor
    + Destructor
    + `addBuffer()` function
+ Buffer Element
    + Essentially the arguments for `glVertexAttribPointer()`
    + `unsigned int type`
    + `unsigned int count`
    + `bool normalized`
+ Buffer Layout

### The Code

> Make sure to make new `.hpp` and `.cpp` files

#### Vertex Array

##### Constructor / Destructor

For now, these can remain empty, as we will be passing information to the class via `addBuffer()` and such.

##### Add Buffer

This function should take in a vertex buffer object reference to add to the vertex array, as well as a layout to tie to that vertex buffer.

```c++
void addBuffer(const VertexBuffer& vb, const VertexBufferLayout& layout);
```

---

> Note: The following two should be in the same file

#### Vertex Buffer Element

#### Vertex Buffer Layout

