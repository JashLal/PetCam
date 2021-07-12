# PetCam

Add description of application

# OpenCV Installation

The OpenCV sdk works in java by utilizing java wrapper files over the native c++ source code.
This repository has packaged the OpenCV sdk as a library dependency. It should build and run
like a normal android application; however, if there any issues, the process for installing
the OpenCV sdk is documented below.

## Installing OpenCV

1. Install version 4 of the OpenCV android sdk from https://opencv.org/releases/

2. Create a new Android Studio project and select the Native C++ template

3. Follow all steps of the following Stackoverflow answer, but continue with the below steps
before syncing and building the project.

4. In build.gradle (:app) (the build.gradle of the main application module), change compile project(':opencv')
to implementation project(':opencv'). Compile is now deprecated.

5. Additionally, you will need to change the cmake cppFlags and arguments in build.gradle (:app). Edit the file
so that it looks like this.

```
...    
android {
    ...
    defaultConfig {
        ...
        externalNativeBuild {
            cmake {
		cppFlags "-std=c++14 -fexceptions -frtti"
                arguments "-DANDROID_ARM_NEON=TRUE",'-DANDROID_STL=c++_shared'	
        }
    }
    buildTypes {
        ...
    }
    externalNativeBuild {
        cmake {
            path "CMakeLists.txt"
        }
    }
}

dependencies {
    ...
    implementation project(':opencv')
}

```
