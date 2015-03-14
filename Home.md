# jQuery dyndatetime widget Documentation #

## Setup ##
Like any jQuery plugin, you will  need to include the main jQuery script and the plugin script.  In addition, you will also need a language script from /lang/  and a calendar CSS file from /css/ .

```
<!-- main jQuery code -->
<script type="text/javascript" src="dont/forget/to/have/jquery-xxx.js"></script>

<!-- plugin code -->
<script type="text/javascript" src="src/jquery.dynDateTime.js"></script>

<!-- Language specific file for calendar -->
<script type="text/javascript" src="lang/calendar-en.js"></script>

<!-- include one of the CSS styles, or make your own -->
<link rel="stylesheet" type="text/css" media="all" href="css/calendar-win2k-cold-1.css"/> 
```



## Usage pattern ##
To get a input field have date support using the default options, the usage is simple; first create a textbox:

```
<input type="textbox" class="dateField"/>
```
Now apply jQuery dyndatetime.  This should be done _after_ the page loads the DOM ( jQuery.ready() ).
```
jQuery( "input.dateField" ).dynDateTime();
```

And you are done.  If your jQuery string matches multiple inputs, they will **all** have independent date pickers.

If you want to configure with options:
```
jQuery( "input.dateField" ).dynDateTime({
  showsTime: true,
  ifFormat: "%Y/%m/%d-%H:%M",
  button: ".next()" //next sibling to input field
});
```

Easy !

## Options ##
| **Key** | **Default value** | **Description** |
|:--------|:------------------|:----------------|
| displayArea | "" | Relative jQuery [traverse](http://docs.jquery.com/Traversing) method(s); find **first** matched element and show the date in it. eg ".siblings('div.dispArea')"  |
| button | "" | Relative jQuery [traverse](http://docs.jquery.com/Traversing) method(s); find **first** matched element and bind show/hide event for calendar. eg ".siblings('button')" |
| flat | "" | (String) relative jQuery [traverse](http://docs.jquery.com/Traversing) method(s); find **first** matched element (Should be a block element) and place the flat calendar within. eg ".parent().siblings('div.flatCal')" |
| eventName | "click" | event that will trigger the calendar popup, no "on" prefix |
| ifFormat | "%Y/%m/%d" | date format that will be stored in the input field |
| daFormat | "%Y/%m/%d" | the date format that will be used to display the date in displayArea |
| singleClick | true | Is the calendar is in single click mode? |
| dateStatusFunc | null | function that receives a JS Date object and should return true if that date has to be disabled in the calendar, or String for CSS classes. |
| dateText | null | Function to translated date to text |
| firstDay | null | numeric: 0 to 6.  "0" means display Sunday first, "1" means display Monday first, etc. Defaults to language setting. |
| align | "Br" | alignment; See below |
| range | [1900, 2999] | array with 2 elements; the range of years available |
| weekNumbers | true | Display week numbers? |
| flatCallback | null | function that receives a JS Date object and returns an URL to point the browser to (for flat calendar) |
| onSelect |  null | function that gets called when a date is selected.  You don't _have_ to supply this (the default is generally okay) |
| onClose | null | function that gets called when the calendar is closed.|
| onUpdate |  null | function that gets called after the date is updated in the input field.  Receives a reference to the calendar. |
| date | null | the date that the calendar will be initially displayed to |
| showsTime | false | Should calendar include a time selector? |
| timeFormat | "24" | the time format; can be "12" or "24" |
| electric | true | if true then given fields/date areas are updated for each move; otherwise they're updated only on close |
| step | 2 | configures the step of the years in drop-down boxes. |
| position | null | configures the calendar absolute position; default: null |
| cache | false | Reuse the same calendar object, where possible ? |
| showOthers | false |Show days from other months too ? |
| multiple | null, | Allow multiple dates - TODO |
| debug | false | Write debug info to firebug console |

## Date format syntax ##
| **Symbol**  | **Meaning**  |
|:------------|:-------------|
| %a | abbreviated weekday name |
| %A | full weekday name |
| %b | abbreviated month name |
| %B | full month name |
| %C | century number |
| %d | the day of the month ( 00 .. 31 ) |
| %e | the day of the month ( 0 .. 31 ) |
| %H | hour ( 00 .. 23 ) |
| %I | hour ( 01 .. 12 ) |
| %j | day of the year ( 000 .. 366 ) |
| %k | hour ( 0 .. 23 ) |
| %l | hour ( 1 .. 12 ) |
| %m | month ( 01 .. 12 ) |
| %M | minute ( 00 .. 59 ) |
| %n | a newline character |
| %p | ```PM'' or ```AM'' |
| %P | ```pm'' or ```am'' |
| %S | second ( 00 .. 59 ) |
| %s | number of seconds since Epoch (since Jan 01 1970 00:00:00 UTC) |
| %t | a tab character |
| %U, %W, %V | the week number |
| %u | the day of the week ( 1 .. 7, 1 = MON ) |
| %w | the day of the week ( 0 .. 6, 0 = SUN ) |
| %y | year without the century ( 00 .. 99 ) |
| %Y | year including the century ( ex. 1979 ) |
| %% | a literal % character  |

## Align ##
The `align` option is a 2 character string indicating where to place the popup.
#### Vertical alignment ####
The first character in `align` can take one of the following values:

| T | completely above the reference element (bottom margin of the calendar aligned to the top margin of the element). |
|:--|:-----------------------------------------------------------------------------------------------------------------|
| t | above the element but may overlap it (bottom margin of the calendar aligned to the bottom margin of the element). |
| c | the calendar displays vertically centered to the reference element. It might overlap it (that depends on the horizontal alignment).|
| b | below the element but may overlap it (top margin of the calendar aligned to the top margin of the element).|
| B | completely below the element (top margin of the calendar aligned to the bottom margin of the element). |

#### Horizontal alignment ####
The second character in `align` can take one of the following values:
| L | completely to the left of the reference element (right margin of the calendar aligned to the left margin of the element). |
|:--|:--------------------------------------------------------------------------------------------------------------------------|
| l | to the left of the element but may overlap it (left margin of the calendar aligned to the left margin of the element).|
| c | horizontally centered to the element. Might overlap it, depending on the vertical alignment. |
| r | to the right of the element but may overlap it (right margin of the calendar aligned to the right margin of the element).|
| R  | completely to the right of the element (left margin of the calendar aligned to the right margin of the element).|