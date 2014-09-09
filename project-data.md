Project Data
============

GET https://secure.omtrak.com/v2/projects/:project_id/?module=site-works&data=:boolean_value&access_token=:ticket

Returns project data and (optionally) project metadata for project_id.

URL Placeholders
----------------
* projectId - the id of the project

Parameters
----------

* access_token - The login access token, see [login](oauth-login.md)
* module - (optional) the module metadata to be load. Right now only "siteworks" is accepted. The "siteworks" metadata includes the asset template, issue template, maintenance template, permissions, teams (assignable)
* data - (optional, default = "false")  "true" to load the project metadata. The project metadata includes the hierarchy values (location, value list, and categories)
* gzip: (optional, default value = false) true to enable gzip compression of the response data (body) to be generated. Any other value will automatically considered false. 

NOTE: If the server compressed the response body (data), a "Content-Encoding" header will appear with value set to gzip.

Example
-------

https://secure.omtrak.com/v2/projects/8?module=siteworks&access_token=xxxxxx&data=true

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
                    }
                ]
            }
        },
        "assetTemplate": [
            {
                "sort": 1,
                "field": "g905",
                "label": "Short Description",
                "type": "INPUT"
            },
            {
                "sort": 2,
                "label": "Location",
                "type": "SELECT",
                "prefix": "h906",
                "source": {
                    "type": "LOCATIONS"
                }
            },
            {
                "sort": 3,
                "label": "Services",
                "type": "SELECT",
                "prefix": "h3273",
                "source": {
                    "type": "CATEGORIES"
                }
            },
            {
                "sort": 5,
                "field": "g907",
                "label": "Make",
                "type": "INPUT"
            }
        ],    
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
                "label": "Defect Type",
                "type": "SELECT",
                "prefix": "h3540",
                "source": {
                    "type": "VALUE_LIST",
                    "id": 1
                }
            },
            {
                "sort": 5,
                "field": "g807",
                "label": "Details",
                "type": "EDITOR"
            },
            {
                "sort": 6,
                "field": "g808",
                "label": "Documents",
                "type": "DOCUMENT"
            }
        ],   
        "maintenanceWorkRequestTemplate": [
            {
                "sort": 1,
                "field": "g105",
                "label": "Short Description",
                "type": "INPUT"
            },
            {
                "sort": 2,
                "label": "Location",
                "type": "SELECT",
                "prefix": "h106",
                "source": {
                    "type": "LOCATIONS"
                }
            },
            {
                "sort": 3,
                "label": "Services",
                "type": "SELECT",
                "prefix": "h273",
                "source": {
                    "type": "CATEGORIES"
                }
            },
            {
                "sort": 4,
                "label": "Defect Type",
                "type": "SELECT",
                "prefix": "h540",
                "source": {
                    "type": "VALUE_LIST",
                    "id": 1
                }
            },
            {
                "sort": 5,
                "field": "g107",
                "label": "Details",
                "type": "EDITOR"
            },
            {
                "sort": 6,
                "field": "g108",
                "label": "Documents",
                "type": "DOCUMENT"
            },
            {
                "sort": 6,
                "field": "g108",
                "label": "Assets",
                "type": "ASSETS"
            }
        ],   
        "team": {  
            "id": 159,
            "name": "Orange & Bronze"
        },
        "teams": [
            {
                "id": 233,
                "name": "AAA Brett"
            },
            {
                "id": 159,
                "name": "Orange & Bronze"
            },
        ],
        "privileges": [
            "DEFECTS_CREATE"
            "MAINTENANCE_WORK_REQUESTS"
            "MAINTENANCE_WORK_REQUEST_FIX"
            "DEFECTS_CLOSE"
            "MAINTENANCE_WORK_REQUEST_ASSIGN"
            "DEFECTS_DELETE"
            "DEFECTS_SET_DUE_DATE"
            "MAINTENANCE_WORK_REQUEST_ADD_COMMENT"
            "DEFECTS_ASSIGN"
            "MAINTENANCE_WORK_REQUEST_SET_DUE_DATE"
            "MAINTENANCE_WORK_REQUEST_VIEW_ALL"
            "MAINTENANCE_WORK_REQUEST_EDIT_ALL"
            "DEFECTS_EDIT_ALL"
            "MAINTENANCE_WORK_REQUEST_DELETE"
            "MAINTENANCE_WORK_REQUEST_CREATE"
            "DEFECTS_VIEW_ALL"
            "MAINTENANCE_WORK_REQUEST_CLOSE"
            "DEFECTS_ADD_COMMENT"
            "DEFECTS_TASK_CREATE"
            "DEFECTS"
            "DEFECTS_FIX"
        ]
    }

### data structure

* project - project name, id
* template, assetTemplate, maintenanceWorkRequestTemplate - defects fields for the project
    * sort - sort order
    * field - field id used in OMTrak system, the field value will match a element in defect data. Field is used for all template types except SELECT
    * prefix - the prefix value will match a element in defect data (from defect list api call).  Prefix is used for template SELECT type
    * label - name of the field
    * type - field type
        * see [here](definitions.md#template-type "definition") for detail
    * source - selector list source
        * type - selector source type
            * CATEGORIES - use category value list as source for selector
            * LOCATIONS - use location value list as source for selector
            * VALUE_LIST - use values in list
        * id - only used for VALUE_LIST type, matches lists.first element
    * validators - validator for a field
    * [find out how template should be displayed](defect-details-view.md)
* categories - category list for defect, used for template.source.type = "CATEGORIES"
    * labels - meta data for each list hierarchy level
        * label - display name,
        * field - used in sync data,
        * sort - sort order
    * value - values for category hierarchy
        * id - identity of hierarchy value
        * label - used for display
        * children - children of this value for building hierarchies
    * for details see [Value List](definitions.md#value-list "Value List")
* location - location list for defect, used for template.source.type = "LOCATIONS"
    * labels - meta data for each list hierarchy level
        * label - display name,
        * field - used in sync data,
        * sort - sort order
    * value - values for category hierarchy
        * id - identity of hierarchy value
        * label - used for display
        * children - children of this value for building hierarchies
    * for details see [Value List](definitions.md#value-list "Value List")
    * for example see [Location Example](location-example.md "Location Example")
* lists
    * id - list id expressed as id value
        * this value matches template.source.id
        * in the example there is a template with template.source.type = VALUE_LIST, template.source.type = 1. this matches list.1
        * labels - meta data for each list hierarchy level
            * label - display name,
            * field - used in sync data,
            * sort - sort order
    * for details see [Value List](definitions.md#value-list "Value List")
    * for example see [List Example](list-example.md "List Example")
* team - the team the logged in user belong to
* teams - if a user have assign privilege, he can assign the defect to a team which is listed here
* privileges - privileges for current user
    * see [Privileges](definitions.md#privileges "Privileges") for more detail

Other Definitions see  

* [Status](definitions.md#status "Status")
* [Status Change](definitions.md#status-change "Status Change")
* [Validators](definitions.md#validator "Validators")

