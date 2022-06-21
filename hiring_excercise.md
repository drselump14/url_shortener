# URL Shortener Project

## Requirements

### Non-Functional Requirements

1. 1,000 daily users, 5-10 short-URL creations per day
2. 100,000 daily visitors, clicking the short URL links

### Functional Requirements

1. API for short URL creation, list, update and delete. No web interface
2. The full URL provided by the customer will always be shortened to an encoded value with our domain. Example: https://www.google.com to https://lin.ks/xCd5a
3. Shortened URLs must be unique for each customer
4. Duplicate shortened links for each customer are not allowed.
   If a customer attempts to create a new shortened link for a URL already existing,
   the existing shortened link will be provided (e.g., a link for https://www.google.com already exists.
   A customer tries to create a new link to the same place, and we return the existing short URL).
5. Reporting function (Total number of clicks, number of clicks by day, Total number of people who clicked links, Total number of people who clicked by day)


## Specs

### Architecture
### Generating encoded value for each url
The standard way would be using MD5 hashing and base32 like TinyURL.
However, this method has some disadvantages. One is we need to query the DB  to ensure the uniqueness of the key.
The other method uses a short unique ID generator with a tiny collision probability.
This way is simpler and faster than the previous method because we can skip the hashing, encoding, and uniqueness checking .
We use https://shortunique.id/ which can generate a unique ID which shorter than UUID but has tiny probability of collision.
Let's assume that we use 6 characters key, then using the shortunique.id library we can have 56 billions ID available.
With 1,000 daily users for 10 short-URL creation per day, we can generate unique ID for 15 thousands years.

Spec: use shortunique ID library to generate 6 characters unique key for each URL

### Storing the data
We need several data to stored for this service. user data, short-url data, and analytic data.
For user data we can use AWS Cognito

### Translating shortened url to fully url
### API Design
### User authentication for API
### Reporting function
### Scheduling
