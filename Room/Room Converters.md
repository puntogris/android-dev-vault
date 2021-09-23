### Room Converters

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