---
layout: post
tags: [DirectX, 3D]
title:  "MinimalDx12DrawText"
date:   2023-11-24 00:00:00 +0000
---

## Short description
Drawing text in Dx12 using a minimum amount of code and **without dependencies** and **header-only** and C++.

### Importance
Now we can display plain text via DirectX12 by calling two C++ functions by connecting one header, and without library/binary dependencies.


It would be nice to have a shortened text output option based on **DirectX Tool Kit** (aka **DirectXTK12**).
Why refactor this particular ToolKit? Because it is the most popular and my code can be useful to more people.
Because in reality everything is very confusing, which is compounded by the greatly increased difficulty of understanding the output for Dx12.
At the same time, the minimum functionality is preserved, this is exactly the option I would like to see when I started to understand the problem.
A training project in essence, but minimal functionality allows, for example, to easily output **FPS**.
By the way, there are examples of basic work with "DirectX memory" and cutting or bypassing them will not work - it won't take off, it may also be useful.
I believe that the project will also be useful to those who want to study the history of the development of DirectX interfaces.
We can be happy that we can get rid of another dependency in the form of DirectXTK12 for **basic** 3D projects.
And I will be glad that another header-only C++ library has appeared.

### Increasing difficulty of drawing
Pseudo code

 - Dx9;
 
```cpp
/* Initialization
*/
	hr = ::D3DXCreateFontW( 
			m_stDxCtx ->m_pcD3dDevice.Get( )
			, detail_::DrawCfg<TInnerDxVer>::getFontSize( ), 0
			, FW_NORMAL, 1, 0 
			, DEFAULT_CHARSET, OUT_DEFAULT_PRECIS, ANTIALIASED_QUALITY, DEFAULT_PITCH
			, detail_::DrawCfg<TInnerDxVer>::getFontFamily( ).c_str( )
			, m_pcFont.ReleaseAndGetAddressOf( )
		);
/* Render
*/
	m_pcFont ->DrawTextW( 
			NULL, stream.str( ).c_str( ), -1
			, &rect, DT_LEFT|DT_NOCLIP, detail_::DrawCfg<TInnerDxVer>::getColor( ) 
		);
```
{: .nolineno }

 - Dx10;
 
```cpp
/* Initialization
*/
	CPtr< IDWriteFactory > pcDWriteFactory;
	CPtr< ID2D1Factory > pcD2DFactory;

	// It's CreateDeviceIndependentResources()
	hr = ::D2D1CreateFactory( 
			D2D1_FACTORY_TYPE_SINGLE_THREADED 
			, pcD2DFactory.ReleaseAndGetAddressOf( ) 
		);

	hr = ::DWriteCreateFactory(
			DWRITE_FACTORY_TYPE_SHARED
			, __uuidof( IDWriteFactory )
			, reinterpret_cast< IUnknown** >( pcDWriteFactory.ReleaseAndGetAddressOf( ) )
		);

	hr = pcDWriteFactory ->CreateTextFormat(
		detail_::DrawCfg<TInnerDxVer>::getFontFamily( ).c_str( ),
		// Font collection (NULL sets it to use the system font collection).
		NULL,
		DWRITE_FONT_WEIGHT_REGULAR,
		DWRITE_FONT_STYLE_NORMAL,
		DWRITE_FONT_STRETCH_NORMAL,
		detail_::DrawCfg<TInnerDxVer>::getFontSize( ),
		L"en-us",
		m_pcTextFormat.ReleaseAndGetAddressOf( )
	);
	// Center align (horizontally) the text.
	hr = m_pcTextFormat->SetTextAlignment(DWRITE_TEXT_ALIGNMENT_LEADING);
	hr = m_pcTextFormat->SetParagraphAlignment(DWRITE_PARAGRAPH_ALIGNMENT_NEAR);

	CPtr< ID3D10Texture2D > pcOffscreenTexture;
	// Allocate a offscreen D3D surface for D2D to render our 2D content into
	D3D10_TEXTURE2D_DESC texDesc = { };
	// ...
	hr = m_stDxCtx ->m_pcD3dDevice ->CreateTexture2D( 
			&texDesc
			, NULL
			, pcOffscreenTexture.ReleaseAndGetAddressOf( ) 
		);
	CPtr< IDXGISurface > pcDxgiSurface;
	hr = pcOffscreenTexture.As( std::addressof( pcDxgiSurface ) );

	// Create the DXGI Surface Render Target.
	D2D1_RENDER_TARGET_PROPERTIES props = D2D1::RenderTargetProperties(
		D2D1_RENDER_TARGET_TYPE_DEFAULT,
		D2D1::PixelFormat(DXGI_FORMAT_UNKNOWN, D2D1_ALPHA_MODE_PREMULTIPLIED),
		96,
		96
	);
	CPtr< ID2D1RenderTarget > pcRenderTarget;
	hr = pcD2DFactory ->CreateDxgiSurfaceRenderTarget(
			pcDxgiSurface.Get( )
			, &props
			, pcRenderTarget.ReleaseAndGetAddressOf( )
		);

	// Create a red brush for text drawn into the back buffer
	hr = pcRenderTarget ->CreateSolidColorBrush(
		detail_::DrawCfg<TInnerDxVer>::getColor( )
		, m_pcBackBufferTextBrush.ReleaseAndGetAddressOf()
	);
	CPtr< IDXGISurface > pcBackBuffer;
	// Get a surface in the swap chain
	hr = m_stDxCtx ->m_pcDxgiSwapChain->GetBuffer(
			0
			, IID_PPV_ARGS( pcBackBuffer.ReleaseAndGetAddressOf( ) )
		);

	// It is assumed that the window will change size.
	DXGI_SWAP_CHAIN_DESC stDxgiSwapChainDesc = { };
	// or IDXGISwapChain1::GetHwnd method (dxgi1_2.h)
	m_stDxCtx ->m_pcDxgiSwapChain->GetDesc(&stDxgiSwapChainDesc);
	FLOAT dpiX, dpiY;
	//pcD2DFactory ->GetDesktopDpi( &dpiX, &dpiY ); // @depr
	dpiX = dpiY = (FLOAT)::GetDpiForWindow(stDxgiSwapChainDesc.OutputWindow);
	D2D1_RENDER_TARGET_PROPERTIES props2 = D2D1::RenderTargetProperties(
		D2D1_RENDER_TARGET_TYPE_DEFAULT,
		D2D1::PixelFormat(DXGI_FORMAT_UNKNOWN, D2D1_ALPHA_MODE_PREMULTIPLIED),
		dpiX,
		dpiY
	);

	// Create a D2D render target which can draw into the surface in the swap chain
	hr = pcD2DFactory ->CreateDxgiSurfaceRenderTarget(
			pcBackBuffer.Get( )
			, &props2
			, m_pcBackBufferRT.ReleaseAndGetAddressOf( )
		);
		
/* Render
*/
	m_pcBackBufferRT ->BeginDraw( );
	m_pcBackBufferRT ->SetTransform( D2D1::Matrix3x2F::Identity( ) );
	// Text format object will center the text in layout
	m_pcBackBufferRT ->DrawTextW(
			stream.str( ).c_str( ), (UINT32)stream.str( ).length( ),
			m_pcTextFormat.Get( ),
			detail_::DrawCfg<TInnerDxVer>::getRect( ),
			m_pcBackBufferTextBrush.Get( )
		);
	hr = m_pcBackBufferRT ->EndDraw( );
```

 - Dx11;
 
```cpp
// Like Dx10 but with minor changes
```
{: .nolineno }

 - Dx12 in ToolKit DirectXTK12 (*.h + *.lib) and a huge amount of code under the hood;

```cpp
/* Global variable
*/
	m_graphicsMemory = std::make_unique< DrawAux::Fps::Spec::D12::GraphicsMemory >( 
		m_stCtx ->m_psstDxCtx ->m_pcD3dDevice12.Get( ) );

/* Initialization
*/
	uptr< Spec::D12::DescriptorHeap > m_resourceDescriptors;
	uptr< Spec::D12::SpriteFont > m_font;
	uptr< Spec::D12::SpriteBatch > m_spriteBatch;
	// load font
	const auto &arrayFont = DxtkFont::CompiledToBinary::getArial28( );
	// prepare special memory
	m_resourceDescriptors = std::make_unique< Spec::D12::DescriptorHeap >(
			device
			, D3D12_DESCRIPTOR_HEAP_TYPE_CBV_SRV_UAV
			, D3D12_DESCRIPTOR_HEAP_FLAG_SHADER_VISIBLE
			, Descriptors::Count
		);
	// start upload font to special memory
	Spec::D12::ResourceUploadBatch resourceUpload( device );
	resourceUpload.Begin( );
	// pass uploader to font object
	m_font = std::make_unique< Spec::D12::SpriteFont >(
			device
			, resourceUpload
			, arrayFont, sizeof( arrayFont )
			, m_resourceDescriptors ->GetCpuHandle( Descriptors::MyFont )
			, m_resourceDescriptors ->GetGpuHandle( Descriptors::MyFont )
		);
	Spec::D12::RenderTargetState rtState(
			DXGI_FORMAT_R8G8B8A8_UNORM
			, DXGI_FORMAT_R8G8B8A8_UNORM
		);
	Spec::D12::SpriteBatchPipelineStateDescription pd( rtState );
	// pass uploader to spriter
	m_spriteBatch = std::make_unique< Spec::D12::SpriteBatch >( device, resourceUpload, pd );
	// wait async upload
	auto uploadResourcesFinished = resourceUpload.End(
			m_stDxCtx ->m_pcCommandQueue.Get( )
		);
	uploadResourcesFinished.wait( );

/* Render
*/
	ID3D12DescriptorHeap* heaps[] = { m_resourceDescriptors ->Heap( ) };
	m_pc_CommandList ->SetDescriptorHeaps(
			static_cast< UINT >( std::size( heaps ) )
			, heaps
		);

	m_spriteBatch ->Begin( m_pc_CommandList.Get( ) );

	auto origin = DirectX::g_XMZero;
	auto scale = DirectX::XMVectorReplicate( 1 );
	auto effects = Spec::D12::SpriteEffects::SpriteEffects_None;
	float layerDepth = 0;
	m_font ->DrawString(
			m_spriteBatch.get( )
			, stream.str( ).c_str( )
			, XMLoadFloat2( &m_fontPos )
			, DirectX::Colors::White
			, 0.f
			, origin
			, scale
			, effects
			, layerDepth
		);

	m_spriteBatch ->End( );
```

 - Dx12 in MinimalDx12DrawText, look at the sources of my project [*MinimalDx12DrawText*](https://github.com/Alex0vSky/MinimalDx12DrawText/).

```cpp
/* Initialization
*/
	auto ctx = Plain::fontWorks( mDevice, mCommandQueue );

/* Render
*/
	auto holder = Plain::drawWorks( ctx, text );
```
{: .nolineno }

In short about Dx12:
   + textures and shaders need to be used
   + you need to have your font in binary form

Also, all the examples of text drawing given above are
can be launched through my open source library [HelloWinHlsl](https://github.com/Alex0vSky/HelloWinHlsl/)
(supports DirectX 9, 10, 11, 12).

### Details
Changes and what has been cut
 - The main thing is that function calls are "straightened" to flat code, i.e. The bodies of almost all functions are built manually into a few main ones. What gives the depth of the call stack is no more than two, this was done deliberately so as not to get lost when studying;
 - Well, I cut out multithreading, there was a problem with the allocator, now everything is "flat" and the allocator as an entity is not needed;
 - Allocators have been removed, as mentioned above, which means that work with memory is not optimized for performance, in fact, unnecessary code has also been removed;
 - Global variables, because I always try to avoid them;
 - Global naked static variables, this evil, I always try to avoid them to the detriment of the architecture, and the latest C++ standard allows us to avoid unnecessary ones;
 - Various presets, extra code;
 - Only for Windows OS, in addition to unnecessary code, there were also a lot of *define*-s;
 - The font as content or resource is hardcoded, unfortunately it is stored without compression;
 - Redundant parameters, and therefore the code that supports them, have been removed;
 - Removed asynchrony, for example, unnecessary waiting for many fonts to load, only one font;
 - It turns out that the **cyclomatic complexity** of the code is significantly reduced;
 - Many ToolKit variable names have been retained and many old comments remain; this will help people who know ToolKit navigate the code;
 - Tested for memory leaks;
 - Macro-free.

### Extern
Here are the posts about the project:
 - [SO](https://stackoverflow.com/questions/36394606/how-do-you-draw-text-in-directx-12/77319552#77319552)
 - [gamedev.net](https://www.gamedev.net/forums/topic/715055-easy-way-to-drawrender-text-in-directx12)

Thanks:
 - For the demo I used the example `firesmoke.c`{: .filepath} by @auth PrzemyslawZaworski​ from [shadertoy.com](https://www.shadertoy.com/view/wtB3RG)

### Conclusion
The result is a header-only solution, I like these and prefer these.
Cleaned up Direct3D 12, did some important work, contributed to the community, and can sleep peacefully.
> Are we mentally prepared for the release of the new **Dx13**?

Link to [*repo*](https://github.com/Alex0vSky/MinimalDx12DrawText/) and demo application
