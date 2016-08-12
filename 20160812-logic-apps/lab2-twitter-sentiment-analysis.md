#Lab 2 - Twitter Sentiment Analysis
In this lab we will use the twitter connector, and also an API from the Microsoft cognetive services

The challenge is to setup a workflow that does the following: 

1) Triggers on messages from Twitter (require that you have Twitter Account to set this up). You should listen to certain tags, take something that have lot of traffic, e.g. `#Microsoft`
2) Send the twitter body text to the Microsoft Text Cognetive Service, to do Sentiment Analytics of the tweet, for help on getting started: https://azure.microsoft.com/en-us/documentation/articles/cognitive-services-text-analytics-quick-start/ 
3) Store tweet and its sentiment score when the sentiment score is above a threshold e.g 0.5 to blob storage
