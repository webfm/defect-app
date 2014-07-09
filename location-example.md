Location Example
================

here is a JSON block of project template from project data api

    "template": [
        {
            "sort": 2,
            "label": "Location",
            "type": "SELECT",
            "field": "h806",
            "source": {
                "type": "LOCATIONS"
            }
        },
    ],

here is a block of location list from project data api

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
                                ]
                            },
                        ]
                    }
                ]
            }
        ]
    },


here is a block of issue data from issue data api

    {
        "id": 229,
        "uid": "#ISS1",
        "status": "CLOSED",
        "assignee": {
            "id": 66,
            "name": "WebFM"
        },
        "h806": 14720,
        "h3540": 2,
        "g805": "Broken Window",
    }

the JSON blocks are simplified

In issue data JSON block, issue have a field ("h806": 14720), this links to template block where template.field = h806 and source.type = "LOCATION".  

The source type indicate that this issue field should reference location list for it's value label.

In location block, there is a location with id 14720 and label "Ground (GF)".  Traverse through location parent, we can build a value string - "Blackwater Mine (BW) - Heavey Vehicle Workshop (BW/HVW) - Ground (GF)"

The template.field = h806 also have template.label = "Location"

Combining the issue field, template and locations, we can build the issue field as following

    feild.field = h806
    field.label = Location
    field.value = "Blackwater Mine (BW) - Heavey Vehicle Workshop (BW/HVW) - Ground (GF)"
    field.type = LOCATION



