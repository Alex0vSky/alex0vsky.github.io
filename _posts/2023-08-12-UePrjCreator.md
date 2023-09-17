---
layout: post
categories: WinApi UnrealEngine 3D
tags: [WinApi, UnrealEngine, 3D]
title:  "UePrjCreator"
---

page with a description of the pieces, 

<!--
		# '{{ site.baseurl }}/assets/asciinema/569377.cast'
![replay_simple](/assets/vhs_UePrjCreator.gif)
<div id="demo"></div>
-->

*replay of the command line call*

For example, the desired fully qualified filename for the *.uproject location would be C:\UePrj1\UePrj1.uproject

<p id="Easy_start">Easy start</p>

<p id="Run_for_a_specific_installed_version_of_the_Ue">Run for a specific installed version of the Ue</p>

<p id="Run_for_installed_Ue_in_certain_path">Run for installed Ue in certain path</p>

<p id="from_an_existing_template_with_path_for_a_specific_installed_version_of_Ue">from an existing template with path for a specific installed version of Ue</p>

<p id="for_a_game_with_one_executable_without_Engine_dll_for_a_specific_installed_version_of_Ue">for a game with one executable without Engine dll for a specific installed version of Ue</p>

<p id="error_This_project_file_already_exists">error: This project file already exists</p>
solution:
`rmdir C:\UePrj1 /s /q`
or
`cmd /c "del /Q /S C:\UePrj1 >nul 2>&1 & rmdir /Q /S C:\UePrj1 >nul 2>&1"`

<link rel="stylesheet" type="text/css" href="{{ site.baseurl }}/assets/asciinema/asciinema-player.css" />
<script src="{{ site.baseurl }}/assets/asciinema/asciinema-player.min.js"></script>
<script>
//AsciinemaPlayer.create(
//		'{{ site.baseurl }}/assets/asciinema/PowerSession/error.cast'
//		, document.getElementById('demo')
//		, {
//			loop: true
//			, theme: 'asciinema'
//			, preload: true
//			, autoPlay: true
//			, controls: "auto" // true
//			, startAt: 12
//			<!-- 
//			, poster: 'npt:1:23' 
//			-->
//			, fit: 'none'
//			<!-- 
//			, terminalFontSize: 'medium'
//			-->
//			, terminalFontSize: 'small'
//			, cols: 127
//			, rows: 30
//			, poster: "data:text/plain,I'm regular \x1b[1;32mI'm bold green\x1b[3BI'm 3 lines down'"
//		}
//	);
function A0S_asciinema_play(name) {
	AsciinemaPlayer.create(
			'{{ site.baseurl }}/assets/asciinema/PowerSession/'+name+'.cast'
			, document.getElementById( name )
			, {
				loop: true
				, theme: 'asciinema'
				, preload: true
				, autoPlay: true
				, controls: "auto" // true
				, startAt: 12
				//, fit: 'none'
				, fit: 'width'
				, cols: 127
				, rows: 30
			}
		);
}
A0S_asciinema_play( 'Easy_start' );
A0S_asciinema_play( 'Run_for_a_specific_installed_version_of_the_Ue' );
A0S_asciinema_play( 'Run_for_installed_Ue_in_certain_path' );
A0S_asciinema_play( 'from_an_existing_template_with_path_for_a_specific_installed_version_of_Ue' );
A0S_asciinema_play( 'for_a_game_with_one_executable_without_Engine_dll_for_a_specific_installed_version_of_Ue' );
A0S_asciinema_play( 'error_This_project_file_already_exists' );
</script>

link to [*repo*](https://github.com/Alex0vSky/UePrjCreator/)
