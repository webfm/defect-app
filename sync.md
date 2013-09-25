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

    For defects updated on the server not but updated on the ipad, update defects on the iPad with server date

    For defect updated on the server and updated on the iPad, leave the changes

    For each defect check update need to be separated into three portions
        1) status update
        2) documents
        3) other defect data include defect fields (from template), assignee, due date


For example for a defect status and field (assignee) has been updated on the server and the defect field (description, due date) has been updated on the iPad
then in step 2 update the status of the iPad defect (the defect is still valid and will need to be pushed to the server later)

When sync documents, we need to sync individual documents in a defect.  

    1) Any new document added on the server, download it to the iPad
    2) Any document removed on the server, remove it on the iPad (regardless of whether the document annotation has changed or not)
    3) After step 1 and 2 is done, any new document on the iPad, upload it to the iPad
    4) Any document changed on the iPad (added annotation), upload it to the server [update document api](sync.md#UPLOAD-UPDATED-DOCUMENT)
    5) Any document deleted on the ipad, remove it on the server

Step 3
------

Check all updated defects on the iPad for permission conflict, i.e. for new defects check if user have create defect permission.
Invalidate defects that failed permission check

    Store conflict message for each defect on the defect

Validate all updated and still valid defects on the iPad, invalidate all defect failed validation (use updated defect template field validators)

    Store validation message in the defect

Step 4
------
Upload all valid and updated or new defects to the server

    If server rejects the defect, and status code is 404 then remove the defect on the iPad

    If server rejects the defect, mark defect as invalidated.  

    There will be issues with iPad app contain defects deleted on the server.  This case is ignored.

Step 5
------
If conflict detected, give summary report if conflicts detected.

Step 6
------
In defect list mark conflicted defect.  User can user filter to see invalid defects.

Step 7 
------
When user tap on an invalide defect, the defect details view will display conflict or validation message.

Permission Conflicts
--------------------
When a defect has permission conflicts, users can not do anything to resolve the issue by them self.
One possible resolution is to call the project managers to obtain the permission.  If they should have the permission from the start
user can logout to flush the conflicted defects.

Sync conflict
-------------
[sync conflict documentation](sync conflict.pdf)

Download Documents
==================

After the defect sync process, the iPad defects document should match the server defects document.  The 
document documents process need to traverse through all defect from the lowest defect id.  For each document
check if the document exist on the iPad, if does not exist download the document else do nothing.



