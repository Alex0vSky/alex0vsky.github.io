---
layout: post
categories: WinApi UnrealEngine 3D
tags: [WinApi, UnrealEngine, 3D]
title:  "UePrjCreator"
---
{% include asciinema.html %}

Clickable qa reports

[![cpplint](https://gist.githubusercontent.com/Alex0vSky/c200bc8d7e3cc3a79b61351963b2d390/raw/GoogleStyle_cpplint.svg)](
https://Alex0vSky.github.io/project-qa-report/UePrjCreator/cpplint.xml
) [![cppcheck](https://gist.githubusercontent.com/Alex0vSky/c200bc8d7e3cc3a79b61351963b2d390/raw/StaticAnalysis_cppcheck.svg)](
https://Alex0vSky.github.io/project-qa-report/UePrjCreator/cppcheck.xml
) [![LinesOfСode](https://gist.githubusercontent.com/Alex0vSky/c200bc8d7e3cc3a79b61351963b2d390/raw/Metrixpp-LinesOfСode.svg)](
https://Alex0vSky.github.io/project-qa-report/UePrjCreator/metrixpp.txt
) [![Comments](https://gist.githubusercontent.com/Alex0vSky/c200bc8d7e3cc3a79b61351963b2d390/raw/Metrixpp-Comments.svg)](
https://Alex0vSky.github.io/project-qa-report/UePrjCreator/metrixpp.txt
) [![amount testsuites](https://gist.githubusercontent.com/Alex0vSky/c200bc8d7e3cc3a79b61351963b2d390/raw/GoogleTest-testsuites-Windows-x64-Debug.svg)](
https://Alex0vSky.github.io/project-qa-report/UePrjCreator/GoogleTestCombinedOutput/index.html
) [![tests coverage](https://gist.githubusercontent.com/Alex0vSky/c200bc8d7e3cc3a79b61351963b2d390/raw/TestsCoverage-Occ-Windows-x64-Debug.svg)](
https://Alex0vSky.github.io/project-qa-report/UePrjCreator/HtmlReportOcc/index.html
)

### Usage

For example, the desired fully qualified filename for the \*.uproject location would be 
<br/>
`C:\UePrj1\UePrj1.uproject`{: .filepath}

<p id="Easy_start">
Easy start for the latest version of the installed Ue:
<br/>
<code class="language-plaintext highlighter-rouge">
UePrjCreator "C:\UePrj1\UePrj1.uproject"
</code>
</p>

<p id="Run_for_a_specific_installed_version_of_the_Ue">
Run for a specific installed version of the Ue: 
<br/>
<code class="language-plaintext highlighter-rouge">
UePrjCreator "C:\UePrj1\UePrj1.uproject" --UeVersion=4.26
</code>
</p>

<p id="Run_for_installed_Ue_in_certain_path">
Run for installed Ue in certain path in quotes:
<br/>
<code class="language-plaintext highlighter-rouge">
UePrjCreator "C:\UePrj1\UePrj1.uproject" --UeInstallDir="C:\Program Files\Epic Games\UE_4.26"
</code>
</p>

<p id="from_an_existing_template_with_path_for_a_specific_installed_version_of_Ue">
Generate from an existing template with a quoted path for a specific installed version of Ue:
<br/>
<code class="language-plaintext highlighter-rouge">
UePrjCreator "C:\UePrj1\UePrj1.uproject" --UeVersion=4.26 --Tpl="C:\Program Files\Epic Games\UE_4.26\Templates\TP_SideScroller\TP_SideScroller.uproject"
</code>
</p>

<p id="for_a_game_with_one_executable_without_Engine_dll_for_a_specific_installed_version_of_Ue">
Generate for a game with one executable, without *Engine.dll, for a specific installed version of Ue:
<br/>
<code class="language-plaintext highlighter-rouge">
UePrjCreator "C:\UePrj1\UePrj1.uproject" --UeVersion=4.26 --DevTpl
</code>
</p>

<p id="error_This_project_file_already_exists">
error: This project file already exists
<br/>
<code class="language-plaintext highlighter-rouge">
UePrjCreator "C:\UePrj1\UePrj1.uproject"
</code>
<br/>
<code class="language-plaintext highlighter-rouge">
UePrjCreator "C:\UePrj1\UePrj1.uproject"
</code>
</p>
Solution, remove directory before using tool:
<br/>`rmdir C:\UePrj1 /s /q`
<br/>or
<br/>`cmd /c "del /Q /S C:\UePrj1 >nul 2>&1 & rmdir /Q /S C:\UePrj1 >nul 2>&1"`


<script>
A0S_asciinema_play( 'Easy_start' );
A0S_asciinema_play( 'Run_for_a_specific_installed_version_of_the_Ue' );
A0S_asciinema_play( 'Run_for_installed_Ue_in_certain_path' );
A0S_asciinema_play( 'from_an_existing_template_with_path_for_a_specific_installed_version_of_Ue' );
A0S_asciinema_play( 'for_a_game_with_one_executable_without_Engine_dll_for_a_specific_installed_version_of_Ue' );
A0S_asciinema_play( 'error_This_project_file_already_exists' );
</script>

### Thanks
Inspired by video "Unreal Engine C++ Project Setup, From Scratch" of youtube blogger _Alex Forsythe_
{% include embed/youtube.html id='94FvzO1HVzY' %}

link to [*repo*](https://github.com/Alex0vSky/UePrjCreator/)
