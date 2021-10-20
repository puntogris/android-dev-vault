### DiffCallBack
Used in adapters like ```ListAdapter``` and ```PagingDataAdapter``` to compare items in the recycler view and update the ui.

```kotlin
class ExampleDiffCallBack: DiffUtil.ItemCallback<Example>() {  
    override fun areItemsTheSame(oldItem: Example, newItem: Example): Boolean {  
        return oldItem.id == newItem.id  
    }  

    override fun areContentsTheSame(oldItem: Example, newItem: Example): Boolean {  
        return oldItem == newItem  
    }  
}
```