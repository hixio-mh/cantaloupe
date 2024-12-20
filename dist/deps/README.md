# About This Folder

Inside each platform-specific folder is a `lib` folder containing the Kakadu
shared library needed by `KakaduNativeProcessor`. See the user manual ->
Processors section -> KakaduNativeProcessor section for setup steps.

# License

All of the software in this directory tree is distributed under a Kakadu Evaluation License which is intended for an individual or organisation wishing to evaluate the Software with a view of procuring a longer term License Type. See the
[Kakadu License Terms](https://kakadusoftware.com/wp-content/uploads/3451-3100-0598_1_Kakadu-Software-Licence-Terms-and-Conditions-FINAL-1-Sept-2021.pdf)
document for detailed terms of use.

# Build Info

## Linux

The Linux binaries were compiled on CentOS 7 x86 64-bit with gcc 4.8.5.

```
export JAVA_HOME=/usr/lib/jvm/java
cd coresys/make
make -f Makefile-Linux-x86-64-gcc
cd ../../managed/make
make -f Makefile-Linux-x86-64-gcc
cd ../../lib/Linux-x86-64-gcc

# Builds `libkdu_vNXX.so` & `libkdu_jni.so`
# Java class files are in `../../../java/kdu_jni`
```

## macOS

The macOS binaries were compiled on macOS 10.13.4 with xcodebuild and
clang 902.0.39.1, for target `x86_64-apple-darwin17.5.0`.

```
cd managed
xcodebuild -project managed.xcodeproj -target kdu_jni -configuration Release clean
xcodebuild -project managed.xcodeproj -target kdu_jni -configuration Release

# Resulting binaries are in ../../bin
# Java class files are in ../../java/kdu_jni
```

(Future note: for Catalina, add `-UseModernBuildSystem=NO` to the `xcodebuild`
commands.)

## Windows

The Windows binaries were compiled on Windows 7 SP1 64-bit with Visual
Studio Community 2015.

### Build Steps

1. Install the JDK
2. Install Visual Studio with the Microsoft Foundation Classes for C++
   component
3. Build `coresys`
    1. Open `coresys\coresys_2015`
    2. Retarget solution to the 8.1 platform version
    3. Build with Release configuration & x64 platform
4. Build `kdu_jni`
    1. Open `managed\kdu_managed_2015`
    2. Add the JDK headers to the include path
        1. Right-click on the `kdu_jni` solution
        2. Go to Properties -> VC++ Directories -> Include Directories
        3. Add `jdk-x.x.x\include` and `jdk-x.x.x\include\win32` paths to JDK
           headers
    3. Retarget solution to the 8.1 platform version
    4. Build with Release configuration & x64 platform

The resulting files are in `..\..\bin_x64`:
  * `kdu_v80R.dll`
  * `kdu_a80R.dll`
  * `kdu_jni.dll`
