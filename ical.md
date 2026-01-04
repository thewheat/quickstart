# iCal format

- rfc5545: https://datatracker.ietf.org/doc/html/rfc5545

## Calendar 
```
BEGIN:VCALENDAR
VERSION:2.0
PRODID:-//ABC Corporation//NONSGML My Product//EN

END:VCALENDAR
```
- `VERSION`
   - https://datatracker.ietf.org/doc/html/rfc5545#section-3.7.4
   - Required
for version number or the minimum and maximum range of the iCalendar specification that is required in order to interpret the iCalendar object

- `PRODID`
   - https://datatracker.ietf.org/doc/html/rfc5545#section-3.7.3
   - Required
for specifies the identifier for the product that created the iCalendar object
- `METHOD`
   - https://datatracker.ietf.org/doc/html/rfc5545#section-3.7.2
   - can be specified

## Event 

### Minimal

```
BEGIN:VEVENT
UID:2026-01-04-unique-123
DTSTAMP:20260104T142400Z
DTSTART:20260110T090000Z
END:VEVENT
```
### More verbose

```
BEGIN:VEVENT
UID:19960401T080045Z-4000F192713-0052@example.com
SUMMARY:Test Event Name
DTSTAMP:19971210T080000Z
DTSTART:20220611T080000Z
DTEND:20220611T084000Z
TRANSP:OPAQUE
LOCATION:
DESCRIPTION: A sharing session on how UNN leverages on big data analytics to drive business decisions and operational excellence\,  touching lightly on the different elements that contributed towards the success of analytics adoption in the organization. The objective of this sessionis to empower and inspire other organisations to take that leap[..]\nhttps://www.bruneitourism.com/events/harnessing-the-power-of-big-data/
URL:https://www.bruneitourism.com/events/harnessing-the-power-of-big-data/
LAST-MODIFIED:20220604T063129Z
CREATED:19960329T133000Z
SEQUENCE:2
END:VEVENT
```

### Required fields
- `UID`: e.g. `UID:19960401T080045Z-4000F192713-0052@example.com`
   - Persistent, globally unique identifier for the calendar component
   - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.4.7
   - Generator of the identifier MUST guarantee that the identifier is unique
   - RECOMMENDED that the right-hand side contain some domain identifier
   - If reimported should replace existing event with same `UID`

- `DTSTAMP`: e.g. `DTSTAMP:20260104T142400Z`
    - if METHOD property defined: the date and time object created
    - if METHOD property not defined: the date and time object last revised
    - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.7.2
    - Required to be UTC time format

### Optional Fields

- `SUMMARY`: e.g. `SUMMARY:New Years Day`
   - The main title shown in entries
   - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.1.12

- `DESCRIPTION`: e.g. `DESCRIPTION:The first day of the year which is typically public holiday`
   - Full text multi line more complete description of the calendar component than that provided by the "SUMMARY" property.
   - https://datatracker.ietf.org/doc/html/rfc5545#page-85

- `DTSTART`: e.g. `DTSTART:19960401T150000Z` / `DTSTART;VALUE=DATE:19980704`
    - Start date and time of a component
    - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.2.4
    - Can be DATE-TIME / DATE value

- `DTEND`: e.g. `DTEND:19960401T150000Z` / `DTEND;VALUE=DATE:19980704`
    - End date and time of a component
    - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.2.2
    - Can be DATE-TIME / DATE value
    - MUST not be the same as the DTSTART and MUST be later than DTSTART
    - Alternatively can use `DURATION` (but cannot use both `DTEND` and `DURATION`)

- `DURATION`: e.g. `DURATION:PT1H`
   - Duration of event
   - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.2.5
   - Duration format time
      - Format `(["+"] / "-") "P" (dur-date / dur-time / dur-week)`
         - `W`: Weeks
         - `D`: Days
         - `H`: Hours
         - `M`: Minutes
         - `S`: Seconds
      - https://datatracker.ietf.org/doc/html/rfc5545#section-3.3.6
      - `P15DT5H0M20S`: 15 days, 5 hours, and 20 seconds
      - `P7W`: 7 weeks
   - Alternatively can use `DTEND` (but cannot use both `DTEND` and `DURATION`)

- `LOCATION`: e.g. `LOCATION:The office`
   - Text to describe location of event
   - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.1.7

- `GEO`:  e.g. `GEO:37.386013;-122.082932`
   - Exact geo location of format `GEO:latitude;longitude` (FLOAT values)
   - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.1.6

- `TRANSP`: e.g. `TRASP:OPAQUE`
   - Determines if event blocks out time as busy
   - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.2.7
   - `OPAQUE`
      - The default value if not specified.
      - Blocks the time slot (shows the user as "Busy").
   - `TRANSPARENT`
      - Does not block the time slot (shows the user as "Free").
      - Used for all-day events that are informational (e.g., "Anniversaries," "Birthdays," or "Reminder: Submit Reports").

- `TZID` and Timezones: e.g. `TZID:America/New_York`
   - Timezone of event
   - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.3.1
   - Alternatively can use timezone in date related fields
      - UTC (Z suffix): e.g. `DTSTART:20260104T140000Z`
      - Local Time with TZID: e.g. `DTSTART;TZID=America/New_York:20260104T140000`
      - Floating Time:
         - No timezone info and no `Z`. (e.g. `DTSTART:20260104T140000`)
         - Remains at 2:00 PM regardless of where the user travels

- `RRULE`: e.g. `RRULE:FREQ=WEEKLY`
   - Repeat rule when to repeat event
   - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.5.3
   - Uses `RECUR` format https://datatracker.ietf.org/doc/html/rfc5545#section-3.3.10
      - `FREQ`
         - The base frequency
         - Required field.
         - Values: `SECONDLY`, `MINUTELY`, `HOURLY`, `DAILY`, `WEEKLY`, `MONTHLY`, `YEARLY`
      - `INTERVAL`
         - How often the frequency repeats
         - Example: `FREQ=WEEKLY;INTERVAL=2` means every two weeks
      - `COUNT`
         - The total number of occurrences before the sequence stops
      - `UNTIL`
         - DATE or DATE-TIME value that bounds the recurrence rule in an inclusive manner
      - `BYSECOND`
         - COMMA-separated list of seconds within a minute.
         - Valid values are 0 to 60.
      - `BYMINUTE`
         - COMMA-separated list of minutes within an hour.
         - Valid values are 0 to 59.
      - `BYHOUR`
         - COMMA-separated list of hours of the day
         - Valid values are 0 to 23.
      - `BYDAY`
         - COMMA-separated list of days of the week;
         - Values: `MO`, `TU`, `WE`, `TH`, `FR`, `SA`, `SU`.
      - `BYMONTHDAY`
         - COMMA-separated list of days of the month.
         - Valid values are 1 to 31 or -31 to -1.
      - `BYYEARDAY`
         - COMMA-separated list of days of the year.
         - Valid values are 1 to 366 or -366 to -1.
      - `BYWEEKNO`
         - COMMA-separated list of ordinals specifying weeks of the year.
         - Valid values are 1 to 53 or -53 to -1.
      - `BYMONTH`
         - COMMA-separated list of months of the year
         - Valid values are 1 to 12.
      - `BYSETPOS`
         - COMMA-separated list of values that corresponds to the nth occurrence within the set of recurrence instances specified by the rule
      - `WKST`
         - Day on which the workweek starts. Default is `MO` (Monday).
         - Valid values are `MO`, `TU`, `WE`, `TH`, `FR`, `SA`, and `SU`.
         - Used with a `WEEKLY` has an interval greater than 1, and a `BYDAY` rule part is specified.
   - Some Examples
      - `RRULE:FREQ=DAILY;COUNT=10`: Every day for 10 days
      - `RRULE:FREQ=WEEKLY;BYDAY=MO,FR`: Every Monday & Friday
      - `RRULE:FREQ=MONTHLY;BYMONTHDAY=15`: The 15th of every month
      - `RRULE:FREQ=MONTHLY;BYDAY=-1FR`: Last Friday of the month
      - `RRULE:FREQ=YEARLY;BYMONTH=1;BYMONTHDAY=1`: Every year on Jan 1st

- `SEQUENCE`: e.g. `SEQUENCE:2`
   - The revision sequence number of the calendar component
   - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.7.4
   - Integer. Default 0
   - Value monotonically incremented by the "Organizer's" user agent each time the "Organizer" makes a significant revision to component

- `CREATED`: e.g. `CREATED:20260104T142400Z`
    - Date and time that the calendar information was created by the calendar user agent in the calendar store.
    - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.7.1
    - Required to be UTC time format
