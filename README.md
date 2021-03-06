# Material Preference [ ![Download](https://api.bintray.com/packages/anggrayudi/maven/materialpreference/images/download.svg)](https://bintray.com/anggrayudi/maven/materialpreference/_latestVersion)
A library designed for people who love simplicity. Hate the old preference style? Try this library.

It combines libraries from `androidx.preference` and `net.xpece.android.support.preference`.
Available from API 17.
<br><a href="https://play.google.com/store/apps/details?id=com.anggrayudi.materialpreference.sample" target="_blank"><img alt="Google Play" height="80" src="https://play.google.com/intl/en_US/badges/images/generic/en_badge_web_generic.png" align="right"/></a><br><br><br>

## Screenshots

![Alt text](art/1-generic.png?raw=true "Material Preference")
![Alt text](art/2-generic.png?raw=true "Material Preference")
![Alt text](art/3-generic.png?raw=true "DatePreference")
![Alt text](art/4-generic.png?raw=true "ListPreference")

## Usage

### Basic

```gradle
dependencies {
    implementation 'com.anggrayudi:materialpreference:3.1.2'
}
```

**Note:** If you encounter error `Failed to resolve com.anggrayudi:materialpreference:x.x.x`, then add the following config:

````gradle
repositories {
    maven { url 'https://dl.bintray.com/anggrayudi/maven/' }
    // If error "Failed to resolve com.afollestad.material-dialogs" appears, add the following line
    maven { url "https://dl.bintray.com/drummer-aidan/maven/" }
}
````

From your `preferences.xml`:

```xml
<PreferenceScreen xmlns:android="http://schemas.android.com/apk/res/android">

    <!-- To make Preferences floating, you must wrap them inside PreferenceCategory -->
    <PreferenceCategory>
        <Preference
            android:key="about"
            android:title="About"
            android:icon="@drawable/..."
            app:tintIcon="?colorAccent"
            app:legacySummary="false"/>
    </PreferenceCategory>
</PreferenceScreen>
```

From your `SettingsFragment`:

```kotlin
class SettingsFragment : PreferenceFragmentMaterial() {

    override fun onCreatePreferences(savedInstanceState: Bundle?, rootKey: String?) {
        addPreferencesFromResource(R.xml.preferences)
    }
}
```

From your `SettingsActivity`:

```kotlin
class SettingsActivity : PreferenceActivityMaterial() {

    private var settingsFragment: SettingsFragment? = null
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        
        if (savedInstanceState == null) {
            settingsFragment = SettingsFragment.newInstance(null)
            supportFragmentManager.beginTransaction().add(R.id.fragment_container, settingsFragment!!, TAG).commit()
        } else {
            settingsFragment = supportFragmentManager.findFragmentByTag(TAG) as SettingsFragment?
            title = settingsFragment!!.preferenceFragmentTitle
        }
    }
}
```

### Preference Key Constants Generator [ ![Download](https://api.bintray.com/packages/anggrayudi/maven/materialpreference-compiler/images/download.svg)](https://bintray.com/anggrayudi/maven/materialpreference-compiler/_latestVersion)

Material Preference has a capability to auto-generate your preference keys in a constant class. By default, this class is named `PrefKey`. With this generator, you don't need to rewrite constant field each time you modify preference key from file `res/xml/preferences.xml`. It improves accuracy in writing constant values.

To enable this feature, simply add the following configuration to your `build.gradle`:

````gradle
apply plugin: 'com.android.application'
apply plugin: 'kotlin-android'
apply plugin: 'kotlin-kapt' // Add this line

dependencies {
    implementation 'com.anggrayudi:materialpreference:3.1.2'
    kapt 'com.anggrayudi:materialpreference-compiler:1.0.0'
}
````

From your `SettingsFragment` class:

````kotlin
@PreferenceKeysConfig() // Add this annotation
class SettingsFragment : PreferenceFragmentMaterial() {

    override fun onCreatePreferences(savedInstanceState: Bundle?, rootKey: String?) {
        addPreferencesFromResource(R.xml.preferences)
        // You can access the constant values with auto-generated class named PrefKey
        findPreference(PrefKey.ABOUT)!!.summary = BuildConfig.VERSION_NAME
    }
}
````

**Note:**
* If `PrefKey` does not update constant fields, click ![Alt text](art/make-project.png?raw=true "Make Project") Make Project in Android Studio.
* This generator wont work with Android Studio 3.3.0 since Google does not fix [this bug](https://issuetracker.google.com/issues/122883561) yet.

## Preferences

- `Preference`
- `CheckBoxPreference`
- `SwitchPreference`
- `EditTextPreference`
- `ListPreference`
- `MultiSelectListPreference`
- `SeekBarDialogPreference`
- `SeekBarPreference`
- `RingtonePreference`
- `IndicatorPreference`
- `FolderPreference`
- `DatePreference`
- `TimePreference`
- `ColorPreference`

### RingtonePreference

`RingtonePreference` will show only system ringtone sounds by default.
If you want to include sounds from the external storage your app needs to request
`android.permission.READ_EXTERNAL_STORAGE` permission in its manifest.
Don't forget to check this runtime permission before opening ringtone picker on API 23.

## Donation
Any donation you give is really helpful for us to develop this library. It feels like energy from power stone.

<a href="https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=TGPGSY66LKUMN&source=url" target="_blank"><img alt="Donate with PayPal" src="https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif" border="0"/></a>

## License

    Copyright 2018-2019 Anggrayudi Hardiannicko A.
 
    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at
 
        http://www.apache.org/licenses/LICENSE-2.0
 
    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
