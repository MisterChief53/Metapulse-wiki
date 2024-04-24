public:: true

- At its core, the Web View is a small application built with the `Chromium Embedded Framework` that uses the framework's off-screen rendering feature to generate a pixel buffer that represents a webpage's color output in a matrix of BGRA values.
- For the source code, visit the [repo](https://github.com/MisterChief53/CEF-Docker-O3DE)
- ## Setting up Development Environment
	- The repo includes a whole binary release of the **Chromium Embedded Framework**. This is made for development productivity and because we make small changes to CEF's CMake configs.
	- Due to this, when cloning the repo, you need to make sure all the `.so` files are pulled correctly, which are stored with git LFS.
	- Currently, the specific version that has been tested to work is: `cef_binary_118.6.9+g7e73645+chromium-118.0.5993.119_linux64.tar.bz2`
	- Use `docker compose up` to execute the `docker-compose.yml` on the `cefsimple` folder. Make sure that your .yml file has this line commented or not present at all:
		- ```yaml
		  command: /bin/bash -c "cd /workspace && while true; do sleep 3600; done"
		  ```
		- This is so that the dbus and ssh are setup from inside the container by the dockerfile and not the docker compose
	- Then, inside clion, for your toolchain, use a `remote-host` with a user `dev` and a password `1234` on `localhost` on port `5000`.
	- Now, CLion will upload the files to the docker container, and you can compile the `cefclient` target.
	- We put the entire CEF here since we make a few modifications to it related to CMake.
	- Once compiled, to run it, you need to go to the docker container's `tmp` folder from **inside a shell invoked from CLion**, and find where the `cefsimple` binary got compiled.
	- Then, you may go to ((65e52d0b-0503-4b0b-9aa9-a88e2f6891de))
- ## Extracting images
	- Whenever we want to extract images, we can use this docker command: `docker cp 4eb851e05df9:/tmp/tmp.tK8sxnRrgB/cmake-build-debug/tests/cefclient/Debug/img.png ./img.png`.
		- So basically, we specify which container id to copy the generated png from the generated `tmp` folder into wherever we invoke that command.
- ## Running the Application
  id:: 65e52d0b-0503-4b0b-9aa9-a88e2f6891de
	- The WebView utilizes a Docker container that makes use of `xvfb` to setup a virtual x server so that the CEF executes.
	- To execute correctly, the application is ran by directly invoking the executable as an argument to `xvfb`, which makes it so that when debugging directly with an IDE like CLion, one has to manually attach to the executable's process.
	- The command to run the application is this: `xvfb-run --server-args="-screen 0 1024x768x24" ./cefclient --off-screen-rendering-enabled --url=https://blank.page/`
		- One thing to note is that, this command uses a placeholder `--url` argument. To connect to the [[WebServer]] while it is **on the same machine** in another Docker container, you would need to use `http://<your_host_public_ip>:300/`, since CEF expects to connect to a public webpage.