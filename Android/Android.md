# Hello Android

## Basis
> Android OS is a **multi-user Linux system**\
* Each app is a different user\
> The system assigns each app a **unique Linux user ID**
* unknown to the app
> The system sets permissions for all the files in an app
* so that only the user ID assigned to that app can access them
> Each process has its own **virtual machine (VM)**, so an app's code runs in isolation from other apps

> By default, every app runs in its own Linux process

## Execution
> The Android ststem perform the process when each components need to be runned

> It then shuts it down when
* It is no longer needed
* system must recover memory for other apps

> Android is based on the principle of least privilege
* Normally, each app has access only to the components needed to do its work
* This creates a very secure environment in which an app cannot access parts of the system for which it is not given permission

## Permissions
> There are some method for an app to share data with others in order to access system services

> Two types of permissions in Android M (6.0+)
* Dangerous permissions (user has to accept)
* Other permissions (user is not asked)

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
* sendBroadcast()
* sendOrderedBroadcast()
* sendStickyBroadcast()

```
Intent broadcastIntent =
          new Intent("uk.ac.shef.oak.myPackage.myFlag");
 sendBroadcast(broadcastIntent);
```

## App organisation
1. The Manifest file
2. The Java program
* providing dynamics in the app
* activities, dynamic changes to the UI, running services, etc.
3. The declarative resources
* static data
* icons, images, layouts, strings
4. The gradle scripts
* information about complication instructions, SDK levels, settings, link to libraries

## Layout for Activities
Each XML layout file is compiled into a View resouce. The layout resource should be load in Activity.onCreate() callback implementation.

``` Java
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
4. ViewPaper

## Controls
* Button
> 1. Button
* Text field
> 1. EditText
> 2. AutoCompleteTextView
* Checkbox
> 1. CheckBox
* Radio button
> 1. RadioGroup
> 2. RadioButton
* Toggle button
> 1. ToggleButton
* Spinner
> 1. Spinner
* Pickers
> 1. DatePicker
> 2. TimePicker

## Event Listeners
1. onClick()
* from **View.OnClickListener()**
2. onLongClick()
* from **View.OnLongClickListener()**
3. onFocusChange()
* from **View.OnFocusChangeListener()**
4. onKey()
* from **View.OnKeyListener()**
5. onTouch()
* from **View.OnTouchListener()**

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
* Do not use onPause() to do long operations
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
``` XML
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
``` XML
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
``` XML
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
* dp= the conversion of dp units to screen pixels is simple: px = dp * (dpi / 160)
* dpi= the quantity of pixels within a physical area of the screen; usually referred to as dpi (dots per inch).

``` XML
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
* The combination of data, state and bussiness logic

> View
* XML files

> Controller
* glue for tying the app together
* master controller for what happens in the application
* handle the event from user and decide to update the state of the view

<img src="https://miro.medium.com/max/606/1*smJy5uFyF5qucw6_7svnQA.png" alt="Controller">

> Presenter
* Activity/Fragment is now part of the view
* Easy for JUnit test

<img src="https://miro.medium.com/max/778/1*TuWeZzR14MmB-RBbjtZl-A.png" alt="Presenter">

> View Model
* responsible for wrapping the model and preparing observable data needed by the view
* provides hooks for the view to pass event to the model
* not tied to the view 

<img src="https://cdn.journaldev.com/wp-content/uploads/2018/04/android-mvvm-pattern.png" alt="Presenter">

## Persisting Data
### Key-Value sets
> SharedPreferences APIIs
``` Java
getShareddPreferences(String fileName)
getPreferences()

// eg.
Context context = getActivity();
SharedPreferences sharedPref = context.getSharedPreferences(“com.example.myapp.PREFERENCE_FILE_KEY”, Context.MODE_PRIVATE);
```
> Write
* get the preference file
``` Java
SharedPreferences sharedPref = getActivity().getPreferences(Context.MODE_PRIVATE);
```
* create a SharedPreferences.Editor by calling edit() on your SharedPreferences
``` Java
SharedPreferences.Editor editor = sharedPref.edit();
```
* Pass the ***keys and values*** as you would do to a HashSet but specifying a type
``` Java
editor.putInt(getString(R.string.saved_high_score), newHighScore);
```
* Use commit to save the change
``` Java
editor.commit();
```
> Read
* get int
``` Java
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
* SD Card
* getExternalFileDir()
2. internal storage
``` Java
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
* built-in non-volatile memory
* getFileDir()
* getCacheDir()
``` Java
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
``` Java 
myFile.delete();

myContext.deleteFile(fileName);
```
### Rooms
* implementation
```
implementation "android.arch.persistence.room:runtime:1.0.0"
```
* annotationProcessor
```
annotationProcessor "android.arch.persistence.room:compiler:1.0.0"
```
* testing Room migrations
```
testImplementation "android.arch.persistence.room:testing:1.0.0"
```
* RxJava
```
implementation "android.arch.persistence.room:runtime:1.0.0"
```
* Denendencies
``` gradle
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
* the database holder
* it serves as the main access point for the underlying connection to the relational data
* The class that's annotated with **@Database** should satisfy the following conditions:
  * abstract class that extends RoomDatabase
  * include the list of entities associated with the database within the annotation
  * Contain an abstract method that has 0 arguments and return the class that is annotated with @ Dao
* call Room.databaseBuilder() or Room.inMemoryDatabaseBuilder() to acquire an instance of DB
2. Entity
* Represents a **table** within the database
3. DAO
* Contains the **methods** used for accessing the database

``` Java
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
``` Java
@Entity(foreignKeys = @ForeignKey(entity = User.class, parentColumns = "id", childColumns = "User_id"))
```

> Use ***@Embeded*** annotation to represent an object that you'd like to decompose into **its subfield within a table**

### DAOs
> Can be either an interface or an abstract class.
``` Java
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