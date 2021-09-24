### ViewHolder
Basic example of a view holder with data binding and a click listener attach to the root.

```kotlin
class ExampleViewHolder(private val binding: ExampleVhBinding): RecyclerView.ViewHolder(binding.root){  

    fun bind(example: Example, shortClickListener: (Example) -> Unit){  
        binding.apply {  
            this.example = example  
            root.setOnClickListener {  
                shortClickListener(example)  
            }  
            executePendingBindings()  
        }  
    }  

    companion object{  
        fun from(parent: ViewGroup): ExampleViewHolder {  
            val layoutInflater = LayoutInflater.from(parent.context)  
            val binding = ExampleVhBinding.inflate(layoutInflater, parent, false)  
            return ExampleViewHolder(binding)  
        }
    }
}
```