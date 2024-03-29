public:: true

- The environment is mainly configured through the use of a batch file that clones the relevant repos, sets up the Docker container, and gives you access to this wiki as well.
- ## Requirements
	- Windows 10+
	- WSL2
	- Docker Desktop (or a functional docker installation accessible through `PATH`)
	- Git (accessible through `PATH`)
	- A Python interpreter
	- Logseq (for editing and viewing the wiki locally)
	- ...
- ## Instructions
	- Clone the [development environment](https://github.com/MisterChief53/Metapulse-dev-env).
	- Download the current CEF binary here: https://drive.proton.me/urls/36ZV7R6SEW#cj64uSQ4UvFq
id:: 65cf7153-dffe-43d2-b517-90207835bd0c
	- Extract the contents to the "WebView" folder **except** for `tests/cefsimple`, since that is the WebView code.
	- **Before** making any changes, it is advised that you run the `checkout_master.py` script so that all submodules are checked out at their master branches, so as to treat them as conventional git repos, independent from the other modules!
	- Now, if you want to work on a specific repo, the instructions are:
		- [[WebServer]]
		- [[Accounts Server]]
		- [[Web View]]
		- [[Inference Server]]
	-