# OpenGL
These are all my notes on the OpenGL API for graphics programming in *C++*. Enjoy!
## Basics
The only notes written in $\LaTeX$. Covers how to open a window and draw a basic "hello world triangle." See the PDF version to view the actual notes.
## Error Handling
Shows how to handle errors in OpenGL using assertions and the `glGetError` method. Will be revised in more detail and with better methods eventually.
## Index Buffers
Shows how to use index buffers in OpenGL to draw a rectangle instead of just one triangle without having to repeat vertices in the vertex buffer.
## Shaders
Shows how to write shaders in *GLSL*, and how to parse, compile, and use them in *C++*. Demo is making the triangle from **Basics** red.
## Uniforms
Shows how to get data from *C++* into *GLSL* (application to shader) and make the rectangle from **Index Buffers** shift colors over time.
## Vertex Arrays
Shows how to make binding the necessary OpenGL objects before drawing easier using vertex arrays, which are necessary in the OpenGL core profile.
## Abstracting
Shows how to abstract the already made concepts in our main file into different classes and header files. See the README in that folder for more details.
