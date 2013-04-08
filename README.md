Defects API
===========

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
* teams
* privileges
