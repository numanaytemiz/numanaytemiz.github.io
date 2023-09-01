## Leaky API

- Closely observer the HTTP reponse to view profile requets.
- We should see passwords are sent back to the client in clear text.
- We should never send passwords in HTTP responses - API Data Leaks

![Image](/img/responsespass.png)

## Storing Passwords in Clear Text

- We discovered that passwords are sent in HTTP response.
- This discloses another crittical vulnerability - passwords are stored in clear text on the server side.
