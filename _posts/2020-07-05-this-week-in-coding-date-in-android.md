---
layout: post
title: This Week in Coding: Date in Android  
---

# This Week in Coding: Date in Android 

For my personal project, I need to save some date and time data in the local database and display them. Like every data format problem, there are quiet a few different ways to save date. Most of them can receive almost identical results. I started with saving date string in the database, then I found myself constantly forgot what's the right format for the date string. After tried a few different ways, I aggregated some short sample code here. 

### 1. Date with Room: TypeConverter

```kotlin
// record entity 
@Entity(tableName = "record_table")
data class Record {
  @PrimaryKey(autoGenerate = true)
  val id :Long,
	val date: Date 
}

// Dao 
public interface RecordDao {
  @Query("SELECT * FROM record_table ORDER BY id") 
  fun getAll(): LiveData<List<Record>>
}

// Room with TypeConverters 
// TypeConverters can also be put else where 
@Database(entities = [Record::class], version = 1, exportSchema = false)
@TypeConverters(Converters::class)
abstract class TimeLogDatabase : RoomDatabase() {
    abstract val dao: RecordDao
}

// TypeConverter 
class Converters {
    @TypeConverter
    fun fromTimestamp(value: Long?): Date? {
        return value?.let { Date(it) }
    }

    @TypeConverter
    fun dateToTimestamp(date: Date?): Long? {
        return date?.time?.toLong()
    }
}
```

### 2. Type conversion

```kotlin
// Long and Date
import java.util.Date 
val curLong = System.currentTimeMillis() 
val curDate = Date(curLong)
println("${curLong == curDate.time}")

// String and Date 
import android.text.format.DateFormat
import java.text.SimpleDateFormat 
// date to string 
val dateString = DateFormat.format("yyyy-MM-dd HH:mm", curDate).toString()
// string to date 
val format = SimpleDateFormat("yyyy-MM-dd HH:mm")
val date = format.parse(dateString)
date == curDate 

// Calendar and Date 
import java.util.Calendar
val calendar = Calendar.getInstance()
calendar.time = curDate 
calendar.set(1990, 1, 1)
val year = calendar.get(Calendar.YEAR)
val newDate = calendar.time 
println("New date $newDate")
```

As I am making this note, I realize there are at least three implementations for `DateFormat`, an Android version, a Kotlin version and a Java version. A safe guess is this will not be the last time I make date related note. 

Have fun coding :) 



Reference: https://developer.android.com/training/data-storage/room/referencing-data 

