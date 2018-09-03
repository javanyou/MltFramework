# MltFramework

Make this project to help someone want to build [mlt.framework](https://www.mltframework.org/) use CMake.

I have make it can debug `src/examples/play.c` in **Clion**.

## 1. Prepare Env

It has been tested on my Mac.


Install FFmpeg and CMake

    brew install ffmpeg
    brew install cmake


## 2. Clion Import

Using Clion to import it.

## 3. Open Clion Run/Debug Configurations

Add `Environment variables`

    MLT_REPOSITORY=/path/to/mlt/src/modules
    MLT_DATA=/path/to/mlt/src/modules
    MLT_PROFILES_PATH=/path/to/mlt/profiles
    MLT_PRESETS_PATH=/path/to/mlt/presets
