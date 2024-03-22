---
layout: post
categories: WinApi DirectX 3D HelloWinHlsl
tags: [DirectX, 3D, HelloWinHlsl]
title:  "HelloWinHlslPrimitives"
date:   2023-08-17 20:23:50 +0000
image: /assets/images/HelloWinHlslPrimitives.png
---

Using [__HelloWinHlsl__](https://github.com/Alex0vSky/HelloWinHlsl/) to draw primitives with shaders in available version of DirectX

I’ll explain why a separate section is dedicated to such a simple topic.
I remember that this was not an easy task, as it seemed at first.
Which is quite strange for **3D**, because everything there consists of so-called *primitives*.
I'm guessing that the desire to draw primitives for a newbie/beginner would come first.
After all, all textbooks and manuals on ordinary *3D* begin with this.
Now I’ll describe what difficulties I encountered so that you don’t have to 😊

And to be honest, the first working shader was obtained for [ball](/posts/HelloWinHlslBall/),
after all, the goal of my study of shaders was the simulation/emulation/visualization of physical processes from particles.
But there's a good chance you'll start with primitives.

## Introduction to the topic
Right off the bat! R&D.
Just a test **poc** project with minimal code containing a shader for DirectX.
Just to understand how the minimum works.
Let's see, the first thing we came across was Hello World: “Direct3D 10 Hello World”
[https://gist.github.com/Overv/3989887](https://gist.github.com/Overv/3989887)

There is a version of the *API* platform *DirectX10/Dx10Direct3D* or simply *Dx10*.
> Make sure we support this version of the *API* using this tool:
[DxCapsViewer](https://github.com/microsoft/DxCapsViewer). Can be taken from this repository.
Or perhaps you already have this file `dxcapsviewer.exe`{: .filepath} in *WDK*.
If this is not supported, then there is nothing wrong with training,
the compiled/built application will be launched in emulation mode:
*WARP* will emulate a *GPU* using a *CPU* and it will be quite slow.

We will implement the solution in the studio, I had *MSVC2019*.
Let's edit the *functions* a little, move `if (msg.message == WM_QUIT)break;` inside the loop `while (PeekMessage(&msg, NULL, 0, 0, PM_REMOVE))`,
so closing the application exists in reality.
Everything is working. From the code you can see that the shader is drawn on the polygon.

Additional checks.
If you have *NVIDIA* and the corresponding option is enabled,
then, working in the system tray (where the clock is), you will see that the example works on the *NVIDIA* adapter.
In the *procexp* tool, when viewing a process in the GPU tab, under GPU Allocation, the graph is not empty.
This means that everything works on the correct graphics adapter, a fast one.

We change the coordinates of the vertices, the picture changes.
We change the colors of the *RGB* shader, the picture changes.
So, **poc** is complete.
You can move on and develop a solution.

### First steps
Naturally, we understand that shaders work, but this is certainly not enough.
We need something beautiful.
When you're quickly searching for shader topics, **shadertoy.com** might catch your eye, it has a ton of great code examples.

#### The shadertoy.com
If anyone doesn't already know, this is a portal where the community publishes examples of their code.
Which can be launched online immediately.

He also has his own system, I would say API, which gives access to the required timer.
Well, access to the mouse allows you to rotate the scene. There's a lot more there.

Searching on the portal is convenient. Registration is simple.
You can read and leave comments.
There is code highlighting. Display error messages.
I can write a lot about this wonderful portal. There are mountains of information there!

#### Other, stay determined
Here's something that's easy to compile/build and might inspire you to take further steps if you've lost your resolve.
- In my opinion, the example with a particle system from the examples *directx-sdk-samples* is called
[NBodyGravityCS11](https://github.com/walbourn/directx-sdk-samples/tree/main/NBodyGravityCS11) looks exciting.
The example was kindly posted in the repository, and the repository is kindly maintained by *Chuck Walborn*;
- Also don't ignore the excellent examples from [bgfx](https://github.com/bkaradzic/bgfx),
There are many of them and the particle system there is also beautiful.
The project is easy to compile/build, but difficult to understand its architecture and its own shader language.

## Forward movement
Based on [https://www.shadertoy.com/view/tlXXzs](https://www.shadertoy.com/view/tlXXzs)
...
SDF
...

## Circle
Blah blah
Link to code from my repo with anchor on the desired line.
> Under construction
{: .prompt-warning }

## Square
Blah blah
Link to code from my repo with anchor on the desired line.
> Under construction
{: .prompt-warning }

## Rectangle
Blah blah
Link to code from my repo with anchor on the desired line.
> Under construction
{: .prompt-warning }

## Triangle
Blah blah
Link to code from my repo with anchor on the desired line.
> Under construction
{: .prompt-warning }

## Polygon
Blah blah
Link to code from my repo with anchor on the desired line.
> Under construction
{: .prompt-warning }

## Line
Blah blah
Link to code from my repo with anchor on the desired line.
> Under construction
{: .prompt-warning }

## Manual for converting from GLSL to HLSL
This will be quite enough, we will use it as a reference:
[https://gamedeveloper.com/programming/state-of-the-art-hlsl-to-glsl-converter](https://gamedeveloper.com/programming/state-of-the-art-hlsl-to-glsl-converter)

<br/>
<br/>
<br/>
a link to [*repo*](https://github.com/Alex0vSky/HelloWinHlslPrimitives/)
