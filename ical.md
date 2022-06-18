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

- `UID`
   - Persistent, globally unique identifier for the calendar component
   - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.4.7
   - Required (VEVENT, VTODO, VJOURNAL, or VFREEBUSY)
   - Generator of the identifier MUST guarantee that the identifier is unique
   - RECOMMENDED that the right-hand side contain some domain identifier
   - If reimported should replace existing event with same `UID`
- `SEQUENCE`:
   - The revision sequence number of the calendar component
   - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.7.4
   - Optional (VEVENT, VTODO, or VJOURNAL)
   - Integer. Default 0
   - Value monotonically incremented by the "Organizer's" user agentt each time the "Organizer" makes a significant revision to component

- `SUMMARY`: 
   - Short summary or subject for the calendar component (capture a short, one-line summary about the activity or journal entry.)
   - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.1.12
   - Optional ("VEVENT", "VTODO", "VJOURNAL", or "VALARM")

- `DTSTART`:
    - Start date and time of a component
    - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.2.4
    - REQUIRED for "VEVENT" contained in iCalendar objects that don't specify the "METHOD" property
    - REQUIRED for recurring components that specify the "RRULE" property
    - Optional ("VEVENT", "VTODO", or "VFREEBUSY", "STANDARD" and "DAYLIGHT")
    - Can be DATE-TIME / DATE value

- `DTEND`:
    - End date and time of a component
    - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.2.2
    - Optional (VEVENT or VFREEBUSY)
    - Can be DATE-TIME / DATE value
    - MUST not be the same as the DTSTART and MUST be later than DTSTART
    - Examples
       - DTEND:19960401T150000Z
       - DTEND;VALUE=DATE:19980704

- `TRANSP`
- `DTSTAMP`:
    - if METHOD property defined: the date and time object created
    - if METHOD property not defined: the date and time object last revised
    - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.7.2
    - Required (VEVENT, VTODO, VJOURNAL, or VFREEBUSY)
    - Required to be UTC time format
- `CREATED`: 
    - Date and time that the calendar information was created by the calendar user agent in the calendar store.    - https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.7.1
    - Optional ("VEVENT", VTODO, or "VJOURNAL")
    - Required to be UTC time format
