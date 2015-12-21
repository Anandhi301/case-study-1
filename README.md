# case-study

#	SESSION BASED AUTHENTICATION

###**AUTHENTICATION:**
	
	The process of identifying an individual,usually based on a username and password. Authentication merely ensures that the individual is who he or she claims to be, but says nothing about the access rights of the individual. 
	It is a process that ensures and confirms a user’s identity. Authentication is one of the five pillars of information assurance (IA). The other four are integrity, availability, confidentiality and nonrepudiation.
	Authentication begins when a user tries to access information. First, the user must prove his access rights and identity. When logging into a computer, users commonly enter usernames and passwords for authentication purposes. This login combination, which must be assigned to each user, authenticates access. However, this type of authentication can be circumvented by hackers.
	A better form of authentication, biometrics, depends on the user’s presence and biological makeup (i.e., retina or fingerprints). This technology makes it more difficult for hackers to break into computer systems.

	The Public Key Infrastructure (PKI) authentication method uses digital certificates to prove a user’s identity. There are other authentication tools, too, such as key cards and USB tokens. One of the greatest authentication threats occurs with email, where authenticity is often difficult to verify. For example, unsecured emails often appear legitimate.

###**SESSION BASED AUTHENTICATION:**
	
	In Session-based Authentication the Server does all the heavy lifting server-side. Broadly speaking a client authenticates with its credentials and receives a session_id (which can be stored in a cookie) and attaches this to every subsequent outgoing request.
	So this could be considered a "token" as it is the equivalent of a set of credentials. There is however nothing fancy about this session_id-String. 
	It is just an identifier and the server does everything else. It is stateful. It associates the identifier with a user account (e.g. in memory or in a database). 
	It can restrict or limit this session to certain operations or a certain time period and can invalidate it if there are security concern and more importantly it can do and change all of this on the fly.
	Furthermore it can log the users every move on the website(s). Possible disadvantages are bad scale-ability (especially over more than one server farm) and extensive memory usage
	
	In case of session based authentication
	  •	User submits a login request sending their credentials
	  •	The credentials are checked against a database
	  •	A session id is generated and is also stored in a db
	  •	Cookie will be set with the user details and a generated session id
	  •	Subsequent calls will compare the session id against the one in the database
	  •	The db is hit every time
###**FEATURES:**
	
	Name-and-password authentication sends the client's name and unencrypted password, and is sent with each request to the server.
	Session-based authentication differs in that the user's name and password information is sent over the network only the first time the user logs in to a server, not each time a request is posted.
	After login, the user's name and logon information is stored in a cookie in the user's browser, and the browser sends the cookie to the server with each request. 
	Before honoring a request, the server verifies the information in the cookie and uses the cookie contents to identify the logged-in user. 
	The session is only valid within the browser in which the login was performed. If the user shuts down the browser in which the session login took place, the user's session will be ended and the cookie will be destroyed.

###**BENEFITS:**
	 
	 Using session-based name-and-password authentication provides greater control over user interaction than basic name-and-password authentication. For example, you can customize the form in which users enter their name and password information. It also allows users to log out of the session without closing the browser.
		
###**SOLUTION:**

	 Session based authentication cant be implemented in android.An alternative method for implementing authentication is HTTP Basic authentication.

	 The standard way of configuring Basic Authentication on the HttpClient – via a CredentialsProvider:


	 	CredentialsProvider provider = new BasicCredentialsProvider();

	 	UsernamePasswordCredentials credentials = new UsernamePasswordCredentials("user1", "user1Pass");

	 	provider.setCredentials(AuthScope.ANY, credentials);

	 	HttpClient client = HttpClientBuilder.create().setDefaultCredentialsProvider(provider).build();

	  

	  	HttpResponse response = client.execute(new HttpGet(URL_SECURED_BY_BASIC_AUTHENTICATION));

	  	int statusCode = response.getStatusLine().getStatusCode();

	  	assertThat(statusCode, equalTo(HttpStatus.SC_OK));

	  As you can see, creating the client with a credentials provider to set it up with Basic Authentication is not difficult.

	  The entire Client-Server communication is now clear:

	  	- the Client sends the HTTP Request with no credentials
		- the Server sends back a challenge
		- the Client negotiates and identifies the right authentication scheme
		- the Client sends a second Request, this time with credentials

	   Using HTTP basic authentication is unsafe,since it sends the username and the password through the request headers.So we can use OAuth instead HTTP basic authentication. 

###**IMPLEMENTATION:**

	  Authenticator class is able to obtain authentication information for a connection in several ways. For this purpose it has to set the default authenticator which extends Authenticator by setDefault(Authenticator a). Then it should override getPasswordAuthentication() which dictates how the authentication info is obtained. Usually, it prompts the user for the required input.

	  setDefault(Authenticator)
	  getPasswordAuthentication()

   *Public constructors:*
   	Authenticator()

   *Public Methods:*
     	
	- synchronized static PasswordAuthentication requestPasswordAuthentication(String rHost, InetAddress rAddr, int rPort, String rProtocol, String rPrompt, String rScheme)
	
		Invokes the methods of the registered authenticator to get the authentication info.

		Parameters:

		rAddr	address of the connection that requests authentication.
		rPort	port of the connection that requests authentication.
		rProtocol	protocol of the connection that requests authentication.
		rPrompt	realm of the connection that requests authentication.
		rScheme	scheme of the connection that requests authentication.
		
		Returns password authentication info or null if no authenticator exists.

	- static PasswordAuthentication	requestPasswordAuthentication(String rHost, InetAddress rAddr, int rPort, String rProtocol, String rPrompt, String rScheme, URL rURL, Authenticator.RequestorType reqType)
	
	  	Invokes the methods of the registered authenticator to get the authentication info.
	
	
	- synchronized static PasswordAuthentication requestPasswordAuthentication(InetAddress rAddr, int rPort, String rProtocol, String rPrompt, String rScheme)
	
		Invokes the methods of the registered authenticator to get the authentication info.
	
	- static void	setDefault(Authenticator a)
	
		Sets a as the default authenticator. It will be called whenever the realm that the URL is pointing to requires authorization.

		Parameters:

		a	authenticator which has to be set as default.
		
   *Protected Methods:*

	- protected PasswordAuthentication getPasswordAuthentication ()

	Returns the collected username and password for authorization. The subclass has to override this method to return a value different to the default which is null.

	Returns null by default.
	
	Returns	collected password authentication data.
	
	- protected final String getRequestingHost ()

	Returns the host name of the connection that requests authentication or null if unknown.

	Returns	name of the requesting host or null.
	
	- protected final int getRequestingPort ()

	Returns the port of the connection that requests authorization.

	Returns	port of the connection.
	
	- protected final String getRequestingPrompt ()

	Returns the realm (prompt string) of the connection that requests authorization.

	Returns	prompt string of the connection.
	
	- protected final String getRequestingProtocol ()

	Returns the protocol of the connection that requests authorization.

	Returns	protocol of the connection.
	
	- protected final String getRequestingScheme ()

	Returns the scheme of the connection that requests authorization, for example HTTP Basic Authentication.

	Returns	scheme of the connection.
	
	- protected final InetAddress getRequestingSite ()

	Returns the address of the connection that requests authorization or null if unknown.

	Returns	address of the connection.
	
	- protected URL getRequestingURL ()

	Returns the URL of the authentication request.

	Returns	authentication request url.
	
	- protected Authenticator.RequestorType getRequestorType ()

	Returns the type of this request, it can be PROXY or SERVER.

	Returns	RequestorType of the authentication request.

