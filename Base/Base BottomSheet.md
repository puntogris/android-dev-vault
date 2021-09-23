### Base BottomSheet

```kotlin
abstract class BaseBottomSheetFragment<T: ViewDataBinding>(@LayoutRes val layout: Int): BottomSheetDialogFragment() {  

    private var _binding : T? = null  
    val binding get() = _binding!!  

    override fun onCreate(savedInstanceState: Bundle?) {  
        super.onCreate(savedInstanceState)  
        preInitializeViews()  
    }  
    override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?): View? {  
        _binding = DataBindingUtil.inflate(inflater, layout, container, false)  
        initializeViews()  
        return binding.root  
    }  

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {  
        super.onViewCreated(view, savedInstanceState)  
        onViewCreated()  
    }  
    open fun preInitializeViews() {}  

    open fun initializeViews() {}  

    open fun onViewCreated(){}  

    override fun onDestroyView() {  
        super.onDestroyView()  
        _binding = null  
    }  
}
```