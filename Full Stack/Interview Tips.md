
### Project Management

#### Deployment process

###### Waterfall model

project planning --> system analysis --> system design --> development & unit testing --> QA testing --> UAT --> production

#### Agile methodology

sprint: 3 weeks
user stories: features from user perspective

feature branch --> qa testing branch --> UAT branch --> production



#### Git merge vs. git rebase

- **Git merge**: git merge takes the contents of the feature branch and integrates it with the master branch.
- Git rebase: git rebase integrates a change from the base of the feature branch to the master branch’s endpoint.

---

### Backend
#### JWT parts
###### **Headers**

The header _typically_ consists of two parts: the type of the token, which is JWT, and the signing algorithm being used, such as HMAC SHA256 or RSA.

```json
{ "alg": "HS256", "typ": "JWT" }
```

###### **Claims**

- Registered claims
- Public claims
- Private claims

###### **Signature**

To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

For example if you want to use the HMAC SHA256 algorithm, the signature will be created in the following way:

```
HMACSHA256(
	base64UrlEncode(header) + "." + base64UrlEncode(payload),
	secret
)
```

The signature is used to verify the message wasn't changed along the way, and, in the case of tokens signed with a private key, it can also verify that the sender of the JWT is who it says it is.

---

### Frontend
Angular ([What is Angular? • Angular](https://angular.dev/overview))
Angular lifecycle hooks ([Lifecycle • Angular](https://angular.dev/guide/components/lifecycle))
