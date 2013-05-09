Project List
============

GET https://secure.omtrak.com/v2/projects?module=:module_name&account=:account_id

Returns a list of projects the user have access to. If the module parameter is set, it will only return the projects where the user have access to the specified module.

Parameters
----------

* module: for now, it should always be set to "defects"
* account: *[temporary]* used for login while oauth is implemented. Only works for account equal to 6.

### Example ###

https://secure.omtrak.com/v2/projects?module=defects&access_token=TGT-59-5syfp0PaYVBLLldwsQeGYzg5ZDeDdTebbky0vHHjJbL06lUcc0-uQT19h4w

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