public:: true

- Open Source Proof-of-Concept of what a metaverse would look like that allows users to:
	- Chat between users and a Large Language Model
	- Render any webpage inside a multiplayer 3D environment
	- Use a shared account for multiple services, using a common API
- All of its dependencies (except CUDA) are open source.
- Metapulse is highly modular. Most services run as their own Docker containers, which can be run with minimal configuration. These services are built to replicate many of the common use-cases we see in modern open-source metaverses, but they can be used independently of each other.
- [[Development Environment Setup]]
- ## Architecture
	- ![arquitecture-metapulse.jpg](../assets/arquitecture-metapulse_1707323665756_0.jpg){:height 524, :width 748}
	  id:: 65cf7153-0859-4d70-92da-58d29293ff58
		- This architecture diagram is a bit outdated, mainly because the chat is now handled within the Accounts Server, and the pixel buffer only offers only webpage rendering.
	- ### [[WebServer]]
	  id:: 65cf7153-ee27-4c68-b221-b769601f34a4
	- ### [[World Server]]
	- ### [[Inference Server]]
	- ### [[Accounts Server]]
	- ### [[Web View]]
- ## Technical Details
	- ![Requirements and formal specification (In Spanish)](../assets/Documento_Final_1707322895598_0.pdf)
		- If the above isn't rendered (due to a Logseq bug), the requirements and formal specification (in spanish) are located [here](https://github.com/MisterChief53/Metapulse-wiki/blob/master/assets/Documento_Final_1707322895598_0.pdf)