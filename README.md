#Google Signup Calendar
A signup calendar widget which can be posted on a Google site and enables arbitrary scheduling rules.
##Purpose
This project is a relatively ugly attempt at fixing a need that came up in a laboratory setting. There were tools that were needed by many people, and thus a calendar management system was needed so that people could schedule and coordinate who could use what tool when. One lab had a solution based on http://sourceforge.net/projects/phpscheduleit, but 1) it required running a server, 2) it wasn't easy to modify and 3) the version that was implemented didn't integrate well with Google calendar.
Attempts were made to use a communal Google calendar where everyone had edit privileges; this quickly led to people flouting informal sign up rules and scheduling far more time than they needed, artificially reducing tool availability. 
This project, written in the Google Apps Script language, enables implementing strict scheduling rules in a Google calendar natively in the Google ecosystem.
##Setup
There are four pieces of this project:

1. A Google calendar owned by the administrator of the tool/resource. People with permission to signup should have read access to this calendar

2. A Google site where the widget will live. People with permission to signup should have read access to this site.

3. The signup widget script. This script should be published to run with the permissions of the person accessing the script, and embedded on the Google site. This script needs to be edited to contain the ID of the calendar and the URL of the published edit calendar script.

4. The edit calendar script. This should be published by the same person who owns the calendar and set to run with their permission. It should be allowed to be accessed by anyone, even anonymous.

Note that most of the functionality lies in the widget script; this is where all rules about scheduling are implemented.
##Caveats
This setup acheives the goal of implementing arbitrary rules for an online signup calendar, and has the nice property that it automatically shows scheduled events as invitations in users' personal calendars. There are some issues though. One is that there is no (easy) way to embed a view of the calendar in the widget, so it has to be placed separately on the site page. This means that creating/deleting events in the calendar does not live update the calendar view. Also, scheduled events are labeled with the email address of the user, not the display name because Google Apps Script does not allow access to display names. Finally, this setup requires a publicly available script to be published which can make arbitrary changes to the administrator's Google calendar. This is obviously not good, but I think it is unavoidable given the way Google Apps Script is implemented. The language does not allow access to information about the active user for scripts authorized to run with the permissions of the script owner. This means that no single script can both know who is using it and edit the calendar of the script of the owner. The only way I saw around this limitation is to pass information between two scripts over an unsecure channel. 
