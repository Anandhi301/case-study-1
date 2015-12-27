#	EDITOR

####TEXT EDITOR:

	A text editor is a type of program used for editing plain text files.

	Text editors are provided with operating systems and software development packages, and can be used to change configuration files, documentation files and programming language source code.

####ECLIPSE:

	Eclipse is an integrated development environment (IDE) for developing applications using the Java programming language and other programming languages such as C/C++, Python, PERL, Ruby etc.

	The Eclipse platform which provides the foundation for the Eclipse IDE is composed of plug-ins and is designed to be extensible using additional plug-ins. 
	
	Developed using Java, the Eclipse platform can be used to develop rich client applications, integrated development environments and other tools. 
	
	Eclipse can be used as an IDE for any programming language for which a plug-in is available.

	The Java Development Tools (JDT) project provides a plug-in that allows Eclipse to be used as a Java IDE.

####Eclipse Releases:

	Every year, since 2006, the Eclipse foundation releases the Eclipse Platform and a number of other plug-ins in June.

**Codename	Year	Platform Version**

Callisto	2006	3.2
Europa	2007	3.3
Ganymede	2008	3.4
Galileo	2009	3.5
Helios	2010	3.6
Indigo	2011	3.7
Juno	2012	3.8 and 4.2
Kepler	2013 (planned)	4.3

####LAUNCHING ECLIPSE:

	On the windows platform, if you extracted the contents of the zip file to c:\, then you can start eclipse by using c:\eclipse\eclipse.exe

	When eclipse starts up for the first time it prompts you for the location of the workspace folder. All your data will be stored in the workspace folder. You can accept the default or choose a new location.

####Parts of an Eclipse Window:

	The major visible parts of an eclipse window are:

		Views
		Editors (all appear in one editor area)
		Menu Bar
		Toolbar
	
	An eclipse perspective is the name given to an initial collection and arrangement of views and an editor area. 
	
	The default perspective is called java.
	
	An eclipse window can have multiple perspectives open in it but only one perspective can be active at any point of time. 
	
	A user can switch between open perspectives or open a new perspective. A perspective controls what appears in some menus and tool bars.

	A perspective has only one editor area in which multiple editors can be open. The editor area is usually surrounded by multiple views.
	
	In general, editors are used to edit the project data and views are used to view the project metadata. For example the package explorer shows the java files in the project and the java editor is used to edit a java file.

	The eclipse window can contain multiple editors and views but only one of them is active any given point of time. 
	
	The title bar of the active editor or view looks different from all the others.

	The UI elements on the menu bar and tool bar represent commands that can be triggered by an end user.

####Using Multiple Windows:

	Multiple Eclipse Windows can be open at the same time. To open a new window, click on the Windows menu and select the New Window menu item.

	Each window can have a different perspective open in them. For example you could open two Eclipse windows one in the Java perspective and the other in the Debug perspective.
	
	The window showing the Java perspective can be used for editing the java code and the window showing the debug perspective can be used for debugging the application being developed.

####Features of Eclipse Juno:

*Java 7 coding support in an IDE.*
	
	Since Java 7 contains many new feature including dynamically-typed languages support and other small enhancements from Coin project, eclipse Java development tooling will include support for these features of Java 7.

*Detecting resource leaks of Closeable/Autocloseable resources.*

	This feature is really cool and it also works with “old code”. The common IO and JDBC resources now implement the relevant interfaces and the warnings are good enough to be shown on these. 
	Resource leaks can be occurred in the following situations: 
	     
	     1. A resource opened but not closed 
	     2. A resource may not closed on all control flows 
	     3. A resource may not closed at a method exit point 
	     4. In a Java 7 program a resource is closed but the code could still be improved by using a try-with-resources statement. 
	
	The new version include the global search bar that gives user quick access to almost any Eclipse feature.

*Code Recommenders*
	
	This is amazing feature that analyzes code of existing applications and extracts common patterns of how other developers have used. It helps deal with the complexity of large APIs using intelligent code completion attribute. 

*Eclipse for Mobile Developers* - now developers can use eclipse more easily with a variety of mobile SDKs, including the Google Android SDK.


