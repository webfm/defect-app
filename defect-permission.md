Defect Permission
=================

Add new defect
--------------
    DEFECTS_CREATE

Add new defect set Assignee
---------------------------
    
    DEFECTS_CREATE
    DEFECTS_ASSIGN

Add new defect set due date
---------------------------

    DEFECTS_CREATE
    DEFECTS_ASSIGN

Edit defect
-----------
    
    defect created by user
or 
    DEFECTS_EDIT_ALL

Edit defect set due date
------------------------

    defect created by user
    DEFECTS_SET_DUE_DATE
or 
    DEFECTS_EDIT_ALL
    DEFECTS_SET_DUE_DATE

Edit defect change assignee
---------------------------

    defect created by user
    DEFECTS_ASSIGN
or 
    DEFECTS_EDIT_ALL
    DEFECTS_ASSIGN

Change status
-------------
In Progress
Inspect now

    DEFECTS_EDIT_ALL
    DEFECTS_FIX
or
    if user's team is the assignee of the defect 
    DEFECTS_FIX


Close 
Rejected

    DEFECTS_EDIT_ALL
    DEFECTS_CLOSE
or
    if defect is created by user 
    DEFECTS_CLOSE


Assigned
Not Assigned

    Defect created by user's team 
    Defect in Close or Reject
    DEFECTS_CLOSE
or
    Defect in Close or Reject
    DEFECTS_CLOSE
    DEFECTS_EDIT_ALL

Delete defect
-------------

    DEFECTS_EDIT_ALL
    DEFECTS_DELETE
or
    Defect created by user's team
    DEFECTS_DELETE

Add Comment
-----------

    DEFECTS_ADD_COMMENT

user's team is found in [project-data](project-data.md)
defect creator team will be added later

<a name="creator"/>
Defect Creator
--------------

* In a defect, there is a list of logs, each log of a type, team and account field.  
* In the project data there is a field Team, the team field represent the team of logged in user.
* The defect logs will contain a log with type = "CREATE"
* Logged in user is the creator of this defect when
    * Team id of the type:CREATE log equals to team id of the logged in user

i.e.

in project data:

    "team": {
        "id": 233,
        "name": "WebFM Team"
    },

in defect data (issue data)



    [
        {
            "id": 229,
            "uid": "#ISS1",
            "status": "CLOSED",
            "assignee": {
                "id": 66,
                "name": "WebFM"
            },
            "h806": 3,
            "h3540": 2,
            "g805": "Broken Window",
            "g807": "Window is Broken in Teleporter room, Scary things are happening\r\nwe need to fix it now",
            "g808": [
                {
                    "id": 12968,
                    "name": "selection popover",
                    "extension": "png"
                }
            ],
            "logs": [
                {
                    "date": "2013-04-08T06:47:40Z",
                    "type": "CREATE",
                    "message": "Zhongtao Ren (OMTrak Support) created the issue."
                    "account": {
                        "id": 2,
                        "email": "z.ren@webfm.net",
                        "firstName": "Zhongtao",
                        "lastName": "Ren"
                    },
                    "team": {
                        "id": 233,
                        "name": "WebFM Team"
                    }
                }
            ]
        }
    ]

* The log with type create have team id 233
* The team id from project data is 223
* Thus the creator of this defect is the logged in user.
