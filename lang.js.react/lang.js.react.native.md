## mac: 2022/11: env ruby rbenv
* brew install rbenv ruby-build
* rbenv install 2.7.5
* rbenv global 2.7.5
* vi .profile
    * eval "$(rbenv init - bash)"


## init
* npm uninstall -g react-native-cli react-native
* npx react-native init foo
* https://reactnative.dev/docs/next/environment-setup
    * brew install node
```
  Run instructions for Android:
    • Have an Android emulator running (quickest way to get started), or a device connected.
    • cd "/Users/mi/data/app/js/react-native/reactNativeInfoFeed" && npx react-native run-android
  Run instructions for iOS:
    • cd "/Users/mi/data/app/js/react-native/reactNativeInfoFeed" && npx react-native run-ios
    - or -
    • Open reactNativeInfoFeed/ios/reactNativeInfoFeed.xcworkspace in Xcode or run "xed -b ios"
    • Hit the Run button
  Run instructions for macOS:
    • See https://aka.ms/ReactNativeGuideMacOS for the latest up-to-date instructions.
```
* npm install
* ios
    * cocoapods
        * brew install cocoapods && cd ios && pod install
* npx react-native run-ios, npx react-native run-android
* npm start
* npm start -- --reset-cache
    * react-native-dotenv 의 .env 변경시


## npm install
* ~~npm install --save react-native-webview && react-native link react-native-webview~~
* npm install --save react-native-webview


## build: device: ios
* https://dev-yakuza.github.io/ko/react-native/ios-test-on-device/
* https://dev-yakuza.github.io/ko/react-native/ios-running-on-device/
* For list available AVDs
    * ~/Library/Android/sdk/tools/emulator -list-avds


## build: release: device: android
* https://dev-yakuza.github.io/ko/react-native/android-running-on-device/ 
    * cd foo/android/app 
    * keytool -genkey -v -keystore foo.keystore -alias foo -keyalg RSA -keysize 2048 -validity 10000 
    * foo.keystore 생성됨 
    * android/gradle.properties 편집 
        ```
        MYAPP_RELEASE_STORE_FILE=foo.keystore
        MYAPP_RELEASE_KEY_ALIAS=foo
        MYAPP_RELEASE_STORE_PASSWORD=*****
        MYAPP_RELEASE_KEY_PASSWORD=*****
        ```
    * android/app/build.gradle 편집
        ```
        ...
        android {
            ...
            defaultConfig { ... }
            signingConfigs {
                release {
                    if (project.hasProperty('MYAPP_RELEASE_STORE_FILE')) {
                        storeFile file(MYAPP_RELEASE_STORE_FILE)
                        storePassword MYAPP_RELEASE_STORE_PASSWORD
                        keyAlias MYAPP_RELEASE_KEY_ALIAS
                        keyPassword MYAPP_RELEASE_KEY_PASSWORD
                    }
                }
            }
            buildTypes {
                release {
                    ...
                    signingConfig signingConfigs.release
                }
            }
        }
        ...
        ```
    * 빌드
        *  cd android && ./gradlew assembleRelease
            * android/app/build/outputs/apk/release/app-release.apk 생성됨
            
