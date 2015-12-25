#	OPEN AUTHORIZATION


####OAUTH:

	OAuth (Open Authorization) is an open standard for token-based authentication and authorization on the Internet.
	
	It  allows a third-party website or application to access a user’s data without the user needing to share login credentials.

	OAuth's open-source protocol enables users to share their data and resources stored on one site with another site under a secure authorization scheme based on a token-based authorization mechanism. OAuth is also known as OAuth Core.
	
	It allows an end user's account information to be used by third-party services, such as Facebook, without exposing the user's password. OAuth acts as an intermediary on behalf of the end user, providing the service with an access token that authorizes specific account information to be shared. The process for obtaining the token is called a flow.

	OAuth allows notifying a resource provider (e.g. Facebook) that the resource owner (e.g. you) grants permission to a third-party (e.g. a Facebook Application) access to their information (e.g. the list of your friends).

	OAuth allows for:

	Different access levels: read-only VS read-write. This allows you to grant access to your user list or a bi-directional access to automatically synchronize your new LinkedIn friends to your GMail contacts.

	Access granularity: you can decide to grant access to only your contact information (uername, e-mail, date of birth, etc.) or to your entire list of friends, calendar and what not.
	
	It allows you manage access from the resource provider's application. If the third-party application does not provide mechanism for cancelling access, you would be stuck with them having access to your information. With OAuth, there is provision for revoking access at any time.

**How it works?**

	OAuth is a way for applications to gain credentials to your information without directly getting your user login information to some website. 
	
	For example if you write an application on your own website and want it to use data from a user's facebook account, you can use OAuth to get a token via a callback url and then use that token to make calls to the facebook API to get their use data until the token expires.
	
	Websites rely on it because it allows programmers to access their data without the user having to directly disclose their information and spread their credentials around online but still provide a level of protection to the data.

**Why oauth is used?**

	OAuth1 (more precisely HMAC) requests seem logical, easy to understand, easy to develop and really, really secure.

	OAuth2, instead, brings authorization requests, access tokens and refresh tokens, and you have to make 3 requests at the very start of a session to get the data you're after. And even then, one of your requests will eventually end up failing when the token expires.

	And to get another access token, you use a refresh token that was passed at the same time as the access token.

####BENEFITS OF OAUTH:

*Simplicity*

	From an implementor's perspective, the main advantage is it reduces complexity. It doesn't require the request signing procedure, which is not exactly difficult but is certainly fiddly. It greatly reduces the work required to act as a client of a service, which is where (in the modern, mobile world) we most want to minimize pain. The reduced complexity on the server->content provider end makes it more scalable in the datacenter.

	OAuth1 (more precisely HMAC) requests seem logical, easy to understand, easy to develop and really, really secure.

	OAuth2, instead, brings authorization requests, access tokens and refresh tokens, and you have to make 3 requests at the very start of a session to get the data you're after. And even then, one of your requests will eventually end up failing when the token expires.

	And to get another access token, you use a refresh token that was passed at the same time as the access token.

	 We can use the same login for web as well as native(mobile) apps
	 
	 We don't have to save session information on the server
	 
	 We can easily set expiry date in token itself

####FEATURES:

	Supports the following OAuth flows via the google-oauth-java-client library:
	
		1.OAuth 1.0a
		2.OAuth 2.0 Explicit Authorization (authorization code)
		3.OAuth 2.0 Implicit Authorization
	
	Automatically handles the OAuth flow in both android.app.DialogFragment and android.support.v4.app.DialogFragment. The dialog UI is fully customizable.
	
	Provides an out-of-the-box credential store implementation via SharedPreferences.
	
	Provides sample applications that already work with popular social network services such as:
	
		Flickr
		Foursquare
		GitHub
		Instagram
		LinkedIn
		Plurk
		Twitter
	
	In general we should prefer OAuth 2.0 Implicit Authorization over OAuth 2.0 Explicit Authorization because implicit authorization does not require the client secret to be stored in the client.

####SOLUTION AND IMPLEMENTATION:

	 The android-oauth-client library can be used in 2 simple steps:

	1. Obtain an instance of OAuthManager by supplying the following 2 parameters:
	
	 An AuthorizationFlow instance which automatically handles the OAuth flow logic,
	 An AuthorizationUIController which manages the UI.
	
	2. Call one of the 3 possible authorize methods on OAuthManager. The call may be called from any thread either synchronously or asynchronously with an OAuthCallback<Credential>.
	 
	 OAuthManager.authorize10a()
	 OAuthManager.authorizeExplicitly()
	 OAuthManager.authorizeImplicitly()

*Obtaining an OAuthManager instance*

	OAuthManager can be obtained by direct instantiation:

		OAuthManager oauth = new OAuthManager(flow, controller);
	
*Obtaining an access token via the OAuthManager*

	To start the OAuth flow and obtain an access token, call one of the authorize() methods according to the authorization flow of your choice.

	You may invoke the authorize() method synchronously:

	Credential credential = oauth.authorizeImplicitly("userId", null, null).getResult();
	// continue to make API queries with credential.getAccessToken()
	We may also invoke the authorize() method asynchronously with an OAuthCallback, executed on a android.os.Handler of your choice.

	OAuthCallback<Credential> callback = new OAuthCallback<Credential>() {
	    
	    @Override 
	    public void run(OAuthFuture<Credential> future) {
	           Credential credential = future.getResult();
		   // make API queries with credential.getAccessToken()
		}
	};
		oauth.authorizeImplicitly("userId", callback, handler);
				
		Note that if a Handler is not supplied, the callback will be invoked on the main thread.

*CredentialStore*

	Use the provided SharedPreferencesCredentialStore, which automatically serializes access tokens to and from SharedPreferences in JSON format.

		SharedPreferencesCredentialStore credentialStore =
			new SharedPreferencesCredentialStore(context, 
				            "preferenceFileName", new JacksonFactory());
*AuthorizationFlow*

	An AuthorizationFlow instance may be obtained via its Builder:

		AuthorizationFlow.Builder builder = new AuthorizationFlow.Builder(
					        BearerToken.authorizationHeaderAccessMethod(),
        	AndroidHttp.newCompatibleTransport(),
				new JacksonFactory(),
					new GenericUrl("https://socialservice.com/oauth2/access_token"),
					new ClientParametersAuthentication("CLIENT_ID", "CLIENT_SECRET"),
						"CLIENT_ID", "https://socialservice.com/oauth2/authorize");
						 builder.setCredentialStore(credentialStore);
						 AuthorizationFlow flow = builder.build();
									
	For OAuth 2.0 flows, you may wish to add OAuth scopes:

		builder.setScopes(Arrays.asList("scope1", "scope2"));
		
	For the OAuth 1.0a flow, you need to set the temporary token request URL:

		builder.setTemporaryTokenRequestUrl("https://socialservice.com/oauth/requestToken");
		
	Note that CLIENT_SECRET may be omitted and be replaced with a null value for the OAuth 2.0 Implicit Authorization flow.

	Also, CLIENT_ID and CLIENT_SECRET are called CONSUMER_KEY and CONSUMER_SECRET in the OAuth 1.0a flow.

*AuthorizationUIController*
						
	Use the provided DialogFragmentController, which automatically handles most of the UI for you via an Android dialog.
			
	The DialogFragmentController has two constructors, one taking android.app.FragmentManager and the other taking android.support.v4.app.FragmentManager as the sole input parameter. 
	
	Depending on how you instantiate the controller, either android.app.DialogFragment or android.support.v4.app.DialogFragment will be used.

		AuthorizationUIController controller = new DialogFragmentController(getFragmentManager()) {

		@Override
			public String getRedirectUri() throws IOException {
				return "http://localhost/Callback";}

			@Override
			public boolean isJavascriptEnabledForWebView() {
				return true;
			     }
			};
																		        


