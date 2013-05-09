List Example
============

here is a block of project template from project data api

    "template": [
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
    ],

here is a block of list from project data api

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

In template block we have template field called Defect Type (from label) that of type SELECT,
and source.type is VALUE_LIST and source.id is 1.

The template.type indicate it's a value list field and template.source.type indicate that it uses value list
for selection values (list from project data api),  the template.source.id is 1, this link to lists.id (block of list)

The template.prefix has value h3540, this value links to an element in issue data block ("h3540": 2).

The value of the element is 2, this links to the id of a value list item in value value list

    {
        "id": 2,
        "label": "Warranty"
    },