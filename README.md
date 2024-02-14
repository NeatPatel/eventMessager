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
   - The UI is designed using xml files for each activity, where an activity is a page of the application, similar to how html websites have different html files for each page site. Create three of these xml files:
      - The first file is for the main page that will show the previously created events, and a FAB button (in the bottom right corner) for creating new events. Call this file activity_main.xml
      - The second xml file will be for actually creating an event, prompting the user to fill out a form-like structured event with the option to customize the type of event they would like to create. This file will be called activity_create_event.xml
      - The third xml will be for sending emails or notifications to others about this event, allowing the user to select "Done" when they have sent all the messages they desire. Call this file activity_email_clients.xml
   - Utilize Android Studio's layout editor to create XML layout files for each screen.
   - 

3. **Database Setup:**
   - Integrate SQLite3 as the local database for storing reminder data.
   - Define the database schema, including tables for reminders and any related information.
   - Implement SQLiteOpenHelper class to manage database creation, version management, and access.

4. **Implementing Reminder Functionality:**
   - Develop Java classes to handle reminder creation, editing, deletion, and retrieval.
   - Implement logic to interact with the SQLite database, including CRUD (Create, Read, Update, Delete) operations.
   - Integrate date and time pickers to set reminder schedules.

5. **Adding Communication Options:**
   - Integrate email plugins to allow users to send reminders via email.
   - Implement functionality to send reminders via text messages (SMS), WhatsApp, or any other text communication app available on the device.
   - Enable copying reminder details to the device clipboard for easy sharing through other apps.

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

**More information**

For more information about this project or access to the actual repository for this application, visit [the Event Messager repository](https://github.com/NeatPatel/eventMessager)
