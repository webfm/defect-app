Defects Detail View, Edit View
==============================

screenshot http://db.tt/HNhcdwdh

dynamic fields
--------------

Dynamic fields are generated based on [Project Data API](project-data.md "Project Data").  
From the api, tempate.type define the way field is displayed 
* INPUT - UITextInput
    * when user enter more text into the UITextInput, we need to put text into multiple lines
* EDITOR - UITextView
    * ability to enter multiple lines
    * ability to enter return key
    * when user enter more text into the UITextInput, we need to put text into multiple lines
* DATE - display as date string d MMM y i.e. 8 May 2013
    * when user tap on date field to edit, show a popover to display a date picker
    * we don't need to show time for the date picker only show date
* SELECT - hierarchical data strcture
    * see [Location example](location-example.md "location example") and [list example](list-example.md "list example")
    * when displays SELECT fields for detail view or edit view we need to display the all hierarchy level
        * for example use data sample from [Location example](location-example.md "location example")
        * we need to display multiple fields in the table view
            * Site : Blackwater Mine (BW)
            * Structure : eavey Vehicle Workshop (BW/HVW)
            * Level : Ground (GF)
        * same example, if the site issue location value is 14721
            * Site : Blackwater Mine (BW)
            * Structure : eavey Vehicle Workshop (BW/HVW)
            * Level : Ground (GF)
            * Space : Workshop (G-01)
    * when user tap on any of the hierachy level we will show the same selector what contain all hierarchy level
        * i.e. the currently [location selector](http://db.tt/jGnBAqMc "location selector")
* DOCUMENTS - document field is displayed as a list of icons see [screenshot](http://db.tt/AloUr4wF "screenshot")
    * if the document is an image display the image
    * if the document is not an image use show [this icon](http://www.iconfinder.com/icons/3784/download/png/128 "icon")
    




