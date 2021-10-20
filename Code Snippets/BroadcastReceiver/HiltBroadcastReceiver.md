### HiltBroadcastReceiver
Used as a wrapper because of an issue with Hilt injecting directly into a BroadcastReceiver.
[Link to the Github issue](https://github.com/google/dagger/issues/1918#issuecomment-644057247)

```kotlin
abstract class HiltBroadcastReceiver : BroadcastReceiver() {  
    @CallSuper  
    override fun onReceive(context: Context, intent: Intent) {}  
}
```