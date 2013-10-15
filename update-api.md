Update api
==========

Description
-----------

Update api will look very simlar to [site-issue api](site-issue.md).  The ios App need to track changes made to defects and upload those to 
the server.

When app is syncing with the server, the update api must be called first if there are any modified defects in the app.  The server will
accept a list of defects from the app, update them and resolve any conflicts.  The server will then respond with a list of defect for 
the app to update (if the app have defects that contain the same id, we need to update those defect with values from server)

The app also need to send any new or updated documents to the server, the api will accept single document upload, the document id also need
to be passed to the server 

(NOTE we can't rename document in the app, so we only need id, file name and extension can be read from file for new files)

update api example 
------------------

We're trying to create a REST API which uses the following CRUD mapping:

Create -> Post  
Read -> Get  
Update -> Put  
Delete -> Delete  

All the value of hierarchy fields (the fields start with 'h') should be submitted as number not a string.

CREATE
======

The creation web service will be something like:

POST https://secure.omtrak.com/v2/projects/8/site-works?access_token=xxyyzz

    {
        "assignee": 66,
        "due": "2013-01-01T12:00:00Z",
        "h806": 3,
        "h3540": 2,
        "g805": "Broken Window",
        "g807": "Window is Broken in Teleporter room, Scary things are happening\r\nwe need to fix it now",
        "g809": 12968
    }

ADD COMMENT
===========

POST https://secure.omtrak.com/v2/projects/8/site-works/123/comments?access_token=xxyyzz

    {
        "comment": "Blah blah blah"
    }

UPDATE
======

The update web service will be something like:

PUT https://secure.omtrak.com/v2/projects/8/site-works/123?access_token=xxyyzz

    {
        "id": 123,
        "assignee": 66,
        "due": "2013-01-01T12:00:00Z",
        "h806": 3,
        "h3540": 2,
        "g805": "Broken Window",
        "g807": "Window is Broken in Teleporter room, Scary things are happening\r\nwe need to fix it now",
        "g809": 12968
    }

CHANGE STATUS
=============

PUT https://secure.omtrak.com/v2/projects/8/site-works/123/status?access_token=xxyyzz
NOTE: There is a bug and it's currently using POST instead.

    {
        "status": "IN_PROGRESS",
        "comment": "This is the reason for rejection." // In case of rejection
    }

DELETE
======

The delete web service will be something like:

    DELETE https://secure.omtrak.com/v2/projects/8/site-works/123?access_token=xxyyzz

DOWNLOAD DOCUMENT
=================

    GET https://secure.omtrak.com/v2/projects/<project-id>/documents/<document-id>/download?access_token=xxx

Thumbnails

    GET https://secure.omtrak.com/v2/project-name/documents/id/download?size=thumbnail?access_token=xxx

UPLOAD DOCUMENT
===============

    POST https://secure.omtrak.com/v2/projects/8/site-works/123/documents?access_token=xxyyzz

    file field name: document

UPLOAD UPDATED DOCUMENT
=======================
    
    POST https://secure.omtrak.com/v2/projects/<project-id>/site-works/<issue-id>/documents/<document-id>?access_token=xxyyzz

UPLOAD DOCUMENT RESPONSE
========================

[Multi-Part]

field name: document

Result:

    HTTP STATUS 201

    {
        id: 3456,
        name: "DCIM-0001",
        extension: "jpg"
    }

REMOVE DOCUMENT
===============

    DELETE https://secure.omtrak.com/v2/projects/8/site-works/123/documents/3456?access_token=xxyyzz
