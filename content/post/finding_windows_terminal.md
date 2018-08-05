---
title: "Finding a good Windows terminal"
date: 2018-08-05T06:56:18+01:00
tags:
  - Windows
  - rxvt-unicode
  - Xming
  - Tools
categories:
  - Technical
---

With my recent purchase of a lovely new Thinkpad T480s from Lenovo, I've been experimenting with using Windows as my main driver after a hiatus of several years. It's quite different from both MacOS and Linux (obviously!) but with the advent of [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/about) (WSL) a lot of my previous pain points are gone. Except for one: a decent terminal emulator. This is what I did.

<!--more-->

## TLDR;

Xming running on startup.

urxvt.bat

    @bash -c "export DISPLAY=':0' && xrdb -merge -I$HOME ~/.Xresources && urxvt"

NoShell.vbs

    If WScript.Arguments.Count >= 1 Then
        ReDim arr(WScript.Arguments.Count-1)
        For i = 0 To WScript.Arguments.Count-1
           Arg = WScript.Arguments(i)
           If InStr(Arg, " ") > 0 Then Arg = """" & Arg & """"
           arr(i) = Arg
        Next

        RunCmd = Join(arr)
        CreateObject("Wscript.Shell").Run RunCmd, 0, True
    End If

Windows Shortcut

    %USERPROFILE%\bin\NoShell.vbs %USERPROFILE%\bin\urxvt.bat

## What?

Both Linux and MacOS have a surfeit of quality terminals. [iTerm2](https://iterm2.com/) and the shipped Terminal.app are both solid offerings, while there are many options on Linux: [GNOME Terminal](https://help.gnome.org/users/gnome-terminal/stable/), [Konsole](https://konsole.kde.org/),  [Terminator](https://www.openhub.net/p/gnome-terminator) and [rxvt-unicode](http://software.schmorp.de/pkg/rxvt-unicode.html) are just a small sample of the most popular. But Windows can only offer WSL, the ancient and unloved command prompt, and PowerShell, which has limited appeal outside dedicated Windows system administrators. 

Third-party options that can be used for terminal emulation are [Putty](https://putty.org/), [Kitty](http://www.9bis.net/kitty/) or [ConEmu](https://conemu.github.io/). Cygwin et al I've used extensively before and found the Windows/Posix seams too grating for day-to-day use.  

What I look for is something that works well with my current workflow:

* Tabbing - I like to have a single window for my terminal and several tabs covering different CLI tasks
* Keyboard shortcuts - shortcuts for creating/destroying tabs and simple, easy copy/paste is essential
* Unicode support - I do not want to see boxes where my characters should be
* Lightweight - I'm a memory control freak and a terminal should only use what it needs (in my view) and no more
* Stable - no bugs. If there are bugs, they should be small annoyances only.
* Tmux support - I use Tmux extensively and some terminals have trouble with it, such as blocking word traversal with Alt+Arrow L/R or Ctrl+Arrow L/R
* Seamless - a single click and I get my terminal up without any manual steps

The basic WSL terminal offers most of these except for tabbing. ConEmu wrapping WSL is too unstable for my liking. Powershell has no tabbing and is a memory hog. The less said about Command Prompt, the better.

## Still no explanation

While looking for something in the internet wasteland of Windows developer tooling, I came across [Nick Janetakis' excellent post](https://nickjanetakis.com/blog/using-wsl-and-mobaxterm-to-create-a-linux-dev-environment-on-windows) about replacing his current VM-driven workflow with one based around WSL. He uses ConEmu which works for him but not me unfortunately. He also mentions using [MobaXterm](https://mobaxterm.mobatek.net/) to run graphical Linux applications. At first thought, I felt this wasn't something that I needed until I realised - why not use a Linux terminal emulator instead using this approach?

How it works is that MobaXterm runs an X server and WSL acts as the X client (X is an aged beast where the common technical terms of server/client are inverted). WSL can run the graphical interface program and the X server acts as a bridge to a window in the Windows UI.

rxvt-unicode (urxvt) is my current terminal emulator at work so it would be an ideal candidate for this approach. MobaXterm is far more than just an X server so I looked for something more lightweight. Xming looked good and seemed to work well in my initial experiments.

But urxvt requires configuration to work well and this configuration is tightly coupled to the X server. Xming has configuration options but I wanted to use urxvt-specific configuration. Thus, I updated the local .Xresources file in the WSL home and tried to load it before firing up urxvt. Succcess! But then disappointment. Since the X server is run from Xming and not WSL, the .Xresources file is not loaded automatically. So each time urxvt is started, the .Xresources file must be loaded.

## I'm beginning to understand...

At this point, I had a lot of manual steps that gave me the terminal I wanted. It had to be seamless, so I tried creating a batch file to run urxvt directly from Windows. This too worked well but left a WSL window lying around while urxvt ran via Xming. A quick search gives me a VB script that runs a batch file without a window. Creating a Windows shortcut that runs the script with my already created batch and I finally have my seamless terminal.

It's not perfect - the terminal opens in the directory where the batch file is and I've seen some lack of consistency in copy/paste between the terminal and my Windows version of Emacs but these are mild annoyances. With some luck I can eradicate this issues but either way I have what I wanted finally!

## TA-DA!

![Beautiful Synergy](/img/beautiful_synergy.png)