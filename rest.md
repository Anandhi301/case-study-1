#	RESTful DESIGN PATTERN

####REST:

	REST (REpresentational State Transfer) is an architectural style, and an approach to communications that is often used in the development of Web services.
	The use of REST is often preferred over the more heavyweight SOAP (Simple Object Access Protocol) style because REST does not leverage as much bandwidth, which makes it a better fit for use over the Internet.
	The SOAP approach requires writing or using a provided server program (to serve data) and a client program (to request data).
	It gives a coordinated set of constraints to the design of components in a distributed hypermedia system that can lead to a higher-performing and more maintainable architecture.
	To the extent that systems conform to the constraints of REST they can be called RESTful. RESTful systems typically, but not always, communicate over Hypertext Transfer Protocol (HTTP) with the same HTTP verbs (GET, POST, PUT, DELETE, etc.) which web browsers use to retrieve web pages and to send data to remote servers.[4] REST interfaces with external systems using resources identified by Uniform Resource Identifiers (URI), for example /people/tom, which can be operated upon using standard verbs, such as DELETE /people/tom.

####Architectural properties:

	The architectural properties affected by the constraints of the REST architectural style are:

		Performance - component interactions can be the dominant factor in user-perceived performance and network efficiency.
		Scalability to support large numbers of components and interactions among components.

####REST design pattern:

	Based on the architectural pattern of the web, "REST" has a growing dominance of the SOA (Service Oriented Architecture) implementation.

####Benefits:

	REST's client–server separation of concerns simplifies component implementation, reduces the complexity of connector semantics, improves the effectiveness of performance tuning, and increases the scalability of pure server components. 
	Layered system constraints allow intermediaries—proxies, gateways, and firewalls—to be introduced at various points in the communication without changing the interfaces between components, thus allowing them to assist in communication translation or improve performance via large-scale, shared caching. 
	REST enables intermediate processing by constraining messages to be self-descriptive: interaction is stateless between requests, standard methods and media types are used to indicate semantics and exchange information, and responses explicitly indicate cacheability.

####Architectural constraints:

	The architectural properties of REST are realized by applying specific interaction constraints to components, connectors, and data elements.
	One can characterise applications conforming to the REST constraints described in this section as "RESTful".[
	If a service violates any of the required constraints, it cannot be considered RESTful. 
	Complying with these constraints, and thus conforming to the REST architectural style, enables any kind of distributed hypermedia system to have desirable non-functional properties, such as performance, scalability, simplicity, modifiability, visibility, portability, and reliability.

	The formal REST constraints are:

*Client–server:*


	A uniform interface separates clients from servers. This separation of concerns means that, for example, clients are not concerned with data storage, which remains internal to each server, so that the portability of client code is improved. Servers are not concerned with the user interface or user state, so that servers can be simpler and more scalable. Servers and clients may also be replaced and developed independently, as long as the interface between them is not altered.

*Stateless:*

	The client–server communication is further constrained by no client context being stored on the server between requests. Each request from any client contains all the information necessary to service the request, and session state is held in the client. The session state can be transferred by the server to another service such as a database to maintain a persistent state for a period and allow authentication. The client begins sending requests when it is ready to make the transition to a new state. While one or more requests are outstanding, the client is considered to be in transition. The representation of each application state contains links that may be used the next time the client chooses to initiate a new state-transition.[8]

*Cacheable:*
	
	As on the World Wide Web, clients and intermediaries can cache responses. Responses must therefore, implicitly or explicitly, define themselves as cacheable, or not, to prevent clients from reusing stale or inappropriate data in response to further requests. Well-managed caching partially or completely eliminates some client–server interactions, further improving scalability and performance.

*Layered system:*
	
	A client cannot ordinarily tell whether it is connected directly to the end server, or to an intermediary along the way. Intermediary servers may improve system scalability by enabling load balancing and by providing shared caches. They may also enforce security policies.

*Code on demand (optional):*
	
	Servers can temporarily extend or customize the functionality of a client by the transfer of executable code. Examples of this may include compiled components such as Java applets and client-side scripts such as JavaScript. "Code on demand" is the only optional constraint of the REST architecture.

*Uniform interface:*

	The uniform interface constraint is fundamental to the design of any REST service.The uniform interface simplifies and decouples the architecture, which enables each part to evolve independently. The four constraints for this uniform interface are:

	Identification of resources:
		Individual resources are identified in requests, for example using URIs in web-based REST systems. The resources themselves are conceptually separate from the representations that are returned to the client. For example, the server may send data from its database as HTML, XML or JSON, none of which are the server's internal representation.
	Manipulation of resources through these representations:
		When a client holds a representation of a resource, including any metadata attached, it has enough information to modify or delete the resource.
	Self-descriptive messages:
		Each message includes enough information to describe how to process the message. For example, which parser to invoke may be specified by an Internet media type (previously known as a MIME type). Responses also explicitly indicate their cacheability.
	Hypermedia as the engine of application state (HATEOAS):
		Clients make state transitions only through actions that are dynamically identified within hypermedia by the server (e.g., by hyperlinks within hypertext). Except for simple fixed entry points to the application, a client does not assume that any particular action is available for any particular resources beyond those described in representations previously received from the server.

####Applied to web services:

	Web service APIs that adhere to the REST architectural constraints are called RESTful APIs. HTTP-based RESTful APIs are defined with these aspects:

		- base URI, such as http://example.com/resources/
		- an Internet media type for the data. This is often JSON but can be any other valid Internet media type (e.g., XML, Atom, microformats, images, etc.)
		- standard HTTP methods (e.g., GET, PUT, POST, or DELETE)
		- hypertext links to reference state

**RESTful API HTTP methods:**

**Resource:**

	hypertext links to reference-related resources:

		GET	
		
			List the URIs and perhaps other details of the collection's members.	
		PUT	
		
			Replace the entire collection with another collection.
		POST	
		
			Create a new entry in the collection. The new entry's URI is assigned automatically and is usually returned by the operation.
		DELETE

			Delete the entire collection.
	Element URI, such as http://api.example.com/resources/item17

		GET	
	
			Retrieve a representation of the addressed member of the collection, expressed in an appropriate Internet media type.
		PUT	
		
			Replace the addressed member of the collection, or if it does not exist, create it.
		POST	
		
			Not generally used. Treat the addressed member as a collection in its own right and create a new entry in it.
		DELETE
			
			Delete the addressed member of the collection.

	The PUT and DELETE methods are referred to as idempotent, meaning that the operation will produce the same result no matter how many times it is repeated. The GET method is a safe method (or nullipotent), meaning that calling it produces no side-effects. In other words, retrieving or accessing a record does not change it. 

####Solution:

	Restful Design Pattern can be implemented in three different ways:

		1.Use a Service API
		2.Use a ContentProvider API
		3.Use the ContentProvider API and a SyncAdapter

####Implementation:

	public class RestfulAPIService extends Service  {

	final RemoteCallbackList<IRemoteServiceCallback> mCallbacks = new RemoteCallbackList<IRemoteServiceCallback>();

	public void onStart(Intent intent, int startId) {
	    super.onStart(intent, startId);
	    }
	    public IBinder onBind(Intent intent) {
	        return binder;
	    }
	public void onCreate() {
	   super.onCreate();
	}
	public void onDestroy() {
		super.onDestroy();
		mCallbacks.kill();
	}
	private final IRestfulService.Stub binder = new IRestfulService.Stub() {
		public void doLogin(String username, String password) {

		Message msg = new Message();
		Bundle data = new Bundle();
		HashMap<String, String> values = new HashMap<String, String>();
		values.put("username", username);
		values.put("password", password);
		String result = post(Config.getURL("login"), values);
		data.putString("response", result);
		msg.setData(data);
		msg.what = Config.ACTION_LOGIN;
		mHandler.sendMessage(msg);
		}
															
		public void registerCallback(IRemoteServiceCallback cb) {
			if (cb != null)
				mCallbacks.register(cb);
			}
		};

		private final Handler mHandler = new Handler() {
		public void handleMessage(Message msg) {

		// Broadcast to all clients the new value.
			final int N = mCallbacks.beginBroadcast();
			for (int i = 0; i < N; i++) {
			try {
				
				switch (msg.what) {
			
					case Config.ACTION_LOGIN:
																											                    mCallbacks.getBroadcastItem(i).userLogIn( msg.getData().getString("response"));
					    break;
																											                default:
																											                    super.handleMessage(msg);
																													    return;
					}
																										            } catch (RemoteException e) {																																							                }																								    			 }
																										        mCallbacks.finishBroadcast();
																										    }
																									        public String post(String url, HashMap<String, String> namePairs) {...}
	    																								    public String get(String url) {...}
	 																							    };

IDL:
																								    package com.something.android
																								    oneway interface IRemoteServiceCallback {
																								        void userLogIn(String result);
																									}

	
     package com.something.android
     import com.something.android.IRemoteServiceCallback;

	interface IRestfulService {
	    void doLogin(in String username, in String password);
	        void registerCallback(IRemoteServiceCallback cb);
	}


Service init and bind:

	// this I'm calling on app onCreate
	servicemanager = new ServiceManager(this);
	servicemanager.startService();
	servicemanager.bindService();
	application = (ApplicationState)this.getApplication();
	application.setServiceManager(servicemanager);

Service function call:

	application = (ApplicationState) getApplication();
	servicemanager = application.getServiceManager();
	servicemanager.setHandler(mHandler);

	try {
	    servicemanager.restfulService.doLogin(args[0], args[1]);
	    } catch (RemoteException e) {
	        e.printStackTrace();
		}
