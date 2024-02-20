# Event Messager Project Blog
This project is an android based Java application that utilizes android studio, email plugins, and sqlite3 as the database to hold reminders for later. The project itself is a reminder app that can be used to create events that can be sent to anyone via email, text, whatsapp, copy paste, or any other form of text communication available as an app on one's phone. 

### Steps to Create this App:

1. #### Setting Up Environment:
- Install Android Studio on your development machine.
- Ensure JDK (Java Development Kit) is properly configured.
- Create a new Android project in Android Studio. At the create project menu, be sure to select Empty Views Activity:

   ![](https://github.com/NeatPatel/eventMessager/blob/main/src/images/emptyViews.png?raw=true)

2. #### Designing User Interface (UI):
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

<details markdown="1">
   <summary>
      [click me main_activity.xml code]
   </summary>

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
<br>

- Notice the pattern of using "36dp" for margins. It is good practice to be consistent with margins through the application for even spacing between views.
- For the `activity_create_events.xml` file, add views (where views are items in the application that can be interacted with by the users) that match the following image:

![](https://github.com/NeatPatel/eventMessager/blob/main/src/images/createActivityLayout.png?raw=true)

- The `xml` for this file should be as follows:

```
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

- Finally for the `activity_email_clients.xml` file, the layout itself should look like the following image:

![](https://github.com/NeatPatel/eventMessager/blob/main/src/images/emailClientsXml.png?raw=true)

- The `xml` for `activity_email_clients.xml` should be as follows:

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

#### 3. Implementing Program Base Functionality:
- The functionality of the application itself will depend on three Java classes: `MainActivity.java`, `CreateEvent.java`, and `EmailClients.java`. Each of these classes corresponds an xml file that was create previously, such as how `activity_main.xml` corresponds to `MainActivity.java`.
   - `MainActivity.java` needs to display all events in the database and have a listener function (created in the xml) that watches for the Create Event FAB button being pressed, taking the user to the next activity via an Intent.
   - `CreateEvent.java` is the second class (which `MainActivity.java` will redirect to after pressing FAB) and consists of a lot of views, with each component collecting data or showing previews to the user. The only way to create a new event is if all of the required fields have been filled out, such as the "Event Name" and "Event Description" for custom events. After creating an event, an Intent will be used to redirect the user to the third class' activity.
   - `EmailClients.java` is the third class and its function is to send out emails/texts or any other form of communication about the event that the user has just created. More information on how this part of the program is constructed is going to be detailed in step 4.

![](https://github.com/NeatPatel/eventMessager/blob/main/src/images/javaClassNames.png?raw=true)

- Here is the code for the first class `MainActivity.java`:
   
```java
package com.example.eventmanager;

import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;
import androidx.cardview.widget.CardView;

import android.content.DialogInterface;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.LinearLayout;
import android.widget.TextView;

import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {

    //For eventList, the first parameter is eventDescription and second is eventName
    private ArrayList<String[]> eventList = new ArrayList<>();
    final private EventDataBase db = new EventDataBase(MainActivity.this);

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        initialize();

        handleViews();
    }

    public void initialize() {
        eventList = db.getAllEvents();
    }

    public void handleViews() {
        for (int i = 0; i < eventList.size(); i++) {
            //Take event list and add CardViews for every item in eventList
            LinearLayout cardLayout = findViewById(R.id.card_layout);
            CardView cardView = new CardView(this);
            LinearLayout.LayoutParams params = new LinearLayout.LayoutParams(LinearLayout.LayoutParams.MATCH_PARENT, LinearLayout.LayoutParams.WRAP_CONTENT);
            if (i > 0) {
                params.topMargin = 36;
            } else {
                params.topMargin = 0;
            }
            cardView.setLayoutParams(params);

            LinearLayout innerCardView = new LinearLayout(this);
            innerCardView.setOrientation(LinearLayout.VERTICAL);
            params = new LinearLayout.LayoutParams(LinearLayout.LayoutParams.MATCH_PARENT, LinearLayout.LayoutParams.WRAP_CONTENT);
            innerCardView.setLayoutParams(params);

            LinearLayout innerTitleLayout = new LinearLayout(this);
            innerTitleLayout.setOrientation(LinearLayout.HORIZONTAL);
            params = new LinearLayout.LayoutParams(LinearLayout.LayoutParams.MATCH_PARENT, LinearLayout.LayoutParams.WRAP_CONTENT);
            innerTitleLayout.setLayoutParams(params);

            createView(innerCardView, innerTitleLayout, eventList.get(i));
            cardView.addView(innerCardView);
            cardLayout.addView(cardView);
        }

        checkEmptyList();
    }

    public void checkEmptyList() {
        if(eventList.size() == 0) {
            LinearLayout cardLayout = findViewById(R.id.card_layout);
            TextView noEventsYet = new TextView(this);
            String noEventsText = "There are no events yet";
            noEventsYet.setText(noEventsText);
            noEventsYet.setTextSize(20);
            LinearLayout.LayoutParams params = new LinearLayout.LayoutParams(LinearLayout.LayoutParams.WRAP_CONTENT, LinearLayout.LayoutParams.WRAP_CONTENT);
            params.topMargin = 100;
            noEventsYet.setLayoutParams(params);
            cardLayout.addView(noEventsYet);
        }
    }

    public void createEventClicked(View v) {
        //Run the create event activity

        Intent createEvent = new Intent(MainActivity.this, CreateEvent.class);
        Bundle bundle = new Bundle();
        for (int i = 0; i < eventList.size(); i++) {
            bundle.putStringArray("KEY_eventList_" + i, eventList.get(i));
        }
        bundle.putInt("KEY_eventList_size", eventList.size());
        createEvent.putExtras(bundle);
        startActivity(createEvent);
    }

    public void createView(LinearLayout innerCardLayout, LinearLayout innerTitleLayout, String[] event) {
        //Create a Card displaying event name and description/items

        LinearLayout.LayoutParams params = new LinearLayout.LayoutParams(LinearLayout.LayoutParams.WRAP_CONTENT, LinearLayout.LayoutParams.WRAP_CONTENT);

        TextView eventDescription = new TextView(this);

        TextView eventName = new TextView(this);
        String message = "Event: " + event[1];
        eventName.setText(message);
        eventName.setTextSize(24);
        params.weight = 0.9f;
        eventName.setLayoutParams(params);

        params = new LinearLayout.LayoutParams(LinearLayout.LayoutParams.WRAP_CONTENT, LinearLayout.LayoutParams.WRAP_CONTENT);
        message = "Event Description:\n" + event[0];
        eventDescription.setText(message);
        eventDescription.setTextSize(14);
        params.topMargin = 10;
        eventDescription.setLayoutParams(params);

        message = "Delete";
        Button delButton = new Button(this);
        delButton.setText(message);
        delButton.setTextSize(14);
        delButton.setOnClickListener(this::deleteView);
        params = new LinearLayout.LayoutParams(LinearLayout.LayoutParams.WRAP_CONTENT, LinearLayout.LayoutParams.WRAP_CONTENT);
        params.weight = 0.1f;
        delButton.setLayoutParams(params);

        innerTitleLayout.addView(eventName);
        innerTitleLayout.addView(delButton);
        innerCardLayout.addView(innerTitleLayout);
        innerCardLayout.addView(eventDescription);
    }

    public void deleteView(View v) {
        DialogInterface.OnClickListener dialogClickListener = (dialog, which) -> {
            if (which == DialogInterface.BUTTON_POSITIVE) {
                LinearLayout cardLayout = findViewById(R.id.card_layout);
                for (int i = 0; i < cardLayout.getChildCount(); i++) {
                    if (cardLayout.getChildAt(i) == v.getParent().getParent().getParent()) {
                        if (db.deleteOne(eventList.get(i)[1], eventList.get(i)[0])) {
                            eventList.remove(i);
                            cardLayout.removeView(cardLayout.getChildAt(i));
                        }
                        break;
                    }
                }

                checkEmptyList();
            }
        };

        AlertDialog.Builder builder = new AlertDialog.Builder(v.getContext());
        builder.setMessage("Are you sure you want to delete this event?").setPositiveButton("Delete", dialogClickListener)
                .setNegativeButton("Cancel", dialogClickListener).show();
    }
}
```

- The code for `CreateEvent.java` is as follows:

```java
package com.example.eventmanager;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.EditText;
import android.widget.LinearLayout;
import android.widget.RadioButton;
import android.widget.TextView;
import android.widget.Toast;

import java.util.ArrayList;
import java.util.Arrays;

public class CreateEvent extends AppCompatActivity {

    //For eventList, the first parameter is eventDescription and second is eventName
    private ArrayList<String[]> eventList = new ArrayList<>();
    final private EventDataBase db = new EventDataBase(CreateEvent.this);

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_create_event);
        LinearLayout customEventLayout = findViewById(R.id.custom_event);
        customEventLayout.setVisibility(View.GONE);

        initialize();
    }

    public void initialize() {
        eventList = db.getAllEvents();
    }

    public void customEvent(View v) {
        RadioButton customEventRadio = findViewById(R.id.custom_event_radio);
        LinearLayout customEventLayout = findViewById(R.id.custom_event);
        LinearLayout regularEventLayout = findViewById(R.id.regular_event);

        if(customEventRadio.isChecked()) {
            customEventLayout.setVisibility(View.VISIBLE);
            regularEventLayout.setVisibility(View.GONE);
        } else {
            customEventLayout.setVisibility(View.GONE);
            regularEventLayout.setVisibility(View.VISIBLE);
        }
    }

    public void submitEvent(View v) {
        RadioButton customEventRadio = findViewById(R.id.custom_event_radio);
        if(customEventRadio.isChecked()) {

            EditText eventDescription = findViewById(R.id.event_description_multi);
            EditText eventName = findViewById(R.id.event_name);
            String eventNameText = String.valueOf(eventName.getText());
            String eventDescriptionText = String.valueOf(eventDescription.getText());

            if(!eventDescriptionText.equals("") && !eventNameText.equals("") && isUnique(eventNameText, eventDescriptionText)) {
                Intent emailClients = new Intent(CreateEvent.this, EmailClients.class);
                Bundle bundle = new Bundle();
                String[] newEvent = {eventDescriptionText, eventNameText};
                if(db.addOne(eventNameText, eventDescriptionText)) {
                    eventList.add(newEvent);
                }

                for(int i = 0; i < eventList.size(); i++) {
                    bundle.putStringArray("KEY_eventList_" + i, eventList.get(i));
                }

                bundle.putInt("KEY_eventList_size", eventList.size());
                bundle.putStringArray("KEY_email_event", eventList.get(eventList.size() - 1));
                emailClients.putExtras(bundle);
                startActivity(emailClients);
            } else {
                Toast.makeText(this, "Please type UNIQUE event Name and Description", Toast.LENGTH_SHORT).show();
              }
        } else {
            EditText eventDescription = findViewById(R.id.event_description_multi_regular);
            EditText eventName = findViewById(R.id.event_name);
            EditText eventDate = findViewById(R.id.event_day);
            String eventNameText = String.valueOf(eventName.getText());
            String eventDescriptionText = String.valueOf(eventDescription.getText());
            String eventDateText = String.valueOf(eventDate.getText());

            String message = eventDescriptionText + "\nDate: " + eventDateText;

            if(!eventDescriptionText.equals("") && !eventNameText.equals("") && !eventDateText.equals("") && isUnique(eventNameText, message)) {
                //Intent mainActivity = new Intent(CreateEvent.this, MainActivity.class);

                Intent emailClients = new Intent(CreateEvent.this, EmailClients.class);
                Bundle bundle = new Bundle();
                String[] newEvent = {message, eventNameText};
                if (db.addOne(eventNameText, eventDescriptionText)) {
                    eventList.add(newEvent);
                }

                for(int i = 0; i < eventList.size(); i++) {
                    bundle.putStringArray("KEY_eventList_" + i, eventList.get(i));
                }

                bundle.putInt("KEY_eventList_size", eventList.size());
                bundle.putStringArray("KEY_email_event", eventList.get(eventList.size() - 1));
                emailClients.putExtras(bundle);
                startActivity(emailClients);
        } else {
                Toast.makeText(this, "Please type UNIQUE event Name, Date, and Description", Toast.LENGTH_SHORT).show();
            }
        }
    }

    public boolean isUnique(String eventName, String eventDescription) {
        String[] checkEvent = {eventDescription, eventName};
        for(int i = 0; i < eventList.size(); i++) {
            if(Arrays.equals(checkEvent, eventList.get(i))) {
                return false;
            }
        }
        return true;
    }

    public void previewEvent(View v) {
        RadioButton customEventRadio = findViewById(R.id.custom_event_radio);

        if(customEventRadio.isChecked()) {
            EditText eventDescription = findViewById(R.id.event_description_multi);
            String eventDescriptionText = String.valueOf(eventDescription.getText());
            TextView tempText = findViewById(R.id.event_preview);

            if(!eventDescriptionText.equals("")) {
                tempText.setText(eventDescriptionText);
            } else {
                Toast.makeText(this, "Please type event Description", Toast.LENGTH_SHORT).show();
            }
        } else {
            EditText eventDescription = findViewById(R.id.event_description_multi_regular);
            EditText eventDate = findViewById(R.id.event_day);
            String eventDescriptionText = String.valueOf(eventDescription.getText());
            String eventDateText = String.valueOf(eventDate.getText());
            TextView tempText = findViewById(R.id.event_preview);

            if(!eventDescriptionText.equals("") && !eventDateText.equals("")) {
                String message = eventDescriptionText + "\nDate: " + eventDateText;
                tempText.setText(message);
            } else {
                Toast.makeText(this, "Please type event Description and Date", Toast.LENGTH_SHORT).show();
            }
        }
    }

    public void cancelCreateEvent(View v) {
        Intent mainActivity = new Intent(CreateEvent.this, MainActivity.class);
        Bundle bundle = new Bundle();

        for(int i = 0; i < eventList.size(); i++) {
            bundle.putStringArray("KEY_eventList_" + i, eventList.get(i));
        }

        bundle.putInt("KEY_eventList_size", eventList.size());
        mainActivity.putExtras(bundle);
        startActivity(mainActivity);
    }
}
```

- With these steps complete, the only parts remaining for the project are email plugins for communication and a database to store events

4. #### Adding Communication Options:
- For this step, `EmailClients.java` is needed in order to send out emails or texts to any recipients of the event that the user would like to notify.
- `EmailClients.java` uses an Intent with a destination called "Send mail..." to send emails or other forms of messages to recipients that the user desires to send them to.
- The code for `EmailClients.java` is as follows:

```java
package com.example.eventmanager;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.EditText;
import android.widget.Toast;

import java.util.ArrayList;

public class EmailClients extends AppCompatActivity {

    private ArrayList<String[]> eventList = new ArrayList<>();
    final private EventDataBase db = new EventDataBase(EmailClients.this);
    private String[] emailEvent = new String[]{};
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_email_clients);

        initialize();
    }

    public void initialize() {
        if(getIntent() != null) {
            Intent contentReceived = getIntent();
            Bundle bundle = contentReceived.getExtras();

            if(bundle != null) {
                emailEvent = bundle.getStringArray("KEY_email_event");
            }
        }
        eventList = db.getAllEvents();
    }

    public void sendEmail(View v) {
        EditText emailBox = findViewById(R.id.manyMailBox);

        if(!String.valueOf(emailBox.getText()).equals("")) {
            Intent emailIntent = new Intent(Intent.ACTION_SEND);
            emailIntent.setType("text/plain");

            String eventName = emailEvent[1];
            String eventDescription = emailEvent[0];
            String[] emails = String.valueOf(emailBox.getText()).split(",", 0);

            emailIntent.putExtra(Intent.EXTRA_EMAIL, emails);
            emailIntent.putExtra(Intent.EXTRA_SUBJECT, "Event Email Notification");
            emailIntent.putExtra(Intent.EXTRA_TEXT, "Hello there!\nYou are being notified about the following Event: " + eventName + "\nThis event has the following description:\n" + eventDescription);

            try {
                startActivity(Intent.createChooser(emailIntent, "Send mail..."));
            } catch (android.content.ActivityNotFoundException ex) {
                Toast.makeText(this, "There is no email client installed.", Toast.LENGTH_SHORT).show();
            }
        } else {
            Toast.makeText(this, "Please enter at least one email address", Toast.LENGTH_SHORT).show();
        }
    }

    public void noEmails(View v) {
        Intent mainActivity = new Intent(EmailClients.this, MainActivity.class);
        Bundle bundle = new Bundle();

        for(int i = 0; i < eventList.size(); i++) {
            bundle.putStringArray("KEY_eventList_" + i, eventList.get(i));
        }

        bundle.putInt("KEY_eventList_size", eventList.size());
        mainActivity.putExtras(bundle);
        startActivity(mainActivity);
    }
}
```

5. #### Database Setup:
- This Event app is a small scale event based reminder app that will mainly only require a small maintainable database to store the data for future use, so a perfect plugin to use for this project is sqlite. Sqlite in android studio requires specific class inherited and interface methods in order to execute so that its SqliteOpenHelper class can be extended and used properly.
- To create a database, add a file called `EventDataBase.java`, and add the following code to it:

```java
package com.example.eventmanager;

import android.content.ContentValues;
import android.content.Context;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;

import androidx.annotation.Nullable;

import java.util.ArrayList;

public class EventDataBase extends SQLiteOpenHelper {

    public static final String TABLE_NAME = "events";
    public static final String COLUMN_EVENT_NAME = "EVENT_NAME";
    public static final String COLUMN_EVENT_DESC = "EVENT_DESC";

    //Constructor for superclass SQLiteOpenHelper
    public EventDataBase(@Nullable Context context) {
        super(context, "events.db", null, 1);
    }

    //This method is executed the first time a database is called in program for initialization
    @Override
    public void onCreate(SQLiteDatabase db) {
        String createTableStatement = "CREATE TABLE " + TABLE_NAME + " (" + COLUMN_EVENT_NAME + " TEXT NOT NULL, " + COLUMN_EVENT_DESC + " TEXT NOT NULL, UNIQUE (" + COLUMN_EVENT_NAME + ", " + COLUMN_EVENT_DESC + "))";

        db.execSQL(createTableStatement);
    }

    //This method is called every time the version number changes
    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {

    }

    public boolean addOne(String eventName, String eventDesc) {
        SQLiteDatabase db = this.getWritableDatabase();
        ContentValues cv = new ContentValues();

        cv.put(COLUMN_EVENT_NAME, eventName);
        cv.put(COLUMN_EVENT_DESC, eventDesc);

        long insert = db.insert(TABLE_NAME, null, cv);

        db.close();

        return insert != -1;
    }

    public boolean deleteOne(String eventName, String eventDesc) {
        SQLiteDatabase db = this.getWritableDatabase();
        //DELETE FROM TABLE_NAME WHERE COLUMN_EVENT_NAME = 'eventName' AND COLUMN_EVENT_DESC = 'eventDesc';
        String queryString = "DELETE FROM " + TABLE_NAME + " WHERE " + COLUMN_EVENT_NAME + " = \"" + eventName + "\" AND " + COLUMN_EVENT_DESC + " = \"" + eventDesc + "\"";

        Cursor cursor = db.rawQuery(queryString, null);

        boolean resultBoolean = !cursor.moveToFirst();
        cursor.close();
        db.close();
        return resultBoolean;
    }

    public ArrayList<String[]> getAllEvents() {
        ArrayList<String[]> events = new ArrayList<>();

        String queryString = "SELECT * FROM " + TABLE_NAME;
        SQLiteDatabase db = this.getReadableDatabase();

        Cursor cursor = db.rawQuery(queryString, null);

        if(cursor.moveToFirst()) {
            do {
                String eventName = cursor.getString(0);
                String eventDesc = cursor.getString(1);

                String[] newEvent = {eventDesc, eventName};
                events.add(newEvent);
            } while(cursor.moveToNext());
        }

        //Close both cursor and database once the connection is complete
        cursor.close();
        db.close();
        return events;
    }
}
```

6. #### Documentation and Deployment:
- This is all of the content required for the implementation of the Event Manager application, and any further additions can be done so by modifying the program according to the way that it was written.

### More information

For more information about this project or access to the actual repository for this application, visit [the Event Messager repository](https://github.com/NeatPatel/eventMessager)
