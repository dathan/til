# Purpose

Learn and retain the details about common auth methods used in mutiple protocols. Specifically Oauth 2.0 and JWT

<p>Started `2020-10-08 11:00:00`</p>


## SUMMARY

OAUTH is an authorization (AUTHZ) frame work with an AUTHN component. JWT is an authentication (AUTHN) framework which is url safe for passing around session information, or object information in a common format. If sharing an applications data use OAUTH 2.0 format. There are RFCs that bridge both formats together. Additionally JWT replaces SAML which is an XML based format for AUTH sharing.




## QUESTIONS

    * Why are their so many formats?
    * How do you bridge multiple technologies together?
    * What are the security concerns?
    




## LEARNING

* Oauth allows to build authorization services because the data request is authorizied due to permissions given by the data owner through a client_id and token while keeping the username and password confidential.

* [Oauth 2.0 is an authorization framework](https://tools.ietf.org/html/rfc6749) `AUTHZ`

* authoriziation layer and seperating the role of the client from the resource ownership solves a lot of issues such as sharing passwords with third-parties: Duh

* uses a token to access the data. a string denoting a
   specific scope, lifetime, and other access attributes

* `Roles`
    * resource owner: entity able to give access to a protected resource
    * resource server: the server hosting the protected resource, capable of of accepting and responding to protected resource requests using access tokens.
    * client: The application making resource requests on behalf of the resource owner with their authoriziation
    * authorization server: The server issuing access tokens to the client after successfully authenticating the resource owner and obtaining authorization.

* `Protocol Flow`
```
     +--------+                               +---------------+
     |        |--(A)- Authorization Request ->|   Resource    |
     |        |                               |     Owner     |
     |        |<-(B)-- Authorization Grant ---|               |
     |        |                               +---------------+
     |        |
     |        |                               +---------------+
     |        |--(C)-- Authorization Grant -->| Authorization |
     | Client |                               |     Server    |
     |        |<-(D)----- Access Token -------|               |
     |        |                               +---------------+
     |        |
     |        |                               +---------------+
     |        |--(E)----- Access Token ------>|    Resource   |
     |        |                               |     Server    |
     |        |<-(F)--- Protected Resource ---|               |
     +--------+                               +---------------+
```

* Authorization Grant: credential representing the resource owner's authorization
* Authorization Code: directs the owner to the authorization server, the code is sent back to the client to verify the request to exchange for the access token
* Access Token: are credentials used to access protected resources
* Refresh tokens: are credentials used to obtain access tokens, when access token time is up

```
 +--------+                                           +---------------+
  |        |--(A)------- Authorization Grant --------->|               |
  |        |                                           |               |
  |        |<-(B)----------- Access Token -------------|               |
  |        |               & Refresh Token             |               |
  |        |                                           |               |
  |        |                            +----------+   |               |
  |        |--(C)---- Access Token ---->|          |   |               |
  |        |                            |          |   |               |
  |        |<-(D)- Protected Resource --| Resource |   | Authorization |
  | Client |                            |  Server  |   |     Server    |
  |        |--(E)---- Access Token ---->|          |   |               |
  |        |                            |          |   |               |
  |        |<-(F)- Invalid Token Error -|          |   |               |
  |        |                            +----------+   |               |
  |        |                                           |               |
  |        |--(G)----------- Refresh Token ----------->|               |
  |        |                                           |               |
  |        |<-(H)----------- Access Token -------------|               |
  +--------+           & Optional Refresh Token        +---------------+
```


* Authorization Code Grant
```  
     +----------+
     | Resource |
     |   Owner  |
     |          |
     +----------+
          ^
          |
         (B)
     +----|-----+          Client Identifier      +---------------+
     |         -+----(A)-- & Redirection URI ---->|               |
     |  User-   |                                 | Authorization |
     |  Agent  -+----(B)-- User authenticates --->|     Server    |
     |          |                                 |               |
     |         -+----(C)-- Authorization Code ---<|               |
     +-|----|---+                                 +---------------+
       |    |                                         ^      v
      (A)  (C)                                        |      |
       |    |                                         |      |
       ^    v                                         |      |
     +---------+                                      |      |
     |         |>---(D)-- Authorization Code ---------'      |
     |  Client |          & Redirection URI                  |
     |         |                                             |
     |         |<---(E)----- Access Token -------------------'
     +---------+       (w/ Optional Refresh Token)

   Note: The lines illustrating steps (A), (B), and (C) are broken into
   two parts as they pass through the user-agent.

```


* Error responses `invalid_request`,`unauthorized_client`,`access_denied`,`unsupported_response_type`,`invalid_scope`,`server_error`,`temporarily_unavailable`


* support for username/password authentication authorization flow, which is not cool IMHO

### JWT - AUTHN (AUTHENTICATION)

* Common flow to authenticate a user with a username and password.
* [RFC7519](https://tools.ietf.org/html/rfc7519)
* JSON Web Token (JWT)
     > A string representing a set of claims as a JSON object that is encoded in a JWS or JWE, enabling the claims to be digitally signed or MACed and/or encrypted.
* Claim
     > A piece of information asserted about a subject.  A claim is represented as a name/value pair consisting of a Claim Name and a Claim Value.

* Register claim Names
    > `"iss" (Issuer) Claim` <br/> 
    > `"sub" (Subject) Claim` <br/> 
    > `"aud" (Audience) Claim` <br/> 
    > `"exp" (Expiration Time) Claim` <br/> 
    > `"nbf" (Not Before) Claim` <br/>
    > `"iat" (Issued At) Claim` <br/>
    > `"jti" (JWT ID) Claim` <br/>
    > `"typ" (Type) Header Parameter` <br/>
    > `"cty" (Content Type) Header Parameter` <br/>

## MINDDUMP (Random thoughts to keep focus on learning)

* OAuth 2.0 SPEC released in 2012
* Learned this multiple times but keep forgetting
* OAuth 2.0 is great for when exposing your REST, GRPC API ENDPOINTS to thirdparty clients

