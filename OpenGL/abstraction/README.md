# Abstraction
Now that we've made most of the required components to render to the screen, we can abstract the code to make it easier to work with (for instance, in a game engine).
## The Plan
Essentially, we'll be taking our already existing code and concepts and moving them into classes to make OpenGL easier to work with on a higher level. This guide will cover the following:

1. Vertex Buffers
1. Index Buffers
1. Vertex Arrays
1. Shaders

We also eventually need to make a **renderer**, which is essentially a layer to handle simple requests and turn them into OpenGL calls and code.

## The Guide
Following this guide can be done through the related `.md` files in the abstraction directory. Let's start abstracting!

