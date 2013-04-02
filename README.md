Defects API
===========

servers
-------

### production server ###

https://secure.omtrak.com - production server, is on at all time, may have older version of the api

### Staging server ###

https://staging.omtrak.com - staging server, is on for short period of time used for testing.  we may need to point the app to the staging server to use newer version of the API from time to time.



Project List
------------

GET https://secure.omtrak.com/v2/projects?account=:account_id

return a list of projects, account param is a temp measure for login, this call only work for: account_id=6

### parameters ###
* account_id: used for login as a temp measure before oauth is implemented temporary
  * temporary

### example ###

https://secure.omtrak.com/v2/projects?account=6

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

GET https://secure.omtrak.com/v2/projects/:project_id/?account=:account_id

return project meta data for project_id

account param is a temp measure for login, this call only work for :account_id=6 and :projects_id = 8

### parameters ###
* project_id:  project id
    * required
* account_id: used for login as a temp measure before oauth is implemented
    * temporary

#### examples ###

https://secure.omtrak.com/v2/projects/8/?account=6

result:

    {
        "project": {
            "id": "8",
            "name": "DEMO - Test Project"
        },
        "template": [
            {
                "sort": "1",
                "field": "g805",
                "label": "Short Description",
                "type": "INPUT",
                validators: []
            },
            {
                "sort": "2",
                "label": "Location",
                "type": "SELECT",
                "validators": [],
                "source": {
                    "type": "LOCATIONS"
                }
            },
            {
                "sort": "3",
                "label": "Services",
                "type": "SELECT",
                "validators": [],
                "source": {
                    "type": "CATEGORIES"
                }
            },
            {
                "sort": "4",
                "field": "g807",
                "label": "Details",
                "type": "EDITOR"
            },
            {
                "sort": "5",
                "field": "g808",
                "label": "Documents",
                "type": "DOCUMENT"
            },

        ],
        "categories": [
            "structure": [
                {
                    "sort": "1",
                    "field": "service",
                    "label": "Service"
                },
                {
                    "sort": "2",
                    "field": "subservice",
                    "label": "Subservice"
                }
            ],
            "values": [
                {
                    "id": "2345",
                    "code": "XXX",
                    "label": "Xxx Yyy Zzz",
                    "children": [
                        {
                            "id": "2346",
                            "code": "WWW",
                            "label": "Www Zzz Sss"
                        }
                    ]
                }
            ]
        ],
        "locations": [
            "structure": [
                {
                    "sort": "1",
                    "field": "facility",
                    "label": "Facility"
                },
                {
                    "sort": "2",
                    "field": "level",
                    "label": "Level"
                },
                {
                    "sort": "3",
                    "name": "room",
                    "label": "Space"
                }
            ],
            "values": [
                {
                    "id": "2345",
                    "code": "XXX",
                    "label": "Xxx Yyy Zzz",
                    "children": [
                        {
                            "id": "2346",
                            "code": "WWW",
                            "label": "Www Zzz Sss",
                            "children": [
                                {
                                    "id": "2346",
                                    "code": "WWW",
                                    "label": "Www Zzz Sss"
                                },
                                {
                                    "id": "2347",
                                    "code": "WWY",
                                    "label": "Wwy Zzz Sss"
                                },
                                {
                                    "id": "2348",
                                    "code": "WWX",
                                    "label": "Wwx Zzz Sssæ
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
        permissions: [
            CREATE,
            ASSIGN,
            FIX
        ]
    }


* project - project name, id
* template - defects fields for the project
    * sort - sort order
    * field - field id used in OMTrak system
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
* category - category list for defect, used for template.source.type = "CATEGORIES"
    * structure - meta data for category
        * label - display name,
        * name - used in sync data,
        * sort - sort order
    * value - values for cateogry hierarchy
        * id - identity of hierarchy value
        * code - used for display
        * name - used for display
        * children - children of this value for building hierarchies
* location - location list for defect, used for template.source.type = "LOCATIONS"
    * structure - meta data for category
        * label - display name,
        * name - used in sync data,
        * sort - sort order
    * value - values for cateogry hierarchy
        * id - identity of hierarchy value
        * code - used for display
        * name - used for display
        * children - children of this value for building hierarchies
