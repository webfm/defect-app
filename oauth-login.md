oAuth login
===========

The system uses oAuth 2.0 for api authentication.  To login We need to take the following steps:

Reqest authentication ticket
----------------------------

First login and obtain a authentication ticket.

    Post https://accounts.webfm.net/v2/access/tickets

**Post Form Data (x-www-form-urlencoded):**

* client_id: client id provided by WebFM
* username: username provided by user
*password: password provided by user
* remeberMe: Set it always to 'true' to have a 1 year expiration for the ticket. 
This field is optional but the value is assumed false which will cause the ticket to have 12 hours expiration

**Response**

Success Response

* Response Code 201
* Authentication ticket in header "Location"

    Location: <host>/cas/v2/access/tickets/:token

* Authentication ticket in response body in JSON format

    {"ticket":":token"}

Failed response

* Response Code 400 (Bad Request)

Subquent API cal will need to add autentication ticket within the call parameter i.e.

    tps://accounts.webfm.net/oauth2.0/profile?access_token="ticket

Obtain user profile
-------------------

https://accounts.webfm.net/oauth2.0/profile?access_token=:ticket

    {
        "id":user_login,
        "attributes":[
            {
                "id":user_id
            },
            {
                "first_name":user_first_name
            },
            {
                "last_name":user_last_name
            },
            {
                "email":user_email
            }
        ]
    }

Parameters

* user_login: email address used in login
* id: id of user in system
* first_name: first name
* last_name: last name
* email: user email address

