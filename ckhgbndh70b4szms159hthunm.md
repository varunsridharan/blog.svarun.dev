## Time-Based Website Theme Using Javascript

In this post, we are going to learn how to load stylesheets on a website based on the current time of the day.  This can be useful if you are planning to add dark mode support which can be auto-enabled. 

---
First, add a basic stylesheet which renders a general version of the page. 
```html
<link rel='stylesheet' href='style.css' type='text/css'>
```

We need to know the current hour of the day using the date & time from the client's machine. it can be done using javascript's [Date API]

```javascript
// Returns The Current Hour In 24-Hrs Format
var current_hour = (new Date()).getHours()
```

Next, we need to define our time condition. I wrote a basic logic splitting a day into 4 parts.

- Morning : `current_hour >= 5 && current_hour <= 12`
- Afternoon : `current_hour >= 12 && current_hour <= 14`
- Evening : `current_hour >= 14 && current_hour <= 18`
- Night : `current_hour >= 18 && current_hour <= 5`

```javascript
if( current_hour >= 5 && current_hour <= 12 ) {
	// Morning 5AM - 12PM
} else if( current_hour >= 12 && current_hour <= 14 ) {
	// Afternoon 12PM - 3PM
} else if( current_hour >= 14 && current_hour <= 18 ) {
	// Evening 3PM - 6PM
} else if( current_hour >= 18 && current_hour <= 5 ) {
	// Night 6PM - 5AM
} 
```

Once the time is decided, we need to load the CSS file for that time of the day. This can be achieved using [`document.write` API ]

```javascript
var current_hour = (new Date()).getHours()

if( current_hour >= 5 && current_hour <= 12 ) {
	// Morning 5AM - 12PM
	document.write( "<link rel='stylesheet' href='morning.css' type='text/css'>" );
} else if( current_hour >= 12 && current_hour <= 14 ) {
	// Afternoon 12PM - 3PM
	document.write( "<link rel='stylesheet' href='afternoon.css' type='text/css'>" );
} else if( current_hour >= 14 && current_hour <= 18 ) {
	// Evening 3PM - 6PM
	document.write( "<link rel='stylesheet' href='evening.css' type='text/css'>" );
} else if( current_hour >= 18 && current_hour <= 5 ) {
	// Night 6PM - 5AM
	document.write( "<link rel='stylesheet' href='night.css' type='text/css'>" );
}
```

> Do keep in mind that we originally loaded the general version of the CSS to begin with. Therefore, the time-based CSS must only contain those elements which you would like to override based on the time.


***Here is a minified version of the Code***
```javascript
var hour     = ( new Date() ).getHours();
var file = ( hour >= 5 && hour <= 12 ) ? 'morning.css' : '';
file     = ( hour >= 12 && hour <= 14 ) ? 'afternoon.css' : file;
file     = ( hour >= 14 && hour <= 18 ) ? 'evening.css' : file;
file     = ( hour >= 18 && hour <= 5 ) ? 'night.css' : file;
document.write( "<link rel='stylesheet' href='" + file + "' type='text/css'>" );
```
---

Questions or feedback?  Please comment below. 

See all my projects at <a href=https://github.com/varunsridharan/>Github</a>.

Follow me on <a href="https://twitter.com/varunsridharan2">Twitter for updates</a>

[Date API]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date
[`document.write` API ]: https://developer.mozilla.org/en-US/docs/Web/API/Document/write
