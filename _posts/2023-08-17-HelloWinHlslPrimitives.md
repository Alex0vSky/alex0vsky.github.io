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
<https://gist.github.com/Overv/3989887>

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
If anyone doesn't already know, this is a portal where the community publishes examples of their **GLSL** code.
Which can be launched online immediately: [shadertoy.com](https://www.shadertoy.com/).

He also has his own system, I would say API, which gives access to the required timer.
Well, access to the mouse allows you to rotate the scene. There's a lot more there.

Searching on the portal is convenient. Registration is simple.
You can read and leave comments.
There is code highlighting. Display error messages.
I can write a lot about this wonderful portal. There are mountains of information there!

There is also [glslsandbox.com](https://glslsandbox.com/).
It is convenient to view changes in the shader made by the community over time. I haven't used it much, I don't know why.

#### Other, stay determined
Here's something that's easy to compile/build and might inspire you to take further steps if you've lost your resolve.
- In my opinion, the example with a particle system from the examples *directx-sdk-samples* is called
[NBodyGravityCS11](https://github.com/walbourn/directx-sdk-samples/tree/main/NBodyGravityCS11) looks exciting.
The example was kindly posted in the repository, and the repository is kindly maintained by *Chuck Walborn*;
- Also don't ignore the excellent examples from [bgfx](https://bkaradzic.github.io/bgfx/examples.html#nbody),
There are many of them and the particle system there is also beautiful.
The project is easy to compile/build, but difficult to understand its architecture and its own shader language.

## Forward movement
If there is inspiration, then we continue the search.
I got lucky and found this shader: [Necromurloc - Basic 2D primitive](https://www.shadertoy.com/view/tlXXzs).
Credits: "Created by [Necromurlok](https://www.shadertoy.com/user/Necromurlok) July 24, 2019."
It has almost everything you need, albeit in **GLSL**.

Well, almost everything is ready,
now you need/can usefully spend your time watching
beautiful and voluminous lesson [thebookofshaders](https://thebookofshaders.com/)
convert **GLSL** to **HLSL**.
The cross-platform tool [SHADERed](https://github.com/dfranx/SHADERed) may be useful.
Run **GLSL** and **HLSL** shaders in real time, as well as instant recompilation and re-running.
It turns out that the shader always shows its work in real time from the current code.
There is also a **GLSL** and **HLSL** shader debugger.

Getting it to work turns out to be easy; Here are a few notes about things that are not obvious.
- In **GLSL** you can use shorthand notations, and `vec2(0.5)` is the same as `vec2(0.5,0.5)`
- In **HLSL** the system/keywords/registered words are not the same as in **GLSL**,
for example, the word "line" is a "preprocessor directive" in **HLSL**.

From theoretical knowledge, the term **SDF**=Signed Distance Fields is useful.
and these tutorials [ronja](https://www.ronja-tutorials.com/post/034-2d-sdf-basics/)

You can take a walk around the portal [shadertoy.com](https://www.shadertoy.com/)
and reading community comments can be helpful.

Here is the link that remained after searching, but it turned out to be not so useful:
- <https://stackoverflow.com/questions/66390181/sv-primitiveid-and-primitives-in-direct3d-11>
- <https://learnopengl.com/Advanced-OpenGL/Geometry-Shader>
- <https://learn.microsoft.com/en-us/windows/uwp/gaming/creating-shaders-and-drawing-primitives>
- “2nd line sdf” <https://www.shadertoy.com/view/cs2Gzw>
- “Shadertoy for absolute beginners” <https://www.youtube.com/watch?v=u5HAYVHsasc>

If you need additional shader code or your own special one with blackjack,
then you can look at [shaderc](https://bkaradzic.github.io/bgfx/tools.html#shader-compiler-shaderc).
This was invented on [bgfx](https://github.com/bkaradzic/bgfx). I can't comment, I didn't spend enough time on **shaderc**.

And yes, the topic of shader compilation and, for example, *DirectXShaderCompiler/DXC* are not touched upon here.

So below you can see the results.
At the same time, the entry point `main` is not presented, because this post turned out to be big anyway,
secondly, in addition to the `uv` transformation, there are simply function calls.
Everything can be viewed in the repo in `resource` directory, for example for
[Dx9](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx9.hlsl#L65)

### Rectangle
The `rectangle` function from [Necromurloc - Basic 2D primitive](https://www.shadertoy.com/view/tlXXzs).
Was `float` became `float1`.
Was `vec2` became `float2`.
Was `vec2(0.0)` became `float2(0.0, 0.0)`.
```hlsl
float1 rectangle(in float2 uv, in float2 size2, in float2 off) {
	float2 d = step(abs(uv - off) - size2, float2(0.0, 0.0));
	return d.x * d.y;
}
```
For all versions of *Dx* everything is the same, only for *Dx9* the screen size constant in the old format is used:
[Dx9](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx9.hlsl#L5)
, [Dx10](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx10.hlsl#L6)
, [Dx11](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx11.hlsl#L6)
, [Dx12](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx12.hlsl#L6)

### Square
The `quad` function from [Necromurloc - Basic 2D primitive](https://www.shadertoy.com/view/tlXXzs).
Was `float` became `float1`.
Was `vec2` became `float2`.
Was `vec2(0.0)` became `float2(0.0, 0.0)`.
```hlsl
float1 quad(in float2 uv, float1 size1, in float2 off) {
	float2 d = step(abs(uv - off) - size1, float2(0.0, 0.0));
	return d.x * d.y;
}
```
For all versions of *Dx* everything is the same, only for *Dx9* the screen size constant in the old format is used:
[Dx9](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx9.hlsl#L10)
, [Dx10](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx10.hlsl#L11)
, [Dx11](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx11.hlsl#L11)
, [Dx12](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx12.hlsl#L11)

### Circle
The `circle` function from [Necromurloc - Basic 2D primitive](https://www.shadertoy.com/view/tlXXzs).
Was `float` became `float1`.
Was `vec2` became `float2`.
```hlsl
float1 circle(in float2 uv, float1 radius, in float2 off) {
	float2 d = off - uv;
	return step(dot(d, d), radius * radius);
}
```
For all versions of *Dx* everything is the same, only for *Dx9* the screen size constant in the old format is used:
[Dx9](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx9.hlsl#L15)
, [Dx10](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx10.hlsl#L16)
, [Dx11](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx11.hlsl#L16)
, [Dx12](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx12.hlsl#L16)

### Line
It's interesting that a simple line requires a lot of code.

The `line` function from [Necromurloc - Basic 2D primitive](https://www.shadertoy.com/view/tlXXzs).
Was `float` became `float1`.
Was `vec2` became `float2`.
```hlsl
float1 line_(float2 uv, float2 p0, float2 p1, float1 pointSize) {
	float2 line__ = p1 - p0;
	float2 dir = uv - p0;

	pointSize *= pointSize;

	float1 h = clamp(dot(dir, line__) / dot(line__, line__), 0.0, 1.0);
	dir -= line__ * h;

	return step(dot(dir, dir) - pointSize, pointSize);
}
```
For all versions of *Dx* everything is the same, only for *Dx9* the screen size constant in the old format is used:
[Dx9](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx9.hlsl#L20)
, [Dx10](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx10.hlsl#L21)
, [Dx11](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx11.hlsl#L21)
, [Dx12](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx12.hlsl#L21)

### Polygon
Not a simple element.
I had to look around and remember: *polar* coordinate system; geometric functions.
I started from here
<https://thebookofshaders.com/07/>.
Come in and look at the illustrations to get aesthetic pleasure from the illustrations and presentation of the material,
if you haven't seen this tutorial yet.

I had to pull the code from the *main* tutorial into a separate function for convenience.
I will not describe all the conversion renamings.

For example, a hexagon, we pass the value *6* for the `N` argument to the `polygonViaPolar` function:
```hlsl
#define PI 3.14159265359
#define TWO_PI 6.28318530718
float1 polygonViaPolar(in float2 uv, float1 size1, in float2 off, in int N) {
	uv = off - uv;
	float1 a = atan2( uv.x,uv.y ) + PI;
	float1 r = TWO_PI / float1(N);
	float1 d = cos(floor(0.5 + a / r) * r - a) * length(uv);
	return smoothstep( 0.41, 0.4, d / size1 );
}
float1 hexagonViaPolar(in float2 uv, float1 size1, in float2 off) {
	return polygonViaPolar( uv, size1, off, 6 );
}
```
For all versions of *Dx* everything is the same, only for *Dx9* the screen size constant in the old format is used:
[Dx9](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx9.hlsl#L32)
, [Dx10](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx10.hlsl#L33)
, [Dx11](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx11.hlsl#L33)
, [Dx12](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx12.hlsl#L33)

### Triangle
The heaviest element, and it would seem that in *3D* everything consists of it.
But with shaders everything is different, it's fun.
Geometry lovers will immediately say that a triangle is a polygon of three vertices,
and there is already a code for the polygon.
What if it's not productive?
And besides, it uses *polar* coordinates, this may not be at all useful when your head is full of other things.

#### First option
Here is the first option, based on the coordinates of the vertices.
Shader used [Simple 2D Triangle](https://www.shadertoy.com/view/4s3fzj),
created by [Rafbeam](https://www.shadertoy.com/user/Rafbeam) on 2018-05-09.

Was `float` became `float1`.
Was `vec2`, became `float2`.
Was `vec3`, became `float3`.
And some renaming of functions.
```hlsl
float1 triangleViaVertsAux_(float2 p1, float2 p2, float2 p3) {
    return (p1.x - p3.x) * (p2.y - p3.y) - (p2.x - p3.x) * (p1.y - p3.y);
}
float3 triangleViaVerts(float3 color, float3 background, float2 vertices[3], float2 uv) {
    bool b1 = triangleViaVertsAux_(uv, vertices[0], vertices[1]) < 0.0f;
    bool b2 = triangleViaVertsAux_(uv, vertices[1], vertices[2]) < 0.0f;
    bool b3 = triangleViaVertsAux_(uv, vertices[2], vertices[0]) < 0.0f;
    if((b1 == b2) && (b2 == b3))return color;
    return background;
}
float4 main(in float2 position : VPOS) : COLOR {
	// ...
	shape += triangleViaPolar(uv, 0.2, float2(0.9, 0.9));
	// ...
	float3 background = float3(0.0, 0.0, 0.0);
	float1 x_ = 0.6, y_ = 0.2;
	float2 VERTS[] = {
			float2(x_ + 0.5, y_ + 0.75)
			, float2(x_ + 0.3, y_ + 0.25)
			, float2(x_ + 0.7, y_ + 0.25)
		};
	shape += triangleViaVerts( float3(1.0, 1.0, 1.0), background, VERTS, uv );
	// ...
}
```
For all versions of *Dx* everything is the same, only for *Dx9* the screen size constant in the old format is used:
[Dx9](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx9.hlsl#L51)
, [Dx10](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx10.hlsl#L52)
, [Dx11](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx11.hlsl#L52)
, [Dx12](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx12.hlsl#L52)

#### Second option
Here is the second option, in polar coordinates:
```hlsl
#define PI 3.14159265359
#define TWO_PI 6.28318530718
float1 polygonViaPolar(in float2 uv, float1 size1, in float2 off, in int N) {
	uv = off - uv;
	float1 a = atan2( uv.x,uv.y ) + PI;
	float1 r = TWO_PI / float1(N);
	float1 d = cos(floor(0.5 + a / r) * r - a) * length(uv);
	return smoothstep( 0.41, 0.4, d / size1 );
}
float1 triangleViaPolar(in float2 uv, float1 size1, in float2 off) {
	return polygonViaPolar( uv, size1, off, 3 );
}
```
For all versions of *Dx* everything is the same, only for *Dx9* the screen size constant in the old format is used:
[Dx9](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx9.hlsl#L32)
, [Dx10](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx10.hlsl#L33)
, [Dx11](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx11.hlsl#L33)
, [Dx12](https://github.com/Alex0vSky/HelloWinHlslPrimitives/blob/main/resource/primitives_ps_Dx12.hlsl#L33)

#### Other publications used
- [Basic Shape:Triangle](https://www.shadertoy.com/view/XlBBWt) Created by [cailven](https://www.shadertoy.com/user/cailven) in in 2018-02-01
- [Triangle Example](https://www.shadertoy.com/view/MlySzw) Created by [Heavybrush](https://www.shadertoy.com/user/Heavybrush) in in 2017-01-04

### Caution!
Everything was so simple, we just renamed the types.
This isn't always the case, the biggest mistake/pitfall I've seen with conversions is differences in the *multiplication* rules.

## Roadmap/Todo
Measure the output performance of each primitive.

## Manual for converting from GLSL to HLSL
This will be quite enough, we will use it as a reference:
<https://gamedeveloper.com/programming/state-of-the-art-hlsl-to-glsl-converter>
<https://anteru.net/blog/2016/mapping-between-HLSL-and-GLSL/>

<br/>
<br/>
<br/>
a link to [*repo*](https://github.com/Alex0vSky/HelloWinHlslPrimitives/)
