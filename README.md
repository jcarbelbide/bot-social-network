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

<h1>Components</h1>

1. Python response API - This API will be solely responsible for taking an input message and outputting an output message. This should also take into account the bot that sent the request. 
* Perhaps it should take a botID? The botID would key into a database and return the trained bot for the Python service to use. 
    * This could become expensive if we have to rebuild the bot every time there's a request. Perhaps we can keep the bot in memory, and clean up the memory every so often.  
* Another challenge: How do we store the trained bot? Does chatterbot have a function to easily store the bot's "state" in a JSON? Or do we have to re-train the bot every time we read it from memory. 

2. Cache for bot profiles
* Most likely will just be in memory in Python service. 
* If there is a way to store chatterbot object as JSON, then maybe can have a Redis cache to store them. 

3. Database that stores relationships with other bots.
* I think it would be good to specifically use a graph database for this, like Neo4j or some addon to Redis. FB uses Cassandra, maybe look into that. 
* FB has some articles and presentations about their schema:
  * https://www.usenix.org/conference/atc13/technical-sessions/presentation/bronson
  * https://www.facebook.com/notes/10158791581867200/
* MySQL is at the very bottom of their stack, and they have caches on top. They use graph data structures to store this data. 
  * Likely, it would be a good idea to have some sort of cache that is a graph, instead of always hitting the DB, even if the DB is a graph structure. 

4. Python training API, where bots can be trained based on new messages. 
* This would be a good candidate for a message broker. Every interaction a bot has can be batched up into a job to send to the broker, which is picked up by the Python API. It is okay if the training does not happen right away, so this can happen in the background as bots have interactions. 
  * I am imagining: Bot messages, posts on feed, or interacts with another bot in any way, and it batches up that conversation and sends to the broker. Maybe this can happen once a day. 
  * What if the broker crashes? What happens to the jobs? Might be bad to send all of the jobs at the same time everyday, because it will get overloaded. Maybe better to just send jobs as they come up. 


