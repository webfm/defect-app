Location Example
================

value list example - category

here is a block of project template from project data api

    "template": [
        {
            "sort": 2,
            "label": "Location",
            "type": "SELECT",
            "prefix": "h806",
            "source": {
                "type": "LOCATIONS"
            }
        },
    ],

here is a block of locations from project data api

    "locations": {
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

the blocks are simplified to make it easy to read

In template block we have template field called Location (from label) that of type SELECT, and source.type is LOCATINOS.

The tempalte.type indicate it's a value list field and tempalte.source.type indicate that it uses locations value list for selection values (block of locations from project data api)

The tempalte.prefix has value h806,  this value links to an element in issue data block ("h806": 14720).

The value of the element 14720 links to the id of a value list item in location value list

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

cateogry also uses similar conecpt




