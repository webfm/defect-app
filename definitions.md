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
    * sort - order of hierachy level heading
    * field - field id (don't need to use this field)
    * label - label for hierarchy level heading
* a value list item have the follow structure
    * id
    * label
    * children - a list contain a number of value list item

<a name="status"/>
Status
------

* A defect record will display one of the following six statuses:
    * Not Assigned
    * Assigned
    * In-Progress
    * Inspect Now
    * Rejected
    * Closed

<a name="privileges"/>
Privileges
----------

there are 10 priviledges

* DEFECTS – if a user has access to the defect module. IGNORE THIS PERMISSION.
* DEFECTS_CREATE – if a user can create a defect.
    * If a user doesn't have the defects create permission, then in defect list view, the add new defect button will be hidden.
* DEFECTS_ASSIGN – if a user can assign the defect to a team.
    * If a user doesn't have defect assign permission, then in defect edit view (http://db.tt/anFvB5TT), the assignee field will not be editable (it will be hidden in the edit view).
* DEFECTS_DELETE – if a user can delete the defect.
    * A user must have the delete permission AND be either the creator OR have both View All and Edit All privileges to be able to delete a task. Otherwise, the delete button will be hidden.
* DEFECTS_ADD_COMMENT – if a user can add comments.
    * If a user doesn't have the add comment permission, then in comment view (http://db.tt/UawQ5Pzi), the add comment button will be hidden.
* DEFECTS_SET_DUE_DATE – if a user can set the due date of the defect.
    * If a user doesn't have this permission, then in defect edit view, the due date field not be editable (it will be hidden in the edit view).
* DEFECTS_EDIT_ALL – if a user can edit all defects.
    * By default, a user can only edit the regular fields of a defect record (all the fields except for assignee, due date and status) if the user is the creator of the record. If a user has the edit all permission, the user will be able to edit the regular fields of all the defects he has access to.
* DEFECTS_FIX – see Status Changes.
* DEFECTS_CLOSE – see Status Changes.
* DEFECTS_VIEW_ALL – see Status Changes.

<a name="status-change"/>

Status Changes
--------------

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

* validators for tempalte.type INPUT
    * DECIMAL - decimal number
    * WHOLE_NUMBER - whole number not decimal
* validators for tempalte.type - INPUT, EDITOR
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
* DOCUMENTS - store files 