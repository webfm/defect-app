Sync process
============

The goal of Sync process is minimise calls betwen ipad and the server.  To do that need to implement most of the validation
on the ipad.  

The iPad will first request updated project data which contains the new permission and validation information.  The iPad then
can run 


Implement system to detect different type of change to defect, one example of the implementation will be

Add 5 flags to defect to mark change 

    New Defect

    Updated Defect
    
    Deleted Defect

    Status Changed

    Assignee Changed

    Due date Changed

    Comment added

Step 1
------

Download and sync project data (teams, validators, value lists), use server as the master list

Step 2 
------
Download defect list from server (incremental update)

    For defects updated on the server not but updated on the ipad, update the ipad defect using server copy

    For defect updated on the server and updated on the ipad, mark it as invalidated

Step 3
------

Check all updated defects on the ipad for permission conflict, use change detection system.  Invalidate defect fails permission check

    Store conflict message for each defect on the defect

Validate all updated and still valid defects on the iPad, invalidate all defect failed validation

    Store validatino message in the defect

Step 4
------
Upload all valid and updated defects to the server

    If server rejects the defect, mark it as invalidated

Step 5
------
If conflict dtected, give summary report if conflicts in a modal view i.e.

    "You no longer have permssion to create site work issue, please contact your project manager"
    "20 site issue contains invalid data"

Step 6
------
In defect list mark conflicted defect by change background color to light red. 
User can user filter to see invalid defects

Step 7 
------
When user tap on an invalide defect, the defect details view will show conflict and validation message.

Sync conflict
-------------
sync conflict.pdf
