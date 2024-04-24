public:: true

- At its core, the Web View is a small application built with the `Chromium Embedded Framework` that uses the framework's off-screen rendering feature to generate a pixel buffer that represents a webpage's color output in a matrix of BGRA values.
- For the source code, visit the [repo](https://github.com/MisterChief53/CEF-Docker-O3DE)
- ## Setting up Development Environment
	- Since GitHub does not allow us to quickly commit big binary files for now, and compiling the full Chromium Embedded Framework from source requires too many resources, our best approach for now is to rely on a binary download of the CEF.
	- Currently, the specific version that has been tested to work is: cef_binary_118.6.9+g7e73645+chromium-118.0.5993.119_linux64.tar.bz2
	- Once one downloads the specific version (it has to be for Linux x86_64), delete the `./tests/cefsimple` folder and replace it with the repo.
		- If you are on Windows, you can extract `.tar.bz2` using `7zip`.
	- Use `docker compose run` to execute the `docker-compose.yml` on the `cefsimple` folder. Make sure that your .yml file has this line commented or not present at all:
		- ```yaml
		  command: /bin/bash -c "cd /workspace && while true; do sleep 3600; done"
		  ```
		- This is so that the dbus and ssh are setup from inside the container by the dockerfile and not the docker compose
	- Then, inside clion, for your toolchain, use a `remote-host` with a user `dev` and a password `1234` on `localhost` on port `5000`.
	- Now, CLion will upload the files to the docker container, and you can compile the `cefsimple` target.
	- Once compiled, to run it, you need to go to the docker container's `tmp` folder from **inside a shell invoked from CLion**, and find where the `cefsimple` binary got compiled.
	- Then, you may run: `xvfb-run --server-args="-screen 0 1024x768x24" ./cefsimple --url=https://blank.page/` to run the webview on a specified webpage.
	- ### Deprecated instructions
		- The open the outer folder in CLion and configure a run configuration using the provided `docker-compose.yml`.
	- Now, debugging will work with everything you have!
- ## Running the Application
	- The WebView utilizes a Docker container that makes use of `xvfb` to setup a virtual x server so that the CEF executes.
	- To execute correctly, the application is ran by directly invoking the executable as an argument to `xvfb`, which makes it so that when debugging directly with an IDE like CLion, one has to manually attach to the executable's process.