# Leaf Date

Leaf Date makes formating date/time really easier, though the method names may appear weird, they're actually very easy to remeber😂.

```js
$date = new Leaf\Date();
```

The Date object has been directly bound to the Leaf object, so we can use it without initialising it.

```js
$leaf = new Leaf\App();

$leaf->date;
```

After this, all the Date methods will be available to us:

**NOTE** that in v2, all method names now use `snake_case` instead of the previous `camelCase`

## Date Methods
Basically, Date just gives you methods to manipulate the date and time, faster and simpler than `DateTime()` would allow. Let's take a look at these methods.

### random_timestamp
random_timestamp as the name implies, generates a new random timestamp. This method was Timestamp in the previous version.

```js
$timestamp = $date->random_timestamp();
```

random_timestamp is already configured to give a wide range of dates, but if you ever feel like customizing this range, just pass in params for random_timestamp
```js
$date->random_timestamp($start, $end);
```

### random_date
random_date as the name implies, generates a new random date.

```js
$timestamp = $date->random_date();
```

Just like randomTimestamp, random_date is already configured with a wide range of dates, but you can set a specific range with:

```js
$date->random_date($start, $end);
```

### get_timezone
This method returns the current time zone of the user

```js
$timeZone = $date->get_timezone();
```

### set_timezone
This method sets the timezone sets the timezone of the user. This method takes in one optional parameter, which is the timezone to set. If nothing is passed in there, the timezone is set to a GMT timezone.

```js
$timeZone = $date->set_timezone('Timezone');
```

You can get a list of all PHP supported timezones [here](https://www.w3schools.com/php/php_ref_timezones.asp)

### now

now returns the timestamp of the current date and time. Now will return the date based on the timezone, therefore, it is recommended to use now together with `setTimeZone`

```js
$date->set_timezone('Africa/Accra');
$timezone = $date->now();
```

### days_ago

This is used to get the date from some days ago.

```js
$now = $date->now(); // returns 2020-04-15 05:21:43 pm
$date->days_ago(2); // returns 2020-04-13
```

You can also pass in a particular date as a second parameter. This will be the date to start counting from.

```js
echo $date->days_ago(10, "2020-04-13"); // returns 2020-04-03
```

### months_ago

This is used to get the date from some months ago.

```js
$now = $date->now(); // returns 2020-04-15 05:21:43 pm
$date->months_ago(2); // returns 2020-02-15
```

You can also pass in a particular date as a second parameter. This will be the date to start counting from.

```js
echo $date->months_ago(10, "2020-04-13"); // returns 2019-06-13
```

### years_ago

This is used to get the date from some years ago.

```js
$now = $date->now(); // returns 2020-04-15 05:21:43 pm
$date->years_ago(2); // returns 2018-04-15
```

You can also pass in a particular date as a second parameter. This will be the date to start counting from.

```js
echo $date->years_ago(10, "2020-04-13"); // returns 2010-04-13
```

### ts_to_date

**Previously `GetDateFromTimeStamp`** 

This method gets the date in `YYYY-MM-DD` format from an existing timestamp

```js
$parsedDate = $date->ts_to_date($timestamp);
```

### ts_to_english_date

**Previously `GetEnglishDateFromTimeStamp`** 

This gets the date in the format (MM DD, YYYY) from an existing timestamp

```js
$parsedDate = $date->ts_to_english_date($timestamp);
```

### ts_to_english_ts

**Previously `GetEnglishTimeStampFromTimeStamp`** 

This gets the date in the format `(DD MM, YYYY HH:MM:SS)` from a timestamp

```js
$parsedDate = $date->ts_to_english_ts($timestamp);
```

### ts_to_time

**Previously `GetTimeFromTimeStamp`** 

This gets the time in the format `(HH:MM:SS)` from a timestamp

```js
$parsedDate = $date->ts_to_time($timestamp);
```

### format

Format a timestamp based on your own rules

```js
$parsedDate = $date->format($timestamp, "d-m-Y");
```

### int_to_month

**Previously `GetMonthFromNumber`** 

This gets the month in words from a number (1-12)

```js
$month = $date->int_to_month($number);
```

### int_to_day

**Previously `GetDayFromNumber`** 

This gets the day in words from a number (1-7)

```js
$month = $date->int_to_day($number);
```

### day

Get current day

```js
$date = $date->day();
```

### month

Get current month

```js
$month = $date->month();
```

### year

Get current year

```js
$year = $date->year();
```


<br>
<hr>

<a href="#/2.1http/request" style="margin: 0px">Request</a>
<a href="#/2.1http/response" style="margin: 0px 10px;">Response</a>
<a href="#/2.1http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/2.1environment" style="margin: 0px 10px;">Environment</a>
<a href="#/2.1database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>