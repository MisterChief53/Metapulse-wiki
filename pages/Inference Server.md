public:: true

- ## Setup Inference Server for Development
	- install the `DevContainers` extension on VSCode.
	- Open the folder in a container using the extension.
	- Wait a bit for it to load. Now, you have the environment in a Docker container. You are able to start new terminals that will have all dependencies,
	- ### On Pycharm
		- Have a Docker engine running
		- Open the project, navigate to `devcontainer.json`
		- Click the blue box ad select create devcontainer and mount sources
- ## State of the LLM
	- Right now, the LLM is running on Mistral7B finetuned for instructions, and provided context for the character being a bartender.
	- Google colab document link: https://colab.research.google.com/drive/18-B3-4522mxzXLmhdfsZxz7L5AMTgVMc?hl=es%2F#scrollTo=WBqjvm7cT6vY
- ## Run the Inference Server
	- Simply navigate to the root of the repo, and run `docker compose up`.
- ## Interacting With Inference Server
	- The server runs on `localhost:7070`.
	- For quick interactions with the LLM, to test inference and basic reply formatting you may visit `/chat/playground` on your browser.
	- For REST requests, you need to send a **POST** request to `/chat/invoke` with a `Content-Type' = 'application/json'` header and your JSON in the body using this template:
		- ```json
		  {
		    "input":{
		      "message":"Hi, how are you?"
		    }
		  }
		  ```
		- You then will be returned a JSON where in `content` is the reply from the LLM.
		- Here is an example of how to make the request using simple PowerShell commands:
			- ```powershell
			  Invoke-RestMethod -Uri 'http://localhost:7070/chat/invoke' -Method Post -Headers @{ 'Content-Type' = 'application/json' } -Body '{"input":{"message":"Hi, how are you?"}}'
			  ```