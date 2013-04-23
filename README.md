Site Works API
==============

Servers
-------

### Production Server ###

https://secure.omtrak.com - Production Server, is on at all time, may have older version of the API.

### Staging Server ###

https://secure.omtrak.net - Staging Server, is on for short period of time used for testing.  we may need to point the app to the staging server to use newer version of the API from time to time.

Project List
------------

GET https://secure.omtrak.com/v2/projects?module=:module_name&account=:account_id

Returns a list of projects the user have access to. If the module parameter is set, it will only return the projects where the user have access to the specified module.

### Parameters ###

* module: for now, it should always be set to "defects"
* account: *[temporary]* used for login while oauth is implemented. Only works for account equal to 6.

### Example ###

https://secure.omtrak.com/v2/projects?module=defects&account=6

    [
        {
            "id": 1,
            "name": "DEMO - Sample Project"
        },
        {
            "id": 8,
            "name": "DEMO - Test Project"
        }
    ]

Project Data
------------

GET https://secure.omtrak.com/v2/projects/:project_id/?module=:module_name&data=:boolean_value&account=:account_id

Returns project data and (optionally) project metadata for project_id.

### Parameters ###
* project: project id.
    * required
* module: for now, it should always be set to "defects"
* data: true or false, whether to return the metadata related to the project.
* account: *[temporary]* used for login while oauth is implemented. Only works for account equal to 6.

#### Example ###

https://secure.omtrak.com/v2/projects/8?module=defects&account=6

    {
        "project": {
            "id": 8,
            "name": "DEMO - Test Project"
        },
        "template": [
            {
                "sort": 1,
                "field": "g805",
                "label": "Short Description",
                "type": "INPUT",
                "validators": [
                    {
                        "type": "MAXIMUM_LENGTH",
                        "value": "255"
                    },
                    {
                        "type": "REQUIRED"
                    }
                ]
            },
            {
                "sort": 2,
                "label": "Location",
                "type": "SELECT",
                "prefix": "h806",
                "source": {
                    "type":"LOCATIONS"
                }
            },
            {
                "sort": 3,
                "label": "Services",
                "type": "SELECT",
                "prefix": "h2273",
                "source": {
                    "type":"CATEGORIES"
                }
            },
            {
                "sort": 4,
                "field": "g807",
                "label": "Details",
                "type": "EDITOR"
            },
            {
                "sort": 5,
                "field": "g808",
                "label": "Documents",
                "type": "DOCUMENT"
            }
        ],
        "categories": [
            "labels": [
                {
                    "sort": 1,
                    "field": "c1",
                    "label": "Service"
                },
                {
                    "sort": 2,
                    "field": "c2",
                    "label": "Subservice"
                }
            ],
            "values": [
                {
                    "id": 2345,
                    "label": "(SBS) Special Building Service",
                    "children": [
                        {
                            "id": 2346,
                            "label": "(TP) Teleporter"
                        }
                    ]
                }
            ]
        ],
        "locations": [
            "labels": [
                {
                    "sort": 1,
                    "field": "11",
                    "label": "Site"
                },
                {
                    "sort": 2,
                    "field": "1230",
                    "label": "Structure"
                },
                {
                    "sort": 3,
                    "field": "1231",
                    "label": "Level"
                }
            ],
            "values": [
                {
                    "id": 2345,
                    "label": "London (LD)",
                    "children": [
                        {
                            "id": 2346
                            "label": "Building A (BA)",
                            "children": [
                                {
                                    "id": 2347,
                                    "label": "Lube Reel - D23 (G-05)"
                                },
                                {
                                    "id": 2348,
                                    "label": "FHR - D24 (G-06)"
                                }
                           ]
                        }
                    ]
                }
            ]
        ],
        "teams": [
            {
                "id": 233,
                "name": "AAA Brett"
            },
            {
                "id": 367,
                "name": "Seasia defect manager"
            },
            {
                "id": 66,
                "name": "WebFM"
            }
        ],
        "privileges": [
            "DEFECTS_CREATE","DEFECTS_ASSIGN","DEFECTS_FIX","DEFECTS_SET_DUE_DATE","DEFECTS_CLOSE","DEFECTS_DELETE"
        ]
    }

* project - project name, id
* template - defects fields for the project
    * sort - sort order
    * field - field id used in OMTrak system
    * prefix - ...
    * label - name of the field
    * type - field type
        * INPUT - text input single line
        * EDITOR - multi lined text input
        * SELECT - selector field, can be chained
        * DOCUMENT - attached document field
    * source - selector list source
        * type - selector source type
            * CATEGORIES - use category value list as source for selector
            * LOCATIONS - use location value list as source for selector
            * source can have other type such as user defined value list, the source type will specify what value list to use
    * validators - ...
* categories - category list for defect, used for template.source.type = "CATEGORIES"
    * labels - meta data for category
        * label - display name,
        * field - used in sync data,
        * sort - sort order
    * value - values for cateogry hierarchy
        * id - identity of hierarchy value
        * label - used for display
        * children - children of this value for building hierarchies
* location - location list for defect, used for template.source.type = "LOCATIONS"
    * labels - meta data for category
        * label - display name,
        * field - used in sync data,
        * sort - sort order
    * value - values for cateogry hierarchy
        * id - identity of hierarchy value
        * label - used for display
        * children - children of this value for building hierarchies
* teams - if a user have assign priviledge, he can assign the defect to a team which is listed here
* privileges - there are 10 priviledges
    * DEFECTS – if a user has access to the defect module. IGNORE THIS PERMISSION.
    * DEFECTS_CREATE – if a user can create a defect.
        * If a user doesn't have the defects create permission, then in defect list view, the add new defect button will be hidden.
    * DEFECTS_ASSIGN – if a user can assign the defect to a team.
        * If a user doesn't have defect assign permission, then in defect edit view (http://db.tt/anFvB5TT), the assignee field will not be editable (it will be hidden in the edit view).
    * DEFECTS_DELETE – if a user can delete the defect.
        * A user must have the delete permission AND be either the creator OR have both View All and Edit All privileges to be able to delete a task. Otherwise, the delete button will be hidden.
    * DEFECTS_ADD_COMMENT – if a user can add comments.
        * If a user doesn't have the add comment permission, then in comment view (http://db.tt/UawQ5Pzi), the add comment button will be hidden.
    * DEFECTS_SET_DUE_DATE – if a user can set the due date of the defect.
        * If a user doesn't have this permission, then in defect edit view, the due date field not be editable (it will be hidden in the edit view).
    * DEFECTS_EDIT_ALL – if a user can edit all defects.
        * By default, a user can only edit the regular fields of a defect record (all the fields except for assignee, due date and status) if the user is the creator of the record. If a user has the edit all permission, the user will be able to edit the regular fields of all the defects he has access to.
    * DEFECTS_FIX – see Status Changes.
    * DEFECTS_CLOSE – see Status Changes.
    * DEFECTS_VIEW_ALL – see Status Changes.

* Statuses
    * A defect record will display one of the following six statuses:
        * Not Assigned
        * Assigned
        * In-Progress
        * Inspect Now
        * Rejected
        * Closed

* Status changes
    * Pending ("Assigned" or "Not Assigned") when:
        * Current status of the record is equal to In-Progress, Inspect Now OR Rejected AND:
            * Their team is set as the Assignee Team for the record OR
            *They have the following three privileges: View All, Edit All and Fix.
        * Current status of the record is equal to Rejected OR Closed AND:
            * Their team is the creator of the record AND they have Close privileges OR
            * They have the following three privileges: View All, Edit All and Close.
    * In-Progress when:
        * Current status of the record is equal to Pending ("Assigned" or "Not Assigned"), Inspect Now OR Rejected AND:
            * Their team is set as the Assignee Team for the record OR
            * They have the following three privileges: View All, Edit All and Fix.
        * Current status of the record is equal to Rejected OR Closed AND:
            * Their team is the creator of the record AND they have Close privileges OR
            * They have the following three privileges: View All, Edit All and Close.
    * Inspect Now when:
        * Current status of the record is equal to Pending ("Assigned" or "Not Assigned"), In-Progress  OR Rejected AND:
            * Their team is set as the Assignee Team for the record OR
            * They have the following three privileges: View All, Edit All and Fix.
        * Current status of the record is equal to Rejected OR Closed AND:
            * Their team is the creator of the record AND they have Close privileges OR
            * They have the following three privileges: View All, Edit All and Close.
    * Rejected when:
        * Current status of the record is NOT equal to Rejected AND:
            * Their team is the creator of the record AND they have Close privileges OR
            * They have the following three privileges: View All, Edit All and Close.
    * Closed when:
        * Current status of the record is NOT equal to Closed AND:
            * Their team is the creator of the record AND they have Close privileges OR
            * They have the following three privileges: View All, Edit All and Close.

Issue Data
----------

GET https://secure.omtrak.com/v2/projects/:project_id/defects?account=:account_id

Returns issues in a project.

### Parameters ###
* project: project id.
    * required
* account: *[temporary]* used for login while oauth is implemented. Only works for account equal to 6.

#### Example ###

https://secure.omtrak.com/v2/projects/8/site-works?account=6

    [
        {
            "id":229,
            "uid":"#DF1",
            "status":"CLOSED",
            "a123":"test",
            "logs": [
                {
                    "date":"2013-03-08T03:19:25Z",
                    "type":"STATUS_CHANGE_CLOSED",
                    "message":"John Smith (ACME) closed the defect."
                },
                {
                    "date":"2013-03-05T04:48:25Z",
                    "type":"ASSIGNED",
                    "message":"Mary Li (ACME) assigned the defect to ACE Electrics."
                },
                {
                    "date":"2013-03-01T03:59:22Z",
                    "type":"CREATE",
                    "message":"John Smith (ACME) created the defect."
                }
            ]
        }
    ]

* id - issue id from server db
* uid - issue id displayed to user
* status - issue status PENDING | REJECTED | IN_PROGRESS | SUBMITTED | CLOSED
* a123 - correspond to Project Data template.field, represent value for field
* logs - logs for issue
    * date - recorded date
    * type - log type
        * STATUS_CHANGE_CLOSED | STATUS_CHANGE_REJECTED | STATUS_CHANGE_SUBMITTED | STATUS_CHANGE_IN_PROGRESS | STATUS_CHANGE_ASSIGNED | STATUS_CHANGE_NOT_ASSIGNED | STATUS_CHANGE_OPEN | ASSIGNED | COMMENT | CREATE | UPDATE
        * message - log message

