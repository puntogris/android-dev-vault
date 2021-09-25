### Coroutine Worker
```kotlin
@HiltWorker  
class UploadReminderWorker @AssistedInject constructor(  
    @Assisted appContext: Context,  
    @Assisted workerParams: WorkerParameters  
): CoroutineWorker(appContext, workerParams) { 

    override suspend fun doWork(): Result = withContext(Dispatchers.IO){  
        try {  
            //do stuff
            Result.success()  
        }catch (e:Exception){  
            Result.failure()  
        }
    }  
}
```