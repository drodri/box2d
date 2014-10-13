# Box2D

This is a fork of the Box2D library (see Readme.txt, http://www.box2d.org), source code hosted in: https://github.com/drodri/box2d
It is used to create a biicode ready version in: http://www.biicode.com/erincatto/box2d

Instead of using the glfw library inside, it uses the biicode one: http://www.biicode.com/diego/glfw

The adaptation required can be seen in: https://github.com/drodri/box2d/commit/7e0259c5db2f01cd6e93a5c2e1969f702169aacb

It requires:

- Simple modification of root CMakeLists.txt. Note that with this simplification no other CMakeLists.txt in the project is required, biicode does not use them.

- Changing a couple of #includes. This will also be protected with #ifdef(BIICODE) guards in order to guarantee proper compilation of the fork without biicode too.

- The DroidSans.ttf is handled as biicode dependency, so it is always retrieved and copied to "bin" folder to guarantee proper functioning. This will also be protected with #ifdef guards.

- Adding glfw dependency in requirements.bii, filtering out glfw in ignore.bii, filtering out stb_truetype.h as having a main in mains.bii, and adding the root folder in paths.bii (so biicode finds #includes starting with "Box2D")

It builds and run on mingw(4.8), Visual Studio 12, Ubuntu 14, Mac OS X.

There are a couple of open (up to my knowledge, not biicode related) issues:

- The testbed fails to run in ubuntu due to GLSL 4.0 unsupported

- The testbed renders at half size in Mac retina displays. The solution involves using glfwGetFramebufferSize() instead of glfwSetWindowSize(), as in most systems they match, but in retina doesnt. As the g_camera is a global object used in other places it is not a straighforward fix.  