### Binding

#### Adapter
##### Example
```kotlin
@BindingAdapter("showOnAction")
fun TextView.setShowOnAction(isAction: Boolean){
    isVisible = isAction
}
```

#### Data
```xml
<import type="android.view.View"/>
```

