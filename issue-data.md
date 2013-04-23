Issue data
==========

GET https://secure.omtrak.com/v2/projects/:project_id/defects?account=:account_id

Returns issues in a project.

Parameters
----------

* project: project id.
    * required
* account: *[temporary]* used for login while oauth is implemented. Only works for account equal to 6.

Example
-------

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