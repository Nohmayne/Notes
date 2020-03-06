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

Then we can define another array to draw vertices based on 
