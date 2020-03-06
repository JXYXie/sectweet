![](https://github.com/Cisco-AMP/sectweet/workflows/Java%20CI/badge.svg)

# SecTweet
SecTweet is a Flink job that streams Twitter posts.  Relevent text containing shas, file paths, etc, are aggregated 
and trends are determined based on the frequency of these terms over time.  

For the Flink workshop, please follow the steps [here](https://github.com/Cisco-AMP/sectweet/wiki/Workshop) instead.

## Requirements
Java 8

## Services Setup
Services: Flink, Elasticsearch Kibana (Optional)

To start all containers:  
``` runDockerContainers.sh ```

To start a specific container:  
``` docker-compose up <flink-jm | flink-tm | elasticsearch | kibana> ```

## Build
To build the project:  
```./gradlew clean build```  

## Running SecTweet
**Arguments**:  
To read live Twitter data using Twitter API:  
```--twitter-source.consumerKey <key> --twitter-source.consumerSecret <secret> twitter-source.token <token> --twitter-source.tokenSecret <tokenSecret>```

One can also provide a list of Twitter IDs and/or terms(hashtags) for Sectweet to subscribe to:  
```--twitter-source-ids <ID1>,<ID2>,... --twitter-source-terms <#Term1>,<#Term2>,...```

To read tweets from a file:  
```--file-source <twitter data file>```  
Note: there are test files available under ./data.  Simply unzip them to use in sectweet.                        

To write to ElasticSearch:  
```--write-es```

To Tweet what is trending:  
```--write-twitter```

To run the project with embedded Flink:  
```./gradlew run --args='<flink args here>'```

## Packaging
To package your job for submission to Flink, use: 
```gradle shadowJar```  
Afterwards, you'll find the
jar to use in the 'build/libs' folder.

