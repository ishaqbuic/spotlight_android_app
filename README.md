
Certainly! Here's a step-by-step guide on configuring a Jenkins job for building an Android app with GitHub on a Jenkins server running on Ubuntu:

Prerequisites:
Jenkins Installed:

Make sure you have Jenkins installed and running on your Ubuntu server.
Android SDK Installed:

Install the Android SDK on the Jenkins server.
GitHub Repository:

Have a GitHub repository containing your Android project.
Jenkins Configuration Steps:
1. Install Required Plugins:
Open Jenkins and navigate to "Manage Jenkins" > "Manage Plugins."
Install the following plugins:
GitHub plugin
Gradle plugin
Android Emulator plugin (if you plan to use an emulator)
Git plugin
2. Configure Global Android SDK Settings:
Navigate to "Manage Jenkins" > "Global Tool Configuration."
Find the "Android SDK" section and set the path to your Android SDK installation.
3. Create a New Jenkins Job:
Click on "New Item" on the Jenkins dashboard.
Enter a name for your project and select "Freestyle project."
4. Configure Source Code Management:
Under the "Source Code Management" section, select "Git."
Enter the GitHub repository URL.
Set the credentials you configured in Jenkins for accessing the GitHub repository.
5. Configure Build Steps:
Under the "Build" section, click on "Add build step" > "Invoke Gradle script."
Set the Gradle wrapper location or specify the path to your Gradle installation.
In the "Tasks" field, enter the Gradle tasks needed for your build (e.g., clean assembleDebug).
6. Configure Post-Build Actions:
Add post-build actions as needed, such as archiving artifacts, triggering other builds, or deploying the APK.
For example, you can use the "Archive the artifacts" action to archive the APK files.
7. Set Up GitHub Webhook (Optional):
In your GitHub repository, go to "Settings" > "Webhooks."
Add a new webhook, set the Payload URL to your Jenkins server's webhook URL, and configure the events to trigger the build.
8. Save and Run the Jenkins Job:
Save your Jenkins job configuration.
Click on "Build Now" to manually trigger the first build.
9. Monitor Build Results:
View the build console output and Jenkins build history to monitor the success or failure of your builds.
Remember to adjust the configuration based on your project's specific requirements, such as unit tests, build flavors, or other Gradle tasks needed for your Android app.

Command to build mannually on terminal  ./gradlew build
