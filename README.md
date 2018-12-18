# Material Preference [ ![Download](https://api.bintray.com/packages/anggrayudi/maven/materialpreference/images/download.svg)](https://bintray.com/anggrayudi/maven/materialpreference/_latestVersion)
A library designed for people who love simplicity. Hate the old preference style? Try this library.

It combines libraries from `android.support.v7.preference` and `net.xpece.android.support.preference`.
Available from API 17.

Want to **try** or **donate** to this library? [Get it on Google Play](https://play.google.com/store/apps/details?id=com.anggrayudi.materialpreference.sample).

## Screenshots

![Alt text](art/1-generic.png?raw=true "Material Preference")
![Alt text](art/2-generic.png?raw=true "Material Preference")
![Alt text](art/3-generic.png?raw=true "DatePreference")
![Alt text](art/4-generic.png?raw=true "ListPreference")

## Usage

This library available in 2 versions:
1. Version `1.0.0` that uses Support Library v28.0.0
2. Version `2.0.0` that uses AndroidX Jetpack

You can choose which version you want to use. But I recommend you to use v2.0.0 since v1.0.0 will not be supported for future release. Notice that [Google announced](https://android-developers.googleblog.com/2018/05/hello-world-androidx.html) where Support Library v28.0.0 is the final version and will be replaced with AndroidX Jetpack soon. So it is your decision whether to migrate to AndroidX Jetpack or not.

```groovy
repositories {
    maven { url 'https://dl.bintray.com/anggrayudi/maven/' }
}

dependencies {
    implementation 'com.anggrayudi:materialpreference:2.1.0'
}
```

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

```java
public class SettingsFragment extends PreferenceFragmentMaterial {
        @Override
        public void onCreatePreferences(Bundle savedInstanceState, String rootKey) {
            addPreferencesFromResource(R.xml.preferences); 
        }
}
```

From your `SettingsActivity`:

```java
public class SettingsActivity extends PreferenceActivityMaterial {
    
    private SettingsFragment mSettingsFragment;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_settings);
        
        if (savedInstanceState == null) {
            mSettingsFragment = SettingsFragment.newInstance(null);
            getSupportFragmentManager().beginTransaction().add(R.id.fragment_container, mSettingsFragment, "Settings").commit();
        } else {
            mSettingsFragment = (SettingsFragment) getSupportFragmentManager().findFragmentByTag("Settings");
            setTitle(mSettingsFragment.getPreferenceFragmentTitle());
        }
    }
}
```

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

### RingtonePreference

`RingtonePreference` will show only system ringtone sounds by default.
If you want to include sounds from the external storage your app needs to request
`android.permission.READ_EXTERNAL_STORAGE` permission in its manifest.
Don't forget to check this runtime permission before opening ringtone picker on API 23.

### TODO-list
- `app:entryIcons` to `ListPreference` and `MultiSelectListPreference`

## License

    Copyright 2018 Anggrayudi Hardiannicko A.
 
    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at
 
        http://www.apache.org/licenses/LICENSE-2.0
 
    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
