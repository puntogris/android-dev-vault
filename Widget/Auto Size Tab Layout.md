
### Auto Size Tab Layout
#### Class
```kotlin
class AutoSizeTabLayout(context: Context, attrs: AttributeSet) : TabLayout(context, attrs) {  
	override fun newTab(): Tab {  
		return super.newTab().apply {  
			setCustomView(R.layout.auto_size_tab_text)  
		}  
	}  
}
```

#### Xml
```xml
<?xml version="1.0" encoding="utf-8"?>  
<androidx.appcompat.widget.AppCompatTextView  
xmlns:android="http://schemas.android.com/apk/res/android"  
xmlns:app="http://schemas.android.com/apk/res-auto"  
android:id="@android:id/text1"  
android:layout_width="wrap_content"  
android:layout_height="wrap_content"  
android:gravity="center"  
android:textAppearance="@style/TextAppearance.Design.Tab"  
android:maxLines="1"  
app:autoSizeMinTextSize="8sp"  
app:autoSizeMaxTextSize="14sp"  
app:autoSizeTextType="uniform" />
```