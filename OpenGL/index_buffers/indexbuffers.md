# Index Buffers

## What are index buffers?
Say we want to draw a square. OpenGL, of course, interprets everything in triangles. Thus, drawing a square is really just two triangles. Anything we draw, in fact, is just a bunch of triangles. Index buffers can help us minimize the work we need to do to figure out how to draw these triangles. Before we jump straight in, let's do an example using our old method of defining vertices.

Let's say we want to draw a rectangle. We'll define the first triangle as the bottom half of the rectangle, going counterclockwise.

```c++
float positions[] = 
{
    -0.5f, -0.5f,
     0.5f, -0.5f,
     0.5f,  0.5
};
```

Then, for the second triangle, we'd have to define 3 more vertices like so:

```c++
float positions[] = 
{
    -0.5f, -0.5f,
     0.5f, -0.5f,
     0.5f,  0.5f,

     0.5f,  0.5f,
    -0.5f,  0.5f,
    -0.5f, -0.5f
};
```

Notice we're re-using two out of the three vertices in the second triangle from the first triangle. Since we don't want to have to define all of our triangles like this and repeat a bunch of vertices, we can instead use an index buffer. Index buffers allow us to define an order in which to use the vertices stored in our positions array, removing the need to repeat vertices.

Now, instead of defining our vertices with repeats, let's just define only unique vertices.

```c++
float positions[] = 
{
    -0.5f, -0.5f,
     0.5f, -0.5f,
     0.5f,  0.5f,
    -0.5f,  0.5f
};
```

Then we can define another array to draw vertices based on the "index" of the vertex within the `positions[]` array (e.g. `0.5f, -0.5f` would have an "index" of 1).

```c++
unsigned int indices[] =
{
    0, 1, 2,
    2, 3, 0
};
```

Now we need to go through the same process of creating a buffer object, but for our index buffer. However, we need to make one small change; instead of putting our buffer in the `GL_ARRAY_BUFFER` slot, we'll put it in the `GL_ELEMENT_ARRAY_BUFFER` slot. Other than that, the code is the same, minus the ID and the size of the data.

```c++
unsigned int ibo;
glGenBuffers(1, &ibo);
glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, ibo);
glBufferData(GL_ELEMENT_ARRAY_BUFFER, 2 * 3 * sizeof(unsigned int), indices, GL_STATIC_DRAW);
```

Finally, we can draw using our index buffer. However, we can't use the `glDrawArrays()` function for this, since that draws `GL_ARRAY_BUFFER`s. Instead, we'll use `glDrawElements()`, which can draw using our index buffer.

```c++
glDrawElements(GL_TRIANGLES, 6, GL_UNSIGNED_INT, nullptr);
```

And we're done! We've successfully drawn a square.
