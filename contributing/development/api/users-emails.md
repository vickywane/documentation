# Users / Emails

## Get list of Collective users and emails

First, get the token of a user who is an admin \(core contributor\) of a collective. After logging in, run this in the inspector: `copy(window.localStorage.accessToken)`. This will copy in you clipboard the access token for the current user.

Then you can run the following query with the token in the header:

```text
curl -H "Authorization: Bearer [accessToken]" https://opencollective.com/api/groups/:collective/users
```

E.g. with the apitestuser:

```text
curl -H "Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzY29wZSI6ImxvZ2luIiwiaWQiOjM5MzksImVtYWlsIjoiYXBpK3Rlc3R1c2VyQG9wZW5jb2xsZWN0aXZlLmNvbSIsImlhdCI6MTUwNzQ0NTg3OSwiZXhwIjoxNTEwMDM3ODc5LCJpc3MiOiJodHRwczovL2FwaS5vcGVuY29sbGVjdGl2ZS5jb20iLCJzdWIiOjM5Mzl9.sXyQvrOPPEnOoMAho_6_KtIGVwunAIK3_y9WRbyhNmI" https://opencollective.com/api/groups/testcollective/users
```

This will return:

```text
[
  {
    "id": 3939,
    "createdAt": "2017-04-02T00:00:00.000Z",
    "name": "API test user",
    "firstName": "API",
    "lastName": "test user",
    "username": "apitestuser",
    "role": "MEMBER",
    "avatar": null,
    "website": null,
    "email": "api+testuser@opencollective.com",
    "twitterHandle": null,
    "totalDonations": null,
    "firstDonation": null,
    "lastDonation": null,
    "tier": "core contributor"
  },
  {
    ...
  }
]
```

