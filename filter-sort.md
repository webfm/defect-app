filter & sort
=============

<a name="location-filter"/>
Location Filter
---------------
Location filter is located in defect list above filer and sort button

* [screen shot](http://db.tt/HNhcdwdh) shown
* Location filter will display the filtered location, the screen shot shown location filter is set to Main Complex and Ground
* when no location is filtered, location filter will show "Location Filter"
* when user tap on location filter a the [Location Selector](http://db.tt/jGnBAqMc) will be displayed

<a name="filter"/>
Filter
------
when user first tap on filter, an empty list. [see screen shot](http://db.tt/rYpazbwB)

on the top navigation bar there are three buttons Close, Edit, Add
* **close** button the filter popover
* **Edit** button allow user to delete current filters
* user can add new filters by click on the plus button

on the bototm of the page remove all button allow user to remove all filters

when user tap on the add new filter button, [add filter view is shown](http://db.tt/adMgvkmu)

* the table view will show all the filter user can add
* we need filters for static fields
    * defect id (filter Uid)
    * status (Assigned, Not Assigned, In Progress, Inspect Now, Rejected, Closed)
    * due date (due date before, show all defect have due date before this date)
    * assigned to Team (filter by assignee field)
* we also need filter for dyanmic fields
    * we don't need filter for location 
    * we don't need to filter for document
* once user tap on a filter item app will take them to a [data entry view](http://db.tt/anFvB5TT)
    * for different type of data we need different dat entry view
    * for text data entry view will show a UITextField
    * for date it'll show a date picker
    * for assigned to team we'll show a table view show list of teams
    * for SELECT field we'll show selectors similar to Location Selector

once user enerted the data, the popover will move back to the [inital filter view](http://db.tt/rYpazbwB)

<a name="sort" />
Sort
----
sort popover will [look like this](http://db.tt/1n94tMif)

sort view will list the follow static fields
* defect id (filter Uid)
* status (Assigned, Not Assigned, In Progress, Inspect Now, Rejected, Closed)
* due date (due date before, show all defect have due date before this date)
* assigned to Team (sort by assignee name)

sort will also include any dyanmic field that's 
* SELECT
* INPUT
* EDITOR

on the sort view, there are active or inactive sort fields and the will have those items in the field in order
* active icon
* sort name
* toggle icon
* sort icon
* active field will have a tick icon in the front of it
    * when user tap on the tick icon the field will be inactivated and moved to end of sort fields
* inactive field will not have the tick and will be greyed out
    * inactive sort field will not have sort icon
    * inactive sort field will not have toggle icon 
    * when user tap on anywhere on the field the field will be activated
* active field will always appear before inactive fields
* user can hold on the sort icon to sort active field, 
    * when drag a active field below inactive field, the active field will be moved to the end of active fields
* user can tap on the toggle icon to switch between sort ascending and sort descending
* sort will be alive, defect list will be updated when user change anything in the sort table view


