Update api (DRAFT)
==================

Description
-----------

Update api will look very simlar to [site-issue api](site-issue.md).  The ios App need to track changes made to defects and upload those to 
the server.

When app is syncing with the server, the update api must be called first if there are any modified defects in the app.  The server will
accept a list of defects from the app, update them and resolve any conflicts.  The server will then respond with a list of defect for 
the app to update (if the app have defects that contain the same id, we need to update those defect with values from server)

(NOTE how to resolve unique validator conflict? will server auto resolve conflict?)

The app also need to send any new or updated documents to the server, the api will accept single document upload, the document id also need
to be passed to the server 

(NOTE we can't rename document in the app, so we only need id, file name and extension can be read from file for new files)

update api example (to be amended later)
----------------------------------------

https://secure.omtrak.com/v2/projects/8/site-works/update?access_token=TGT-59-5syfp0PaYVBLLldwsQeGYzg5ZDeDdTebbky0vHHjJbL06lUcc0-uQT19h4w

posted payload

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

return payload


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
            "g805": "Broken Window updated",
            "g807": "UPDATED - Window is Broken in Teleporter room, Scary things are happening\r\nwe need to fix it now",
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

