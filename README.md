Building App Navigation
In this session, you will build user-friendly app navigation through three primary patterns:
bottom navigation, the navigation drawer, and tabbed navigation. Through guided theory and
practice, you will learn how each of these patterns works so that users can easily access your
app’s content. This session will also focus on making the user aware of where they are in the app
and which level of your app’s hierarchy they can navigate to.
By the end of this session, you will know how to use these three primary navigation patterns
and understand how they work with the app bar to support navigation.
In the previous session, you explored fragments and the fragment lifecycle and employed
Jetpack navigation to simplify their use in your apps. In this session, you will learn how to add
different types of navigation to your app while continuing to use Jetpack navigation.
You will start off by learning about the navigation drawer, the earliest widely adopted navigational
pattern used in Android apps, before exploring bottom navigation and tab navigation. You’ll learn
about the Android navigation user flow, how it is built around destinations, and how they govern
navigation within the app.
The difference between primary and secondary destinations will be explained, as well as which one of
the three primary navigation patterns is more suitable, depending on your app’s use case.
We will cover the following topics in this session:
• Navigation overview
• Navigation drawer
• Bottom navigation
• Tabbed navigation

Building App Navigation

Navigation overview
The Android navigation user flow is built around destinations within your app. There are
primary destinations available at the top level of your app and, subsequently, are always displayed in the
main app navigation and secondary destinations. A guiding principle of each of the three navigation
patterns is to contextually provide information about the main section of the app the user is in at any
point in time.
This can take the form of a label in the top app bar of the destination the user is in, optionally
displaying an arrow hint that the user is not at the top level, and/or providing highlighted text and
icons in the user interface (UI) that indicate the section the user is in. Navigation in your app
should be fluid and natural, intuitively guiding the user while also providing some context of
where they are at any given point in time.
Each of the three navigation patterns you will explore accomplishes this goal in varying ways.
Some of these navigational patterns are more suitable for use with a higher number of top-level
primary destinations to display, and others are suitable for less.

Navigation drawer
The navigation drawer is one of the most common navigation patterns used in Android apps
and was certainly the first pattern to be widely adopted. The following is a screenshot of the
culmination of the next exercise, which shows a simple navigation drawer in its closed state:

Figure 4.1 – App with the navigation drawer closed

Navigation drawer

The navigation drawer is accessed through what has become commonly known as the hamburger
menu, which is the icon with three horizontal lines at the top left of Figure 4.1. The navigation options
are not visible on the screen, but contextual information about the screen you are on is displayed in
the top app bar.
An overflow menu can also accompany this on the right-hand side of the screen, through which other
contextually relevant navigation options can be accessed. The following screenshot is of a navigation
drawer in the open state, showing all the navigation options:

Figure 4.2 – App with the navigation drawer open

Upon selecting the hamburger menu, the navigation drawer slides out from the left with the current
section highlighted. This can be displayed with or without an icon. Due to the nature of the navigation
occupying the height of the screen, it is best suited to five or more top-level destinations.
The destinations can also be grouped together to indicate multiple hierarchies of primary destinations
(shown by the dividing line in the preceding screenshot), and these hierarchies can also have labels. In
addition, the drawer content is also scrollable. In summary, the navigation drawer is a very convenient
way to provide quick access to many different app destinations.
A weakness of the navigation drawer is that it requires the user to select the hamburger menu for the
destinations to become visible. Tabs and bottom navigation (with fixed tabs), in contrast, are always
visible. However, this is conversely also a strength of the navigation drawer as more screen space can
be used for the app’s content.
Let’s get started with the first exercise of this session and create a navigation drawer so that we
can access all the sections of an app.

Building App Navigation

Exercise 4.01 – creating an App with a navigation drawer
In this exercise, you will create a new app in Android Studio named Navigation Drawer using
the Empty Activity project template while leaving all the other defaults as they are. There are
wizard options where you can create a new project with all the navigation patterns you are going
to produce in the exercises within this session, but we will build the apps incrementally to guide
you through the steps.
You will build an app that often uses a navigation drawer, such as a news or mail app. The sections we
will be adding are Home, Favorites, Recents, Archive, Bin, and Settings.
Perform the following steps to complete this exercise:
1.

Create a new project with an Empty Activity called Navigation Drawer. Do not
use the Navigation Drawer Activity project template, as we are going to use incremental steps
to build the app.

2.

Add the Gradle dependencies you will require to app/build.gradle:
implementation
'androidx.navigation:navigation-fragment-ktx:2.5.3'
implementation
'androidx.navigation:navigation-ui-ktx:2.5.3'

3.

Update strings.xml and themes.xml in the res/values folder with the following content:

strings.xml
<string name="nav_header_desc">Navigation header</
string>
<string name="home">Home</string>
<string name="settings">Settings</string>
<string name="content">Content</string>
<string name="archive">Archive</string>
<string name="recent">Recent</string>
<string name="favorites">Favorites</string>
<string name="bin">Bin</string>
<string name="home_fragment">Home Fragment</string>
<string name="settings_fragment">Settings Fragment</
string>
<string name="content_fragment">Content Fragment</
string>
<string name="archive_fragment">Archive Fragment</

Navigation drawer

string>
<string name="recent_fragment">Recent Fragment</
string>
<string name="favorites_fragment">Favorites
Fragment</string>
<string name="bin_fragment">Bin Fragment</string>
<string name="link_to_content_button">Link to Content
Button</string>

themes.xml
<style name="Theme.NavigationDrawer.NoActionBar">
<item name="windowActionBar">false</item>
<item name="windowNoTitle">true</item>
</style>
<style name="Theme.NavigationDrawer.AppBarOverlay"
parent="ThemeOverlay.AppCompat.Dark.ActionBar" />
<style name="Theme.NavigationDrawer.PopupOverlay"
parent="ThemeOverlay.AppCompat.Light" />
4.

Next, update the activity element with name MainActivity in the AndroidManifest.
xml to NOT use an Action Bar. This will be provided by the Navigation Drawer layout. Go to
app | manifests | AndroidManifest.xml and add the android:theme attribute
with the NoActionBar style as in the snippet of code shown here:
<activity
android:name=".MainActivity"
android:exported="true"
android:theme=
"@style/Theme.NavigationDrawer.NoActionBar">

5.

Create the following fragments (File | New | Fragment | Fragment (Blank) making sure you
have app selected in the Project window:
 HomeFragment
 FavoritesFragment
 RecentFragment
 ArchiveFragment

Building App Navigation

 SettingsFragment
 BinFragment
 ContentFragment
6.

Change each of these fragment layouts to use the following content:
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
xmlns:android=
"http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
android:layout_width="match_parent"
android:layout_height="match_parent">
<TextView
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:layout_margin="8dp"
android:text="@string/home_fragment"
android:textAlignment="center"
android:layout_gravity="center_horizontal"
android:textSize="20sp"
app:layout_constraintBottom_toBottomOf="parent"
app:layout_constraintEnd_toEndOf="parent"
app:layout_constraintStart_toStartOf="parent"
app:layout_constraintTop_toTopOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>
The only difference is the android:text attribute, which will have the corresponding string
from the strings.xml file. So, create these fragments with the correct string, indicating
which fragment the user is viewing.
This may seem a bit repetitive, and one single fragment could be updated with this text, but it
demonstrates how you would separate different sections in a real-world app.

7.

Update the fragment_home.xml with the following content, which adds a button (this is
the body content you can see in Figure 4.1, with the closed navigation drawer):
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
xmlns:android=

Navigation drawer

"http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
android:layout_width="match_parent"
android:layout_height="match_parent">
<TextView
android:id="@+id/text_home"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:layout_margin="8dp"
android:text="@string/home_fragment"
android:textAlignment="center"
android:layout_gravity="center_horizontal"
android:textSize="20sp"
app:layout_constraintBottom_toBottomOf="parent"
app:layout_constraintEnd_toEndOf="parent"
app:layout_constraintStart_toStartOf="parent"
app:layout_constraintTop_toTopOf="parent" />
<Button
android:id="@+id/button_home"
android:layout_width="140dp"
android:layout_height="140dp"
android:layout_marginTop="16dp"
android:text="@string/link_to_content_button"
app:layout_constraintEnd_toEndOf="parent"
app:layout_constraintStart_toStartOf="parent"
app:layout_constraintTop_toBottomOf="@+id/text_
home" />
</androidx.constraintlayout.widget.ConstraintLayout>
TextView is the same as what’s specified in the other fragment layouts, except it has an ID
(id) with which it constrains the button below it.
8.

Create the navigation graph that will be used in the app. Select File | New | Android Resource
File (making sure the res folder is selected in the Project see this option. Select Navigation
as the Resource Type value and name it mobile_navigation.xml.

Building App Navigation

This creates the navigation graph:

Figure 4.3 – The Android Studio New Resource File dialog

9.

Open the mobile_navigation.xml file in the res/navigation folder and update it
with the code from the file in the following link. A truncated version of the code is shown here.
Use this link to access the entire code: https://packt.link/ZRDiT.

mobile_navigation.xml
<?xml version="1.0" encoding="utf-8"?>
<navigation xmlns:android=
"http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:id="@+id/mobile_navigation"
app:startDestination="@+id/nav_home">
<fragment
android:id="@+id/nav_home"
android:name="com.example.navigationdrawer.
HomeFragment"

Navigation drawer

android:label="@string/home"
tools:layout="@layout/fragment_home">
<action
android:id="@+id/nav_home_to_content"
app:destination="@id/nav_content"
app:popUpTo="@id/nav_home" />
</fragment>
…
This creates all the destinations in your app. However, it doesn’t specify whether these are
primary or secondary destinations. This should be familiar from the fragment Jetpack
navigation exercise from the previous session.
The most important point to note here is app:startDestination="@+id/nav_home,
which specifies what will be displayed to start with when the navigation loads and that there is
an action available from within HomeFragment to move to the nav_content destination
in the graph:
<action
android:id="@+id/nav_home_to_content"
app:destination="@id/nav_content"
app:popUpTo="@id/nav_home" />
You are now going to see how this is set up in HomeFragment and its layout.
10. Open HomeFragment and add two import statements for the Button and Navigation
imports and update onCreateView to set up the button:

HomeFragment
import android.widget.Button
import androidx.navigation.Navigation
override fun onCreateView(
inflater: LayoutInflater,
container: ViewGroup?,
savedInstanceState: Bundle?
): View? {
val view = inflater.inflate(R.layout.fragment_
home, container, false)
view.findViewById<Button> (R.id.button_home)?.
setOnClickListener(

Building App Navigation

Navigation.createNavigateOnClickListener
(R.id.nav_home_to_content, null)
)
return view
}
This uses the ClickListener navigation to complete the R.id.nav_home_to_content
action when button_home is clicked.
However, these changes will not do anything yet as you still need to set up the navigation host
for your app and add all the other layout files, along with the navigation drawer.
11. Create a Nav host fragment by creating a new file in the layout folder called content_main.xml.
This can be done by right-clicking on the layout folder in the res directory and then going to
File | New | Layout Resource File. Once created, update it with FragmentContainerView:
<?xml version="1.0" encoding="utf-8"?>
<androidx.fragment.app.FragmentContainerView
xmlns:android=
"http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
android:id="@+id/nav_host_fragment"
android:name="androidx.navigation.fragment.
NavHostFragment"
android:layout_width="match_parent"
android:layout_height="match_parent"
app:defaultNavHost="true"
app:navGraph="@navigation/mobile_navigation" />
12. You’ll notice that the navigation graph is set to the graph you just created:
app:navGraph="@navigation/mobile_navigation"
13. With that, the body of the app and its destination have been set up. Now, you need to set up
the UI navigation. Create another layout resource file called nav_header_main.xml and
add the following content:
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android=
"http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
android:layout_width="match_parent"

Navigation drawer

android:layout_height="176dp"
android:background="@color/teal_700"
android:gravity="bottom"
android:orientation="vertical"
android:paddingStart="16dp"
android:paddingTop="16dp"
android:paddingEnd="16dp"
android:paddingBottom="16dp"
android:theme="@style/ThemeOverlay.AppCompat.Dark">
<ImageView
android:id="@+id/imageView"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:contentDescription="@string/nav_header_
desc"
android:paddingTop= "8dp"
app:srcCompat="@mipmap/ic_launcher_round" />
<TextView
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:paddingTop= "8dp"
android:text="@string/app_name"
android:textAppearance= "@style/TextAppearance.
AppCompat.Body1" />
</LinearLayout>
This is the layout that’s displayed in the header of the navigation drawer.
14. Create the app bar with a toolbar layout file called app_bar_main.xml, and include the
following content:
<?xml version="1.0" encoding="utf-8"?>
<androidx.coordinatorlayout.widget.CoordinatorLayout
xmlns:android=
"http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"

Building App Navigation

android:layout_height="match_parent"
tools:context=".MainActivity">
<com.google.android.material.appbar.AppBarLayout
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:theme= "@style/Theme.NavigationDrawer.
AppBarOverlay">
<androidx.appcompat.widget.Toolbar
android:id="@+id/toolbar"
android:layout_width="match_parent"
android:layout_height="?attr/actionBarSize"
android:background="?attr/colorPrimary"
app:popupTheme= "@style/Theme.
NavigationDrawer.PopupOverlay" />
</com.google.android.material.appbar.AppBarLayout>
<include layout="@layout/content_main" />
</androidx.coordinatorlayout.widget.CoordinatorLayout>
This integrates the main body layout of the app with the app bar that appears above it. The
remaining part is to create the items that will appear in the navigation drawer and create and
populate the navigation drawer with these items.
15. To use icons with these menu items, you need to copy the vector assets in the drawable folder
of the completed exercise to the drawable folder of your project. Vector assets use coordinates
for points, lines, and curves to layout images with associated color information.
They are significantly smaller when compared to PNG and JPG images, and vectors can be
resized to different sizes without loss of quality. You can find them here: https://packt.
link/CurtF.
Copy the following drawables:
 favorites.xml
 archive.xml
 recent.xml
 home.xml
 bin.xml

Navigation drawer

16. Create a menu with these items. To do this, go to File | New | Android Resource File, select
Menu as the resource type, call it activity_main_drawer, and then populate it with the
following content:
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android=
"http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools"
tools:showIn="navigation_view">
<group
android:id="@+id/menu_top"
android:checkableBehavior="single">
<item
android:id="@+id/nav_home"
android:icon="@drawable/home"
android:title="@string/home" />
<item
android:id="@+id/nav_recent"
android:icon="@drawable/recent"
android:title="@string/recent" />
<item
android:id="@+id/nav_favorites"
android:icon="@drawable/favorites"
android:title="@string/favorites" />
</group>
<group
android:id="@+id/menu_bottom"
android:checkableBehavior="single">
<item
android:id="@+id/nav_archive"
android:icon="@drawable/archive"
android:title="@string/archive" />
<item
android:id="@+id/nav_bin"
android:icon="@drawable/bin"
android:title="@string/bin" />

Building App Navigation

</group>
</menu>
This sets up the menu items that will appear in the navigation drawer itself. The name of the
IDs is the magic that ties up the menu items to the destinations within the navigation graph.
If the IDs of the menu items (in activity_main_drawer.xml) exactly match the IDs of
the destinations in the navigation graph (which, in this case, are fragments within mobile_
navigation.xml), then the destination is automatically loaded into the navigation host.
17. The layout for MainActivity ties the navigation drawer to all the layouts specified previously.
Open activity_main.xml and update it with the following content:
<?xml version="1.0" encoding="utf-8"?>
<androidx.drawerlayout.widget.DrawerLayout
xmlns:android=
"http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:id="@+id/drawer_layout"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:fitsSystemWindows="true"
tools:openDrawer="start">
<include
layout="@layout/app_bar_main"
android:layout_width="match_parent"
android:layout_height="match_parent" />
<com.google.android.material.navigation.NavigationView
android:id="@+id/nav_view"
android:layout_width="wrap_content"
android:layout_height="match_parent"
android:layout_gravity="start"
android:fitsSystemWindows="true"
app:headerLayout="@layout/nav_header_main"
app:menu="@menu/activity_main_drawer" />
</androidx.drawerlayout.widget.DrawerLayout>
As you can see, an include is used to add app_bar_main.xml. The <include> element
allows you to add layouts that will be replaced at compile time with the actual layout itself.

Navigation drawer

18. They allow us to encapsulate different layouts as they can be reused in multiple layout files
within the app. NavigationView (the class that creates the navigation drawer) specifies
the layout files you have just created to configure its header and menu items:
app:headerLayout="@layout/nav_header_main"
app:menu="@menu/activity_main_drawer"
19. Now that you have specified all the layout files, update MainActivity by adding the following
interaction logic:
package com.example.navigationdrawer
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import androidx.navigation.findNavController
import androidx.navigation.fragment.NavHostFragment
import androidx.navigation.ui.*
import com.google.android.material.navigation.
NavigationView
class MainActivity : AppCompatActivity() {
private lateinit var appBarConfiguration:
AppBarConfiguration
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
setContentView(R.layout.activity_main)
setSupportActionBar(findViewById(R.id.toolbar))
val navHostFragment = supportFragmentManager.
findFragmentById(R.id.nav_host_fragment) as
NavHostFragment
val navController = navHostFragment.navController
//Creating top level destinations
//and adding them to the draw
appBarConfiguration = AppBarConfiguration(
setOf(
R.id.nav_home, R.id.nav_recent, R.id.nav_
favorites, R.id.nav_archive, R.id.nav_bin
), findViewById(R.id.drawer_layout)
)
setupActionBarWithNavController(navController,
appBarConfiguration)

Building App Navigation

findViewById<NavigationView>(R.id.nav_view)
?.setupWithNavController(navController)
}
override fun onSupportNavigateUp(): Boolean {
val navController = findNavController(R.id.nav_
host_fragment)
return navController.
navigateUp(appBarConfiguration) || super.
onSupportNavigateUp()
}
}
Now, let’s go through the preceding code. The setSupportActionBar(toolbar) line
configures the toolbar used in the app by referencing it from the layout and setting it. Retrieving
NavHostFragment is done with the following code:
val navHostFragment = supportFragmentManager
.findFragmentById(R.id.nav_host_fragment) as
NavHostFragment
val navController = navHostFragment.navController
Next, you add the menu items you want to display in the navigation drawer:
appBarConfiguration = AppBarConfiguration(
setOf(
R.id.nav_home, R.id.nav_recent, R.id.nav_
favorites, R.id.nav_archive, R.id.nav_bin
), findViewById(R.id.drawer_layout)
)
The drawer_layout is the container for the nav_view, the main app bar, and its
included content.
This may seem like you are doing this twice as these items are displayed in the activity_
main_drawer.xml menu for the navigation drawer. However, the function of setting these
in AppBarConfiguration is that these primary destinations will not display an up arrow
when they are selected as they are at the top level.
It also adds drawer_layout as the last parameter to specify which layout should be used when
the hamburger menu is selected to display in the navigation drawer. The next line is as follows:
setupActionBarWithNavController(navController,
appBarConfiguration)

Navigation drawer

This sets up the app bar with the navigation graph so that any changes that are made to the
destinations are reflected in the app bar:
findViewById<NavigationView> (R.id.nav_view)?.
setupWithNavController(navController)
This is the last statement in onCreate, and it specifies the item within the navigation drawer
that should be highlighted when the user clicks on it. The next function in the class handles
pressing the up button for the secondary destination, ensuring that it goes back to its parent
primary destination:
override fun onSupportNavigateUp(): Boolean {
val navController = findNavController(R.id.nav_host_
fragment)
return navController.navigateUp(appBarConfiguration)
|| super.onSupportNavigateUp()
}
The app bar can also display other menu items through the overflow menu, which, when
configured, is displayed as three vertical dots at the top on the right-hand side. Let’s create an
overflow menu to display the Settings screen.
20. To add the overflow menu to the app bar, go to File | New | Android Resource File. Select
Menu for the resource type and call the filename main.xml.
Update it with the following content:
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android=
"http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto">
<item
android:id="@+id/nav_settings"
android:title="@string/settings"
app:showAsAction="never" />
</menu>
This configuration shows one item: Settings. Since it specifies the same ID as the
SettingsFragment destination in the navigation graph, android:id="@+id/nav_
settings" it will open the SettingsFragment fragment.
The attribute being set to app:showAsAction="never" ensures it will stay as a menu
option within the three dots overflow menu and will not appear on the app bar itself. There
are other values for app:showAsAction, which set menu options to always appear on the
app bar and if there is room.

Building App Navigation

See the full list here: https://developer.android.com/guide/topics/resources/
menu-resource.
21. To add the overflow menu to the app bar, add the following to the MainActivity class:
override fun onCreateOptionsMenu(menu: Menu): Boolean {
menuInflater.inflate(R.menu.main, menu)
return true
}
override fun onOptionsItemSelected(item: MenuItem):
Boolean {
return item.onNavDestinationSelected(findNavController
(R.id.nav_host_fragment))
}
You will also need to add the following imports:
import android.view.Menu
import android.view.MenuItem
The onCreateOptionsMenu function selects the menu to add to the app bar, while
onOptionsItemSelected handles what to do when the item is selected using the
item.onNavDestinationSelected(findNavController(R.id.nav_host_
fragment)) navigation function. This is used to navigate to the destination within the
navigation graph.
22. Run the app and navigate to a top-level destination using the navigation drawer. The following
screenshot shows an example of navigating to the Recent destination:

Figure 4.4 – Recent menu item opened from the navigation drawer

Navigation drawer

23. When you open the navigation drawer again you will see that the Recent menu item is selected:

Figure 4.5 – The highlighted Recent menu item in the navigation drawer

24. Select the Home menu item again to display the button with the label LINK TO
CONTENT BUTTON:

Figure 4.6 – The Home screen with a button for the secondary destination

Building App Navigation

25. Click this button to go to the secondary destination. You will see an up arrow displayed:

Figure 4.7 – Secondary destination with an up arrow displayed

In all the preceding screenshots, the overflow menu is displayed. After selecting it, you will see a
Settings option appear. Upon pressing it, you will be taken to the Settings fragment with the up
arrow displayed:

Figure 4.8 – Settings Fragment

Although there are quite a few steps to go through to set up an app with a navigation drawer, once
created, it is very configurable. By adding a menu item entry to the drawer menu and a destination to
the navigation graph, a new fragment can be created and set up for use immediately.

Bottom navigation

This removes a lot of the boilerplate code you needed to use fragments in the previous session.
The next navigational pattern you’ll explore is bottom navigation. This has become the most
popular navigational pattern in Android, largely because it makes the main sections of the app easily
accessible.

Bottom navigation
Bottom navigation is used when there are a limited number of top-level destinations, and these
can range from three to five primary destinations that are not related to each other. Each item
on the bottom navigation bar displays an icon and an optional text label.
This navigation allows quick access as the items are always available, no matter which
secondary destination of the app the user navigates to.

Exercise 4.02 – adding bottom navigation to your app
Create a new app in Android Studio named Bottom Navigation using the Empty Activity
project template, leaving all the other defaults as they are. Do not use the Bottom Navigation
Activity project template, as we are going to use incremental steps to build the app.
You will build a loyalty app that provides offers, rewards, and so on for customers who have
signed up to use it. Bottom navigation is quite common for this kind of app because there will
typically be limited top-level destinations.
Let’s get started:
1. Many of the steps are very similar to the previous exercise, as you will be using Jetpack navigation
and defining destinations in a navigation graph and a corresponding menu.
2.

Create a new project with an Empty Activity called Bottom Navigation.

3.

Add the Gradle dependencies you will require to app/build.gradle:
implementation
'androidx.navigation:navigation-fragment-ktx:2.5.3'
implementation
'androidx.navigation:navigation-ui-ktx:2.5.3'

4.

Append strings.xml in the res/values folder with the following values:

strings.xml
<!-- Bottom Navigation -->
<string name="home">Home</string>
<string name="tickets">Tickets</string>

Building App Navigation

<string name="offers">Offers</string>
<string name="rewards">Rewards</string>
<!-- Action Bar -->
<string name="settings">Settings</string>
<string name="cart">Shopping Cart</string>
<string name="content">Content</string>
<string name="home_fragment">Home Fragment</string>
<string name="tickets_fragment">Tickets Fragment</
string>
<string name="offers_fragment">Offers Fragment</
string>
<string name="rewards_fragment">Rewards Fragment</
string>
<string name="settings_fragment"> Settings Fragment</
string>
<string name="cart_fragment"> Shopping Cart
Fragment</string>
<string name="content_fragment">Content Fragment</
string>
<string name="link_to_content_button"> Link to
Content Button</string>
5.

Create eight fragments with the following names:
 HomeFragment
 ContentFragment
 OffersFragment
 RewardsFragment
 SettingsFragment
 TicketsFragment
 CartFragment

6.

Apply the same layout that you applied in the previous exercise for all the fragments adding
the corresponding string resource except for fragment_home.xml. For this layout, use
the same layout file that you used in Exercise 4.01 – creating an App with a navigation drawer.

Bottom navigation

7.

Create the navigation graph as you did in the previous exercise and call it mobile_navigation.
xml. Update it with the code from the following file provided in the link. A truncated version
of the code is shown here. See the link for the entire code block you need to use: https://
packt.link/Fwuyl.

mobile_navigation.xml
<navigation xmlns:android=
"http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:id="@+id/mobile_navigation"
app:startDestination="@+id/nav_home">
<fragment
android:id="@+id/nav_home"
android:name="com.example.bottomnavigation.
HomeFragment"
android:label="@string/home"
tools:layout="@layout/fragment_home">
<action
android:id="@+id/nav_home_to_content"
app:destination="@id/nav_content"
app:popUpTo="@id/nav_home" />
</fragment>
…
8.

Update the onCreateView function in HomeFragment to use the destination in the navigation
graph to navigate to ContentFragment. You will also need to add the following imports:
import android.widget.Button
import androidx.navigation.Navigation
override fun onCreateView(
inflater: LayoutInflater,
container: ViewGroup?,
savedInstanceState: Bundle?
): View? {
val view = inflater.inflate(R.layout.fragment_home,
container, false)

Building App Navigation

view.findViewById<Button>(R.id.button_home)
?.setOnClickListener(
Navigation.createNavigateOnClickListener (R.id.
nav_home_to_content, null)
)
return view
}
9.

Now that the destinations have been defined in the navigation graph, create the menu in the
bottom navigation to reference these destinations. First, however, you need to gather the icons
that will be used in this exercise. Go to the completed exercise on GitHub and find the vector
assets in the drawable folder: https://packt.link/pUXvC.
Copy the following drawables to the drawable folder of your project:
 cart.xml
 home.xml
 offers.xml
 rewards.xml
 tickets.xml

10. Create a bottom_nav_menu.xml file (right click on the res folder and select Android
Resource File) and select Menu and then replace the contents with the following using all of
these icons except the cart.xml vector asset, which will be used for the top toolbar. Notice
that the IDs of the items match the IDs in the navigation graph:

bottom_nav_menu.xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android=
"http://schemas.android.com/apk/res/android">
<item
android:id="@+id/nav_home"
android:icon="@drawable/home"
android:title="@string/home" />
<item
android:id="@+id/nav_tickets"
android:icon="@drawable/tickets"
android:title="@string/tickets"/>
<item

Bottom navigation

android:id="@+id/nav_offers"
android:icon="@drawable/offers"
android:title="@string/offers" />
<item
android:id="@+id/nav_rewards"
android:icon="@drawable/rewards"
android:title="@string/rewards"/>
</menu>
11. Update the activity_main.xml file with the following content:

activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
xmlns:android=
"http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
android:id="@+id/container"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:paddingTop="?attr/actionBarSize">
<com.google.android.material.bottomnavigation.
BottomNavigationView
android:id="@+id/nav_view"
android:layout_width="0dp"
android:layout_height="wrap_content"
android:layout_marginStart="0dp"
android:layout_marginEnd="0dp"
android:background="?android:attr/windowBackground"
app:layout_constraintBottom_toBottomOf="parent"
app:layout_constraintStart_toStartOf="parent"
app:layout_constraintEnd_toEndOf="parent"
app:menu="@menu/bottom_nav_menu"
app:labelVisibilityMode="labeled"/>
<androidx.fragment.app.FragmentContainerView
android:id="@+id/nav_host_fragment"
app:layout_constraintStart_toStartOf="parent"

Building App Navigation

app:layout_constraintEnd_toEndOf="parent"
app:layout_constraintTop_toTopOf="parent"
android:name ="androidx.navigation.fragment.
NavHostFragment"
android:layout_width="match_parent"
android:layout_height="match_parent"
app:defaultNavHost="true"
app:navGraph="@navigation/mobile_navigation" />
</androidx.constraintlayout.widget.ConstraintLayout>
The BottomNavigation view is configured with the menu you created previously, that
is, app:menu="@menu/bottom_nav_menu", while FragmentContainerView is
configured with app:navGraph="@navigation/mobile_navigation". As the
bottom navigation in the app is not connected directly to the app bar, there are fewer layout
files to set up.
12. Update MainActivity with the following content:
package com.example.bottomnavigation
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import androidx.navigation.findNavController
import androidx.navigation.fragment.NavHostFragment
import androidx.navigation.ui.*
import com.google.android.material.bottomnavigation.
BottomNavigationView
class MainActivity : AppCompatActivity() {
private lateinit var appBarConfiguration:
AppBarConfiguration
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
setContentView(R.layout.activity_main)
val navHostFragment = supportFragmentManager.
findFragmentById (R.id.nav_host_fragment) as
NavHostFragment
val navController = navHostFragment.navController
//Creating top level destinations
//and adding them to bottom navigation
appBarConfiguration = AppBarConfiguration(setOf(
R.id.nav_home, R.id.nav_tickets, R.id.nav_

Bottom navigation

offers, R.id.nav_rewards))
setupActionBarWithNavController(navController,
appBarConfiguration)
findViewById<BottomNavigationView>(R.id.nav_view)
?.setupWithNavController(navController)
}
override fun onSupportNavigateUp(): Boolean {
val navController = findNavController(R.id.nav_
host_fragment)
return navController.
navigateUp(appBarConfiguration) || super.
onSupportNavigateUp()
}
}
The preceding code should be very familiar because it was explained in the previous exercise. The
main change here is that instead of a NavigationView that holds the main UI navigation for
the navigation drawer, it is now replaced with a BottomNavigationView. The configuration
after this is the same.
13. Run the app. You should see the following output:

Figure 4.9 – Bottom navigation with Home selected

Building App Navigation

14. The display shows the four menu items you set up, with the Home item selected as the start
destination. Click the square button to be taken to the secondary destination within Home:

Figure 4.10 – Secondary destination within Home

15. The action that makes this possible is the nav_home_to_content action specified in the
navigation graph:

mobile_navigation.xml (snippet)
<fragment
android:id="@+id/nav_home"
android:name="com.example.bottomnavigation.
HomeFragment"
android:label="@string/home"
tools:layout="@layout/fragment_home">
<action
android:id="@+id/nav_home_to_content"
app:destination="@id/nav_content"
app:popUpTo="@id/nav_home" />
</fragment>

Bottom navigation

16. Since only a limited amount of items are added to the bottom navigation (typically three to
five), sometimes action items (those that have a dedicated icon) are added to the app bar. Create
another menu called main.xml and add the following content:

main.xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android=
"http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto">
<item
android:id="@+id/nav_cart"
android:title="@string/cart"
android:icon="@drawable/cart"
app:showAsAction="always" />
<item
android:id="@+id/nav_settings"
android:title="@string/settings"
app:showAsAction="never" />
</menu>
17. This menu will be used in the overflow menu in the app bar. The overflow menu will be available
when you click on the three dots. A cart vector asset will also be displayed on the top app
bar because the app:showAsAction attribute is set to always. Configure the overflow
menu within MainActivity by adding the following:
Add these two imports at the top of the file:
import android.view.Menu
import android.view.MenuItem
And then these two functions:
override fun onCreateOptionsMenu(menu: Menu): Boolean {
menuInflater.inflate(R.menu.main, menu)
return true
}
override fun onOptionsItemSelected(item: MenuItem):
Boolean {
super.onOptionsItemSelected(item)
return item.onNavDestinationSelected(findNavController

Building App Navigation

(R.id.nav_host_fragment))
}
18. This will now display the main menu in the app bar. Run the app again, and you’ll see the following:

Figure 4.11 – Bottom navigation with the overflow menu

Selecting the shopping cart takes you to the secondary destination we configured in the navigation graph:

Figure 4.12 – Bottom navigation with the overflow menu in the secondary destination

Tabbed navigation

As you’ve seen in this exercise, setting up bottom navigation is quite straightforward. The navigation
graph and the menu setup simplify linking the menu items to the fragments. Additionally, integrating
the action bar and the overflow menu are also small steps to implement.
If you are developing an app that has very well-defined top-level destinations and switching between
them is important, then the visibility of these destinations makes bottom navigation an ideal choice.
The final primary navigation pattern to explore is tabbed navigation.
This is a versatile pattern as it can be used as an app’s primary navigation and as secondary navigation
with the other navigation patterns we’ve studied.

Tabbed navigation
Tabbed navigation is mostly used when you want to display related items. It is common to have fixed
tabs if there’s only a few of them (typically between two and five tabs) and scrolling horizontal tabs
if you have more than five tabs. They are used mostly for grouping destinations that are at the same
hierarchical level.
This can be the primary navigation if the destinations are related. This might be the case if the app you
developed is in a narrow or specific subject field where the primary destinations are related, such as a
news app. More commonly, it is used with bottom navigation to present secondary navigation that’s
available within a primary destination. The following exercise demonstrates using tabbed navigation
for displaying related items.

Exercise 4.03 – using tabs for app navigation
Create a new app in Android Studio with an Empty Activity named Tab Navigation. You
are going to build a skeleton movies app that displays the genres of movies. Let’s get started:
1.

Update the strings.xml with the following content:

strings.xml
<string name="action">Action</string>
<string name="comedy">Comedy</string>
<string name="drama">Drama</string>
<string name="sci_fi">Sci-Fi</string>
<string name="family">Family</string>
<string name="crime">Crime</string>
<string name="history">History</string>
<string name="dummy_text">
Lorem ipsum dolor sit amet, consectetuer

Building App Navigation

adipiscing elit. Aenean commodo ligula eget dolor.
Aenean massa. Cum sociis natoque penatibus et magnis dis
parturient montes, nascetur ridiculus mus. Donec quam
felis, ultricies nec, pellentesque eu, pretium quis,
sem. Nulla consequat massa quis enim. Donec pede justo,
fringilla vel, aliquet nec, vulputate eget, arcu. In enim
justo, rhoncus ut, imperdiet a, venenatis vitae, justo.
Nullam dictum felis eu pede mollis pretium. Integer
tincidunt. Cras dapibus. Vivamus elementum semper nisi.
Aenean vulputate eleifend tellus. Aenean leo ligula,
porttitor eu, consequat vitae, eleifend ac, enim. Aliquam
lorem ante, dapibus in, viverra quis, feugiat a, tellus.
Phasellus viverra nulla ut metus varius laoreet. Quisque
rutrum. Aenean imperdiet. Etiam ultricies nisi vel augue.
Curabitur ullamcorper ultricies nisi.
</string>
The <string name="dummy_text"> file specified provides some body text for each
movie genre:
2.

In order to be able to swipe through the tabs left and right, we need to use a ViewPager
component. Add the following dependency to app build.gradle:
implementation "androidx.viewpager2:viewpager2:1.0.0"

3.

Create a new blank MoviesFragment fragment which will display some body text and
replace the layout file content with the code following code snippet.

fragment_movies.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
xmlns:android=
"http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent"
tools:context=".MoviesFragment">
<TextView
android:layout_width="wrap_content"
android:layout_height="wrap_content"

Tabbed navigation

android:textSize="16sp"
android:text="@string/dummy_text"
android:padding="16dp"
app:layout_constraintStart_toStartOf="parent"
app:layout_constraintEnd_toEndOf="parent"
app:layout_constraintTop_toTopOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>
4.

Update the activity_main.xml file with the following content:
<androidx.constraintlayout.widget.ConstraintLayout
xmlns:android="http://schemas.android.com/apk/res/
android" xmlns:app="http://schemas.android.com/apk/
res-auto"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:orientation="vertical">
<com.google.android.material.tabs.TabLayout
app:layout_constraintTop_toTopOf="parent"
android:id="@+id/tab_layout"
android:layout_width="match_parent"
android:layout_height="wrap_content"
app:tabMode="fixed"/>
<androidx.viewpager2.widget.ViewPager2
app:layout_constraintTop_toBottomOf="@id/tab_layout"
android:id="@+id/view_pager"
android:layout_width="match_parent"
android:layout_height="wrap_content"/>
</androidx.constraintlayout.widget.ConstraintLayout>
The layout displays TabLayout at the top and notices that it sets the tabs to be fixed with the
app:tabMode="fixed" attribute. To display the required content, you will use ViewPager,
a swipeable layout that allows you to add multiple views or fragments so that when a user swipes
to change one of the tabs, the body content displays the corresponding view or fragment. For
this exercise, you are going to swipe between movie fragments.
The format of the tabs can be fixed so all are visible on the screen at the same time or scrollable, so
some tabs will initially be off-screen if they don’t fit within the horizontal screen space available.

Building App Navigation

Next, we need to provide the content for ViewPager. The component that provides the data
that’s used in ViewPager is called an adapter.
5.

Create a simple adapter that will be used to display our movies. Go to File | New | Kotlin Class/
File to create the class and call it MovieGenresAdapter:
package com.example.tabnavigation
import androidx.fragment.app.Fragment
import androidx.fragment.app.FragmentManager
import androidx.lifecycle.Lifecycle
import androidx.viewpager2.adapter.FragmentStateAdapter
val TAB_GENRES_SCROLLABLE = listOf(
R.string.action,
R.string.comedy,
R.string.drama,
R.string.sci_fi,
R.string.family,
R.string.crime,
R.string.history
)
val TAB_GENRES_FIXED = listOf(R.string.action, R.string.
comedy, R.string.drama)
class MovieGenresAdapter(fragmentManager:
FragmentManager, lifecycle: Lifecycle) :
FragmentStateAdapter(fragmentManager, lifecycle) {
override fun getItemCount(): Int {
return TAB_GENRES_FIXED.size
}
override fun createFragment(position: Int): Fragment
{
return MoviesFragment()
}
}

Tabbed navigation

First, look at the MovieGenresAdapter class header. It extends from
FragmentStateAdapter, which is an adapter used to populate fragments within
ViewPager.
The callback method’s functions are as follows:
 getItemCount(): This returns the total number of fragments we will be inserting,
which, as we are matching the number of pages to the number of tabs, is the size of the
TABS_GENRE_FIXED constant.
 createFragment(position Int): This creates the fragment to be displayed in
ViewPager at the passed in argument position. Here we are setting this to be the same
fragment, but in a real app, you would populate it with different fragments.
6.

Update MainActivity so that it uses tabs with ViewPager:
package com.example.tabnavigation
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import androidx.viewpager2.widget.ViewPager2
import com.google.android.material.tabs.TabLayout
import com.google.android.material.tabs.TabLayoutMediator
class MainActivity : AppCompatActivity() {
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
setContentView(R.layout.activity_main)
val viewPager = findViewById<ViewPager2>(R.
id.view_pager)
val tabLayout = findViewById<TabLayout>(R.id.tab_
layout)
val adapter =
MovieGenresAdapter(supportFragmentManager, lifecycle)
viewPager.adapter = adapter
TabLayoutMediator(tabLayout, viewPager) { tab,
position ->
tab.text = resources.getString(TAB_GENRES_

Building App Navigation

FIXED[position])
}.attach()
}
}
7.

You then retrieve the Views from the layout and link the tabs to ViewPager with the
TabLayoutMediator. The tab itself is exposed for you to customize. In this instance, we
are just setting the text. The position is also available to link the tab position to the fragment
position in ViewPager. Creating this tab navigation is simple and effective.

8.

Run the app up, and you should see the following:

Figure 4.13 – Tab layout with fixed tabs

You can swipe left and right in the body of the page to go to each of the three tabs, and you can
also select one of the respective tabs to perform the same action. Now, let’s change the tab data
that’s being displayed and set the tabs so that they can be scrolled through.
9.

First, change MovieGenresAdapter to use a few extra genres by updating the
getItemCount function:
override fun getItemCount(): Int {
return TAB_GENRES_SCROLLABLE.size
}

Tabbed navigation

10. In MainActivity, set TabLayoutMediator to use the updated item count in the Adapter
to set the tab text for these extra pages:
TabLayoutMediator(tabLayout, viewPager) { tab, position
->
tab.text = resources.getString(TAB_GENRES_
SCROLLABLE[position])
}.attach()
11. You will also need to change the a p p : t a b M o d e = " f i x e d " line to
app:tabMode="scrollable" in the activity_layout.xml file.
12. Run the app now, and you should see the following:

Figure 4.14 – The Tab Navigation layout with scrollable tabs

The list of tabs continues to display off the screen. The tabs can be swiped and selected, and the body
content can also be swiped so that you can go left and right through the tab pages.
With this exercise, you learned how versatile tabs are when it comes to providing navigation in an
app. Fixed-width tabs can be used for both primary and secondary navigation. At the same time,

Building App Navigation

scrollable tabs can be used to group related items together for secondary navigation, so you also need
to add primary navigation to the app.
In this example, the primary navigation has been omitted for simplicity, but for more real-world and
complex apps, you can either add a navigation drawer or bottom navigation.

Activity 4.01 – building primary and secondary app navigation
You have been tasked with creating a sports app. It can have three or more top-level destinations. One
of the primary destinations, however, must be called My Sports and should link to one or more
secondary destinations, which are sports. You can use any one of the navigation patterns we
have explored in this session or a combination of them, and you can also introduce any
customizations that you feel are appropriate.
There are different ways of attempting this activity. One approach would be to use bottom navigation
and add the individual secondary sports destinations to the navigation graph so that it can link to
these destinations. It is fairly simple and delegates to the navigation graph using actions. Here is what
the home screen should look like after using this approach:

Figure 4.15 – Bottom navigation for the My Sports app

Note
The solution to this activity can be found at: https://packt.link/By7eE.

Summary

Summary
This session covered the most important navigation techniques you need to know about in order
to create clear and consistent navigation in your apps. You started off by learning how to create an
Android Studio project with a navigation drawer to connect navigation menu items to individual
fragments using Jetpack navigation. You then progressed to actions within Jetpack navigation to
navigate to other secondary destinations in your app within the navigation graph.
The next exercise then used bottom navigation to display primary navigation destinations that are
always visible on the screen. We followed this by looking at tabbed navigation, where you learned
how to display both fixed and scrollable tabs. For each navigational pattern, you were shown
when it might be more suitable, depending on the type of app you were building. We finished this
session by building our own app using one or more of these navigational patterns and adding both
primary and secondary destinations.
This session built upon the comprehensive introduction we provided to Android with Android
Studio in session 1, Creating Your First App, as well as what you learned about activities and
fragments in session 2, Building User Screen Flows, and session 3, Developing the UI with Fragments.
These chapters covered the knowledge, practice, and fundamental Android components you
need to create apps. This session tied these previous chapters together by guiding you through the
primary navigational patterns available to make your apps stand out and be easy to use.
The next session will build on these concepts and introduce you to more advanced ways of
displaying app content. You will start off by learning about binding data with lists using
RecyclerView. After that, you will explore the different mechanisms you can use to retrieve and
populate content within apps.


