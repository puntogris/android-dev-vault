### Scroll Aware Extended Fab Behaviour
```kotlin
class ScrollAwareExtendedFabBehavior(  
	context: Context,  
	attrs: AttributeSet  
) : CoordinatorLayout.Behavior<ExtendedFloatingActionButton>(context, attrs) {  

	override fun onStartNestedScroll(  
		coordinatorLayout: CoordinatorLayout,  
		child: ExtendedFloatingActionButton,  
		directTargetChild: View,  
		target: View,  
		axes: Int,  
		type: Int  
	): Boolean {  
		return axes == ViewCompat.SCROLL_AXIS_VERTICAL ||  
		super.onStartNestedScroll(coordinatorLayout, child,  
		directTargetChild, target, axes, type)  
	}  
	override fun onNestedScroll(  
		coordinatorLayout: CoordinatorLayout,  
		child: ExtendedFloatingActionButton,  
		target: View,  
		dxConsumed: Int,  
		dyConsumed: Int,  
		dxUnconsumed: Int,  
		dyUnconsumed: Int,  
		type: Int,  
		consumed: IntArray  
	) {  
		super.onNestedScroll(coordinatorLayout, child, target,  
			dxConsumed, dyConsumed, dxUnconsumed, dyUnconsumed,  
			type, consumed)  

		if (dyConsumed > 5 && child.isExtended) {  
			child.shrink()  
		} else if (dyConsumed < -5 && !child.isExtended) {  
			child.extend()  
		}
	}
}
```