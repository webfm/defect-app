document example
================

from the project data api call we will get this block for documents

    {
        "sort": 11,
        "field": "g808",
        "label": "Documents",
        "type": "DOCUMENT"
    },

this indicate that the tempatle field is a document field and the template id is g808


now we have a look at the issue data api

    {
        "id": 467,
        "uid": "#ISS5",
        "status": "IN_PROGRESS",
        "assignee": {
            "id": 66,
            "name": "WebFM"
        },
        "due": "2013-04-30T00:00:00Z",
        "g805": "fire up task?",
        "h806": 6,
        "h2273": 6,
        "h3540": 2,
        "g3545": "EQ005",
        "g3541": "sa-588",
        "g3544": "2013-05-01T00:00:00Z",
        "g3543": "1",
        "g3542": "500",
        "g807": "what's happening",
        "g808": [
            {
                "id": 12968,
                "name": "selection popover",
                "extension": "png"
            }
        ],
        "g3951": "what",
        "h3955": 14722,
        "g4012": "",
        "logs": [
            {
                "date": "2013-04-08T06:47:40Z",
                "type": "CREATE",
                "message": "Zhongtao Ren (OMTrak Support) created the issue."
            }
        ]
    }

Look at the issue data fields and we can find block below.  We match issue data field g808 with project data template.field g808,
and this tells us that the issue data block contain data for the document field

    "g808": [
        {
            "id": 12968,
            "name": "selection popover",
            "extension": "png"
        }
    ],

in side the document field value we find blocks indicate documents attached to the defect
* id=12968
* name=selection popover
* extension=png

The document data is used in defect details view and edit view.

* for image docuemnt we have to display the image in defect document view using uiimageview (api for download document will be done later)
    * see this document for [compatible extension type](http://developer.apple.com/library/ios/#documentation/UIKit/Reference/UIImage_Class/Reference/Reference.html)
* for another documents display a icon from [there](defect-details-view.md#doc-icon)


