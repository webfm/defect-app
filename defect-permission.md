Defect Permission
=================

Add new defect
--------------
    DEFECTS_CREATE

Add new defect set Assignee
---------------------------
    
    DEFECTS_CREATE
    DEFECTS_ASSIGN

Add new defect set due date
---------------------------

    DEFECTS_CREATE
    DEFECTS_ASSIGN

Edit defect
-----------
    
    defect created by user
or 
    DEFECTS_EDIT_ALL

Edit defect set due date
------------------------

    defect created by user
    DEFECTS_SET_DUE_DATE
or 
    DEFECTS_EDIT_ALL
    DEFECTS_SET_DUE_DATE

Edit defect change assignee
---------------------------

    defect created by user
    DEFECTS_ASSIGN
or 
    DEFECTS_EDIT_ALL
    DEFECTS_ASSIGN

Change status
-------------
In Progress
Inspect now

    DEFECTS_EDIT_ALL
    DEFECTS_FIX
or
    if user's team is the assignee of the defect 
    DEFECTS_FIX


Close 
Rejected

    DEFECTS_EDIT_ALL
    DEFECTS_CLOSE
or
    if defect is created by user 
    DEFECTS_CLOSE


Assigned
Not Assigned

    Defect created by user's team 
    Defect in Close or Reject
    DEFECTS_CLOSE
or
    Defect in Close or Reject
    DEFECTS_CLOSE
    DEFECTS_EDIT_ALL

Delete defect
=============

    DEFECTS_EDIT_ALL
    DEFECTS_DELETE
or
    Defect created by user's team
    DEFECTS_DELETE

Add Comment
===========

    DEFECTS_ADD_COMMENT

user's team is found in [project-data](project-data.md)
defect creator team will be added later



