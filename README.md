## Running the app using the main.jsbundle file (iOS)

First generate the jsbundle file:

```
react-native bundle --entry-file='index.js' --bundle-output='./ios/UdemyFastlane/main.jsbundle' --dev=false --platform='ios' --assets-dest='./ios'
```

Then in [ios/UdemyFastlane/AppDelegate.m](ios/UdemyFastlane/AppDelegate.m) comment out the line that loads the jsbundle via http:

```
jsCodeLocation = [[RCTBundleURLProvider sharedSettings] jsBundleURLForBundleRoot:@"index" fallbackResource:nil];
```

...and uncomment the line that loads the static jsbundle file:

```
jsCodeLocation = [[NSBundle mainBundle] URLForResource:@"main" withExtension:@"jsbundle"];
```

Ensure that the main.jsbundle file is included in the projects assets. This can be done by opening the project in XCode, selecting the main.jsbundle file and setting the 'Target Mebership' to the main project (UdemyFastlane).

Now try out the app in the ios simulator and you will see it's loading the static jsbundle file:

```
react-native run-ios
```

More details on these ad hoc doc changes [here](https://github.com/facebook/react-native/pull/16551/commits/21053cfe0110898f26908916fc33e223a6b30e3f)
