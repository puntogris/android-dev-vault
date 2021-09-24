### Types
Classes used as type for a clear way to show a result instead of using ```true / false``` for example.
##### Example

```kotlin
when(result){
    SimpleResult.Success -> {
        //update Ui
    }
    SimpleResult.Failure -> {
        //update Ui
    }
}
```

#### Simple
```kotlin
sealed class SimpleResult{  
    object Success: SimpleResult()  
    object Failure: SimpleResult()
}
```

#### Generic
```kotlin
sealed class Result<out T : Any> {  
    data class Success<out T : Any>(val data: T) : Result<T>()  
    data class Error(val exception: Exception) : Result<Nothing>()  
}
```