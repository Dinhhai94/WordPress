# WordPress for Android #

[![Build Status](https://travis-ci.org/wordpress-mobile/WordPress-Android.svg?branch=develop)](https://travis-ci.org/wordpress-mobile/WordPress-Android)

If you're just looking to install WordPress for Android, you can find
it on [Google Play](https://play.google.com/store/apps/details?id=org.wordpress.android). If you're a developer wanting to contribute, read on.


## Build Instructions ##

1. Install [JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
2. Install [Android Studio](https://developer.android.com/studio/index.html).
3. Run Android Studio and do a "Standard setup"
4. Clone this GitHub repository.
5. Find the Android SDK path (in Android Studio under Preferences → Appearance → System Settings → Android SDK).
6. Create a new `local.properties` file in your local repository containing `sdk.dir=ANDROID_SDK_PATH`, replacing `ANDROID_SDK_PATH` with your path from the previous point.
7. Copy `gradle.properties-example` to `gradle.properties`.
8. Run Android Studio.
9. Import the project from the local repository as a Gradle project.
9. Configure device with AVD Manager (Tools → Android → AVD Manager).
10. Run.

Notes:

* To use WordPress.com features (login to WordPress.com, access Reader and Stats, etc) you need a WordPress.com OAuth2 ID and secret. Please read the
[OAuth2 Authentication](#oauth2-authentication) section.

Once installed, you can now build, install and test the project from the command line:

    $ ./gradlew assembleVanillaDebug # assemble the debug .apk
    $ ./gradlew installVanillaDebug  # install the debug .apk if you have an
                                     # emulator or an Android device connected
    $ ./gradlew cAT                  # assemble, install and run unit tests


## Directory structure ##

    |-- libs                    # dependencies used to build debug variants
    |-- tools                   # script collection
    |-- gradle.properties       # properties imported by the build script
    `-- WordPress
        |-- build.gradle        # main build script
        `-- src                 # android specific Java code
            |-- androidTest     # test assets, resources and code
            |-- main            #
            |   |-- assets      # main project assets
            |   |-- java        # main project java code
            |   `-- res         # main project resources
            |-- vanilla         # vanilla variant specific manifest
            `-- wasabi          # wasabi variant specific resources and manifest

## OAuth2 Authentication ##

In order to use WordPress.com functions you will need a client ID and
a client secret key. These details will be used to authenticate your
application and verify that the API calls being made are valid. You can
create an application or view details for your existing applications with
our [WordPress.com applications manager](https://developer.wordpress.com/apps/).

When creating your application, you should select "Native client" for the
application type. The applications manager currently requires a "redirect URL",
but this isn't used for mobile apps. Just use "https://localhost".

Once you've created your application in the [applications manager][5], you'll
need to edit the `./gradle.properties` file and change the
`WP.OAUTH.APP_ID` and `WP.OAUTH.APP_SECRET` fields. Then you can compile and
run the app on a device or an emulator and try to login with a WordPress.com
account.

Read more about [OAuth2](https://developer.wordpress.com/docs/oauth2/) and the [WordPress.com REST endpoint](https://developer.wordpress.com/docs/api/).

## How we work ##

You can read more about [Code Style Guidelines](CODESTYLE.md) we adopted, and
how we're organizing branches in our repository in the
[Contribution Guide](CONTRIBUTING.md).

## Need help to build or hack? ##

Say hello on our [Slack](https://make.wordpress.org/chat/) channel: `#mobile`.

## FAQ ##

* Q: I can't build/test/package the project because of a `PermGen space` error.
* A: Create a `gradle.properties` file in the project root directory with the
following: `org.gradle.jvmargs=-XX:MaxPermSize=1024m`.

## License ##

WordPress for Android is an Open Source project covered by the
[GNU General Public License version 2](LICENSE.md). Note: code
in the `libs/` directory comes from external libraries, which might
be covered by a different license compatible with the GPLv2.
