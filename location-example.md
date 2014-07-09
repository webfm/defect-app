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

The issue data have a field ("h806": 14720), this links to template block where template.field = h806 and source.type = "LOCATION".  The source type indicate that this issue field should reference location list for it's value label.

In location block, there is a location with id 14720 and label "Ground (GF)".  Traverse through location parent, we can build a location string "Blackwater Mine (BW) - Heavey Vehicle Workshop (BW/HVW) - Ground (GF)"

<a name="generate-view"/>
to generate data for displaying the SELECT field, we need to combine tempalte data with site issue with project data
* in project data locations.labels contain a list of fields the location need to be displayed
    * site, structure, level, space
    * we use the data to build the frame on how locations should be displayed
* also know that site issue location data links to Ground {"id": 14720, "label": "Ground (GF)", ...}
* now we have the botom of the hierarchical data, we can work our way back the tree
    * location id 14720 have parent location id 14719 which have parent 14718
    * use this data we can build the location hierarchy data
        * Blackwater Mine (BW)
        * Heavey Vehicle Workshop (BW/HVW)
        * Ground (GF)
        * Workshop (G-01)
* the last part we combine location labels with location data to get
    * Site : Blackwater Mine (BW)
    * Structure : Heavey Vehicle Workshop (BW/HVW)
    * Level : Ground (GF)
    * Space : Workshop (G-01)

cateogry also uses similar conecpt




