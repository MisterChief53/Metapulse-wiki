public:: true

- Repository: https://github.com/MisterChief53/Metapulse-accounts-server/tree/master
- ## How to run
	- Clone the accounts server repo.
	- Run the `convert-line-endings.ps1` script to remove the line endings for the `gradlew` file:
		- ```powershell
		  ./convert-line-endings.ps1 -File gradlew
		  ```
	- Run your Docker engine instance and on the root folder do `docker compose up` to run the accounts server.
	- The **Database Seeder** will run each time you execute the server by default. To change this, check ((662a6627-09bc-43df-bb14-4076e748ac5c))
- ## Access The Accounts Server Development Environment
	- Open IntelliJ IDE on the Accounts Server folder.
	  id:: 65cf733c-dab5-4209-97c0-f77ef430c473
	- Configure a run configuration that uses the `docker-compose.yml` file.
	- Now, if you want to run it, just execute that run configuration and it will execute the code.
- ## Dependencies
	- Since we are building a docker container that will use spring and deal with PostgreSQL, we will probably use the following Spring Dependencies:
		- Spring Web
		- Spring Data JPA
		- Spring Security
		- PostgreSQL Driver
- ## Classes and endpoints
	- ### Entities
	  collapsed:: true
		- #### User
			- This class creates an entity in the data base called User and its getters and setters, this table contains this fields:
				- id (Integer): This field is an Integer that identifies the user, it is created automatically.
				- name (String): This field is the username of the user.
				- password (String): This field contains the password for the user, this password is encrypted when the user register into the system.
				- money (Double): This field contains the total money of the user.
		- #### Item
			- This class creates an entity in the data base called Item and its getters and setters, this table contains this fields:
				- id (Integer): This field is an Integer that identifies the item, it is created automatically.
				- name (String): This field is the name of the item, its a String.
				- description (String): This field contains a short description about what the item does.
				- code (String): This field contains the path of the file that contains the code of the item.
				- worldIP (String): This field contains the IP of the world where the item is executing its code.
				- username (String): This field contains the username of the user owner of the item.
				- imagePath (String): This field contains the path of the image used to show the item in the web page or in the inventory inside metapulse.
		- #### ItemForSale
			- This class creates an entity in the data base called ItemForSale and its getters and setters, this table contains this fields:
				- id (Long): This field is a Long that identifies the item for sale, it is created automatically.
				- description (String): This field contains a short description made by the user owner to sell the item.
				- price (double): This field its the price at which the item will be sold.
				- item (Item): This field contains the item that is going to be sold.
		- #### Trade
			- This class creates an entity in the data base called Trade and its getters and setters, this table contains this fields:
				- id (Integer): This field is an Integer that identifies the item for sale, it is created automatically.
				- user1 (User): This field contains one of the users related with the trade.
				- user2 (User): This field contains the other of the users related with the trade.
				- tradableMoneyUser1 (Double): This field contains the money that the user 1 wants to transfer.
				- tradableMoneyUser2 (Double): This field contains the money that the user 2 wants to transfer.
				- acceptedTradeUser1 (Boolean): This field contains a boolean that checks if the user 1 has accepted the trade.
				- acceptedTradeUser2 (Boolean): This field contains a boolean that checks if the user 2 has accepted the trade.
		- #### Chat
			- This class creates an entity in the data base called Chat and its getters and setters, this table contains this fields:
				- id (Integer): This field is an Integer that identifies the chat, it is created automatically.
		- #### Message
			- This class creates an entity in the data base called Message and its getters and setters, this table contains this fields:
				- id (Integer): This field is an Integer that identifies the message, it is created automatically.
				- content (String): This field contains the text of the message.
				- username (String): This field contains the username of the user that send the message.
				- chat (Chat): This field contains the chat to which the message belongs.
				  >>>>>>> 740a6b843194c6dca30ea4c5f33737dd9975e6eb
	- ### Repositories
	  collapsed:: true
		- The repositories in the API are to extend CRUD methods from the class CrudRepository to the entities class, the account server contains these three repositories:
			- UserRepository
			- ItemRepository
			- ItemForSaleRepository
			- TradeRepository
			- MessageRepository
			- ChatRepository
	- ### Controllers (API)
		- The controllers contains the endpoints of the API, the account server contains four controllers:
			- **MainController**: This controller primarily consists of helpful endpoints for developers to directly modify some data that cannot be altered through official endpoints. The endpoints located in this controller are:
				- `/demo/add`
					- Description: This endpoint is used to register an user, not recommended to use because there is a better endpoint in the AuthenticationController.
					- **Method**: Post
					- Parameters:
						- name (String): Username of the user.
						- password (String): Password of the user.
					- Response: If the parameters are correct this endpoint returns a string saying "Saved the user! <3".
				- `/demo/all`
					- Description: This endpoint is used to get all users in the database.
					- Method: Get
					- Parameters: None
					- Response: Returns all users in the database.
				- /demo/setMoney
					- Description: This endpoint is used to modify all users money manually.
					- Method: Put
					- Parameters: None
					- Response: Returns a string saying "All users have been updated with money 500".
				- /demo/addItem
					- Description: This endpoint is used to add an Item into the database.
					- Method: Post
					- Parameters:
						- name (String): Name of the item.
						- description (String): Description of the item.
						- code (String): Path of the code file of the item.
						- ip (String): IP of the world that is executing the code.
						- username (String): User that is going to own the item (need to be already registered)
						- imagePath (String): URL of the image of the item.
					- Response: If the parameters are correct this endpoint returns a string saying "Saved the item!", in case that the user owner isn't find the it returns "The user owner of the item doesn't exist", if there's another error then it returns "Unable to add the item".
				- /demo/allItems
					- Description: This endpoint is used to get all the items in the database.
					- Method: Get
					- Parameters: None
					- Response: Returns all items in the database.
				- /demo/allTrades
					- Description: This endpoint is used to get all the trades in the database.
					- Method: Get
					- Parameters: None
					- Response: Returns all trades in the database.
			- AuthenticationController: This controller primarily consists of endpoints used to create and authenticate a user. The endpoints located in this controller are:
			  collapsed:: true
				- /auth/register
					- Description: This endpoint is used to register a user in the database.
					- Method: Post
					- Parameters:
						- name (String): Username of the user.
						- password (String): Password of the user.
					- Response: If thereis no problem registering the user then this endpoint returns a string saying "User registered successfully", otherwise it would say "Unable to register user".
				- /auth/login
					- Description: This endpoint is used to login users with their credentials.
					- Method: Post
					- Parameters:
						- name (String): Username of the user.
						- password (String): Password of the user.
					- Response: If the credentials are correct then this endpoint returns a string with an autehntication token, otherwise it would return a string saying "Invalid username or password".
				- /auth/secure
					- Description: This is a test endpoint to prove the functionality of the token obtained with the login endpoint.
					- Method: Get
					- Parameters:
						- token (String) [Header]: Authentication token.
					- Response: If the token is correct then this endpoint would return a string with the username of the token owner, otherwise it would return a string saying "Invalid or expired token".
				- /auth/userInfo
					- Description: This endpoint is used to get the username and money of a user through its token.
					- Method: Get
					- Parameters:
						- token (String) [Header]: Authentication token.
					- Response: If the token is correct then this endpoint would return the name and the money of the user, otherwise it would return a string saying "Invalid or expired token".
			- ItemController: This controller contains an endpoint used to get all the items of a user. The endpoint located in this controller is:
			  collapsed:: true
				- /items/getItemUser
					- Description: This endpoint is used to get the items of a user.
					- Method: Post
					- Parameters:
						- name (String): Username of the user.
					- Response: If the username is incorrect then this endpoint return a string saying "This user doesn't exist", if the username is correct then it returns all the items information, in case theres a problem it would return a string saying "Unable to find items".
			- SalesController: This controller primarily consists of endpoints used in the purchase and sale of an item. The endpoints located in this controller are:
			  collapsed:: true
				- /sales/items
					- Description: This endpoint is used to get all items in sale.
					- Method: Get
					- Parameters: None
					- Response: This endpoint returns the information of all the items for sale.
				- /sales/items/{id}
					- Description: This endpoint is used to get an item through its id.
					- Method: Get
					- Parameters:
						- id (int) [Path variable "id"]: Id of the item is going to be displayed.
					- Response: This endpoint returns the information of the current item, if the id is incorrect then it would return a string saying "Item not found".
				- /sales/items
					- Description: This endpoint is used to put an item for sale.
					- Method: Post
					- Parameters:
						- item_id: Id of the item in sale.
						- price: Cost of the item.
						- description: Description of the item.
						- token (String) [Header]: Authentication token.
					- Response: This endpoint returns a string saying "Item added for sale successfully" if the process was done correctly, otherwise, if the token is incorrect it would say "Invalid or expired token", if the username doesn't match with the username of the item owner it would say "You are not the owner of the item", if there's another problem in the process it would say "Failed to add item for sale".
				- /sales/buy/{id}
					- Description: This endpoint is used to make the sale of an item.
					- Method: Post
					- Parameters:
						- id (int) [Path variable "id"]: Id of the item is going to be displayed.
						- token (String) [Header]: Authentication token.
					- Response: This endpoint returns a string saying "Item purchased successfully" if the process was done correctly, otherwise, if the token is incorrect it would say "Invalid or expired token", if the item is not found then it would say "Item not found or already sold", if there's another problem in the process it would say "Failed to buy item".
			- TradeController: This controller primarily consists of endpoints used in the trade of items and money between two users. The endpoints located in this controller are:
				- /trade/create
					- Description: This endpoint is used to add a trade into the database
					- Method: Post
					- Parameters:
						- user1Id (int): Id of one of the users related with the trade.
						- user2Id (int): Id of the other of the users related with the trade.
					- Response: This endpoint returns a string saying "Trade created successfully, id = " and the id of the trade if the process was done correctly, if at least one of the users isn't found then it would say "Some user does not exist".
				- /trade/tradeItem
					- Description: This endpoint is used to set an item like tradable.
					- Method: Post
					- Parameters:
						- itemId (int): Id of the item that is going to be set like tradable.
						- userId (int): Id of the user that wants to set the item like tradable.
					- Response: This endpoint returns a string saying "Item is tradable" if the process was done correctly, if the item is not found then it would say "The item does not exist", if the user is not found then it would say "The user does not exist",
				- /trade/tradeItems
					- Description: This endpoint is used to get all the items of the user 1 and 2 that are going to be trade.
					- Method: Get
					- Parameters:
						- tradeId (int): Id of the trade.
					- Response: This endpoint returns a string with the name of all the items of both users divided with a string like this "-----", if theres an error getting this info then it would return a string saying "Unable to find items".
				- /trade/tradeData
					- Description: This endpoint is used to get all the data of the trade, the items and the money that are going to be trade and also if the trade status of both users (If they have already accepted the trade).
					- Method: Get
					- Parameters:
						- tradeId (int): Id of the trade.
					- Response: This endpoint returns a string all the data of both users divided with a string like this "-----", if theres an error getting this info then it would return a string saying "Unable to find data".
				- /trade/tradeMoney
					- Description: This endpoint is used to set the money that is going to be trade.
					- Method: Post
					- Parameters:
						- money (Double): money that is going to be trade.
						- userId (int): Id of the user that wants to set its money to trade.
						- tradeId(int): Id of the trade.
					- Response: This endpoint returns a string saying "User 1 trade money updated" or "User 2 trade money updated", depending of what user is going to update its tradable money, if the user doesn't have that amount of money the string would say "The user doesn't have enough money", if the user is found but its not part of the trade the string would say "The user is not part of the trade" and if the user is not found it would say "The user does not exist".
				- /trade/execute
				- Description: This endpoint is used to execute the trade, exchanging tradable items and money between the users, after the execution the tarde is deleted from the database.
				- Method: Post
				- Parameters:
					- tradeId(int): Id of the trade.
					- userId (int): Id of the user that is trying to execute the trade.
				- Response: This endpoint returns a string saying "Trade executed successfully" if the process was done correctly and both acceptedTradeUser booleans are true, if both booleans aren't true then the string would say "Both users must accept the trade", if the user is found but its not part of the trade the string would say "The user is not part of the trade" and if theres is an error trying to executing the trade it would say "Unable to execute trade".
			- ChatController: This controller consist of the endpoints needed to create, end and get the messages, the endpoints are:
				- /chat/createChat
					- Description: The first thing you need to start chatting is to create a chat, this will generate and save in the database a chat
					- Method: Post
					- Parameters: This endpoint does not require any parameter.
					- Respones: The response is going to be the whole chat object, which only consists of the id.
				- /chat/sendMessage
					- Description: Creates a message.
					- Method: Post
					- Parameters
						- chatId (Integer): The id of the chat that owns this message.
						- content (String): The content that is going to be send.
					- Headers
						- Authentication (token): The token that confirms that a user is logged.
					- Response: Saved the Message! if okey, some other bad request responses if the token is invalid or if the chat is not found.
				- /chat/getMessages
					- Description: Fetch all the messages from a particular chat.
					- Method: GET.
					- Parameters:
						- chatId (integer): The chat whose messages we want to get.
					- Response: A List containing all the message objects that belongs to the chat.
	- **Seeders**
	  id:: 662a6627-09bc-43df-bb14-4076e748ac5c
		- Currently, there exists only one seeder for the database:
			- DatabaseSeeder.
				- This seeder will delete all the previous content of the database, and will create two new users "edson" and "angel", both having the password "12345", as well as three items, Red, Green, and Blue.
				- For safety, all the content in the "run" method is commented, in order to prevent the unintended deletion of the database if you did any changes.
				- If you want to use this, you need to delete the comment and run the server, the seed will be automatically planted, this means that **the seeder needs to be disabled manually**.
- ## CORS
	- Currently, you need to add the public ip of the webview client into CORS for item fetching.