## Extensions functions

### Views
#### Visibility
```kotlin
fun View.gone() {  
    visibility = View.GONE  
}  
  
fun View.visible() {  
    visibility = View.VISIBLE  
}
```

#### Lottie
```kotlin
fun LottieAnimationView.playAnimationOnce(@RawRes animation: Int){  
    setAnimation(animation)  
    repeatCount = 0  
    playAnimation()  
}
```

### Activity
#### Navigation
```kotlin 
fun AppCompatActivity.getNavController() = getNavHostFragment().navController  
  
fun AppCompatActivity.getNavHostFragment() =  
    (supportFragmentManager.findFragmentById(R.id.nav_host_fragment) as NavHostFragment)
```

### Fragment
#### Theme
```kotlin
fun Fragment.isDarkThemeOn() =  
    (resources.configuration.uiMode and  
    Configuration.UI_MODE_NIGHT_MASK == Configuration.UI_MODE_NIGHT_YES)
```

#### Toolbar
```kotlin
fun Fragment.registerToolbarBackButton(toolbar: MaterialToolbar){  
    toolbar.setNavigationOnClickListener {  
        findNavController().navigateUp()  
    }  
}
```

#### Intent
```kotlin
fun Fragment.launchWebBrowserIntent(uri: String, packageName: String? = null){  
    try {  
        Intent(Intent.ACTION_VIEW).let {  
            it.data = Uri.parse(uri)  
            if (packageName != null) it.setPackage(packageName)  
            startActivity(it)  
        }  
    }catch (e:Exception){  
        //handle error
    }
 }
```

#### Coroutine lifecycle
```kotlin
inline fun Fragment.launchAndRepeatWithViewLifecycle(  
    minActiveState: Lifecycle.State = Lifecycle.State.STARTED,  
    crossinline block: suspend CoroutineScope.() -> Unit  
) {  
    viewLifecycleOwner.lifecycleScope.launch {  
        viewLifecycleOwner.lifecycle.repeatOnLifecycle(minActiveState) {  
            block()  
        }  
    }
}

```

### Keyboard
```kotlin
fun Context.hideKeyboard(view: View) {  
    val inputMethodManager = getSystemService(Activity.INPUT_METHOD_SERVICE) as InputMethodManager  
    inputMethodManager.hideSoftInputFromWindow(view.windowToken, 0)  
}  
  
fun Fragment.hideKeyboard() {  
    view?.let { requireActivity().hideKeyboard(it) }  
}

fun Activity.hideKeyboard(){
    hideKeyboard(currentFocus ?: View(this))
}
```

### Preferences
```kotlin
inline fun PreferenceFragmentCompat.preference(key: String, block: Preference.() -> Unit){  
    findPreference<Preference>(key)?.apply {  
        block(this)  
    }  
}  

inline fun Preference.onClick(crossinline block: () -> Unit){  
    setOnPreferenceClickListener {  
        block()  
        true  
    }  
}  
  
inline fun PreferenceFragmentCompat.preferenceOnClick(key: String, crossinline block: () -> Unit){  
    findPreference<Preference>(key)?.setOnPreferenceClickListener {  
        block()  
        true  
    }  
}
```