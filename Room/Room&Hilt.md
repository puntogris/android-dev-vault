### Room & Hilt

#### Database

```kotlin
@Database(
entities = [  
    Example::class  
            ], version = 1, exportSchema = false)

@TypeConverters(Converters::class)  
abstract class AppDatabase : RoomDatabase() {  
    abstract fun exampleDao(): ExampleDao  
}
```

#### Module
```kotlin
@InstallIn(SingletonComponent::class)  
@Module  
class AppDatabaseModule {  
    
    private val roomDbName = "app_database"

    @Provides  
    fun providesExampleDao(appDatabase: AppDatabase) = appDatabase.exampleDao()  

    @Provides  
    @Singleton 
    fun provideExampleDatabase(@ApplicationContext appContext: Context): AppDatabase {  
        return Room  
            .databaseBuilder(  
                appContext,  
                AppDatabase::class.java,  
                roomDbName  
            )  
            .build()  
    }
}
```