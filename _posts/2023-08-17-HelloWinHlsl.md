---
layout: post
categories: WinApi DirectX 3D HelloWinHlsl
tags: [DirectX, 3D, HelloWinHlsl]
title:  "HelloWinHlsl"
date:   2023-08-17 20:08:52 +0000
pin: true
---

## Hello Windows Hlsl
Hlsl shader C++ library. Supports DirectX 9, DirectX 10, DirectX 11, DirectX 12. 
An attempt to understand the history of the development of shaders in DirectX.
Provides an interface to customized DirectX of all versions, in one source file.
You can see how the program code on the DirectX client side becomes more complicated.
There are several [examples](/tags/hellowinhlsl/) of working with the library.

In general, it is suggested to use the library as follows:
```cpp
using CurDxVer = DxVer::v12;

template<class T> class seascape; // primary template

template<> class seascape<DxVer::v9> : public CurClientApp<DxVer::v9> { using T = DxVer::v9;
	bool init(DxCtx<T>::cref_ptr_t crpustDxCtx, ToolCtx<T>::cref_ptr_t puoTools, Adjust<T>* poAdjustDxAux) {
		// ... puoTools ->shader( ) ->loader( )
		// ... crpustDxCtx ->m_pcD3dDevice ->SetVertexShader( ... );
		// ... puoTools ->quad( ) ->createVertexBuf( );
	}
	void render_frame(DxCtx<T>::cref_ptr_t crpustDxCtx, Dynamic<T>::cref_ptr_t) {
		// ... crpustDxCtx ->m_pcD3dDevice ->BeginScene( );
	}
};

template<> class seascape<DxVer::v12> : public CurClientApp<DxVer::v12> { using T = DxVer::v12;
	bool init(DxCtx<T>::cref_ptr_t, ToolCtx<T>::cref_ptr_t puoTools, Adjust<T>* poAdjustDxAux) {
		// ... puoTools ->shader( ) ->loader( )
		// ... poAdjustDxAux ->onSetPso( ... )
	}
	void render_frame(DxCtx<T>::cref_ptr_t, Dynamic<T>::cref_ptr_t crpsoDynamic) {
		// ... crpsoDynamic ->m_pcCommandList ->IASetVertexBuffers( 0, 1, &m_stVertexBufferView );
	}
};

uptr<Sys::HolderClientApp> ClientTy::entryPoint() { return std::make_unique< Sys::HolderClientApp >( new seascape<CurDxVer> ); }
Config::uptrc_t ClientTy::configure() { return ClientApp::Configurator::Predef::getDefault( ); }
```
You can see that `CurDxVer = DxVer::v12;` indicates that the software will be compiled to work with DirectX 12.

## Reports
### StaticAnalysis
[![cpplint](https://gist.githubusercontent.com/Alex0vSky/f15941c4c8858c6209ad8800fa810539/raw/GoogleStyle_cpplint.svg)](
https://Alex0vSky.github.io/project-qa-report/HelloWinHlsl/cpplint.xml
) [![cppcheck](https://gist.githubusercontent.com/Alex0vSky/f15941c4c8858c6209ad8800fa810539/raw/StaticAnalysis_cppcheck.svg)](
https://Alex0vSky.github.io/project-qa-report/HelloWinHlsl/cppcheck.xml
) 
### CodeMetrix
[![LinesOfСode](https://gist.githubusercontent.com/Alex0vSky/f15941c4c8858c6209ad8800fa810539/raw/Metrixpp-LinesOfСode.svg)](
https://Alex0vSky.github.io/project-qa-report/HelloWinHlsl/metrixpp.txt
) [![Comments](https://gist.githubusercontent.com/Alex0vSky/f15941c4c8858c6209ad8800fa810539/raw/Metrixpp-Comments.svg)](
https://Alex0vSky.github.io/project-qa-report/HelloWinHlsl/metrixpp.txt
) 
### GoogleTest
[![amount testsuites](https://gist.githubusercontent.com/Alex0vSky/f15941c4c8858c6209ad8800fa810539/raw/GoogleTest-testsuites-Windows-x64-Debug.svg)](
https://Alex0vSky.github.io/project-qa-report/HelloWinHlsl/GoogleTestCombinedOutput/index.html
) [![tests coverage](https://gist.githubusercontent.com/Alex0vSky/f15941c4c8858c6209ad8800fa810539/raw/TestsCoverage-Occ-Windows-x64-Debug.svg)](
https://Alex0vSky.github.io/project-qa-report/HelloWinHlsl/HtmlReportOcc/index.html
)

a link to [*repo*](https://github.com/Alex0vSky/HelloWinHlsl/)

> Under construction
{: .prompt-warning }

## TODO
- [x] Dx9
- [x] Dx10
- [x] Dx11
- [x] Dx12
- [ ] API documentation
- [ ] get rid of dependence on the boost::pfr library
- [ ] get rid of dependence on the DirectXTK12 library
- [ ] to header-only library

## API documentation
### TODO(Alex0vSky): makeme
