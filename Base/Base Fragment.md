### Base Fragment
```kotlin
abstract class BaseFragment<T: ViewDataBinding>(@LayoutRes open val layout: Int): Fragment() {  
  
	private var _binding : T? = null  
	val binding get() = _binding!!  

	override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?): View? {  
		_binding = DataBindingUtil.inflate(inflater, layout, container, false)  
		initializeViews()  
		return binding.root  
	}  

	open fun initializeViews() {}  

	override fun onDestroyView() {  
		super.onDestroyView()  
		_binding = null  
	}  

}
```