TaskPaperDaily
==============

Extension for [TaskPaper](http://www.hogbaysoftware.com/products/taskpaper) (and [TodoPaper](http://widefido.com/products/todopaper/)) to handle @due-tags and get them up-to-date.

## Preconditions:
1. ruby >= 1.9
2. gem 'chronic'
3. *.taskpaper files, of course ;)
4. an alway-on device (dropbox + uberspace for example)

## The problem:
TaskPaper uses duetags, for example: @today or @due(2013-10-21). But these due-dates will not update automaticly. @today will be @today, as long as you change it manually.
I wanted to get an @overdue if I tag an item with @today and don't close it until tomorrow. Automagicly.

I would like to start my workday with opening my TaskPaper without getting through all tags and getting the actual date for them.

## The solution:
TaskPaperDaily, a little rubyscript which does the trick.

### simple dates
The Script:

1. replaces @today and @tomorrow with their absolute days, e.g. @due(2013-10-21)
2. replaces relative weekdays with their absolute days, like @due(2013-10-21) for @due(monday)...@due(friday)
3. adds @today @tomorrow and @overdue based on the new absolute dates

### calendar weeks
for my job I mostly use calendar weeks, therefor TaskPaperDaily is aware of them too: @due(kw43) is the appropriate tag for this.
On the sunday before the start of the given week @tomorrow will be added. Through the whole week @today will be added. After the week a @overdue-tag will be added as normal.

All these actions will not apply to tasks which have a @done tag.

### Example

- getting milk @today

after running the script the same day:

- getting milk @due(2013-10-20) @today

and if you don't get the milk today, tomorrow it wil look like this:

- getting milk @due(2013-10-20) @overdue

## Ho to use:
The script schould at least run once a day over all your TaskPaper files, and this schould be done before you start the new day. You can run it as often as you like. In my setup it runs every hour via chronjob. Because I am using TaskPaper and TodoPaper on three different machines, my files are located in my dropbox and sync across all devices. The Script is running on my uberspace, where dropbox is running too.

Don't forget to set the correct path to your *.taskpaper-files:
	
	files = Dir["/path/to/your/TaskPaperFiles/*.taskpaper"]

##ToDo:
- I would like to have reminders for a special time, getting an iOS-Push or mail. The tag could look like @reminder(tomorrow,9:00)

