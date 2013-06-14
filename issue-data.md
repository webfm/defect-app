Issue data
==========

GET https://secure.omtrak.com/v2/projects/:project_id/defects?access_token=:ticket

Returns issues in a project.

Parameters
----------

* project: project id.
    * required
* account: *[temporary]* used for login while oauth is implemented. Only works for account equal to 6.

Example
-------

https://secure.omtrak.com/v2/projects/8/site-works?access_token=TGT-59-5syfp0PaYVBLLldwsQeGYzg5ZDeDdTebbky0vHHjJbL06lUcc0-uQT19h4w

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
                    "date": "2013-04-23T06:58:32Z",
                    "type": "UPDATE",
                    "message": "Charlie Wu updated the issue."
                },
                {
                    "date": "2013-04-24T00:04:05Z",
                    "type": "COMMENT",
                    "message": "Charlie Wu added a comment.",
                    "comment": "hey thing is not fixed, what happened"
                },
                {
                    "date": "2013-04-16T01:21:17Z",
                    "type": "STATUS_CHANGE_IN_PROGRESS",
                    "message": "Zhongtao Ren (OMTrak Support) changed the status to In-Progress."
                },
                {
                    "date": "2013-04-08T06:47:40Z",
                    "type": "CREATE",
                    "message": "Zhongtao Ren (OMTrak Support) created the issue."
                }
            ]
        }
    ]

* id - issue id from server db
* uid - issue id displayed to user
* status - issue status
    * PENDING
    * REJECTED
    * IN_PROGRESS
    * SUBMITTED
    * CLOSED
* a123 - link to a project template
    * links to Project Data template.prefix for SELECT type
    * links to Project Date template.field for all except SELECT type
* logs - logs for issue
    * date - recorded date
    * type - log type (we don't have to display this)
        * STATUS_CHANGE_CLOSED
        * STATUS_CHANGE_REJECTED
        * STATUS_CHANGE_SUBMITTED
        * STATUS_CHANGE_IN_PROGRESS
        * STATUS_CHANGE_ASSIGNED
        * STATUS_CHANGE_NOT_ASSIGNED
        * STATUS_CHANGE_OPEN
        * ASSIGNED
        * COMMENT
        * CREATE
        * UPDATE
        * if type is COMMENT then log be displayed in Comment section,
        * if type is not COMMENT then log will be displayed in Log section
        * log and comment section is display here http://db.tt/U4xXVqno
    * comment - user created comment
        * user can only create comment, comment content is add to this field (log with type "COMMENT")
        * if log is type COMMET comment display "comment" as the detail in the table view
    * message - log message
        * if log is not type COMMET comment display "message" as the detail in the table view