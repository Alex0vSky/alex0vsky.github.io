---
layout: post
categories: WinApi UnrealEngine 3D
tags: [WinApi, UnrealEngine, 3D]
title:  "UePrjCreator"
---
{% include asciinema.html %}


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

<script>
A0S_asciinema_play( 'Easy_start' );
A0S_asciinema_play( 'Run_for_a_specific_installed_version_of_the_Ue' );
A0S_asciinema_play( 'Run_for_installed_Ue_in_certain_path' );
A0S_asciinema_play( 'from_an_existing_template_with_path_for_a_specific_installed_version_of_Ue' );
A0S_asciinema_play( 'for_a_game_with_one_executable_without_Engine_dll_for_a_specific_installed_version_of_Ue' );
A0S_asciinema_play( 'error_This_project_file_already_exists' );
</script>

Inspired by video "Unreal Engine C++ Project Setup, From Scratch" of youtube blogger Alex Forsythe
{% include embed/youtube.html id='94FvzO1HVzY' %}

link to [*repo*](https://github.com/Alex0vSky/UePrjCreator/)
