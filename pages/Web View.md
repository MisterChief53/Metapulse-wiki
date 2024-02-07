public:: true

- At its core, the Web View is a small application built with the `Chromium Embedded Framework` that uses the framework's off-screen rendering feature to generate a pixel buffer that represents a webpage's color output in a matrix of BGRA values.
- For the source code, visit the [repo](https://github.com/MisterChief53/CEF-Docker-O3DE)
- ## Setting up Development Environment
	- Since GitHub does not allow us to quickly commit big binary files for now, and compiling the full Chromium Embedded Framework from source requires too many resources, our best approach for now is to rely on a binary download of the CEF.
	- Currently, the specific version that has been tested to work is: cef_binary_118.6.9+g7e73645+chromium-118.0.5993.119_linux64.tar.bz2
	- Once one downloads the specific version (it has to be for Linux x86_64), delete the `./tests/cefsimple` folder and replace it with the repo.
- ## Running the Application
	- The WebView utilizes a Docker container that makes use of `xvfb` to setup a virtual x server so that the CEF executes.
	- To execute correctly, the application is ran by directly invoking the executable as an argument to `xvfb`, which makes it so that when debugging directly with an IDE like CLion, one has to manually attach to the executable's process.