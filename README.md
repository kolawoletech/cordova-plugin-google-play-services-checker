#Cordova Plugin Google Play Services Checker
Cordova/Ionic/Phonegap plugin for checking that the Google Play Services are installed, updated and enabled on Android device.

#Why
Users' Google Play Services should be updated if you want to have more accurate and fast GPS.
There is a native way to check and update it. No need to ask user to do it manual, just install this plugin.

#Installation
The plugin can be installed via Cordova-CLI and is publicly available on NPM.

Execute from the project root folder:

```shell
$ cordova plugin add cordova-plugin-google-play-services-checker
```

Or with Ionic

```shell
$ ionic cordova plugin add cordova-plugin-google-play-services-checker
```

#Usage
The plugin creates the object GooglePlayServicesChecker, and it's accessible after deviceready has been fired.

```js
document.addEventListener("deviceready", function () {
  var success = function (installedAndUpdated) {
    if (installedAndUpdated.status) {
      console.log("Google Play Services is installed and updated");
    } else {
      console.log("Showing user native update window");
    }
  };
  var failure = function (reason) {
    console.error("error: " + reason);
  };
  GooglePlayServicesChecker.check(success, failure);
});
```

Or for Ionic-v4:

```typescript
import { Platform } from '@ionic/angular';
@Component({...})
export class MyPage {
  constructor(public platform: Platform) {
    platform.ready().then(() => {
      var success = function(installedAndUpdated) {
        if (installedAndUpdated.status) {
          console.log('Google Play Services is installed and updated');
        } else {
          console.log('Showing user native update window');
        }
      }
      var failure = function(reason) {
        console.error('error: ' + reason)
      }
      (<any>window).GooglePlayServicesChecker.check(success, failure);
    });
  }
}
```

Or enhanced example for Ionic-v1:

```js
var googlePlayCheckedAndInstalled = false;
function googlePlayCheck() {
  if (window.cordova && !googlePlayCheckedAndInstalled) {
    var success = function (installedAndUpdated) {
      console.log("Google Play Services success: ", installedAndUpdated);
      if (installedAndUpdated.status) {
        console.log("Google Play Services is installed and updated");
        googlePlayCheckedAndInstalled = true;
      } else {
        console.log("Trying to show user native update window");
      }
    };
    var failure = function (reason) {
      console.error("Google Play Services error: " + reason);
    };
    GooglePlayServicesChecker.check(success, failure);
  }
}

googlePlayCheck();
$ionicPlatform.on("resume", function () {
  googlePlayCheck();
});
```
