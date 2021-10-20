## Extensions functions
Commonly used extension functions that make life easier and code cleaner.

### View
```kotlin
fun View.gone() {  
    visibility = View.GONE  
}  
  
fun View.visible() {  
    visibility = View.VISIBLE  
}
```

### Lottie
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


### Recycler view

```kotlin
fun RecyclerView.scrollToTop() {  
    layoutManager?.let {  
        val firstVisibleItemPosition = it.findFirstVisibleItemPosition()  
        if (firstVisibleItemPosition > 6) {  
            scrollToPosition(6)  
    } 
    smoothScrollToPosition(0)  

    if (it is StaggeredGridLayoutManager) {  
            it.invalidateSpanAssignments()  
        }
    }  
}  

fun RecyclerView.LayoutManager?.findFirstVisibleItemPosition(): Int {  
    return when (this) {  
        is LinearLayoutManager -> findFirstVisibleItemPosition()  
        is GridLayoutManager -> findFirstVisibleItemPosition()  
        is StaggeredGridLayoutManager -> findFirstVisibleItemPositions(null).first()  
        else -> RecyclerView.NO_POSITION  
    }  
}
```

### LiveData
Will trigger the observable when updating a field.
```kotlin
inline fun <T> MutableLiveData<T>.setField(transform: T.() -> Unit) {
    this.value = this.value?.apply(transform) 
}
```

### Broadcast Receiver
```kotlin
@DelicateCoroutinesApi  
fun BroadcastReceiver.goAsync(  
    coroutineScope: CoroutineScope = GlobalScope,  
    block: suspend () -> Unit  
) {  
    val result = goAsync()  
    coroutineScope.launch {  
        try {  
            block()  
        } catch (e:Exception) {  
            Timber.d(e.message.toString())  
        }finally {  
            result?.finish()  
        }
    }  
}
```

### Context
Used with Android 12 as it requires to check this when using Alarm Manager.
```kotlin
fun Context.isIgnoringBatteryOptimizations(): Boolean{  
    val pm = getSystemService(PowerManager::class.java)  
    return (pm.isIgnoringBatteryOptimizations(packageName))  
}
```

### View Pager
```kotlin
fun ViewPager2.setPageFadeTransformer(){  
    setPageTransformer { page, position ->  
        page.alpha = when {  
            position <= -1.0F || position >= 1.0F -> 0.0F  
            position == 0.0F -> 1.0F  
            else -> 1.0F - abs(position)  
        } 
    }  
}
```

### Primitives

```kotlin
fun String.capitalizeFirstChar() =  
    replaceFirstChar { if (it.isLowerCase()) it.titlecase(Locale.getDefault()) else it.toString() }  
  
fun String.capitalizeWords(): String = split(" ").joinToString(" ") { it.capitalizeFirstChar() }
```