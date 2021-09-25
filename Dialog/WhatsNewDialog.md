### What's New Dialog
Dialog to show when we detect that a new version has been installed.

```kotlin
class WhatsNewDialog: DialogFragment() {  
  
    override fun onCreateDialog(savedViewState: Bundle?): Dialog {  
        return MaterialAlertDialogBuilder(requireContext())  
            .setTitle(getString(R.string.updated_version, BuildConfig.VERSION_NAME))  
            .setPositiveButton(android.R.string.ok, null)  
            .setNeutralButton(R.string.whats_new) { _, _ ->  
                launchWebBrowserIntent("https://website.com/versions/v${BuildConfig.VERSION_NAME}.html")  
            }  
            .create()  
    }
}
```

#### Use
I use shared preferences or data store and save the ```VERSION_CODE``` and compare it to the current one.

```kotlin
val appVersionStatus = liveData {  
    if (sharedPref.lastVersionCode() < BuildConfig.VERSION_CODE) {  
        sharedPref.updateLastVersionCode()  
        emit(true)  
    }
}
```

Then we observe and show the dialog.

```kotlin
private fun checkAppCurrentVersion() {  
    viewModel.appVersionStatus.observe(this) { isNewVersion ->  
        if (isNewVersion) navController.navigate(R.id.whatsNewDialog)  
    }  
}
```

#### Content
##### String resources
```xml
<string name="updated_version">Updated to v%1$s</string>  
<string name="whats_new">What\'s new</string>
```

##### Intent
Function ```launchWebBrowserIntent(url)``` can be found here: [[Functions#Intent]]
 