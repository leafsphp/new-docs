<!-- markdownlint-disable no-inline-html -->
# 📆 Leaf Date

Leaf Date makes formating date/time really easier, though the method names may appear weird, they're actually very easy to remeber😂

<div class="alert -warning">
All methods with deprecation warnings have been removed in v2.4
</div>

```php
$date = new Leaf\Date;
```

The Date object has been directly bound to the Leaf object, so we can use it without initialising it.

```php
$app = new Leaf\App;

$app->date;
```

After this, all the Date methods will be available to us:

## Date Methods

Basically, Date just gives you methods to manipulate the date and time, faster and simpler than `DateTime()` would allow. Let's take a look at these methods.

### randomTimestamp

randomTimestamp as the name implies, generates a new random timestamp. This method was Timestamp in the previous version.

```php
$timestamp = $date->randomTimestamp();
```

randomTimestamp is already configured to give a wide range of dates, but if you ever feel like customizing this range, just pass in params for randomTimestamp

```php
$date->randomTimestamp($start, $end);
```

### randomDate

random_date as the name implies, generates a new random date.

```php
$timestamp = $date->randomDate();
```

Just like randomTimestamp, randomDate is already configured with a wide range of dates, but you can set a specific range with:

```php
$date->randomDate($start, $end);
```

### getTimezone

This method returns the current time zone of the user

```php
$timeZone = $date->getTimezone();
```

### setTimezone

This method sets the timezone sets the timezone of the user. This method takes in one optional parameter, which is the timezone to set. If nothing is passed in there, the timezone is set to a GMT timezone.

```php
$timeZone = $date->setTimezone('Timezone');
```

You can get a list of all PHP supported timezones [here](https://www.w3schools.com/php/php_ref_timezones.asp)

### now

now returns the timestamp of the current date and time. Now will return the date based on the timezone, therefore, it is recommended to use now together with `setTimeZone`

```php
$date->setTimeZone('Africa/Accra');
$timezone = $date->now();
```

### daysAgo

This is used to get the date from some days ago.

```php
$now = $date->now(); // returns 2020-04-15 05:21:43 pm
$date->daysAgo(2); // returns 2020-04-13
```

You can also pass in a particular date as a second parameter. This will be the date to start counting from.

```php
echo $date->daysAgo(10, "2020-04-13"); // returns 2020-04-03
```

### monthsAgo

This is used to get the date from some months ago.

```php
$now = $date->now(); // returns 2020-04-15 05:21:43 pm
$date->monthsAgo(2); // returns 2020-02-15
```

You can also pass in a particular date as a second parameter. This will be the date to start counting from.

```php
echo $date->monthsAgo(10, "2020-04-13"); // returns 2019-06-13
```

### yearsAgo

This is used to get the date from some years ago.

```php
$now = $date->now(); // returns 2020-04-15 05:21:43 pm
$date->yearsAgo(2); // returns 2018-04-15
```

You can also pass in a particular date as a second parameter. This will be the date to start counting from.

```php
echo $date->yearsAgo(10, "2020-04-13"); // returns 2010-04-13
```

### toDate

This method gets the date in `YYYY-MM-DD` format from an existing timestamp

```php
$parsedDate = $date->toDate($timestamp);
```

### toEnglishDate

This gets the date in the format (MM DD, YYYY) from an existing timestamp

```php
$parsedDate = $date->toEnglishDate($timestamp);
```

### toEnglishTs

This gets the date in the format `(DD MM, YYYY HH:MM:SS)` from a timestamp

```php
$parsedDate = $date->toEnglishTs($timestamp);
```

### toTime

This gets the time in the format `(HH:MM:SS)` from a timestamp

```php
$parsedDate = $date->toTime($timestamp);
```

### format

Format a timestamp based on your own rules

```php
$parsedDate = $date->format($timestamp, "d-m-Y");
```

### intToMonth

This gets the month in words from a number (1-12)

```php
$month = $date->intToMonth($number);
```

### intToDay

This gets the day in words from a number (1-7)

```php
$month = $date->intToDay($number);
```

### day

Get current day

```php
$date = $date->day();
```

### month

Get current month

```php
$month = $date->month();
```

### year

Get current year

```php
$year = $date->year();
```

<br>
<hr>

<a href="#/v/2.0/http/request" style="margin: 0px">Request</a>
<a href="#/v/2.0/http/response" style="margin: 0px 10px;">Response</a>
<a href="#/v/2.0/http/session" style="margin: 0px; 10px;">Session</a>
<a href="#/v/2.0/environment" style="margin: 0px 10px;">Environment</a>
<a href="#/v/2.0/database" style="margin: 0px 10px;">Using a database</a>

<br>
Built with ❤ by <a href="https://mychi.netlify.com" style="font-size: 20px; color: #111;" target="_blank">Mychi Darko</a>
