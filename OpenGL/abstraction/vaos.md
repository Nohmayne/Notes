# Vertex Arrays

## Reasoning

### We need to:

+ Tie together vertex buffers with some kind of data
    + Layout, content, etc.
+ *Possibly* add in an index buffer
+ Store the data on the CPU

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



