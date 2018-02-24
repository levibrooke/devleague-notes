Topic: User Authentication
Date: 2/12/18
***

## Authentication process
- Clients send a request to login to server.
- Server checks database for user credentials. 
- Credentials are stored in a new object and in a new session on the server.
- A cookie containing the hash id is sent back to the client for authentication.
- On a second request, the cookie gets sent and checked against the session contained on the server. No call to database is required.