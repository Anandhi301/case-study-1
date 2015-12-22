
#	SESSION BASED AUTHENTICATION

###**AUTHENTICATION:**
	The process of identifying an individual,usually based on a username and password. Authentication merely ensures that the individual is who he or she claims to be, but says nothing about the access rights of the individual. 
	It is a process that ensures and confirms a user’s identity. Authentication is one of the five pillars of information assurance (IA). The other four are integrity, availability, confidentiality and nonrepudiation.
	Authentication begins when a user tries to access information. First, the user must prove his access rights and identity. When logging into a computer, users commonly enter usernames and passwords for authentication purposes. This login combination, which must be assigned to each user, authenticates access. However, this type of authentication can be circumvented by hackers.
	A better form of authentication, biometrics, depends on the user’s presence and biological makeup (i.e., retina or fingerprints). This technology makes it more difficult for hackers to break into computer systems.

	The Public Key Infrastructure (PKI) authentication method uses digital certificates to prove a user’s identity. There are other authentication tools, too, such as key cards and USB tokens. One of the greatest authentication threats occurs with email, where authenticity is often difficult to verify. For example, unsecured emails often appear legitimate.

###**AUTHORIZATION:**

	Authorization is the process of giving someone permission to do or have something. In multi-user computer systems, a system administrator defines for the system which users are allowed access to the system and what privileges of use (such as access to which file directories, hours of access, amount of allocated storage space, and so forth).
	It  is the function of specifying access rights to resources related to information security and computer security in general and to access control in particular.
	The process of granting or denying access to a network resource. Most computer security systems are based on a two-step process. The first stage is authentication, which ensures that a user is who he or she claims to be. The second stage is authorization, which allows the user access to various resources based on the user's identity.

###**TOKEN BASED AUTHENTICATION:**
	
	Token based authentication is prominent everywhere on the web nowadays.Tokens are the best way to handle authentication for multiple users.
	It allows users to enter their username and password in order to obtain a token which allows them to fetch a specific resource - without using their username and password.Once thier token has been obtained,the user can offer the token - which offers access to a specific resource for a time period - to the remote site.
	There are some very important factors when choosing token based authentication for our application. The main reasons for tokens are:

	1.Stateless and scalable servers
	2.Mobile application ready
	3.Pass authentication to other applications
	4.Extra security

###**BENEFITS:**

	The main advantage is the user could pass the token, once they've obtained it, on to some other automated system which they're willing to trust for a limited time and a limited set of resources, but would not be willing to trust with their username and password (i.e., with every resource they're allowed to access, forevermore or at least until they change their password).


###**SOLUTION:**

        Token based authentication works as:

		User Requests Access with Username / Password
	
		Application validates credentials
	
		Application provides a signed token to the client
	
		Client stores that token and sends it along with every request
	
		Server verifies token and responds with data

###**IMPLEMENTATION:**

	There are a number of ways to use/ create tokens:

		a) using a hash mechanism e.g. HMAC-SHA1

		token = user_id|expiry_date|HMAC(user_id|expiry_date, k) 

		--id and expiry_id are sent in plaintext with the resulting hash attached (k is only know to the server)

		b) encrypting the token symmetrically e.g. with AES

		token = AES(user_id|expiry_date, x) 

		--x represents the en-/decryption key

		c) encrypting it asymmetrically e.g. with RSA

		token = RSA(user_id|expiry_date, private key)


