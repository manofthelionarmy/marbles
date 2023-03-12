<iframe width="560" height="315" src="https://www.youtube.com/embed/t18YB3xDfXI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
[Open Id Connect](https://auth0.com/intro-to-iam/what-is-openid-connect-oidc#!)
^ this article makes more sense after watching all videos
<iframe width="560" height="315" src="https://www.youtube.com/embed/rTzlF-U9Y6Y?start=705" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
^ starts later, gives a better reason as to why we need OIDC. It seems like oauth2 was being misused and some implementations were using it for authentication.
<iframe width="560" height="315" src="https://www.youtube.com/embed/VI3G4Quzsb8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Summary:
- This video beatifully gives an example of the oauth2 auth flow in a high level way from a general end user's perspective without using the jargon (or domain language in oauth).
- They then cover all of the terminology in a very simple way.
- They then go over the example again and apply the terminology to explain how the flow works.
- The Oauth2 flow allows a client (third party application) to get an access token. This token can be used to get resources from the resource server, but it is scoped. By that, I mean the client only has specific permissions to specific resources.
- Though we have an access token, authentication is missing. OpenID Connect (OIDC) is a thin layer that works on top of Oauth2.0 and cannot work without it. This transforms the authorization server into an identify provider, and instead of it giving an access token to the client, it gives something more like a badge. This badge provides the same granular, scoped permissions as an access token and it contains minimum information about the resource owner, also known as identity.
- Oauth2 Auth Flow enables authorization from one app to another, OIDC enables login sessions for clients.
- This enables scenarios where one login can be used across mutliple applications.
# Related Stuff:
[[PCKE - Oauth]]
# Notes
- Resource owner - me, I own the resources (contacts, data, etc) in an application.
- Client - the third party application that wants granular access to my resources made available by an applications api. The third party application acts like a client in the client-server model later on in the flow (the client is communicated with authorization and resource server).
- Authorization server: the server the resource owner logins in to verify it us (authentication). We then provide permission for which resources a client can have access too. The authorization server will then redirect to the client (the client is an application with their own server, and the redirect uri is pretty much a web hook on the clients server).
- Resource server is the api server.
- Redirect uri: this is the where the resource owner is redirected to when they grant access of resources to the client. This redirect uri is an api route handled by the client application. The redirect uri is used as a query parameter when the user is granting access to the resources.
- Scope - the granular level of permissions for specific resources a resource owner will permit a client to have access to.
- Client id and client secret: the client id is what the authorization server will use to identify a client (third party application). Normally, the client will register with the application that owns the resource server and will get a client id and secret key. The secret key acts like a assigned password for the client.
- Authorization code: a temporary code that will be used by the client to make an exchange with the authorization server. The client gives the authorization server the auth code while the authorization server gives it the access token (only if the auth code is valid).
- Access token: the token a client can use to communicate with the resource server. When the client makes calls to the resource server's api, it will check if the access token is valid. Once it is proven valid, the client has access to only the permitted resources/scopes.
- After the resource owner authenticates and grants permissions to the listed scopes in the browser, the authorization server will then use the redirect uri to make an api call to the client's server (the redirect uri is a route that the client handles on its server). The client server will handle the call via it's route handler and in the request is a authorization code. The client will then exchange the authorization code with the auth server for an access token.
- Voila, this is the auth flow.
## OpenId and where it fits in Oauth2.0 Auth Flow
- Although we do login in during the flow, in the end the client gets an access token making it authorized and have permissions to scoped resources. This token has no information regarding who you are, meaning the client service can't verify the identity of the resource owner. Thus, how can the client prove that it is acting on someone's obehalf apart from already getting the token?
- OpenID Connect (OIDC) is a small layer that works on top of Oauth2.0 and adds capabilities for login as well as providing non-harmful personal information about the user who is logged in.
- Instead of a client receiving an access token, OpenID is like a identity badge given to the client. Not only does this badge give the client specific permissions (same permissions from the access tokne), it gives the client mininum info about who the user is. The badge is given to the client by the authorization server. 
- It is said an authorization server that gives the client this bade is an identity provider.
- Oauth2.0 Flow allows enables an application to be authorized from one app to another, OIDC allows a client to establish a login session via the badge provided.
- Terminology:
	- Identity: information about the resource owner and this information is made available to the client via the badge it receives from the identity provider.
- An analogy is that we need to make a withdrawl from the ATM and we used a credit/debit card. The debit card has minimal information about who we are, and this information is needed to prove who we are, as well as permit the atm to have access to banking information (our statements). However, the ATM cannot really work without the underlying banking infrastructure.
- From the analogy, OIDC cannot work standalone and we need infrastructure provided by oauth2.0 already.
- OIDC enalbes scenarios where one login can be used across multiple applications, also known as single sign on, or SSO.
## 2023-02-26:
- UPDATE: I got some help from Stuart with this and I believe I understand OpenID Connect. 
- The capability of having one login session for multiple apps is this case:
	- You recall how I can create a new application for a website via google/facebook/microsoft. If I create an account with google (identity provider) for that app (the client), then the client will  be able to get personal info about me with my consent (as is the process in order to create the account in the first place). That client (third party app) is registered with the google openid connect provider. This enables an ecosystem of applications to be accessible from one login. All thanks to the fact that OpenID connect is built ontop of Oauth2.0 auth flow and the infrastructure exists because of Oauth2.0.
	- The client app will use my info for the account details it needs in order to have an account.
- To prove this:
	- I signed into my google account, and in the `Privacy and Data` section, I was able to see all of the applications I have created an account with via the Google Openid Connect Provider. I was able to remove one of them too (for exmaple, I removed Udemy as an account for Google, hopefully Udemy updates this on their end in their database).