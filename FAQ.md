# Introduction #

LiteIDE FAQ

# FAQ #

## LiteEnv Plugin ##
> LiteIDE environment setup plugin
### Select Environment ###
> Select current use environment, default system
  * Windows - win64 or win32
  * Linux - linux64 or linux32
  * MacOSX - darwin64 or darwin32
> Configure Environment
  1. Menu: View -> Options -> LiteEnv or Welcome: Options -> LiteEnv
  1. Double clicked .env file to editor
> Example win32.env
```
#win32 environment

GOROOT=c:\go
GOARCH=386
GOOS=windows

PATH=%GOROOT%\bin;%PATH%

LITEIDE_GDB=gdb
LITEIDE_MAKE=mingw32-make
LITEIDE_TERM=%COMSPEC%
LITEIDE_TERMARGS=
LITEIDE_EXEC=%COMSPEC%
LITEIDE_EXECOPT=/C
```
> Example linux64.env
```
#linux64 environment

GOROOT=$HOME/go
GOARCH=amd64
GOOS=linux

PATH=$GOROOT/bin:$PATH

LITEIDE_GDB=gdb
LITEIDE_MAKE=make
LITEIDE_TERM=/usr/bin/gnome-terminal
LITEIDE_TERMARGS=
LITEIDE_EXEC=/usr/bin/xterm
LITEIDE_EXECOPT=-e
```

## LiteBuild Plugin ##
> LiteIDE build system, build project or file, if file belong a project
### Configure Build ###
  1. Menu: View -> Options -> LiteBuild or Welcome: Options -> LiteBuild
  1. Double clicked .xml file to editor
> example gosrc.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<mime-info xmlns='http://www.freedesktop.org/standards/shared-mime-info'>
	<mime-type type="text/x-gosrc" id="gosrc" work="$(EDITOR_DIR)" ver="1">
		<config id="Go" name="GO" value="$(GOROOT)/bin/go"/>
		<config id="GoExec" name="GOEXEC" value="$(LITEAPPDIR)/goexec"/>
		<config id="ErrRegex" name="ERRREGEX" value="([\w\d_\\/\.]+):(\d+):"/>
		<custom id="TargetArgs" name="TARGETARGS" value=""/>
		<custom id="BuildArgs" name="BUILDARGS" value=""/>
		<custom id="InstallArgs" name="INSTALLARGS" value=""/>
		<action id="Build" img="blue/build.png" key="Ctrl+B;F7" cmd="$(GO)" args="build $(BUILDARGS)" save="all" output="true" codec="" regex="$(ERRREGEX)" />
		<action id="Install" menu="Build" img="blue/install.png" key="Ctrl+F8" cmd="$(GO)" args="install $(INSTALLARGS)" save="all" output="true"/>
		<action id="Clean" menu="Build" img="blue/clean.png" cmd="$(GO)" args="clean" save="all" output="true"/>
		<action id="CleanAll" menu="Build" img="blue/cleanall.png" cmd="$(GO)" args="clean -i" save="all" output="true"/>
		<action id="BuildAndRun" img="blue/buildrun.png" key="Ctrl+R;Ctrl+F7" task="Build;Run"/>
		<action id="Run" menu="BuildAndRun" img="blue/run.png" key="Ctrl+F5" cmd="$(EDITOR_DIRNAME_GO)" args="$(TARGETARGS)" output="true" codec="utf-8" readline="true"/>
		<action id="RunTerm" menu="BuildAndRun" img="blue/runterm.png" key="Ctrl+Shift+F5" cmd="$(LITEIDE_EXEC)" args="$(LITEIDE_EXECOPT) $(GOEXEC) $(EDITOR_DIRNAME_GO) $(TARGETARGS)" output="false" readline="true"/>
		<action id="FileRun" menu="BuildAndRun" img="gray/filerun.png" key="Alt+F6" cmd="$(GO)" args="run $(EDITOR_NAME)" save="editor" output="true" codec="utf-8" readline="true"/>
		<action id="Test" img="blue/test.png" key = "Ctrl+T" cmd="$(GO)" args="test" save="all" output="true" codec="utf-8"/>
		<action id="Get" menu="Test" img="blue/get.png" cmd="$(GO)" args="get -v ." save="all" output="true" codec="utf-8"/>
		<action id="Fmt" menu="Test" img="blue/fmt.png" cmd="$(GO)" args="fmt" save="all" output="true" regex="$(ERRREGEX)"/>
		<action id="Vet" menu="Test" img="blue/vet.png" cmd="$(GO)" args="vet" save="all" output="true" regex="$(ERRREGEX)"/>
		<debug id="Debug" cmd="$(EDITOR_DIRNAME_GO)" args="$(TARGETARGS)" work="$(EDITOR_DIR)"/>
	</mime-type>	
</mime-info>
```

## How to use GOBIN ##
1. Edit current env , example linux64.env
```
  GOBIN=$HOME/bin
  PATH=$GOBIN:$PATH
```
2. LiteIDE -> Option -> LiteBuild -> Edit gosrc.xml
```
<config id="Go" name="GO" value="$(GOROOT)/bin/go"/>
```
```
<config id="Go" name="GO" value="$(GOBIN)/go"/>
```
3. Restart LiteIDE

## GolangCode Plugin ##
> Use gocode word complete, example fmt.
### Install gocode ###
```
$ export GOROOT=$HOME/go
$ export PATH=$HOME/go/bin:$PATH
$ go get -u github.com/nsf/gocode 
```
### Load gocode incorrect ###
> Test gocode status (my = my computer name)
```
$ gocode status
```
> dial unix /tmp/acrserver.my: dial unix /tmp/acrserver.my: connection refused
```
$ rm /tmp/acrserver.my 
```
Reload LiteIDE

## GolangDoc Plugin ##
> Golang doc browser and search
### Find package ###
> example input "zip"
```
archive/zip
compress/bzip2
compress/gzip
```
> The result best matche is archive/zip, auto open zip package document.

## CodeSearch Plugin ##
> Editor code search and replace
### Regex ###
> (Colo)(u)(r) -> \1\3

## LiteDebug Plugin ##
> LiteIDE debug plugin
### Gdb version >= 7.1 ###
> Golang debug request gdb version 7.1 or high
### Source path ###
> The file or project source path cannot include outsite space or latin1 char
### Environment LITEIDE\_GDB ###
> example LiteEnv -> win64.env
```
PATH=c:/go-w64/bin;%PATH%
GOROOT=c:/go-w64
GOBIN=c:/go-w64/bin
GOARCH=amd64
GOOS=windows
LITEIDE_GDB=gdb64
```
### WIN32 and WIN64 ###
> WIN32 request gdb.exe,WIN64 request gdb64.exe.