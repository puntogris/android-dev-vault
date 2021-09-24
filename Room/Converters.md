### Room Converters
Common room converters, to use it we annotate our room db with ```@TypeConverters``` like this:

#### Example
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

#### Converters
```kotlin
private val gson = Gson()  
  
@TypeConverter  
fun fromString(value: String): List<Int> {  
    val type = object: TypeToken<List<Int>>() {}.type  
    return gson.fromJson(value, type)  
}  

@TypeConverter  
fun fromList(list: List<Int>): String {  
    val type = object: TypeToken<List<Int>>() {}.type  
    return gson.toJson(list, type)  
}  

@JvmStatic  
@TypeConverter  
fun toTimestamp(dateLong: Long?): Timestamp? = dateLong?.let { Timestamp(Date(dateLong)) }  

@JvmStatic  
@TypeConverter  
fun fromTimestamp(date: Timestamp?): Long? = date?.toDate()?.time
```