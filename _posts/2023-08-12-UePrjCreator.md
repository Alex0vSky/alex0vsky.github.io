---
layout: post
categories: WinApi UnrealEngine 3D
tags: [UnrealEngine]
title:  "UePrjCreator"
date: 2023-08-12 00:00:00 +0000
---

{% include asciinema.html %}

## Usage
For example, the desired fully qualified filename for the \*.uproject location would be 
<br/>
`C:\UePrj1\UePrj1.uproject`{: .filepath}

### Generate a standart blank project

#### Easy start for the latest version of the installed Ue
`UePrjCreator "C:\UePrj1\UePrj1.uproject"`
<div id="Easy_start" class="asciinema-placeholder"></div>

#### Run for a specific installed version of the Ue
`UePrjCreator "C:\UePrj1\UePrj1.uproject" --UeVersion=4.26`
<div id="Run_for_a_specific_installed_version_of_the_Ue" class="asciinema-placeholder"></div>

#### Run for installed Ue in certain path in quotes
`UePrjCreator "C:\UePrj1\UePrj1.uproject" --UeInstallDir="C:\Program Files\Epic Games\UE_4.26"`
<div id="Run_for_installed_Ue_in_certain_path" class="asciinema-placeholder"></div>

### Generate from an existing template with a quoted path for a specific installed version of Ue
`UePrjCreator "C:\UePrj1\UePrj1.uproject" --UeVersion=4.26 --Tpl="C:\Program Files\Epic Games\UE_4.26\Templates\TP_SideScroller\TP_SideScroller.uproject"`
<div id="from_an_existing_template_with_path_for_a_specific_installed_version_of_Ue" class="asciinema-placeholder"></div>

### Generate for a game with one executable, without *Engine.dll, for a specific installed version of Ue
`UePrjCreator "C:\UePrj1\UePrj1.uproject" --UeVersion=4.26 --DevTpl`
<div id="for_a_game_with_one_executable_without_Engine_dll_for_a_specific_installed_version_of_Ue" class="asciinema-placeholder"></div>

### Help output
`UePrjCreator`
<div id="help" class="asciinema-placeholder"></div>

## Common mistake
> error: This project file already exists
{: .prompt-danger }
```console
UePrjCreator "C:\UePrj1\UePrj1.uproject"
UePrjCreator "C:\UePrj1\UePrj1.uproject"
```
<div id="error_This_project_file_already_exists" class="asciinema-placeholder"></div>

The solution is to delete the directory before using the tool:
: `cmd /c "rmdir C:\UePrj1 /s /q"`

or
: `cmd /c "del /Q /S C:\UePrj1 >nul 2>&1 & rmdir /Q /S C:\UePrj1 >nul 2>&1"`


<script>
A0S_asciinema_play( 'Easy_start' );
A0S_asciinema_play( 'Run_for_a_specific_installed_version_of_the_Ue' );
A0S_asciinema_play( 'Run_for_installed_Ue_in_certain_path' );
A0S_asciinema_play( 'from_an_existing_template_with_path_for_a_specific_installed_version_of_Ue' );
A0S_asciinema_play( 'for_a_game_with_one_executable_without_Engine_dll_for_a_specific_installed_version_of_Ue' );
A0S_asciinema_play( 'help' );
A0S_asciinema_play( 'error_This_project_file_already_exists' );
</script>

## Qa
Clickable reports

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

## Thanks
Inspired by video "Unreal Engine C++ Project Setup, From Scratch" of youtube blogger _Alex Forsythe_
{% include embed/youtube.html id='94FvzO1HVzY' %}

## More
A series of projects is planned - Unreal Engine for a system developer
- [x] Fast and easy create new project 
- [ ] UBT proxy and optimizer, to avoid expensive loading .Net stuff for little action
- [ ] Minimal Unreal Engine 4 executable
- [ ] UHT proxy and optimizer
- [ ] NppCodeAccess plugin 
- [ ] SublimeCodeAccess plugin 

Trick with GetProcAddress is necessary because I don't know how to link static symbols and use "delay-import" at the same time.

link to [*repo*](https://github.com/Alex0vSky/UePrjCreator/)
