# Errors

The Meetupcall API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Params are missing or invalid.
401 | Unauthorized -- x-api-key header is missing or invalid.
404 | Not Found -- Could not find a Signup with that email address created with your API token.
409 | Conflict -- User already exists with specified email.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.