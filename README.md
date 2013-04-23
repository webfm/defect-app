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
        "categories": {
            "labels": [
                {
                    "sort": 1,
                    "field": "c1",
                    "label": "Service"
                },
                {
                    "sort": 2,
                    "field": "c47",
                    "label": "Sub Service"
                }
            ],
            "values": [
                {
                    "id": 5,
                    "label": "(SBS) Special Building Service",
                    "children": [
                        {
                            "id": 7,
                            "label": "(TP) Teleporter"
                        },
                        {
                            "id": 6,
                            "label": "(LDC) Lock Down Chamber"
                        }
                    ]
                },
                {
                    "id": 14600,
                    "label": "(1.0) Building Fabric & Finishes",
                    "children": [
                        {
                            "id": 14601,
                            "label": "(1.0) Amenities Joinery"
                        },
                        {
                            "id": 14602,
                            "label": "(2.0) Balustrades And Rails"
                        },
                        {
                            "id": 14603,
                            "label": "(3.0) Bollards"
                        },
                    ]
                },
                {
                    "id": 14649,
                    "label": "(2.0) Building Structure",
                    "children": [
                        {
                            "id": 14650,
                            "label": "(49.0) Brick Stone Or Concrete"
                        },
                        {
                            "id": 14651,
                            "label": "(50.0) Concrete Construction"
                        }
                    ]
                },
                {
                    "id": 14662,
                    "label": "(3.0) Communications, Security & IT",
                    "children": [
                        {
                            "id": 14663,
                            "label": "(61.0) Access Controls"
                        },
                        {
                            "id": 14664,
                            "label": "(62.0) Anti Theft Systems"
                        },
                        {
                            "id": 14665,
                            "label": "(63.0) Audio-Visual Equipment"
                        },
                        {
                            "id": 14666,
                            "label": "(64.0) Call Systems"
                        }
                    ]
                }
            ]
        },
        "locations": {
            "labels": [
                {
                    "sort": 1,
                    "field": "l1",
                    "label": "Site"
                },
                {
                    "sort": 2,
                    "field": "l230",
                    "label": "Structure"
                },
                {
                    "sort": 3,
                    "field": "l231",
                    "label": "Level"
                },
                {
                    "sort": 4,
                    "field": "l232",
                    "label": "Space"
                }
            ],
            "values": [
                {
                    "id": 5,
                    "label": "London (LD)"
                },
                {
                    "id": 3,
                    "label": "Orange (OR)",
                    "children": [
                        {
                            "id": 4,
                            "label": "Building A (BA)",
                            "children": [
                                {
                                    "id": 6,
                                    "label": "jjj (k)"
                                }
                            ]
                        }
                    ]
                },
                {
                    "id": 14718,
                    "label": "Blackwater Mine (BW)",
                    "children": [
                        {
                            "id": 14719,
                            "label": "Heavey Vehicle Workshop (BW/HVW)",
                            "children": [
                                {
                                    "id": 14720,
                                    "label": "Ground (GF)",
                                    "children": [
                                        {
                                            "id": 14721,
                                            "label": "Workshop (G-01)"
                                        },
                                        {
                                            "id": 14722,
                                            "label": "FHR - D21 (G-02)"
                                        },
                                        {
                                            "id": 14723,
                                            "label": "Lube Reel - D21 (G-03)"
                                        }
                                    ]
                                },
                                {
                                    "id": 14748,
                                    "label": "Level 1 (L01)",
                                    "children": [
                                        {
                                            "id": 14749,
                                            "label": "Office Area 1 (01-01)"
                                        },
                                        {
                                            "id": 14750,
                                            "label": "Office Area 2 (01-02)"
                                        },
                                        {
                                            "id": 14751,
                                            "label": "Photocopier / Printer Area (01-03)"
                                        }
                                    ]
                                },
                                {
                                    "id": 14760,
                                    "label": "Roof (RF)"
                                }
                            ]
                        }
                    ]
                }
            ]
        },
        "lists": {
            "1": {
                "labels": [
                    {
                        "sort": 1,
                        "field": "v1",
                        "label": "Type"
                    }
                ],
                "values": [
                    {
                        "id": 2,
                        "label": "Warranty"
                    },
                    {
                        "id": 3,
                        "label": "Certificate"
                    },
                    {
                        "id": 4,
                        "label": "Commissioning"
                    }
                ]
            }
        },
        "template": [
            {
                "sort": 1,
                "field": "g805",
                "label": "Short Description",
                "type": "INPUT"
            },
            {
                "sort": 2,
                "label": "Location",
                "type": "SELECT",
                "prefix": "h806",
                "source": {
                    "type": "LOCATIONS"
                }
            },
            {
                "sort": 3,
                "label": "Services",
                "type": "SELECT",
                "prefix": "h2273",
                "source": {
                    "type": "CATEGORIES"
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
            },
            {
                "sort": 6,
                "label": "Defect Type",
                "type": "SELECT",
                "prefix": "h3540",
                "source": {
                    "type": "VALUE_LIST",
                    "id": 1
                }
            }
        ],
        "teams": [
            {
                "id": 233,
                "name": "AAA Brett"
            },
            {
                "id": 159,
                "name": "Orange & Bronze"
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
            "DEFECTS",
            "DEFECTS_CREATE",
            "DEFECTS_ASSIGN",
            "DEFECTS_VIEW_ALL",
            "DEFECTS_FIX",
            "DEFECTS_SET_DUE_DATE",
            "DEFECTS_CLOSE",
            "DEFECTS_DELETE",
            "DEFECTS_EDIT_ALL",
            "DEFECTS_ADD_COMMENT"
        ]
    }

* project - project name, id
* template - defects fields for the project
    * sort - sort order
    * field - field id used in OMTrak system, the field value will match a element in defect data. Field is used for all tempalte types except SELECT
    * prefix - the prefix value will match a elemnt in defect data (from defect list api call).  Prefix is used for template SELECT type
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
            * VALUE_LIST - use values in list
        * id - only used for VALUE_LIST type, matchs lists.first element
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
* list - value list group
    * id - this element is presented as the actual id, this value matches template.source.id
        * in the example there is a tempate with template.source.type = VALUE_LIST, template.source.type = 1. this matches list.1

#### privileges - there are 10 priviledges
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
#### Status
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
* status - issue status
    * PENDING
    * REJECTED
    * IN_PROGRESS
    * SUBMITTED
    * CLOSED
* a123 - correspond to Project Data template.field, represent value for field
* logs - logs for issue
    * date - recorded date
    * type - log type
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
    * message - log message
