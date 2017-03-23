# Run Cordova Projects in Android Studio

## Table of Contents
  * [Getting Started](#getting-started)
  * [Prerequisites](#prerequisites)
  * [Install Cordova Plugin](#install-cordova-plugin)
      * [Prepare Cordova Project](#prepare-Cordova-Project)
      * [Build Cordova Project](#build-cordova-project)
  * [Import to Android Studio](#import-to-android-studio)
  * [Run Project](#run-project)
  * [Conclusion](#conclusion)

## Getting Started               
  
  A Simple Guide to import existing Cordova Projects to Android Studio and Run 

### Prerequisites

* Any Cordova Project
* Cordova CLI
* Android Studio
* Cordova Plugin

## Install Cordova Plugin

In Android Studio 

   * Choose File->Settings or (Ctrl+Alt+s) 
   * Navigate to Plugins Tab
   * Choose ##Install JetBrains Plugins
   * Search for Phonegap/Cordova Plugin
   * Install the Plugin
   * restart Android Studio

## Prepare Cordova Project
   
   * Navigate to Cordova Project Folder
   * Open Cordova CLI
   
   ### Prepare Cordova Project

      Run this Command 
      ```
      $ cordova prepare android
      ```
      
   
    It will Prepares the Cordova Project for Android

   
   ### Build Cordova Project

      Run this Command 

      ```
      $ cordova build android
      ```

    It will Builds the Cordova Project for Android. (If the Required Gradle is Not Available it will be downloaded Automatically)


## Import to Android Studio

   * Open Android Studio
   * Choose File -> New -> Import Project
   * Navigate to The CordovaProject's Directory/platform
   * Select the Folder Android and Press Ok

   After that the Gradle build will begins and let it to be finish. 

## Run Project

   * Once the Gradle Build finished Click the RUN Icon or shift+F10 to Run the Project

  ##Note :no_entry_sign: 

## Conclusion
   
   :astonished: Yea hooo we did it  :raised_hands:  :smiley: 

* [Official Documentation](https://cordova.apache.org/docs/en/latest/guide/platforms/android/#opening-a-project-in-android-studio) - by Cordova

