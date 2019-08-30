Table of Contents
=================

  1. [install Ionic](#install-ionic)
  2. [Install Scooploop App](#install-scooploop-app)
  3. [Android](#android)
        1. [Install Android Studio](#install-android-studio)
            1. [Gradle for Linux](#gradle-forlinux)
            2. [Gradle for Ios](#gradle-for-ios)
        2. [Release App Android](#release-app-android)
  4. [Ios](#ios)
        1. [xCode](#xcode)
        2. [Release App Ios](#release-app-ios)
  5. [Issues](#issues)
  6. [Nvm](#nvm)



# install Ionic

```bash
npm install -g ionic@3.20.0
npm install -g cordova
```

## Install Scooploop App

```bash
mkdir sl3
git clone https://code.scooploop.com/Scooploop/scooploop-mobile.git .
npm i
```

test app on browser
```bash
ionic serve
```

## Android

### Install Android Studio

install Java 8
```bash
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```

[Download Android Studio](https://developer.android.com/studio)
```bash
sudo unzip android-studio-ide-141.2178183-linux.zip -d /opt
cd /opt/android-studio/bin
./studio.sh
```

Android SDK Tools PATH
```bash
export ANDROID_HOME=${HOME}/Android/Sdk
export PATH="${ANDROID_HOME}/tools:${PATH}"
```

#### Gradle for Linux
```bash
wget https://services.gradle.org/distributions/gradle-5.0-bin.zip -P /tmp
sudo unzip -d /opt/gradle /tmp/gradle-*.zip
```

```bash
sudo nano /etc/profile.d/gradle.sh
```

Paste the following configuration:
```bash
export GRADLE_HOME=/opt/gradle/gradle-5.0
export PATH=${GRADLE_HOME}/bin:${PATH}
```

```bash
sudo chmod +x /etc/profile.d/gradle.sh
source /etc/profile.d/gradle.sh
```

verify the gradle instalation
```bash
gradle -v
```

#### Gradle for Ios
```bash
brew install gradle
```
ionic cordova platform add android
ionic cordova run android
```

open project in android studio and install all upgrade needed
```bash
(project)/platform/android
```

when show "Error: spawn EACCES"
```bash
sudo chmod 755 (project)/platform/android/gradlew
```

javascript memory crash
```bash
node --max-old-space-size=4096 /usr/local/bin/ionic cordova build android --prod --release
```

### Release App Android
```bash
node --max-old-space-size=4096 /usr/local/bin/ionic cordova build android --prod --release
```

in main project folder
```bash
mkdir output

cd output

cp ../platforms/android/build/outputs/apk/release/android-release-unsigned.apk .
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore Scooploop.keystore android-release-unsigned.apk Scooploop
~/Android/Sdk/build-tools/28.0.3/zipalign -v 4 android-release-unsigned.apk scooploop.apk
```

open this link and login as app.Scooploop.com
[link](https://play.google.com/apps/publish/signup/)
```
click at Scooploop
go to release managment
then app releases 		
choose track
click manage
click create release

upload you .apk
add desc
save and review
```


##Ios

### xCode

Add platform ios
```bash
ionic cordova platform add ios
```

open this in xCode go to general tab in Signing and add new account
```
(project)/platform/ios/Scooploop.xcodeproj
```

in Info tab add
```
Privacy - Camera Usage Description, Microphone Usage Desctription, Photo Liblary Desctription
```

add Certifications
```
Creating Apple Certificates and Provisioning Profiles

In order to be able run and build apps you need to have Apple Developer Certificates and Profisioning Profiles. Login to Apple Developer page using info@scooploop.com account or ask the admin for an invitation to join the team.

[Apple Developer page] https://developer.apple.com
How to create a certificate to develop the app?

On Apple Developer page, from the sidemenu choose CERTIFICATES->Development->IOS App Development and press CONTINUE button, then follow the instructions on the screen (keep this page opened) then on your MAC open Keychain:

KEYCHAIN ACCESS->Certificate Assistant->Request a Certificate From a Certificate Authority

Fill up the information: User Email Address then choose Request is Saved to disc -> Click Continue and Save Back to Apple Developer page, click CONTINUE and Choose File… point at the certificate saved on your local machine. Done, now you can download the certificate and install it.
How to create a certificate to distribute the app?

For Distribution there is just exactly the same procedure as above. So on Apple Developer page choose CERTIFICATES->Production->IOS APP Production etc.
How to create a provisioning profile for development?

On Apple Developer page click Provisioning Profile->Development->IOS App Development, then click CONTINUE button and choose AppID (com.scooploop.app), click CONTINUE and select appropriate certificate from the list, click CONTINUE and choose the appropriate device (Adding devices is described in the section How to add a device) and then typein right name for the profile, click CONTINUE button and download and install your provisioning profile on your mac. Done
How to create a provisioning profile for distribution?

On Apple Developer page click Provisioning Profile->Distribution->App Store click CONTINUE, then select App ID (com.scooploop.app) and then choose the Certificate for the distribution, add a name for the profile, download and install it on your mac.
How to add a device?

On Apple Developer page choose DEVICES and add your iphone UUID to the list.
```

```bash
npm install -g ios-deploy
ionic cordova run ios
```

### Release App Ios
```bash
node --max-old-space-size=4096 /usr/local/bin/ionic cordova build ios --prod --release
```

open in xCode
```
(project)/platform/ios/Scooploop.xcworkspace
```


## Issues

[LICENCE issue](https://stackoverflow.com/questions/39760172/you-have-not-accepted-the-license-agreements-of-the-following-sdk-components)

```cordova plugin add cordova-android-support-gradle-release```

## NVM
[LINK](https://www.liquidweb.com/kb/how-to-install-nvm-node-version-manager-for-node-js-on-ubuntu-12-04-lts/)
