Definitions
===========

<a name="value-list"/>
Value Lists
-----------

value list include Locations, categories and Lists
* value list contain two part
    * labels - describe the structure of value list, heading for each hierarchy level
    * value - value of each value list item
* labels contains
    * sort - order of hierarchy level heading
    * field - field id (don't need to use this field)
    * label - label for hierarchy level heading
* a value list item have the follow structure
    * id
    * label
    * children - a list contain a number of value list item

<a name="privileges"/>
Privileges
----------

there are 10 privileges

* DEFECTS – if a user has access to the defect module. IGNORE THIS PERMISSION.
* DEFECTS_CREATE – if a user can create a defect.
    * If a user doesn't have the defects create permission, then in defect list view, 
      the add new defect button will be hidden.
* DEFECTS_ASSIGN – if a user can assign the defect to a team.
    * If a user doesn't have defect assign permission, then in defect edit view add add defect view
      (http://db.tt/anFvB5TT), the assignee field will not be editable 
      (it will be hidden in the edit view and add view).
* DEFECTS_DELETE – if a user can delete the defect.
    * A user must have the delete permission AND be either the creator OR have both View All 
      and Edit All privileges to be able to delete a task. Otherwise, the delete button will be hidden.
* DEFECTS_ADD_COMMENT – if a user can add comments.
    * If a user doesn't have the add comment permission, 
      then in comment view (http://db.tt/UawQ5Pzi), 
      the add comment button will be hidden.
* DEFECTS_SET_DUE_DATE – if a user can set the due date of the defect.
    * If a user doesn't have this permission, then in defect edit view and add defect view, 
      the due date field not be editable (it will be hidden in the edit view and add defect view).
* DEFECTS_EDIT_ALL – if a user can edit all defects.
    * By default, a user can only edit the regular fields of a defect record 
      (all the fields except for assignee, due date and status) if the user is the creator of the 
      record. If a user has the edit all permission, the user will be able to edit the regular 
      fields of all the defects he has access to.
* DEFECTS_FIX – see Status Changes.
* DEFECTS_CLOSE – see Status Changes.
* DEFECTS_VIEW_ALL – see Status Changes.

<a name="status"/>
Status
------

* Defect status field will contain one of the 5 status:
    * pending
    * rejected
    * in_progress
    * submitted
    * closed

* A defect record will display one of the following six statuses:
    * Not Assigned - defect have **pending** status, assignee team is empty
    * Assigned - defect have **pending** status assignee team is not empty
    * In Progress - defect have **in_progress** status
    * Inspect Now - defect have **submitted** status
    * Rejected - defect have **rejected** status
    * Closed - defect have **closed** status

<a name="status-change"/>
Status Changes
--------------

User status can be changed in defect view (http://db.tt/HNhcdwdh).  

A status button is used to both allow user change the status 
and show the current status (currently shown as assigned). When user tap on the status button, a popover will appear giving user a list of 
selection for change the status to.  The list of selection will vary depend on user permission, the defect creator and assignee.

Since we can not change the status to assigned or not assigned (it'll be based on assignee field).  We uses a derived status called Pending.
When user change the defect status to pending.  The defect will actually show assigned (if assignee team is not empty) or not assigned (if assignee team is empty)

* Pending ("Assigned" or "Not Assigned") when:
    * Current status of the record is equal to In-Progress, Inspect Now OR Rejected AND:
        * Their team is set as the Assignee Team for the record OR
        *They have the following three privileges: View All, Edit All and Fix.
    * Current status of the record is equal to Rejected OR Closed AND:
        * Their team is the creator of the record AND they have Close privileges OR
        * They have the following three privileges: View All, Edit All and Close.
* In-Progress when:
    * Current status of the record is equal to Pending ("Assigned" or "Not Assigned"), Inspect Now OR Rejected AND:
        * Their team is set as the Assignee Team for the record OR
        * They have the following three privileges: View All, Edit All and Fix.
    * Current status of the record is equal to Rejected OR Closed AND:
        * Their team is the creator of the record AND they have Close privileges OR
        * They have the following three privileges: View All, Edit All and Close.
* Inspect Now when:
    * Current status of the record is equal to Pending ("Assigned" or "Not Assigned"), In-Progress  OR Rejected AND:
        * Their team is set as the Assignee Team for the record OR
        * They have the following three privileges: View All, Edit All and Fix.
    * Current status of the record is equal to Rejected OR Closed AND:
        * Their team is the creator of the record AND they have Close privileges OR
        * They have the following three privileges: View All, Edit All and Close.
* Rejected when:
    * Current status of the record is NOT equal to Rejected AND:
        * Their team is the creator of the record AND they have Close privileges OR
        * They have the following three privileges: View All, Edit All and Close.
* Closed when:
    * Current status of the record is NOT equal to Closed AND:
        * Their team is the creator of the record AND they have Close privileges OR
        * They have the following three privileges: View All, Edit All and Close.

<a name="validator"/>
Validators
----------

there are 8 validators can be applied to a template

* validators for template.type INPUT
    * DECIMAL - decimal number
    * WHOLE_NUMBER - whole number not decimal
* validators for template.type - INPUT, EDITOR
    * REQUIRED
    * UNIQUE
    * MAXIMUM_LENGTH
    * REGEX - regular expression validator, the value will be a regular expression
* validators for template.type - SELECT
    * REQUIRED_LEVEL - must fill in the hierarchy level for a field
        * i.e. for location like 'site', 'structure', 'level', 'room', REQUIRED_LEVEL = 2 means user must select a 'site' and a 'structure'. level and room can be left blank
    * END_LEVEL_DISPLAY - how many level in hierarchy level to be displayed in the selector
        * i.e. for location like 'site', 'structure', 'level', 'room', END_LEVEL_DISPLAY = 3 only 'site', 'structure', 'level' are displayed in the selector

<a name="template-type"/>
There are 5 type of template field

* INPUT - single line of text
* EDITOR - multiple line of text
* DATE - stores date
* SELECT - stores value list hierarchy
    * [see location example](location-example.md)
    * [see list example](list-example.md)    
* DOCUMENTS - store files 
    * [see example](document-example.md)

[click here](defect-details-view.md) for how template type should be displayed

