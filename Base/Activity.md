### Base Activity

Base Activity with data binding to reduce boilerplate.

Includes ```preInitializeViews()```, that i normally use to show a splash screen.

Function ```onBackPressed()``` is optional, it fixes a memory leak that is caused when pressing back to finish an activity which is a task root.

[Link to the google issue tracker](https://issuetracker.google.com/issues/139738913?pli=1)

```kotlin
abstract class BaseActivity<T : ViewDataBinding>(@LayoutRes val layout: Int): AppCompatActivity(){  
    private var _binding: T? = null  
    val binding get() = _binding!!  
    
    open fun initializeViews() {}  
    open fun preInitializeViews() {}  

    override fun onCreate(savedInstanceState: Bundle?) {  
        preInitializeViews()  
        super.onCreate(savedInstanceState)  
        _binding = DataBindingUtil.setContentView(this, layout)  
        initializeViews()  
    }  
 
    override fun onDestroy() {  
        super.onDestroy()  
        _binding = null  
    }  

    override fun onBackPressed() {  
        if (isTaskRoot &&  
            getNavHostFragment().childFragmentManager.backStackEntryCount == 0 &&  
            supportFragmentManager.backStackEntryCount == 0  
        ) {  
            finishAfterTransition()  
        } else super.onBackPressed()  
    }
}
```