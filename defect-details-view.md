Defects Detail View, Edit View
==============================

[view screenshot](http://db.tt/HNhcdwdh "view screenshot")

<a name="dynamic-fields"/>
Dynamic fields
--------------

Dynamic fields are generated based on [Project Data API](project-data.md "Project Data").  
From the api, template.type define the way field is displayed 
* INPUT - UITextInput
    * when user enter more text into the UITextInput
    * we need to put text into multiple lines if they don't fit in a single line
* EDITOR - UITextView
    * ability to enter multiple lines
    * ability to enter return key
    * we need to put text into multiple lines if they don't fit in a single line
* DATE - display as date string d MMM y i.e. 8 May 2013
    * when user tap on date field to edit, show a popover to display a date picker
    * we don't need to show time for the date picker only show date
* SELECT - hierarchical data structure
    * see [Location example](location-example.md "location example") and [list example](list-example.md "list example")
    * when displays SELECT fields for detail view or edit view we need to display the all hierarchy level and their value
        * for example use data from [sample](location-example.md "location example")
        * we need to display multiple fields in the table view for location
            * Site : Blackwater Mine (BW)
            * Structure : eavey Vehicle Workshop (BW/HVW)
            * Level : Ground (GF)
        * for the same example, if the site issue location value is 14721, we'll display these fields
            * Site : Blackwater Mine (BW)
            * Structure : eavey Vehicle Workshop (BW/HVW)
            * Level : Ground (GF)
            * Space : Workshop (G-01)
        * [how to display SELECT field](defect-details-view.md#generate-view)
    * when user tap on any of the field for a SELECT we will show the same selector what contain all hierarchy level
        * i.e. the currently [location selector](http://db.tt/jGnBAqMc "location selector")
* DOCUMENTS - document field is displayed as a list of icons see [screenshot](http://db.tt/AloUr4wF "screenshot")
    * if the document is an image display the image
    * <a name="doc-icon"/> if the document is not an image use show [this icon](https://www.dropbox.com/s/ioyoz0ka5wqnjzn/document-icon.png "icon")
    * document view will have take photo icon in edit view
    * take photo behavior can be [found here](photo-annotation.md)

<a name="static-fields"/>
Static fields
-------------

* defect status - match status field in the site-issues api. 
    * status is displayed as the status button
    * see [status](definitions.md#status ""status) for status definition and how to display definitions
    * see [status change](definitions.md#status-changes "status change") for how to change status
    * defect status is displayed right next to the first dyanic field (in view screenshot next to short description)
* assignee
    * assignee field displays the value from site-issues api assignee.name
    * assignee field is displayed as the second field after the 1st dyanmic field (dyanimc field with sort = 1)
    * assignee field maybe empty (not assignee field from api call), if assignee is empty:
        * in details view do not show assignee field
        * in edit view show assignee field as empty
    * edit assignee field requires permission [defintion.md](definitions.md#privileges "defintion.md")
    * when edit assignee field, a popover is shown display a list of teams in from the [project-data api](project-data.md "project-data api")
        * table view show team.name
        * set defect.assignee field to team.id
* due date
    * due date field display the value from site-issues api due
    * not every site issue have due date (due date field not present in api call result)
    * if due date is empty
        * in details view do not show due date
        * in edit view show empty due date
    * edit due date field requires permission [defintion.md](definitions.md#privileges "defintion.md")
