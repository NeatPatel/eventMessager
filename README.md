[Back to Main Page](https://neatpatel.github.io)
# Event Messager Project Blog
This project is an android based Java application that utilizes android studio, email plugins, and sqlite3 as the database to hold reminders for later. The project itself is a reminder app that can be used to create events that can be sent to anyone via email, text, whatsapp, copy paste, or any other form of text communication available as an app on one's phone. 

### Steps:

1. **Setting Up Environment:**
- Install Android Studio on your development machine.
- Ensure JDK (Java Development Kit) is properly configured.
- Create a new Android project in Android Studio. At the create project menu, be sure to select Empty Views Activity:

   ![](https://github.com/NeatPatel/eventMessager/blob/main/src/images/emptyViews.png?raw=true)

2. **Designing User Interface (UI):**
- The UI is designed using `xml` files for each activity, where an activity is a page of the application, similar to how html websites have different html files for each page site. Create three of these xml files:
  - The first file is for the main page that will show the previously created events, and a FAB button (in the bottom right corner) for creating new events. Call this file `activity_main.xml`
   - The second xml file will be for actually creating an event, prompting the user to fill out a form-like structured event with the option to customize the type of event they would like to create. This file will be called `activity_create_event.xml`
   - The third xml will be for sending emails or notifications to others about this event, allowing the user to select "Done" when they have sent all the messages they desire. Call this file `activity_email_clients.xml`

![](https://github.com/NeatPatel/eventMessager/blob/main/src/images/xmlFiles.png?raw=true)

- Before creating the initial UI, it is good practice to store all of the strings that will be hardcoded into the UI (such as text that says "Add new event") into a file known as `strings.xml`. This file should be under the `values` folder in the android studio application, but if not then create a file called `strings.xml` under the `values` directory. This would then be next to the `colors.xml` and `activity_decoration.xml` files. Here is an image of the types of strings and IDs associated with the xml strings that will be used later in this project:

![](https://github.com/NeatPatel/eventMessager/blob/main/src/images/stringFile.png?raw=true)

- For the `main_activity.xml` file, add a scroll view with a linear layout and a FAB (Floating Action Button) with the attributes specified in the images below. This activity has an intially blank linear layout because the program will update it as more events are created, or display a message "there are no events" when no events have been initialized (The scrollView's constraints should match the given image of constraints):

![](https://github.com/NeatPatel/eventMessager/blob/main/src/images/constraintLayout.png?raw=true)
![](https://github.com/NeatPatel/eventMessager/blob/main/src/images/FABAttributes.png?raw=true)
![](https://github.com/NeatPatel/eventMessager/blob/main/src/images/linearLayoutMainAttributes.png?raw=true)

- The `xml` file's contents are expressed as shown below:

<details>
   <summary>main_activity.xml code</summary>
   <br>
   
   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
       xmlns:app="http://schemas.android.com/apk/res-auto"
       xmlns:tools="http://schemas.android.com/tools"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:screenOrientation="portrait"
       tools:context=".MainActivity">
   
       <com.google.android.material.floatingactionbutton.FloatingActionButton
           android:id="@+id/floatingActionButton"
           android:layout_width="wrap_content"
           android:layout_height="109dp"
           android:layout_marginEnd="48dp"
           android:layout_marginBottom="48dp"
           android:clickable="true"
           android:contentDescription="@string/event_text"
           android:focusable="true"
           android:onClick="createEventClicked"
           app:fabCustomSize="60dp"
           app:fabSize="auto"
           app:layout_constraintBottom_toBottomOf="parent"
           app:layout_constraintEnd_toEndOf="parent"
           app:maxImageSize="50dp"
           app:shapeAppearanceOverlay="@style/fab_circle"
           app:srcCompat="@android:drawable/ic_input_add" />
   
       <ScrollView
           android:layout_width="0dp"
           android:layout_height="0dp"
           android:contentDescription="@string/first_fragment_label"
           app:layout_constraintBottom_toBottomOf="parent"
           app:layout_constraintEnd_toEndOf="parent"
           app:layout_constraintHorizontal_bias="0.0"
           app:layout_constraintStart_toStartOf="parent"
           app:layout_constraintTop_toTopOf="parent"
           app:layout_constraintVertical_bias="0.0">
   
           <LinearLayout
               android:id="@+id/card_layout"
               android:layout_width="match_parent"
               android:layout_height="wrap_content"
               android:layout_marginStart="36dp"
               android:layout_marginTop="100dp"
               android:layout_marginEnd="36dp"
               android:orientation="vertical" />
       </ScrollView>
   
   </androidx.constraintlayout.widget.ConstraintLayout>
   ```
</details>

- Notice the pattern of using "36dp" for margins. It is good practice to be consistent with margins through the application for even spacing between views.
- For the `activity_create_events.xml` file, add views (where views are items in the application that can be interacted with by the users) that match the following image:

![](https://github.com/NeatPatel/eventMessager/blob/main/src/images/createActivityLayout.png?raw=true)

- The `xml` for this file should be as follows:

<details>
   <summary>activity_create_events.xml code</summary>
   <br>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
       xmlns:app="http://schemas.android.com/apk/res-auto"
       xmlns:tools="http://schemas.android.com/tools"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       android:screenOrientation="portrait"
       tools:context=".CreateEvent">
   
       <ScrollView
           android:layout_width="match_parent"
           android:layout_height="match_parent"
           app:layout_constraintStart_toStartOf="parent"
           app:layout_constraintTop_toTopOf="parent">
   
           <LinearLayout
               android:layout_width="match_parent"
               android:layout_height="wrap_content"
               android:orientation="vertical"
               android:visibility="visible"
               tools:visibility="visible">
   
               <com.google.android.material.textfield.TextInputLayout
                   android:id="@+id/textInputLayout"
                   android:layout_width="335dp"
                   android:layout_height="wrap_content"
                   android:layout_marginStart="36dp"
                   android:layout_marginTop="120dp">
   
                   <com.google.android.material.textfield.TextInputEditText
                       android:id="@+id/event_name"
                       android:layout_width="match_parent"
                       android:layout_height="match_parent"
                       android:background="#ffffff"
                       android:hint="@string/new_event_input_name_text"
                       android:inputType="text"
                       android:maxLines="1"
                       android:overScrollMode="always"
                       android:scrollHorizontally="true"
                       android:textSize="24sp" />
               </com.google.android.material.textfield.TextInputLayout>
   
               <RadioGroup
                   android:layout_width="wrap_content"
                   android:layout_height="68dp"
                   android:layout_marginStart="36dp"
                   android:layout_marginTop="36dp"
                   android:orientation="horizontal">
   
                   <RadioButton
                       android:id="@+id/regular_event_radio"
                       android:layout_width="wrap_content"
                       android:layout_height="match_parent"
                       android:checked="true"
                       android:onClick="customEvent"
                       android:text="@string/regular_event" />
   
                   <RadioButton
                       android:id="@+id/custom_event_radio"
                       android:layout_width="wrap_content"
                       android:layout_height="match_parent"
                       android:onClick="customEvent"
                       android:text="@string/custom_event" />
   
               </RadioGroup>
   
               <LinearLayout
                   android:id="@+id/regular_event"
                   android:layout_width="match_parent"
                   android:layout_height="match_parent"
                   android:orientation="vertical">
   
                   <TextView
                       android:id="@+id/textView4"
                       android:layout_width="match_parent"
                       android:layout_height="wrap_content"
                       android:layout_marginStart="36dp"
                       android:layout_marginTop="36dp"
                       android:layout_marginEnd="36dp"
                       android:text="@string/regular_event_description_text" />
   
                   <EditText
                       android:id="@+id/event_description_multi_regular"
                       android:layout_width="wrap_content"
                       android:layout_height="wrap_content"
                       android:layout_marginStart="36dp"
                       android:layout_marginEnd="36dp"
                       android:autofillHints="@string/event_description_custom"
                       android:ems="10"
                       android:gravity="start|top"
                       android:hint="@string/event_description_regular"
                       android:inputType="textMultiLine"
                       android:textColorHint="@android:color/widget_edittext_dark"
                       android:textSize="20sp" />
   
                   <TextView
                       android:id="@+id/textView2"
                       android:layout_width="match_parent"
                       android:layout_height="wrap_content"
                       android:layout_marginStart="36dp"
                       android:layout_marginTop="36dp"
                       android:layout_marginEnd="36dp"
                       android:text="@string/regular_event_date_text" />
   
                   <EditText
                       android:id="@+id/event_day"
                       android:layout_width="wrap_content"
                       android:layout_height="wrap_content"
                       android:layout_marginStart="36dp"
                       android:layout_marginEnd="36dp"
                       android:autofillHints="@string/event_description_custom"
                       android:ems="10"
                       android:gravity="start|top"
                       android:hint="@string/event_date_regular"
                       android:inputType="textMultiLine"
                       android:textColorHint="@android:color/widget_edittext_dark"
                       android:textSize="20sp" />
               </LinearLayout>
   
               <LinearLayout
                   android:id="@+id/custom_event"
                   android:layout_width="match_parent"
                   android:layout_height="match_parent"
                   android:orientation="vertical"
                   android:visibility="visible"
                   tools:visibility="visible">
   
                   <TextView
                       android:id="@+id/textView"
                       android:layout_width="wrap_content"
                       android:layout_height="wrap_content"
                       android:layout_marginStart="36dp"
                       android:layout_marginTop="36dp"
                       android:layout_marginEnd="36dp"
                       android:text="@string/event_description_custom_title" />
   
                   <EditText
                       android:id="@+id/event_description_multi"
                       android:layout_width="wrap_content"
                       android:layout_height="wrap_content"
                       android:layout_marginStart="36dp"
                       android:layout_marginEnd="36dp"
                       android:autofillHints="@string/event_description_custom"
                       android:ems="10"
                       android:gravity="start|top"
                       android:hint="@string/event_description_custom"
                       android:inputType="textMultiLine"
                       android:textColorHint="@android:color/widget_edittext_dark"
                       android:textSize="20sp" />
               </LinearLayout>
   
               <Button
                   android:id="@+id/button2"
                   android:layout_width="wrap_content"
                   android:layout_height="wrap_content"
                   android:layout_marginStart="36dp"
                   android:layout_marginTop="36dp"
                   android:layout_marginEnd="36dp"
                   android:onClick="previewEvent"
                   android:text="@string/preview_event_button" />
   
               <TextView
                   android:id="@+id/event_preview"
                   android:layout_width="wrap_content"
                   android:layout_height="wrap_content"
                   android:layout_marginStart="36dp"
                   android:layout_marginEnd="36dp"
                   android:text="@string/event_preview" />
   
               <LinearLayout
                   style="?android:attr/buttonBarStyle"
                   android:layout_width="match_parent"
                   android:layout_height="match_parent"
                   android:layout_marginStart="36dp"
                   android:layout_marginTop="36dp"
                   android:layout_marginEnd="36dp"
                   android:orientation="horizontal">
   
                   <Button
                       android:id="@+id/button3"
                       style="?android:attr/buttonBarButtonStyle"
                       android:layout_width="wrap_content"
                       android:layout_height="wrap_content"
                       android:onClick="cancelCreateEvent"
                       android:text="@string/button_cancel" />
   
                   <Button
                       android:id="@+id/button"
                       style="?android:attr/buttonBarButtonStyle"
                       android:layout_width="wrap_content"
                       android:layout_height="wrap_content"
                       android:layout_marginStart="5dp"
                       android:layout_marginEnd="36dp"
                       android:onClick="submitEvent"
                       android:text="@string/button_create_event_name" />
               </LinearLayout>
   
           </LinearLayout>
       </ScrollView>
   
   </androidx.constraintlayout.widget.ConstraintLayout>
   ```
</details>

- Finally for the `activity_email_clients.xml` file, the layout itself should look like the following image:

![](https://github.com/NeatPatel/eventMessager/blob/main/src/images/emailClientsXml.png?raw=true)

- The `xml` for `activity_email_clients.xml` should be as follows:

<details>
   <summary>activity_email_clients.xml code</summary>
   <br>

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
       xmlns:app="http://schemas.android.com/apk/res-auto"
       xmlns:tools="http://schemas.android.com/tools"
       android:layout_width="match_parent"
       android:layout_height="match_parent"
       tools:context=".EmailClients">
   
       <ScrollView
           android:layout_width="match_parent"
           android:layout_height="match_parent"
           android:layout_marginTop="104dp"
           app:layout_constraintStart_toStartOf="parent"
           app:layout_constraintTop_toTopOf="parent">
   
           <LinearLayout
               android:layout_width="match_parent"
               android:layout_height="wrap_content"
               android:layout_marginStart="36dp"
               android:layout_marginEnd="36dp"
               android:orientation="vertical">
   
               <TextView
                   android:id="@+id/textView3"
                   android:layout_width="match_parent"
                   android:layout_height="wrap_content"
                   android:layout_marginLeft="36dp"
                   android:layout_marginTop="36dp"
                   android:layout_marginRight="36dp"
                   android:text="@string/email_text" />
   
               <EditText
                   android:id="@+id/manyMailBox"
                   android:layout_width="match_parent"
                   android:layout_height="wrap_content"
                   android:layout_marginStart="36dp"
                   android:layout_marginTop="36dp"
                   android:layout_marginEnd="36dp"
                   android:autofillHints="@string/email_example_text"
                   android:ems="10"
                   android:gravity="start|top"
                   android:hint="@string/email_example_text"
                   android:inputType="textMultiLine"
                   android:textColorHint="#716F6F"
                   android:textSize="24sp" />
   
               <Button
                   android:id="@+id/button4"
                   android:layout_width="match_parent"
                   android:layout_height="wrap_content"
                   android:layout_marginStart="36dp"
                   android:layout_marginTop="36dp"
                   android:layout_marginEnd="36dp"
                   android:onClick="sendEmail"
                   android:text="@string/button_send_email_text" />
   
               <Button
                   android:id="@+id/button5"
                   android:layout_width="match_parent"
                   android:layout_height="wrap_content"
                   android:layout_marginLeft="36dp"
                   android:layout_marginRight="36dp"
                   android:onClick="noEmails"
                   android:text="@string/button_cancel_emails_text" />
   
           </LinearLayout>
       </ScrollView>
   </androidx.constraintlayout.widget.ConstraintLayout>
   ```
</details>

3. **Implementing Program Base Functionality:**
- Develop Java classes to handle reminder creation, editing, deletion, and retrieval.
- Implement logic to interact with the SQLite database, including CRUD (Create, Read, Update, Delete) operations.
- Integrate date and time pickers to set reminder schedules.

4. **Adding Communication Options:**
- Integrate email plugins to allow users to send reminders via email.
- Implement functionality to send reminders via text messages (SMS), WhatsApp, or any other text communication app available on the device.
- Enable copying reminder details to the device clipboard for easy sharing through other apps.

5. **Database Setup:**
- Integrate SQLite3 as the local database for storing reminder data.
- Define the database schema, including tables for reminders and any related information.
- Implement SQLiteOpenHelper class to manage database creation, version management, and access.

6. **Testing and Debugging:**
- Test the application on various Android devices and screen sizes to ensure compatibility.
- Perform unit testing for individual components and functionality.
- Utilize Android Studio's debugging tools to identify and fix any issues.

7. **User Experience Enhancements:**
- Implement features to enhance user experience, such as notifications for upcoming reminders.
- Include options for customizing reminder preferences, such as sound alerts or recurring reminders.
- Ensure smooth navigation and intuitive interactions throughout the app.

8. **Optimization and Refinement:**
- Optimize code for performance and efficiency, considering factors like memory usage and battery consumption.
- Refine UI elements based on user feedback and usability testing.
- Continuously update and improve the app based on user suggestions and technological advancements.

9. **Documentation and Deployment:**
- Create comprehensive documentation covering app functionality, usage instructions, and technical details.
- Package the application for deployment on the Google Play Store or any other distribution platform.
- Follow platform-specific guidelines for app submission, including providing necessary metadata and assets.

### More information

For more information about this project or access to the actual repository for this application, visit [the Event Messager repository](https://github.com/NeatPatel/eventMessager)
