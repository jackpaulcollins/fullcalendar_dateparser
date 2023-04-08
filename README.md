# FullCalendar DateParser Plugin

This is a plugin for the [FullCalendar](https://fullcalendar.io/) library that allows for parsing of custom date formats.

## Installation

You can install this plugin via npm:

```
npm install fullcalendar_dateparser
```

## Usage

```javascript
  someInitFunction() {
    const currentDate = this.calendar.currentData.viewTitle; // the current date rendered by fullcalendar
    const [startDate, endDate] = DateParser.parse(currentDate);

    // this method is aribtrary, but the important thing to note is that startDate and endDate have been parsed by the library
    this.fetchEvents(startDate, endDate).then(({ events, resources }) => {
      this.calendar.setOption('events', events);
      this.calendar.setOption('resources', resources);
      this.calendar.render();
    });
  }
```

 fullcallendar will render date strings in the following formats
 
  * a single month: "April 2023"
  * a single day: "April 7, 2023"
  * a single week: "Apr 2 – 8, 2023"
  * a single week straddling a month: "Mar 26 – Apr 1, 2023"
  * a single week staddling a month & year: "Dec 31, 2023 – Jan 6, 2024"
  

`fullcalendar_dateparser` accepts any of these fullcalendar date string formats and returns an array containing two date objects representing the start and end of the specified date range. Here are some examples:

### Example A

Two date objects representing the same date (single day view, same start/end)

```javascript
const currentDate = this.calendar.currentData.viewTitle;
console.log(currentDate)
// Returns: "April 7, 2023"
fullcalendar_dateparser(currentDate);
// Returns: ["Fri Apr 07 2023 00:00:00 GMT-0700 (Pacific Daylight Time)", "Fri Apr 07 2023 00:00:00 GMT-0700 (Pacific Daylight Time)"]
```

### Example B

Two date objects separated by a range ("Dec 31, 2023 – Jan 6, 2024")

```javascript
const currentDate = this.calendar.currentData.viewTitle;
console.log(currentDate)
// Returns: "Dec 31, 2023 – Jan 6, 2024"
fullcalendar_dateparser(currentDate);
// Returns: ["Fri Apr 07 2023 00:00:00 GMT-0700 (Pacific Daylight Time)", "Fri Apr 07 2023 00:00:00 GMT-0700 (Pacific Daylight Time)"]
```

### Example C

a solitary month

```javascript
const currentDate = this.calendar.currentData.viewTitle;
console.log(currentDate)
// Returns: "April 2023"
fullcalendar_dateparser(currentDate);
// Returns: ["Fri Apr 01 2023 00:00:00 GMT-0700 (Pacific Daylight Time)", "Sun Apr 30 2023 00:00:00 GMT-0700 (Pacific Daylight Time)"]
```

Contributing
If you find any bugs or would like to contribute to the project, please feel free to open an issue or a pull request on the GitHub repository.

License
This plugin is licensed under the MIT License.