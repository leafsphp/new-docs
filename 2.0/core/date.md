# Leaf Date
Leaf Date makes formating date/time really easier, though the method names may appear weird, they're actually very easy to remeber😂

```js
$date = new Leaf\Date();
```

<span style="background: rgb(11, 200, 70); color: white; padding: 3px 7px; font-size: 14px;">New in v2</span> The Date object has been directly bound to the Leaf object, so we can use it without initialising it.

```js
$leaf = new Leaf\App();

$leaf->date;
```

After this, all the Date methods will be available to us:

## Date Methods
Basically, Date just gives you methods to manipulate the date and time, faster and simpler than `DateTime()` would allow. Let's take a look at these methods.

### randomTimestamp
randomTimestamp as the name implies, generates a new random timestamp. This method was Timestamp in the previous version.

```js
$timestamp = $date->randomTimestamp();
```

randomTimestamp is already configured to give a wide range of dates, but if you ever feel like customizing this range, just pass in params for randomTimestamp
```js
$date->randomTimestamp($start, $end);
```

### randomDate
randomDate as the name implies, generates a new random date.

```js
$timestamp = $date->randomDate();
```

Just like randomTimestamp, randomDate is already configured with a wide range of dates, but you can set a specific range with:

```js
$date->randomDate($start, $end);
```

### getTimeZone
This method returns the current time zone of the user

```js
$timeZone = $date->getTimeZone();
```

### setTimeZone
This method sets the timezone sets the timezone of the user. This method takes in one optional parameter, which is the timezone to set. If nothing is passed in there, the timezone is set to a GMT timezone.

```js
$timeZone = $date->setTimeZone('Timezone');
```

You can get a list of all PHP supported timezones [here](https://www.w3schools.com/php/php_ref_timezones.asp)

### now
now returns the timestamp of the current date and time. Now will return the date based on the timezone, therefore, it is recommended to use now together with `setTimeZone`

```js
$date->setTimeZone('Africa/Accra');
$timeZone = $date->now();
```

### GetDateFromTimeStamp
This method gets the date in `YYYY-MM-DD` format from an existing timestamp

```js
$parsedDate = $date->GetDateFromTimeStamp($timestamp);
```

### GetMonthFromNumber
This gets the month in words from a number (1-12)

```js
$month = $date->GetMonthFromNumber($number);
```

### GetDayFromNumber
This gets the day in words from a number (1-7)

```js
$month = $date->GetDayFromNumber($number);
```

### GetEnglishDateFromTimeStamp
This gets the date in the format (MM DD, YYYY) from an existing timestamp

```js
$parsedDate = $date->GetEnglishDateFromTimeStamp($timestamp);
```

### GetEnglishTimeStampFromTimeStamp
This gets the date in the format `(DD MM, YYYY HH:MM:SS)` from a timestamp

```js
$parsedDate = $date->GetEnglishTimeStampFromTimeStamp($timestamp);
```

### GetTimeFromTimeStamp
This gets the time in the format `(HH:MM:SS)` from a timestamp

```js
$parsedDate = $date->GetTimeFromTimeStamp($timestamp);
```

<br>
<hr>

<a href="#/2.0/http/request" style="margin: 0px">Request</a>
<a href="#/2.0/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/2.0/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/2.0/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>