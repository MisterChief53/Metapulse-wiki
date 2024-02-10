public:: true

- The environment is mainly configured through the use of a batch file that clones the relevant repos, sets up the Docker container, and gives you access to this wiki as well.
- ## Requirements
	- Windows 10+
	- WSL2
	- Docker Desktop (or a functional docker installation accessible through `PATH`)
	- Git (accessible through `PATH`)
	- A Python interpreter
	- ...
- ## Instructions
	- Download the current CEF binary here: https://drive.proton.me/urls/36ZV7R6SEW#cj64uSQ4UvFq
	- Extract the contents to the "WebView" folder **except** for `tests/cefsimple`, since that is the WebView code.