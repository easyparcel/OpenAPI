### Steps to get OAuth Authorization Access token

#### [More details on Oauth](Oauth%20Authentication.md) | [Steps to get started with EASY PARCEL API](../Get%20started%20with%20EASY%20PARCEL%20OPEN%20API.md)
1.) Pass the below params to the urls
`https://developer.easyparcel.com/ep_auth/login`

Request:
- client_id
- redirect_uri
- state (optional)

| **Requested Parameters** | **Type** | **Required** | **Details**                                                                                                                   |
| ------------------------ | -------- | ------------ | ----------------------------------------------------------------------------------------------------------------------------- |
| client_id                | string   | Yes          | client_id of your application                                                                                                 |
| redirect_uri             | string   | Yes          | The URI to which the client was redirected from the authorization server. The url of your app to redirect to                  |
| state                    | string   | Optional     | Generate and pass a unique string that helps ensure the response comes from the same client request, preventing CSRF attacks. |

2.) Will be prompt to login (these below steps are to authorize linking the application to your easyparcel account)
1. Login to your easyparcel account
   
		
	![Login%20Page.png](../pictures/Login%20Page.png)

2. Select an account desire to link
   
		
   	![select account](../pictures/select%20account.png)


3.  Allow access to Authorize link the account to with the application
   
		
	 ![allow access.png](../pictures/allow%20access.png)


2.) Respond param in redirect url
Sample redirect url respond: 
`https://your-callback-url/callback?code=(code that requires to regenerate access token)`
- code(pass in get access token url)
- state (if got pass in auth url request)

| Responded Parameters | Type   | Required | Details                                                                                           |
|----------------------|--------|----------|---------------------------------------------------------------------------------------------------|
| Code                 | string | Yes      | The authorization code to pass to ep_auth to get the access token.                                |
| state                | string | (depend if got request on auth url) | A unique string that helps ensure the response comes from the same client request, preventing CSRF attacks. |



3.) Pass the below params to get access token url or refresh access token url
`https://developer.easyparcel.com/ep_auth/token`

Request:
- grant_type = “authorization_code”
- redirect_uri
- code
- refresh_token (if want refresh access token)
- state (optional)

| Requested Parameters | Type   | Required                              | Details                                                                                                 |
|----------------------|--------|---------------------------------------|---------------------------------------------------------------------------------------------------------|
| grant_type           | string | Yes                                   | The authorization_code to generate the access token.                                                    |
| redirect_uri code    | string | Yes                                   | The URI to which the client was redirected from the authorization server. The URL of your app to redirect to. |
| refresh_token        | string | (if want to refresh access token)     | The token that requests to generate a new access token once the current token expires. |
| state                | string | Optional                              | Request to check the state. A unique string that helps ensure the response comes from the same client request, preventing CSRF attacks. |


4.) then will respond back with the access_token

```
{
	"token_type": "Bearer",
	"expires_in": 36000,
	"expires_at": "2024-12-12T13:03:23.013Z",
	"access_token": "your access token",
	"refresh_token": "Your refresh token",
	"refresh_token_expires_in": 31557600,
	"refresh_token_expires_at": "2025-12-12T09:03:23.013Z",
	
	"app": {
	"client_id": "your client-id",
	"callbackUrls": [],
	"redirectUris": [ "Your redirect uri"]
	}
}
```

L1 Respond

| Responded Parameters     | Type      | Details                                                                            |
| ------------------------ | --------- | ---------------------------------------------------------------------------------- |
| token_type               | string    | Token type                                                                         |
| expires_in               | int       | The token life span in seconds                                                     |
| expires_at               | date time | The Access token expiry date                                                       |
| access Token             | string    | The access token, required to access the API                                       |
| refresh_token            | string    | The new Refresh token for the next refresh (Depends if requested on ep_auth/token) |
| refresh_token_expires_in | int       | The refresh token life span in seconds                                             |
| refresh_token_expires_at | date time | The refresh token expiry date                                                      |
| App                      | array     | Refer to [L2 (App)](#App)                                                          |

L2 Respond
(**App**)
##### App

| Responded Parameters | Type   | Details                                                                               |
| -------------------- | ------ | ------------------------------------------------------------------------------------- |
| client_id            | string | Client ID of the application                                                          |
| callbackUris         | string | Destination that sends the user back after they have authenticated and granted access |
| redirectUris         | string | Redirect destination for the user after the authorization process                     |

5.) Use the access token to call the api