## Introduction ##
> LiteIDE X is golang developer editor

## Install golang, if needed ##
> http://golang.org/doc/install.html


## Install LiteIDE ##
> http://code.google.com/p/golangide/downloads/list

> Download and unarchive to $HOME

## Install Gocode ##
> https://github.com/nsf/gocode
```
$ export GOROOT=$HOME/go
$ export PATH=$HOME/go/bin:$PATH
$ go get -u github.com/nsf/gocode 
```

## Build LiteIDE Source ##
> http://code.google.com/p/liteide/

### Windows ###
```
> hg clone http://code.google.com/p/liteide/ 
> set QTDIR=c:\Qt\Qt474
> set MINGWDIR=c:\Qt\MinGW
> cd liteide/build
> build_mingw.cmd
```

### Linux ###
```
$ hg clone http://code.google.com/p/liteide/ 
$ export QTDIR=$HOME/QtSDK/Desktop/Qt/474/gcc
$ cd liteide/build
$ ./build_linux.sh
```

### MacOSX ###
```
$ hg clone http://code.google.com/p/liteide/ 
$ export QTDIR=$HOME/QtSDK/Desktop/Qt/474/gcc
$ cd liteide/build
$ ./build_osx.sh
```