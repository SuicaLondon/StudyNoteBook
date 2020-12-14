# Hello Android

## Basis

> Android OS is a **multi-user Linux system**\

- Each app is a different user\
  > The system assigns each app a **unique Linux user ID**
- unknown to the app
  > The system sets permissions for all the files in an app
- so that only the user ID assigned to that app can access them
  > Each process has its own **virtual machine (VM)**, so an app's code runs in isolation from other apps

> By default, every app runs in its own Linux process

## Execution

> The Android ststem perform the process when each components need to be runned

> It then shuts it down when

- It is no longer needed
- system must recover memory for other apps

> Android is based on the principle of least privilege

- Normally, each app has access only to the components needed to do its work
- This creates a very secure environment in which an app cannot access parts of the system for which it is not given permission

## Permissions

> There are some method for an app to share data with others in order to access system services

> Two types of permissions in Android M (6.0+)

- Dangerous permissions (user has to accept)
- Other permissions (user is not asked)

## App Components

Each type provide a **distinct purpose** and has a **distinct lifecycle**

1. Activities
2. Services
3. Broadcast receivers
4. Content providers
   <img src="https://www.tutorialspoint.com/android/images/content.jpg" alt="content provider"/>

## Android has no Java main program

Entry point are the components

## Activate another component

Android runs **each app in a separate process with file permissions** that restrict access to other apps

Your app **cannot directly activate a component** from its own space or from another app

It will deliver a message to the **system** which specifies your **intent** to start a particular component

```
 Intent intent = new Intent(this, MyActivity.class);
 startActivity(intent);
// or startActivityForResult(intent)
```

> Pass an intent to methods such as

- sendBroadcast()
- sendOrderedBroadcast()
- sendStickyBroadcast()

```
Intent broadcastIntent =
          new Intent("uk.ac.shef.oak.myPackage.myFlag");
 sendBroadcast(broadcastIntent);
```

## App organisation

1. The Manifest file
2. The Java program

- providing dynamics in the app
- activities, dynamic changes to the UI, running services, etc.

3. The declarative resources

- static data
- icons, images, layouts, strings

4. The gradle scripts

- information about complication instructions, SDK levels, settings, link to libraries

## Layout for Activities

Each XML layout file is compiled into a View resouce. The layout resource should be load in Activity.onCreate() callback implementation.

```Java
protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
}
```

## Directory

Android use R supersede slashes under the main directory and omits the .xml suffix

## Attribute

### ID

```
android:id="@+id/my_button"
android:id="@android:id/my_button"
```

## Layouts

1. Linear Layout
   > use **android:orientation** to specify the layout direction

### Layout Weight

```
android:layout_weight
```

2. Relative Layout
3. Web View

### Adapter view

1. List View/RecyclerView
2. Grid View

### Others

1. Frame Layout
2. ScrollView
3. ViewPaper

## Controls

- Button
  > 1. Button
- Text field
  > 1. EditText
  > 2. AutoCompleteTextView
- Checkbox
  > 1. CheckBox
- Radio button
  > 1. RadioGroup
  > 2. RadioButton
- Toggle button
  > 1. ToggleButton
- Spinner
  > 1. Spinner
- Pickers
  > 1. DatePicker
  > 2. TimePicker

## Event Listeners

1. onClick()

- from **View.OnClickListener()**

2. onLongClick()

- from **View.OnLongClickListener()**

3. onFocusChange()

- from **View.OnFocusChangeListener()**

4. onKey()

- from **View.OnKeyListener()**

5. onTouch()

- from **View.OnTouchListener()**

## Lifecycle

four various phases:

1. Activity is created
2. Activity becomes visible to the user
3. Activity becomes invisible to the user (e.g. minimised)
4. Activity is destroyed (e.g. swiped out)

<img src="https://miro.medium.com/max/513/0*qMxQY8nlZQnqokrZ.png" alt="life cycle">

### onCreate()

> setContentView() must be called

### onStart()

> this callback will be implemented when it becomes visible to the user

### onResume()

> before the activity starts interacting with the user

### onPause()

> The onPause() callback always follows onResume()
> It is called when the activity loses focus and enters a Paused state
> It is still visible

- Do not use onPause() to do long operations
  > next callback ether onStop() or onResume()

### onStop()

> The system calls onStop() when the activity is no longer visible to the user
> The next callback that the system calls is either onRestart(), if the activity is coming back to interact with the user, or by onDestroy() if this activity is completely terminating

### onRestart()

> It will be called after it restart from stopped state
> It is always followed by onStart()

### onDestrop()

> The system invokes this callback before an activity is destroyed.

## Toolbar

1. Navigation
2. Menu items
3. Collapsed Menu

```XML
<android.support.design.widget.AppBarLayout
    android:layout_width="match_parent"
    android:layout_height="200dp">
    <android.support.design.widget.CollapsingToolbarLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:contentScrim="?attr/colorPrimary"
        app:layout_scrollFlags="scroll|exitUntilCollapsed">
        <android.support.v7.widget.Toolbar
            android:layout_width="match_parent"
            android:layout_height="?attr/actionBarSize"
            app:layout_collapseMode="pin"/>
    </android.support.design.widget.CollapsingToolbarLayout>
</android.support.design.widget.AppBarLayout>
```

```XML
<android.support.design.widget.AppBarLayout
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="?attr/colorPrimary">
    <android.support.design.widget.CollapsingToolbarLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:contentScrim="?attr/colorPrimary"
        app:layout_scrollFlags="scroll|exitUntilCollapsed"
        app:expandedTitleTextAppearance="@style/TextAppearance.AppCompat.Title">
        <ImageView
            android:layout_width="match_parent"
            android:layout_height="200dp"
            app:layout_collapseMode="parallax"/>
        <android.support.v7.widget.Toolbar
            android:id="@+id/toolbar"
            android:layout_width="match_parent"
            app:layout_collapseMode="pin"
            android:layout_height="?attr/actionBarSize"
            app:popupTheme="@style/ThemeOverlay.AppCompat.Light"
            app:theme="@style/ToolBarStyle" />
    </android.support.design.widget.CollapsingToolbarLayout>
</android.support.design.widget.AppBarLayout>
```

## Coherence

### Colors and styles

```XML
<Button
    ...
    style="@style/Seta_BlueButton"
/>

<resources>
    <color name="colorPrimary">#3F51B5</color>
    <color name="colorPrimary">#011993</color>
    <color name="colorPrimary">#FF4081</color>
</resources>

<style name="AppTheme" parent="Theme.AppCompat.Light.DarkActionBar">
    <item name="colorPrimary">@color/colorPrimary</item>
    <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
    <item name="colorAccent">@color/colorAccent</item>
</style>
<style name="Seta_BlueButton">
    <item name="android:background">#6CBDFC</item>
    <item name="android:textColor">#FFF</item>
    <item name="android:textStyle">bold</item>
</style>
```

color.adobe.com

## Materials

> Material uses 8dp grid for components(4dp for text)

> All sizes and distances are multiples of 8 and 4

- dp= the conversion of dp units to screen pixels is simple: px = dp \* (dpi / 160)
- dpi= the quantity of pixels within a physical area of the screen; usually referred to as dpi (dots per inch).

```XML
<Button
    ...
    android:layout_marginLeft="@dimen/activity_horizontal_margin"
    android:layout_marginRight="@dimen/activity_horizontal_margin"
/>
<!-- dimen.xml  -->
<resources xmlns:tools="bttp://schemas.android.com/tools">
    <dimen name="activity_horizontal_marigin">16dp</dimen>
    <dimen name="activity_vertical_marigin">16dp</dimen>
</resources>
```

## Design Patterns

1. SRP: Single responsibility priciple
2. OCP: Open/closed principle
3. LSP: Liskov substitution principle
4. ISP: Interface segregation principle
   5/ DIP: Dependency inversion priciple

> Model

- The combination of data, state and bussiness logic

> View

- XML files

> Controller

- glue for tying the app together
- master controller for what happens in the application
- handle the event from user and decide to update the state of the view

<img src="https://miro.medium.com/max/606/1*smJy5uFyF5qucw6_7svnQA.png" alt="Controller">

> Presenter

- Activity/Fragment is now part of the view
- Easy for JUnit test

<img src="https://miro.medium.com/max/778/1*TuWeZzR14MmB-RBbjtZl-A.png" alt="Presenter">

> View Model

- responsible for wrapping the model and preparing observable data needed by the view
- provides hooks for the view to pass event to the model
- not tied to the view

<img src="https://cdn.journaldev.com/wp-content/uploads/2018/04/android-mvvm-pattern.png" alt="Presenter">

## Persisting Data

### Key-Value sets

> SharedPreferences APIIs

```Java
getShareddPreferences(String fileName)
getPreferences()

// eg.
Context context = getActivity();
SharedPreferences sharedPref = context.getSharedPreferences(“com.example.myapp.PREFERENCE_FILE_KEY”, Context.MODE_PRIVATE);
```

> Write

- get the preference file

```Java
SharedPreferences sharedPref = getActivity().getPreferences(Context.MODE_PRIVATE);
```

- create a SharedPreferences.Editor by calling edit() on your SharedPreferences

```Java
SharedPreferences.Editor editor = sharedPref.edit();
```

- Pass the **_keys and values_** as you would do to a HashSet but specifying a type

```Java
editor.putInt(getString(R.string.saved_high_score), newHighScore);
```

- Use commit to save the change

```Java
editor.commit();
```

> Read

- get int

```Java
 SharedPreferences sharedPref = getActivity().getPreferences(Context.MODE_PRIVATE);
 int defaultValue = 10;
 long highScore = sharedPref.getInt(“AGE_KEY”, defaultValue);

 // other way
 SharedPreferences sharedPref = getActivity().getPreferences(Context.MODE_PRIVATE);
 int defaultValue = getResources().getInteger(R.string.saved_age_default);
 long highScore = sharedPref.getInt(getString(R.string.saved_age), defaultValue);
```

### Files

> for large amount of data, eg. image

1. external storage

- SD Card
- getExternalFileDir()

2. internal storage

```Java
public boolean isExternalStorageWritable() {
    String state = Environment.getExternalStorageState();
    if (Enivornment.MEDIA_MOUNTED.equals(state)) {
        return true;
    } else {
        return false;
    }
}

public boolean isExternalStorageReadable() {
    String state = Environment.getExternalStorageState();
    if (Enivornment.MEDIA_MOUNTED.equals(state) || Enivornment.MEDIA_MOUNTED_READ_ONLY.equals(state)) {
        return true;
    } else {
        return false;
    }
}
```

- built-in non-volatile memory
- getFileDir()
- getCacheDir()

```Java
File file = new File(context.getFileDir(), filename);

String filename = "myfile";
String string = "Hello World"
File file = new File(context.getFileDir(), filename)
try {
    outputStreem = openFileOutput(filename, Context.MODE_PRIVATE);
    outputStream.write(string.getBytes());
    outputStream.close();
} catch (Exception e) {
    e.printStackTrace()
}

public File getTempFile(Context context, String url) {
    File file;
    try {
        String fileName = URL.parse(url).getLastPathSegment();
        file = File.createTempFile(fileName, null, context.getCacheDir);
    } catch (IOException e) {
        // Error while creating file
    }
    return file;
}
```

> Delete a File

```Java
myFile.delete();

myContext.deleteFile(fileName);
```

### Rooms

- implementation

```
implementation "android.arch.persistence.room:runtime:1.0.0"
```

- annotationProcessor

```
annotationProcessor "android.arch.persistence.room:compiler:1.0.0"
```

- testing Room migrations

```
testImplementation "android.arch.persistence.room:testing:1.0.0"
```

- RxJava

```
implementation "android.arch.persistence.room:runtime:1.0.0"
```

- Denendencies

```gradle
dependencies {
    def room_version = "2.2.5"
    implementation "androidx.room.room:runtime:$room_version"
    annotationProcessor "androidx.room.room:room-compiler:$room_version"

    // optional - RxJava support for Room
    implementation "androidx.room.room:rxjava2:$room_version"

    // optional - Guava support for Room, include Optional and ListenableFuture
    implementation "androidx.room.room:guava:$room_version"

    // optional - Test helpers
    testImplementation "androidx.room.room:runtime:$room_version"
}
```

> Room provides an abstraction layer over SQLite

> handle non-trivial amounts of structured data

> The most common use case is to cache relevant pieces

> There are 3 major components in Room

1. Database

- the database holder
- it serves as the main access point for the underlying connection to the relational data
- The class that's annotated with **@Database** should satisfy the following conditions:
  - abstract class that extends RoomDatabase
  - include the list of entities associated with the database within the annotation
  - Contain an abstract method that has 0 arguments and return the class that is annotated with @ Dao
- call Room.databaseBuilder() or Room.inMemoryDatabaseBuilder() to acquire an instance of DB

2. Entity

- Represents a **table** within the database

3. DAO

- Contains the **methods** used for accessing the database

```Java
@Entity(indices = {@Index(value = {"first_name", "last_name"}, unique = ture)}) // optional parameters
public class User {
    @PrimaryKey()
    private int uid;

    @ColumnInfo(name = "first_name")
    private String firstName;

    @ColumnInfo(name = "last_name")
    private String lastName;
}
```

<img src="https://miro.medium.com/max/600/0*KoNREm-uuyv4i5tp.png" alt="room">

### SQLite databases

> relational database

> Room forbid entity objects to reference each other

> It requires the definition of foreign keys

```Java
@Entity(foreignKeys = @ForeignKey(entity = User.class, parentColumns = "id", childColumns = "User_id"))
```

> Use **_@Embeded_** annotation to represent an object that you'd like to decompose into **its subfield within a table**

### DAOs

> Can be either an interface or an abstract class.

```Java
@Dao
public interface UserDao {
    @Query("SELECT * FROM user")
    List<User> getAll();

    @Query("SELECT * FROM user WHERE uid IN (:userIds)")
    List<User> loadAllByIds(int[] userIds);

    @Query("SELECT * FROM user WHERE first_name LIKE :first AND last_name LIKE :last LIMIT 1")
    List<User> findByName(String first, String last);

    @Insert
    void insertAll(User... users);

    @Delete
    void delete(User user)
}
```

> Room creates each DAO implementation at compile time.

> Room does not support database access on the main thread unless you have called **allowMainThreadQueries()**

### DataBase

- It must be Abstract
- it must extend RoomDatabase
- It declares an abstract Dao

```Java
@DataBase(entities = {User.class}, version = 1)
public abstract class AppDatabase extends RoomDatabase {
    public abstract UserDao userDao();
}

AppDatabase db = Room.databaseBuilder(getApplicationContext(), AppDatabase.class, "database-name").build();
```

## Application Not Responding(ANR)

> It will show the ANR dialog if

1. No response to an input event within 5 seconds
2. A broadcaseReceiver hasn't finished excuting within 10 seconds
   > Activities should do as little as possible to set up in key life-cycle methods such as onCreate() and onResume()

- To create a worker thread for longer operations use **AsyncTask class**
  - Extend AsyncTask and implement the doInBackground() method to perform the work
  - To post progress to the user interface, call publishProgress(), which invokes the onProgressUpdate() callback method

```Java
private class DownloadFilesTask extends AsyncTask<URL, Interger, Long> {
    // Do the long-running work in here
    protected Long doInBackground(URL... urls) {
        int count = urls.length;
        long totalSize = 0;
        for(int i = 0; i<count; i++>) {
            totalSize += Downloader.downloadFile(urls[i]);
            publishProgress((int)(i/(float) count) * 100);
            if (isCancelled()) break;
        }
        return totalSize;
    }

    protected void onProgressUpdate(Integer...progress) {
        setProgressPercent(progress[0])
    }

    protected void onPostExcute(Long result) {
        showNotification("Downloaded" + result + " bytes");
    }
}

new DownloadFilesTask().execute(url1, url2, url3);
```

> Use runOnUiTread() when you want to update your UI from a Non-UI Thread

## Jetpack
* a collection of Android software components
* eliminating boilerplate code

### Architecture
> Manage your app's lifecycle with ease
* New lifecycle-aware components help you manage your activity and fragment lifecycles
* Survive configuration changes, avoid memory leaks and easily load data into your UI.
> Use LiveData to build data objects that notify views when the underlying database changes.
> ViewModel to store UI-related data that isn't destroyed throughout the app’s lifecycle
> Room for databases

### LiveData
* LiveData is an observable data holder class
* UI components subscribe to the live data and are immediately notified of any changee
#### View
``` Java
@Override
protected void onCreate(Bundle savedInstanceState) {
    myViewModel = ViewModelProviders.of(this).get(MyViewModel.class);
    myViewModel.getMyStrings().observe(this, new Observer<List<String>>(){ 
        @Override
        public void onChanged(@Nullable final List<String> newValue) { 
            // Update the UI
        }
    });
}
```
#### ViewModel
``` Java
public class MyViewModel extends AndroidViewModel {
    private LiveData<List<String>> mStringList;
    LiveData<List<String>> getStringList() {
        if (mStringList == null) {
            mStringList = new MutableLiveData<List<String>>();
            // launch operation in the Model that fetches the data for the
            // first time (typically and async process)
        }
        return mStringList; 
    }
}   
// create a connection to the repository
private MyRepository mRepository;

// Initialise the ViewModel
public MyViewModel (Application application) { super(application);
mRepository = new MyRepository(application);
mValueGetter = mRepository.valueGetter(); }
```

## Debug
> insert Log.i, Log.d, and Log.e traces to identify the area where the error is
``` Java
try{
    /// code
} catch (Exception e){
    Log.e(“Class name”, “descriptive string “+ e.getMessage()
}
```

## Connecting to a server
``` Java
// Get
OkHttpClient client = new OkHttpClient();

String run(String url) throws IOException {
    Request request = new Request.Builder()
        .url(url)
        .build();
    Response response = client.newCall(request).excute();
    return response.body().string();
}

// Post
public static final MediaType JSON = MediaType.parse("application/json; charset=utf-9");
OkHttpClient client = new OkHttpClient();

String post(String url, String json) throws IOException {
    RequestBody body = RequestBody.create(JSON, json)
    Request request = new Request.Builder()
        .url(url)
        .post(body)
        .build();
    Response response = client.newCall(request).excute();
    return response.body().string();
}

// Final
private final OkHttpClient client = new OkHttpClient();

public void run() throws IOException {
    Request request = new Request.Builder()
        .url("url")
        .build()
    
    client.newCall(request).enqueue(new Callback() {
        @Overide public void onFailure(Call call, IOException e) {
            e.printStackTrace();
        }
        @Overide public void onResponse(Call call, Response response) throws IOException {
            try (ResponseBody responseBody = response.body()) {
                if (!response.isSuccessful()) throw new IOException("Unexcepted code" + response.body);

                Headers responseHeaders = response.headers();
                for (int i = 0, size = responseHeaders.size(); i< size; i++) {
                    System.out.println(responseHeaders.name(i) + ": " + responseHeaders.value(i))
                }
                System.out.println(responseBody.string());
            }
        }
    })
}
```


## Sensor
1. Motion sensors
    1. accerkerineter
    2. gravity
    3. gyroscopes
    4. ritatuibak vector
2. Environmental sensors
    1. ambient air temperature (thermometers)
    2. pressure (barometers)
    3. illumination (photometers)
    4. humidity
3. Position sensors
    1. orientation
    2. magnetometers

## Time
``` Java
Date date = new Date(msecs);
DataFormat formatter = new SimpleDateFormat("HH:mm:ss");
formatter.setTimeZone(TimeZone.getTimeZone("UTC"));
String dateString = formatter.format(date);
```

## Location
> Permissions
``` XML
<manifest xmlns:android="http://schemas.android.com/apk/res/android" package="com.google.android.gms.location.sample.basiclocationsample">
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
    <!-- <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/> -->
</manifest>
```

``` Java
implementation 'com.google.android.gms:play-services-location:11.0.2'
```

``` Java
private FusedLocationProviderClient mFusedLocationClient;

@Override
protected void onCreate(Bundle savedInstanceState) {
    mFusedLocationClient = LocationServices.getFusedLocationProviderClient(this)
}

mFusedLocationClient.getLastLocation()
    .addOnSuccessListener(this, new OnSuccessListener<Location>() {
        @Override
        public void onSuccess(Location location) {
            // Got last known location. In some rate situations. this can be null
            if(location!=null) {
                // Logic to handle location object
            }
        }
    })
```

> connect to location services and make a location request
``` Java
LocationRequest mLocationRequest = new LocationRequest();
mLocationRequest.setInterval(10000);
mLocationRequest.setFastestInterval(5000);
mLocationRequest.setPriority(LocationRequest.PRIORITY_HIGH_ACCURACY);
startLocationUpdates();

private void startLocationUpdates() {
    mFusedLocationClient.requestLocationUpdates(myLocationRequest, mLocationCallback, null)
}

mLocationCallback = new LocationCallback() {
    @Override
    public void onLocationResult(LocationResult locationResult) {
        super.onLocationResult(locationResult);
        mCurrentLocation = locationResult.getLastLocation();
    }
}
```

> Stopping
``` Java
private void stopLocationUpdates() {
    FusedLocationProviderClient.removeLocationUpdates(mLocationCallback);
}
```

* ActivityCompat.checkSelfPermission
``` Java
if ((Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) && (ActivityCompat.checkSelfPermission(activity, android.Manifest.permission.ACCESS_FINE_LOCATION)) != PackageManager.PERMISSION_GRANTED) {
    if (ActivityCompact.shouldShowRequestPermissionRationale(thisActivity, android.Manifest.permission.ACCESS_FINE_LOCATION)) {

    } else {
        ActivityCompact.requestPermissions(thisActivity, new String[] {Manifest.permission.ACCESS_FINE_LOCATION}, MY_PERMISSIONS_REQUEST_LOCATION);
    }
}
```

* Handle the permissions request response
``` Java
@Override
public void onRequestPermissionsResult(int requestCode, String permissions[], int[] grantResults) {
    switch (requestCode) {
        case MY_PERMISSIONS_REQUEST_LOCATION: {
            if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                // oernussuib was grabted
            } else {
                // permission denied
            }
        }
    }
}
```

## Computations
### Heavy computation
1. AsyncTask
    *  for short-ish background computation
2. Threads
    * for parallel computation
3. Service
    * for active computation on the UI thread (Service) or a separate thread (IntentService)

### Services
1. Foreground
    * performs some operation which is noticeable to the user
    * must display a status bar icon
    * continues running even when the user isn't interacting with the app
    * is the only safe way to do long running currently
2. Background
    * performs an operation that isn't directly noticed by the user
    * Increasingly unreliable in order to save battery
3. Bound
    * when an application component binds to it by calling **bindService()**
    * offers a **client-server interface** that allows components to interact with the service send requests, receive results, and
    * A bound service runs only as long as another

> Method
* OnCreate()
* OnStartCommand()
    * called when the **startService()** was exerted
* OnBind()
    * invokes this method by calling bindService() when another component wants to bind with the service.
* OnDestroy()
``` XML
<manifest ... > ...
  <service android:name=".ExampleService" />
 ...
 </application>
 </manifest>
```

<img src="https://www.tutlane.com/images/android/android_services_started_bound_services_life_cycle.png" alt="service life cycle">


* service was called by **startService()** which results in a call to the service’s **OnStartCommand()**
* The service can run in the background indefinitely, even if the component that started it is destroyed
* The service should stop itself when its job is completed by calling **stopSelf()**
* Or another component can stop it by calling **stopService()**
* An application component such as an activity can start the service by calling **startService()** and passing an Intent that specifies the service and includes any data for the service to use.
* The service receives the Intent in the **OnStartCommand()**

> Confusion about the Service
* A Service is not a separate process
* A Service is not a thread
* Thus a Service itself is very simple, two main features:
    * A facility for the application to tell the system about something it wants to be doing in the background
    * A facility for an application to expose some of its functionality to other applications.

``` Java
 Intent intent = new Intent(this, HelloService.class);
 startService(intent);
```

> An app is considered to be in the foreground if any of the following is true:
* It has a visible activity, whether the activity is started or paused
* It has a foreground service

> Another foreground app is connected to the app, either by binding to one of its services or by making use of one of its content providers. For example, the app is in the foreground if another app binds to its:
* IME (Input Method Editor) 
* Wallpaper service 
* Notification listener
* Voice or text service
> If none of those conditions is true, the app is considered to be in the background.

### Limitations
> To reduce the danger of apps sucking resources while in the background
* Android 8.0 (API level 26) imposes limitations on what apps can do while running in the background
* The system doesn't allow a background app to create a background service
* Android 8.0 requires the apps to call **startForegroundService()** to start a new service in the foreground
    * After the system has created the service, the app has five seconds to call the service's startForeground() method to show the new service's user-visible notification.
* If the app does not call startForeground() within the time limit, the system stops the service and declares the app to be ANR

``` Java
ForegroundService sensorService = new ForegroundService("Hello"); Intent serviceIntent = new Intent(getApplicationContext(), sensorService.getClass());
startForegroundService(serviceIntent);
```
``` XML
<application
    android:allowBackup="true" 
    android:icon="@mipmap/ic_launcher" 
    android:label="@string/app_name" 
    android:roundIcon="@mipmap/ic_launcher_round" 
    android:supportsRtl="true" 
    android:theme="@style/AppTheme">
    <activity android:name=".MainActivity">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" /> 
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter> 
    </activity>
    <service 
        android:name=".ForegroundService" 
        android:enabled="true" >
    </service> 
</application>
```
``` Java
public class ForegroundService extends IntentService {
    private static final int FOREGROUND_ID = 123456; 
    private static final String CHANNEL_ID = "9876543"; 
    public int counter=0;
    private Timer timer;
    private TimerTask timerTask;
    private String textTitle= "This is the Title";
    private String textContent= "This is the content of the notification";

    /**
    * Creates an IntentService. Invoked by your subclass's constructor.
    *
    * @param name Used to name the worker thread, important only for debugging. */
    public ForegroundService(String name) { 
        super(name);
    }
    public ForegroundService() { 
        super("this is my service");
    }
    @Override
    public void onCreate() {
        super.onCreate();
        Notification notification = mBuilder.build();
        startForeground(FOREGROUND_ID, notification)
    }
    @Override
    public int onStartCommand(Intent intent, int flags, int startId) { 
        super.onStartCommand(intent, flags, startId);
        startTimer();
        return START_STICKY;
    }
    NotificationCompat.Builder mBuilder = new NotificationCompat.Builder(this, CHANNEL_ID) 
        .setSmallIcon(R.drawable.notification_icon)
        .setContentTitle(textTitle)
        .setContentText(textContent)
        .setPriority(NotificationCompat.PRIORITY_LOW);
    public void startTimer() {
        //set a new Timer
        timer = new Timer();
        //initialize the TimerTask's job 
        initializeTimerTask();
        //schedule the timer, to wake up every 1 second 
        timer.schedule(timerTask, 1000, 1000); 
    }
    public void initializeTimerTask() {
         timerTask = new TimerTask() {
            public void run() {
            Log.i("in timer", "in timer ++++ "+ (counter++));
            }
        };
    }
}
```

## Location Tracking
* specifies a number of parameters
* A **callback function** called when a fix(a location) has been found
* A Looper (ignore)

> App must connect to location services and make a location request before requesting location updates

> Once a location request is in place you can start the regular updates by calling **requestLocationUpdates()**
``` Java
LocationRequest mLocationRequest = new LocationRequest();
mLocationRequest.setInterval(10000); // in msecs
mLocationRequest.setFastestInterval(5000); // in secs
mLocationRequest.setPriority(LocationRequest.PRIORITY_HIGH_ACCURACY);
startLocationUpdates();

 private void startLocationUpdates() {
     mFusedLocationClient.requestLocationUpdates(mLocationRequest, mLocationCallback, null /* Looper */);
 }

 mLocationCallback = new LocationCallback() { 
    @Override
    public void onLocationResult(LocationResult locationResult) { 
        super.onLocationResult(locationResult);
        mCurrentLocation = locationResult.getLastLocation(); 
        mLastUpdateTime = DateFormat.getTimeInstance().format(new Date()); 
        updateLocationUI(); // do something with the location
    } };
 private void stopLocationUpdates() {
     mFusedLocationClient.removeLocationUpdates(mLocationCallback);
 }
```

### Location in background
> Tracking locations in the background requires an **IntentService**
    * Define an **onHandleIntent** method to capture the identification of the location

> **onclicklistener** for start
``` Java
Intent intent = new Intent(context, LocationIntent.class);
mLocationPendingIntent = PendingIntent.getService(context, 1, intent, PendingIntent.FLAG_UPDATE_CURRENT); 
Task<Void> locationTask = mFusedLocationClient.requestLocationUpdates(mLocationRequest,
mLocationPendingIntent);
// ^^^^^^^^^^^^^^^^^^^^ this is instead of the callback and the Looper
if (locationTask != null) { 
    locationTask.addOnFailureListener(new OnFailureListener() {
        @Override
        public void onFailure(@NonNull Exception e) {
            if (e instanceof ApiException) {
                Log.w(TAG, ((ApiException) e).getStatusMessage());
            } else {
                Log.w(TAG, e.getMessage());
            } 
        }
    });
    locationTask.addOnCompleteListener(new OnCompleteListener<Void>() { 
        @Override
        public void onComplete(@NonNull Task<Void> task) { 
            Log.d(TAG, "restarting gps successful!");
        } 
    });
    } 
}
```

> The Location Intent
``` Java
public static class LocationIntent extends IntentService { 
    public LocationIntent(String name) {
        super(name);
    }
    public LocationIntent() {
        super("Location Intent"); 
    }
    /**
    * called when a location is recognised * @param intent
    */
    @Override
    protected void onHandleIntent(Intent intent) { 
        if (LocationResult.hasResult(intent)) {
            LocationResult locResults = LocationResult.extractResult(intent); 
            if (locResults != null) {
                for (Location location : locResults.getLocations()) {
                    if (location == null) continue;
                        //do something with the location
                        Log.i("New Location", "Current location: " + location); mCurrentLocation = location;
                        mLastUpdateTime = DateFormat.getTimeInstance().format(new Date()); Log.i("MAP", "new location " + mCurrentLocation.toString());
                        // check if the activity has not been closed in the meantime
                        if (MapsActivity.getActivity()!=null)
                            // any modification of the user interface must be done on the UI Thread. // The Intent Service is running
                            // in its own thread, so it cannot communicate with the UI. 
                            MapsActivity.getActivity().runOnUiThread(new Runnable() {
                            public void run() {
                                Log.i(“New Location”, “Current location: “+ location);
                            } 
                        });
                }
            }
        }
}
```

> If the app requires constant tracking of values even when app is in the background
* set up the sensor in onCreate
``` Java
@Override
public void onCreate() {
    super.onCreate();
    barometer= new StandardAndroidBarometer(this, database);
}
```
* start sensing in onStartCommand
``` Java
@Override
public int onStartCommand(Intent intent, int flags, int startId) {
    super.onStartCommand(intent, flags, startId);
    barometer.start(this)
}
```

### The Sensor (Barometer)
``` Java
public StandardAndroidBarometer() {
    timePhoneWasLastRebooted = System.currentTimeMillis() -SystemClock.elapsedRealtime();
    mSamplingRateNano = (long) (BAROMETER_READING_FREQUENCY) * 1000000;
    mSamplingRateInMSecs = (long) BAROMETER_READING_FREQUENCY;
    mSensorManager = (SensorManager) context.getSystemService(Context.SENSOR_SERVICE);
    mBarometerSensor = mSensorManager.getDefaultSensor(Sensor.TYPE_PRESSURE);
}

/**
*/
... }
 /** it starts the braometer if it is to be started check via isUseBarometer() and if it is
 not already started
 * @param context
 */
 public void start(final Context context){
    Log.d(TAG, "Using Standard Barometer");
    mPressureListener = new SensorEventListener() {
    @Override
    public void onSensorChanged(SensorEvent event) {
 ...
 @Override
 public void onAccuracyChanged(Sensor sensor, int accuracy) {
 }
```

### Never ending processes
* Create a delayed broadcast to a receiver in the onDestroy of the service
    * The receiver will restart the service

``` Java
public class SensorRestarterBroadcastReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) { 
        Log.i(SensorRestarterBroadcastReceiver.class.getSimpleName(), "Service Stops! Oooooooooooooppppssssss!!!!"); 
        context.startService(new Intent(context, SensorService.class));;
} }
```
``` XML
<application 
...
    <receiver
    android:name=".SensorRestarterBroadcastReceiver" android:enabled="true"
    android:exported="true" android:label="RestartServiceWhenStopped">
    </receiver>
... 
</application>
```
``` Java
// in the Service
public void onDestroy() {
    super.onDestroy();
    Log.i("EXIT", "onDestroy!");
    Intent broadcastIntent = new Intent(this, SensorRestarterBroadcastReceiver.class); sendBroadcast(broadcastIntent);
}
```
> If it is necessary to send by a couple of seconds so to wait for the process to die
``` Java
new java.util.Timer().schedule(
    new java.util.TimerTast() {
        @Override
        public void run() {
            // your code here
        }
    }
);
```
> This method will not work in Android 7 onwards

### Job Services
* A specialised type of services that performs based on conditions (e.g. when the phone is charging)
* it must be declared in the manifest as any other service
* it must be set up with conditions of execution attached
``` Java
 // create a component of type JobService
 ComponentName componentName = new ComponentName(this, MyJobService.class); 
//Create the conditions for running the job (connection to a specific network, charging, etc.).
// you must have at least one constraint
// If you want to run it in any case, use
// .setOverrideDeadline(0)
// see https://stackoverflow.com/questions/51064731/firing-jobservice-without-constraints
JobInfo jobInfo = new JobInfo.Builder(12, componentName) 
    .setRequiresCharging(true) 
    .setRequiredNetworkType(JobInfo.NETWORK_TYPE_UNMETERED) 
    .build();
// now schedule the job service
JobScheduler jobScheduler = (JobScheduler)getSystemService(JOB_SCHEDULER_SERVICE);
int resultCode = jobScheduler.schedule(jobInfo);
if (resultCode == JobScheduler.RESULT_SUCCESS) {
    Log.d(TAG, “Job scheduled!”);
} else {
    Log.d(TAG, “Job not scheduled”);
}

/**
* The state of at least one job has changed. Here is where we
* could enforce various
* policies on when we want to execute jobs.
* Right now the policy is such:
* If >1 of the ready jobs is idle mode we send all of them off
* if more than 2 network connectivity jobs are ready we send them all off.
* If more than 4 jobs total are ready we send them all off.
* TODO: It would be nice to consolidate these sort of high-level policies
somewhere.
*/

```

### Doze
* In Doze mode, the system attempts to **conserve battery by restricting apps' access to network and CPU-intensive services**
    * It also prevents apps from accessing the network and defers their jobs, syncs, and standard alarms.
* Periodically, the system exits Doze for a brief time to let apps complete their deferred activities. During this maintenance window, the system runs all pending syncs, jobs, and alarms, and lets apps access the network

> Restriction
* Network access is suspended
* The system ignores wake locks
* Standard AlarmManager alarms (including setExact() and setWindow()) are deferred to the next maintenance window
    * Alarms set with setAlarmClock() continue to fire normally — the system exits Doze shortly before those alarms fire
* The system does not perform Wi-Fi scans
* The system does not allow sync adapters to run

### Register a receiver
``` Java
void registerDozeReceiver(Context context) {
    IntentFilter filter = new IntentFilter(); 
    filter.addAction(PowerManager.ACTION_DEVICE_IDLE_MODE_CHANGED); 
    context.registerReceiver(mDozeReceiver, filter);
}
/**
 * RECEIVER FOR ANDROID 6 ENTERING DOZE
 * note that the receiver MUST be declared in code and NOT in AndroidManifest
 */
BroadcastReceiver mDozeReceiver = new BroadcastReceiver() { 
    @Override
    public void onReceive(Context context, Intent intent) {
        actOnDoze(context, intent, mNotification, mNotificationId); 
    }
};
```