# Android Studio相关目录解析

## `%USERPROFILE%\.<CONFIGURATION_FOLDER>`

其中`CONFIGURATION_FOLDER`与Android Studio版本相关，比如对于Android Studio 3.0.1来说，该目录是指`C:\Users\jiang\.AndroidStudio3.0`。这个目录中保存着用户对于Android Studio的配置修改情况，比如你修改了字体、JVM参数等，都会在该文件中体现。如果你想重置Android Studid的设置，直接删除该文件夹，并重启Android Studio即可。想了解更详细的情况可以参考：[Configure Android Studio: <https://developer.android.com/studio/intro/studio-config.html>]

## `%USERPROFILE%\AppData\Local\Android\Sdk`

该目录保存了下载的SDK，该目录可以修改：`Settings -> Appearance & Behavior -> System Settings -> Android SDK`

## `%USERPROFILE%\.android`

该目录中保存了你的自定义AVD的配置，这些配置会覆盖SDK目录中的相关配置。如果你想重置Android Studid的设置除了要删除`%USERPROFILE%\.<CONFIGURATION_FOLDER>`，最好把该目录也删除，然后重启Android Studio。