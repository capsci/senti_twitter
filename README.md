# Twitter Sentiment Analysis

## Analyze real time tweets to extract sentiments based on love hate keywords.

* Used [Twitter’s streaming API](https://dev.twitter.com/streaming/public) to perform a basic sentiment analysis on the tweet stream. [ntwitter](https://www.npmjs.com/package/ntwitter) Node package was used to get tweet stream. API keys can obtained from [Twitter Developers website](http://apps.twitter.com). It is advisable to update your $HOME/.bashrc file as follows to store keys:
```
	export TWITTER_CONSUMER_KEY = your_key_from_twitter
	export TWITTER_CONSUMER_SECRET = your_secret_from_twitter
	export TWITTER_ACCESS_TOKEN = your_access_token_from_twitter
	export TWITTER_ACCESS_SECRET = your_access_secret_from_twitter
```

The environment variables can be accessed using Node, you can run following command to test: 

```
	node -e "console.log(process.env.TWITTER_CONSUMER_KEY)"
	node -e "console.log(process.env.TWITTER_CONSUMER_SECRET)"
```

Here is what program does on server-side and client-side

1. **Server**
	1. Retrives data from Twitter's streaming API:
		* Uses API keys to fetch tweets from twitter.
		* Stay tuned for more data(tweets) to become available for application.
	2. Extracts meaning from the data stream:
		* Subsribe from twitter to get only tweets that contain either ‘love’ or ‘hate’ words. Parse the data received in the JSON format.
		* Test that only tweets of interest are displayed on the server console.
	3. Push/emit the data to the web browser client:
		* Establishes the socket.io connection with the web client requesting the connection.
		* Emits information on user name and tweet text from every filtered tweet to the client as a JSON object.
	4. Analyzes the tweet streams:
		* Updates the summary statistics on
			1. the total number of tweets containing love or hate
			2. the total number of tweets containing love
			3. the total number of tweets containing hate.
		* Calculates the percentages for love and hate counts.
		* Keep the total as actual count.
		* Sends the above calculated three metrics to the client.
2. **Client**
	1. Establishes the socket.io connection with the server.
	2. Receive the tweets from the server.
	4. Receives updates from the server on the summary statistics about the love-hate sentiments on Twitter.
	5. Display the tweets and summary statistics on the webpage.
	6. Display the Love and Hate stats as percentages.

### How to run
Navigate to directory containing above code. Start the server using following command:
>  node app.js
In web browser, enter following URL to execute [localhost:3000/twitter_sentiment](http://localhost:3000/twitter_sentiment)