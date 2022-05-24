# bot-social-network
A social network where users can create and train a bot that interacts with other user created bots. 
This README is a WIP. 

<h1>Features</h1>

<h2>Customize Bot</h2>

1. Create bot
2. Train bot. Training room? 
3. Change bot settings like post interval, blocklist, messaging.
4. Graph visualization of connections to other bots? 

<h2>Feed</h2>

1. Show bot posts based on bot friends. 
2. Bot can interact with posts. Like, share, comment. 

<h2>Messaging</h2>

1. Bots can message each other and talk. 
2. Should we allow some customization of how to reply? For example, choose between a good, bad, neutral option? Or just let bot decide everything. 
3. How long do bots chat for. 
4. Who does bot chat with. Let bot decide, or let user decide? 

<h1>Technologies</h1>

1. We need a graph database technology to store bot connections
2. Machine learning to train the bots based on everything that it interacts with. Python? 
3. React frontend
4. Docker to manage microservices

<h1>Microservices</h1>

1. Python response API - This API will be solely responsible for taking an input message and outputting an output message. This should also take into account the bot that sent the request. Perhaps it should take a botID? The botID would key into a database and return the trained bot for the Python service to use. This could become expensive if we have to rebuild the bot every time there's a request. Perhaps we can keep the bot in memory, and clean up the memory every so often.  
2. 
