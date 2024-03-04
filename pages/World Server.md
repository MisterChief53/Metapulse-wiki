public:: true

- The server that takes care of the World's multiplayer instance and the [[Web View]].
- [[O3DE Auth Arquitecture]]
- ## Requirements
	- Visual Studio 2022 with the C++ desktop development workload, with the windows 11 and 10 SDK (latest) installed, along with the C++ Video Game Development workload.
	- All other dependencies in [[Development Environment Setup]]
	- At least 16gb of RAM and another 16gb swap file, preferably on an SSD.
	- A recent **stable** version of CMake in the path.
- ## Initial Setup
	- The world server setup is not part of the `setup.py` script, since it does not rely on docker, and includes many dependencies.
	- So, once cloned, you first need to follow the o3de documentation to make sure that our fork of the o3de engine is registered as an engine correctly, and o3de's custom python version is downloaded. This includes the setup involving enabling git lfs.
	- When following those steps, you should not build the engine or generate build files, instead, we navigate to the `o3de-metapulse` folder and execute:
	  `cmake -B build/windows -S . -G "Visual Studio 17" -DLY_UNITY_BUILD=OFF`
	  To make the necessary build files (this uses Visual Studio 2022).
	- Then, make your way to the `World/Libraries` folder, where you will do: `cmake -B build/windows -S . -G "Visual Studio 17"` to generate build configuration for the 3rd party libraries needed. (right now only curl is avaiable)
	- Then, open the `.sln` file in `World/Libraries/build/windows` to build the library in `Release` mode.
	- Then, in `build/windows`, execute `cmake --install .` to generate the necessary files the 3rd party library needs.
	- After this, go to `World` and do: `cmake -B build/windows -S . -G "Visual Studio 17" -DLY_UNITY_BUILD=OFF` to generate the build files for the project.
	- After this, you should be able to go to `World/build/windows` and open the solution there, where you will be able to choose a build configuration suited for your needs.
	- Once built, you can access the editor by doing `.\build\windows\bin\profile\Editor.exe --project-path . -rhi=vulkan`.
		- We use Vulkan to ensure compatibility with some older graphics cards.