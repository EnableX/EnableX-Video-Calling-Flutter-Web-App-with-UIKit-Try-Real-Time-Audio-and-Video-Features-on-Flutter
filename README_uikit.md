# EnableX Video Calling Flutter-Web App with UIKit : Try Real-Time Audio and Video Features on Flutter

To develop a Flutter web application seamlessly integrated using EnableX Flutter UIKit, harnessing the power of EnableX infrastructure, APIs, and Toolkit for exceptional real-time video and audio experiences. With this sample flutter web application, developers can explore and implement cutting-edge video calling functionalities.

Unlock the potential of this app to:

1. Establish Virtual Rooms: Utilize REST video APIs to effortlessly generate virtual rooms, providing a platform for seamless communication.

2. Secure Room Credentials: Acquire room credentials, including the unique Room ID, ensuring robust security and privacy for your users.

3. Join Virtual Rooms: Seamlessly participate in virtual rooms either as a moderator or participant, guaranteeing a secure and immersive video calling experience.

Experience the future of video communication with this Flutter web application, powered by EnableX for Flutter video calling, EnableX infrastructure, real-time video, audio features, and more.

## 1. Get started

### 1.1 Prerequisites

#### 1.1.1 App ID and App Key

You would need API Credentials to access EnableX platform. To do that, simply create an account with us. It’s absolutely free!

* Create an account with EnableX - https://portal.enablex.io/cpaas/trial-sign-up/
* Create your Project
* Get your App ID and App Key delivered to your email

#### 1.1.2 Requirement

* Android Studio/Visual Studio
* Language: Dart


#### 1.1.3 Sample Flutter Client

* Clone or download this Repository : https://github.com/EnableX/EnableX-Video-Calling-Flutter-Web-App-with-UIKit-Try-Real-Time-Audio-and-Video-Features-on-Flutter.git

#### 1.1.4 Application Server

An Application Server is required for your Flutter web Application to communicate with EnableX. We have different variants of Application Server Sample Code. Pick the one in your preferred language and follow instructions given in README.md file of respective Repository.

* NodeJS: https://github.com/EnableX/Video-Conferencing-Open-Source-Web-Application-Sample.git
* PHP: https://github.com/EnableX/Group-Video-Call-Conferencing-Sample-Application-in-PHP

Note the following:
•	You need to use App ID and App Key to run this Service.
•	Your Flutter Client EndPoint needs to connect to this Service to create Virtual Room and Create Token to join the session.
•	Application Server is created using [EnableX Server API](https://www.enablex.io/developer/video-api/server-api) while Rest API Service helps in provisioning, session access and post-session reporting.

If you would like to test the quality of EnableX video call before setting up your own application server,  you can run the test on our pre-configured environment. Refer to point 2 for more details on this.

### 1.2 Configure Flutter Client

* Open the App
* Go to constants.dart, it's reads:

``` 
 /* To try the App with Enablex Hosted Service you need to set the kTry = true
    When you setup your own Application Service, set kTry = false */
    
   const String urlBase =  'https://demo.enablex.io/';
   /* To try the app with Enablex hosted service you need to set the kTry = true */
    const bool kTry = true;
     /*Use enablec portal to create your app and get these following credentials*/
     const String kAppId = "app-id";
     const  String kAppkey = "app-key";

 
 ```

### 1.3 Test

#### 1.3.1 Open the App

* Open the flutter web application on any browser. You will get a form to enter Name, Room ID.
* If you don't have a Room ID, create a Room by clicking the "Create Room" button.
* Enter the Room ID in the Form to connect to the Virtual Room to carry out an RTC Session either as a Moderator or a Participant.
* Share Room ID with others to join the Virtual Room with you.

Note:
* This Sample Application created a Virtual Room with limited Participant and 1 Moderator only.
* In case of emulator/simulator your local stream will not create. It will create only on real device.

## 2. Testing Environment

If you would like to test the quality of EnableX video call before setting up your own Application server,  you can run the test on our [pre-configured environment.](https://try.enablex.io/)
In this environment, you will only be able to:

* Conduct a single session with a total durations of not more than 15 minutes
* Host a multiparty call with no more than 6 participants

> More information on Testing Environment: https://developer.enablex.io/video/sample-code/#demo-app-server

Once you have tested it, it is important that you set up your own Application Server to continue building a one to one or multiparty Flutter video calling app. Refer to section 1.1.4 on how to set up the Application Server.

## 3. Flutter UIKit

This Sample flutter web application uses EnableX Flutter UIKit to communicate with EnableX Servers to initiate, manage Real-Time Communications and create a beautify & customized Audio/Video/chat call UI. Please update your Application with latest version of EnableX Flutter UIKit as and when a new release is available.

## Flutter Web
Need to run on secure service like local host run on secure host .

To serve your Flutter web app over HTTPS using a custom certificate and key file while running it directly with Flutter's command-line tool, you currently need to use a workaround since Flutter's `flutter run -d chrome` doesn't natively support passing SSL certificate options. Instead, you can use a local HTTPS server to serve the built Flutter web app.

Here's how you can do it:

1. **Generate SSL Certificate and Key with `mkcert`**:
   - Follow the previous steps to install `mkcert` and generate a certificate and key for `localhost`.

    ```sh
    mkcert localhost
    ```

   This generates `localhost.pem` and `localhost-key.pem`.

2. **Build Your Flutter Web App**:
   - Build the Flutter web app to generate the necessary files.

    ```sh
    flutter build web
    ```

3. **Serve the Built Web App with an HTTPS Server**:
   - Use a simple HTTPS server, such as `http-server` with SSL support, to serve the built Flutter web app.

   **Install `http-server`**:
    ```sh
    npm install -g http-server
    ```

   **Run `http-server` with HTTPS**:
    ```sh
    http-server build/web -S -C localhost.pem -K localhost-key.pem -p 8080
    ```

   This serves the `build/web` directory over HTTPS on port 8080.

4. **Open Chrome with Flags**:
   - Open Chrome with the `--ignore-certificate-errors` flag to ignore self-signed certificate warnings.

   **On Linux or macOS**:
    ```sh
    google-chrome --ignore-certificate-errors --user-data-dir=/tmp/foo --allow-insecure-localhost https://localhost:8080
    ```

   **On macOS, if `google-chrome` command doesn't work**:
    ```sh
    /Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --ignore-certificate-errors --user-data-dir=/tmp/foo --allow-insecure-localhost https://localhost:8080
    ```

   **On Windows**:
    ```sh
    "C:\Program Files (x86)\Google\Chrome\Application\chrome.exe" --ignore-certificate-errors --user-data-dir=/tmp/foo --allow-insecure-localhost https://localhost:8080
    ```

### Alternative: Custom Web Server for Local Development

If you want a more integrated solution, you can create a simple custom server script in Dart to serve your Flutter web app with HTTPS. Below is an example using `shelf` and `shelf_static` packages.

**1. Add Dependencies**:
Add `shelf` and `shelf_static` to your `pubspec.yaml`.

```yaml
dependencies:
  shelf: ^1.3.0
  shelf_static: ^1.1.0
```

**2. Create a Custom Server Script (`server.dart`)**:
Create a Dart script to serve your Flutter web app with HTTPS.

```dart
import 'dart:io';
import 'package:shelf/shelf_io.dart' as io;
import 'package:shelf_static/shelf_static.dart';

void main() async {
   var handler = createStaticHandler('build/web', defaultDocument: 'index.html');
   var server = await io.serve(
      handler,
      InternetAddress.loopbackIPv4,
      8080,
      securityContext: SecurityContext()
         ..useCertificateChain('localhost.pem')
         ..usePrivateKey('localhost-key.pem'),
   );

   print('Serving at https://${server.address.host}:${server.port}');
}
```

**3. Run the Custom Server Script**:
Run the script using the Dart VM.

```sh
dart run server.dart
```

This serves your Flutter web app over HTTPS on `https://localhost:8080`.

### Summary

By building your Flutter web app and serving it with an HTTPS server like `http-server` or a custom Dart server using `shelf`, you can achieve running your Flutter web app over HTTPS. This workaround addresses the current limitation of `flutter run -d chrome` not supporting SSL certificate options directly.




# Here to beautify & customized the UI as follow

## Customize Bottom Bar

var setting = EnxSetting.instance;
setting.createBottomOption(BottomOption.audio);
setting.createBottomOption(BottomOption.video);
setting.createBottomOption(BottomOption.groupChat);
setting.createBottomOption(BottomOption.disconnect);
setting.createBottomOption(BottomOption.cameraSwitch);
T

## Customize Top Bar

var setting = EnxSetting.instance;
setting.createTopOption(TopOption.userList);
setting.createTopOption(TopOption.requestFloor);
setting.createTopOption(TopOption.menu);



# For more check this below document
* Documentation: https://www.enablex.io/developer/video/solutions/video-ui-kit/flutter-video-ui-kit/
* Download: https://pub.dev/packages/enx_uikit_flutter


## 4. Support

EnableX provides a library of Documentations, How-to Guides and Sample Codes to help software developers get started.

> Go to https://developer.enablex.io/.

You may also write to us for additional support at support@enablex.io.   
