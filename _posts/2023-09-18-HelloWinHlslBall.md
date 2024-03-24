---
layout: post
categories: WinApi DirectX 3D HelloWinHlsl
tags: [DirectX, 3D, HelloWinHlsl]
title:  "HelloWinHlslBall"
date:   2023-09-18 00:00:00 +0000
image: /assets/images/HelloWinHlslBall.gif
---

Using [__HelloWinHlsl__](https://github.com/Alex0vSky/HelloWinHlsl/) to draw ball with shaders in available version of DirectX
Supports DirectX 9, DirectX 10, DirectX 11, DirectX 12

This is the first shader that I managed to get working.
Therefore, a separate post appeared on this topic, as well as a separate project.
A study was also carried out on shader constants and their differences for different versions of *Dx*.
Of course, the constants also included a time value, which made it possible to animate the shader.
At first, I naively thought that I would construct a particle system *nbody* from balls.

More geometric primitives and tricks for beginners in this post: [HelloWinHlslPrimitives](/posts/HelloWinHlslPrimitives/).

Here I got acquainted with the outdated **Visual Studio Graphics Analyzer/VsGa**,
This shader analyzer/debugger now successfully replaces **PIX**.
Learned to use the **fxc** compiler.
I will also note that while working on this project I struggled with the "effects",
similar to `ID3D10Effect`, but still received errors: “Effects deprecated for D3DCompiler_47.”
Regarding this, here are some comments from [SO](https://stackoverflow.com/questions/2352514/direct3d-11-effect-files-deprecated):
- "Many professional game and graphics developers don't use the effects interfaces in Direct3D, and many of the leading game engines do not use them either."
- "So in short, yes you are discouraged from using it but you still can at the moment if you can live with the disclaimers."

Everything can be viewed in the repository in the `resource` directory, for example for
[Dx12](https://github.com/Alex0vSky/HelloWinHlslBall/blob/main/resource/ball_ps_Dx12.hlsl).

## Conversion
We find the simplest example, of course it will be in **GLSL**:
[simple metaball shader](https://gist.github.com/julien/d7e71b837392f5239c6553098b5cac0c).
Which will lead to the sandbox <https://glslsandbox.com/e#41187.0>
where you can observe the results in real time by changing the code.

Useful <https://shadertoy.com>,
basic knowledge about this portal can be seen in this 21-minute video
["Shadertoy for absolute beginners"](https://www.youtube.com/watch?v=u5HAYVHsasc).
I wrote about it here because the ball shader is created step by step.

The cross-platform tool [SHADERed](https://github.com/dfranx/SHADERed) will also come in handy.
We create a new *QuadGLSL* project and throw the shader code there.

Convert **GLSL** to **HLSL**.
Was `float` became `float1`.
Was `vec2` became `float2`.
Was `vec3` became `float3`.

Solving differences in coordinate systems **GLSL** from **HLSL**. Flipping the two-dimensional *Y* axis.
```hlsl
	float2 uv = position.xy / ve4Resolution.xy;
	uv.y = 1 - uv.y;
```

## Code differences between different Dx versions
Signature *main* for old *Dx9*:
`float4 main(in float2 position : VPOS) : COLOR`

Signature *main* for the rest *Dx*:
`float4 main(float4 position : SV_POSITION) : SV_TARGET`

Shader constants for the new *Dx12*:
```hlsl
cbuffer ConstantBuffer : register(b0) {
	float1 iTime;
	float2 iResolution;
};
```

Shader constants for the rest *Dx*:
```hlsl
cbuffer cb0 {
	float4 ve4Resolution;
	float1 fTime;
};
```

## Result
The ball will be moving
looped from the lower left corner to the upper right.
In `fSpeed` the motion speed coefficient is set,
in `qwe` looping.
The logic differs from the original example in simplification:
the calls `max(mod(...), min(...))` that have no special impact have been removed.
```hlsl
float4 main(in float2 position : VPOS) : COLOR {
	float1 fSpeed = 2;
	float1 qwe = ((fTime) % fSpeed) / fSpeed;
	
	float2 uv = position.xy / ve4Resolution.xy;
	uv.y = 1 - uv.y;
	uv -= qwe;
	uv.x *= ( ve4Resolution.x / ve4Resolution.y );

	float2 r = float2( uv.x, uv.y );
	float1 length_r = length(r);
	float1 ball = 0.05 / length_r;
	float1 col = ball;
	return float4(col * 0.8, 0, 0, 1.0);
}
```

<br>
<br>
<br>
a link to [*repo*](https://github.com/Alex0vSky/HelloWinHlslBall/)
