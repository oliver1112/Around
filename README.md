# Around
This is a Cloud and React based Social Network application. The backend is based on Golang and ElasticSearch. The frontend is based on ReactJS. 


## Backend
The backend complete code can be seen in the [backend folder](https://github.com/oliver1112/Around/tree/main/around-backend).

### Structure
I use Go to build a web service that has two main APIs: upload and search. The upload API allows users to submit a post which can include a message and a media file. The search API allows users to search other users' posts based on the user name or the keywords. I also created registration and login functions and used token-based authentication to protect my upload and search services.

The structure of golang backend is as follows:

<img src="https://github.com/oliver1112/Around/blob/main/assets/structure.png" alt="structure" width="1000"/>


The HTTP Router recieves HTTP from client, and then handle all kinds of responses on handler layer. Next, the service layer process the function and perform database operations on database layer.


### ElasticSearch and GCS
[Elasticsearch](https://www.elastic.co/elasticsearch) is an open-source, distributed, RESTful search engine.
I use Elasticsearch as a NoSQL database to store data posted by users. In addition, I create an inverted index for the message of each post so that I can provide a quick keyword-based search for my users.


[Google Cloud Storage](https://cloud.google.com/storage/docs/) is a Powerful, Simple and Cost-effective Object Storage Service. 

I use GCS to store all media files posted by users because database is not good for storing a binary media files like images or videos. The corresponding link of each media file is stored as metadata in Elasticsearch.

### Authentication and Authorization
I implement Authentication and Authorization with JSON Web Token(JWT).

The principle of token-based authentication:
1. A user enters their login credentials (=username + password).
2. The server verifies the credentials are correct and created an encrypted and signed token with a private key ( { username: “abcd”, exp: “2021/1/1/10:00” }, private key => token).
3. Client-side stores the token returned from the server.
4. On subsequent requests, the token is decoded with the same private key and if valid the request is processed.
5. Once a user logs out, the token is destroyed client-side, no interaction with the server is necessary.


## Frontend

The complete code of the frontend can be seen in the [frontend folder](https://github.com/oliver1112/Around/tree/main/frontend).
### Structure
