Issue data
==========

GET https://secure.omtrak.com/v2/projects/{projectId}/site-works/work-requests

Description
-----------
Loads all work requests (issue and maintenance) in a project.

URL Placeholders
----------------
* projectId - the id of the project
* Request Parameters
* access_token - The login access token
* gzip (optional, default value = false) - true to enable gzip compression of the response data (body) to be generated. Any other value will automatically considered false. 

NOTE: If the server compressed the response body (data), a "Content-Encoding" header will appear with value set to gzip.
 
* since (optional, default value = 0) - The date represented in seconds since the standard base time ("the epoch"), January 1, 1970, 00:00:00 GMT.
* If 0, the server will generate a response containing all work request as created.
* If > 0, the server will generate a response containing work requests that are created, updated, and deleted at the start of the "since" date up to the current time.

Response Status
---------------
* 200 OK - The response body is the generated work request list JSON

Response Header
---------------
* Content-Encoding: gzip - If the server was able to compress the asset list using gzip compression (see gzip request parameter).

Response Body
-------------
* The response body is a JSON with the work requests items.
* If "since" parameter is not provided, or is 0, the JSON is a object that contains "issues", and "maintenance" field in which are objects that contains "created", "updated", and "deleted" fields. The "created" fields contains the items corresponds to the issues or maintenance. The "updated" and "deleted" fields will always be an empty array.

    {
        "issues" : {
            "created" : [
                {
                    // issue data
                },
                // more issues ...
            ],
            "updated" : [],
            "deleted" : []
        }
        "maintenance" : {
            "created" : [
                {
                    // maintenance data
                },
                // more maintenance ...
            ],
            "updated" : [],
            "deleted" : []
        }
    }

* If "since" parameter is > 0, the JSON is a object that contains "issues", and "maintenance" field in which are objects that contains "created", "updated", and "deleted" fields.
* "deleted" field will only contain id per item.

    {
        "issues" : {
            "created" : [
                {
                    // issue data
                },
                // more created issues ...
            ],
            "updated" : [
                {
                    // issue data
                },
                // more updated issues ...
            ],
            "deleted" : [
                {
                    id: 1
                },
                // more deleted issues ...
            ]
        }
        "maintenance" : {
            "created" : [
                {
                    // maintenance data
                },
                // more created maintenance ...
            ],
            "updated" : [
                {
                    // maintenance data
                },
                // more updated maintenance ...
            ],
            "deleted" : [
                {
                    id: 1
                },
                // more deleted maintenance ...
            ]
        }
    }
