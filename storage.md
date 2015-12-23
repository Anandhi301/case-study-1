#	PERSISTENT STORAGE

##PERSITENT STORAGE:

	Persistent storage is any data storage device that retains data after power to that device is shut off. It is also sometimes referred to as non-volatile storage.
	
	Hard disk drives and solid-state drives are common types of persistent storage. This can be in the form of file, block or object storage. On the other hand, RAM and cache are typically non-persistent, and are erased of data when power is turned off. However, certain types such as non-volatile RAM and flash-based RAM are persistent.

	Persistence is beneficial so that in the event of a crash or reboot, data is not lost.

##PERSISTENT STORAGE IN ANDROID:

	Android provides several options to save persistent application data. The solution depends on our specific needs, such as whether the data should be private to our application or accessible to other applications (and the user) and how much space your data requires.

	Your data storage options are the following:

####	Shared Preferences:
	Store private primitive data in key-value pairs.
####	Internal Storage:
	Store private data on the device memory.
####	External Storage:
	Store public data on the shared external storage.
####	SQLite Databases:
	Store structured data in a private database.
####	Network Connection:
	Store data on the web with your own network server.

##BENEFITS:

	**SharedPreferences:**

		SharedPreferences is a key/value store where you can save a data under certain key. To read the data from the store you have to know the key of the data. This makes reading the data very easy. But as easy as it is to store a small amount of data as difficult it is to store and read large structured data as you need to define key for every single data, furthermore you cannot really search within the data except you have a certain concept for naming the keys.

	**Internal Storage:**

		Consider a user in an application has stored data in internal storage, then only that user of that application has access to that data on the mobile and that data is automatically deleted when the user uninstalls the application. Speaking of which internal memory is private.

		The apps internal storage directory is stored using the name package name in a special place in the android file system.

		Other apps or users of current app have no access to the file set by a particular user and a particular app unless it is explicitly made available to the user for readable/writable access.

	**External Storage:**

		The dropbox app probably uses external storage to store the user's dropbox folder, so that the user has easy access to these files outside the dropbox application, for instance, using the file manager.

	**SQlite Databases:**

		Large amounts of same structured data should be stored in a SQLite database as databases are designed for this kind of data. As the data is structured and managed by the database, it can be queried to get a sub set of the data which matches certain criteria using a query language like SQL. This makes it possible to search in the data. Of course managing and searching large sets of data influences the performance so reading data from a database can be slower than reading data from SharedPreferences.

		Sqlite is very helpful in storing complex and large data which can be downloaded once and can be used again and again until the application is running. When the application is closed the sqlite database is also destroyed.
	
	**Network Connection:**

		It refers to storing data on the cloud. HTTP or FTP file and content transfers through the java.net.* packages makes this happen.

##SOLUTION:

	**Shared Preferences:**

		The SharedPreferences class provides a general framework that allows you to save and retrieve persistent key-value pairs of primitive data types. You can use SharedPreferences to save any primitive data: booleans, floats, ints, longs, and strings. This data will persist across user sessions (even if your application is killed).

		To get a SharedPreferences object for your application, use one of two methods:

		*getSharedPreferences() *- Use this if you need multiple preferences files identified by name, which you specify with the first parameter.
		*getPreferences() *- Use this if you need only one preferences file for your Activity. Because this will be the only preferences file for your Activity, you don't supply a name.
		
		To write values:

		Call edit() to get a SharedPreferences.Editor.
		Add values with methods such as putBoolean() and putString().
		Commit the new values with commit()
		To read values, use SharedPreferences methods such as getBoolean() and getString().

	**Internal Storage:**

		 You can save files directly on the device's internal storage. By default, files saved to the internal storage are private to your application and other applications cannot access them (nor can the user). When the user uninstalls your application, these files are removed.

		 To create and write a private file to the internal storage:

		 Call openFileOutput() with the name of the file and the operating mode. This returns a FileOutputStream.
		 Write to the file with write().
		 Close the stream with close().

		MODE_PRIVATE will create the file (or replace a file of the same name) and make it private to your application. Other modes available are: MODE_APPEND, MODE_WORLD_READABLE, and MODE_WORLD_WRITEABLE.

		To read a file from internal storage:

		Call openFileInput() and pass it the name of the file to read. This returns a FileInputStream.
		Read bytes from the file with read().
		Then close the stream with close().

		*Methods:*

		*getFilesDir()*
			Gets the absolute path to the filesystem directory where your internal files are saved.
		*getDir()*
			Creates (or opens an existing) directory within your internal storage space.
		*deleteFile()*
			Deletes a file saved on the internal storage.
		*fileList()*
			Returns an array of files currently saved by your application.
	
	**External Storage:**

		Every Android-compatible device supports a shared "external storage" that you can use to save files. This can be a removable storage media (such as an SD card) or an internal (non-removable) storage. Files saved to the external storage are world-readable and can be modified by the user when they enable USB mass storage to transfer files on a computer.

		*Access to external storage:*
			
			In order to read or write files on the external storage, your app must acquire the READ_EXTERNAL_STORAGE or WRITE_EXTERNAL_STORAGE system permissions. 

			If you need to both read and write files, then you need to request only the WRITE_EXTERNAL_STORAGE permission, because it implicitly requires read access as well.

	
		*Checking media availability:*

			Before you do any work with the external storage, you should always call getExternalStorageState() to check whether the media is available. The media might be mounted to a computer, missing, read-only, or in some other state.
	
			The getExternalStorageState() method returns other states that you might want to check, such as whether the media is being shared (connected to a computer), is missing entirely, has been removed badly, etc. You can use these to notify the user with more information when your application needs to access the media.

		*Saving files that can be shared with other apps:*

			To get a File representing the appropriate public directory, call getExternalStoragePublicDirectory(), passing it the type of directory you want, such as DIRECTORY_MUSIC, DIRECTORY_PICTURES, DIRECTORY_RINGTONES, or others. By saving your files to the corresponding media-type directory, the system's media scanner can properly categorize your files in the system (for instance, ringtones appear in system settings as ringtones, not as music).

		*Saving files that are app-private:*

			If you are handling files that are not intended for other apps to use (such as graphic textures or sound effects used by only your app), you should use a private storage directory on the external storage by calling getExternalFilesDir(). This method also takes a type argument to specify the type of subdirectory (such as DIRECTORY_MOVIES). If you don't need a specific media directory, pass null to receive the root directory of your app's private directory.

	**SQLite Databases:**

		Android provides full support for SQLite databases. Any databases you create will be accessible by name to any class in the application, but not outside the application.

		The recommended method to create a new SQLite database is to create a subclass of SQLiteOpenHelper and override the onCreate() method, in which you can execute a SQLite command to create tables in the database. 

		To write to and read from the database, call getWritableDatabase() and getReadableDatabase(), respectively. These both return a SQLiteDatabase object that represents the database and provides methods for SQLite operations.

		We can execute SQLite queries using the SQLiteDatabase query() methods, which accept various query parameters, such as the table to query, the projection, selection, columns, grouping, and others. For complex queries, such as those that require column aliases, you should use SQLiteQueryBuilder, which provides several convienent methods for building queries.

		Every SQLite query will return a Cursor that points to all the rows found by the query. The Cursor is always the mechanism with which you can navigate results from a database query and read rows and columns.


	**Network Connection:**

		We can use the network (when it's available) to store and retrieve data on your own web-based services. To do network operations, use classes in the following packages:

			java.net.*
			android.net.*

##IMPLEMENTATION:

	**Shared Preferences:**

		 public static final String PREFS_NAME = "MyPrefsFile";

		 SharedPreferences settings = getSharedPreferences(PREFS_NAME, 0);

		 SharedPreferences settings = getSharedPreferences(PREFS_NAME, 0);
		        
		 SharedPreferences.Editor editor = settings.edit();
		
		 editor.putBoolean("silentMode", mSilentMode);
		 
		 // Commit the edits!
		
		 editor.commit();

	**Internal Storage:**

		String FILENAME = "hello_file";
		String string = "hello world!";

		FileOutputStream fos = openFileOutput(FILENAME, Context.MODE_PRIVATE);
		fos.write(string.getBytes());
		fos.close();

	**External Storage:**

		<manifest ...>
		    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
		        ...
			</manifest>


	**SQLite Database:**

		public class DictionaryOpenHelper extends SQLiteOpenHelper {

		    private static final int DATABASE_VERSION = 2;
		    private static final String DICTIONARY_TABLE_NAME = "dictionary";
 		    private static final String DICTIONARY_TABLE_CREATE =
			              "CREATE TABLE " + DICTIONARY_TABLE_NAME + " (" +
				       KEY_WORD + " TEXT, " + KEY_DEFINITION + " TEXT);";

		    DictionaryOpenHelper(Context context){
		    	super(context, DATABASE_NAME, null, DATABASE_VERSION);
			 }
			 @Override
				public void onCreate(SQLiteDatabase db) {
					db.execSQL(DICTIONARY_TABLE_CREATE);
				   }
		 }
