# Paradox-Object-Tools
a package of hoi effects/triggers and other configuration info, to enable to usage of psuedo-objects in paradox coding, primarily used and tested in HOI4.

## Explaination

this utilises paradoxes token structure, meta coding to allow for human readable, automated, and predictable "Table-Based Systems" used by Extremis Ultimus team, that other developers may find helpful 

This has been used in the Social Media GUI to prevent code inflation (and i am lazy)

Full examples will be found in the EXAMPLE folder, to explain the individual components from GUI integration to the generalised effects we can use to modify the individual rows/attributes.

## Terminology

Due to paradox, not actually supporting objects, i am goint to explain the terminology here, 
[OBJECT]_[ATTRIBUTE]^ROW

the object is the root, this will always be idnetical, 

social_media_post_df_post <br>
social_media_post_df_posted_by <br>
social_media_post_df_like <br>
social_media_post_df_comment <br>
social_media_post_df_share <br>
social_media_post_df_response_to

these are all arrays, for the social_media_post_df object, 
in this case its attributes would be post, posted_by, like, comment, share, response_to. 

and if you check index 0 (row 0)<br>
e.g.<br>
social_media_post_df_post^1 <br>
and <br> 
social_media_post_df_posted_by^1

belong to the same row/post/attribute, 
going forward,<br>  
object = the first part of your encoded array
attribute = the second part of your encoded array
index,row = ^i part of your variable statement 

beyond this, there is little reason to have a further understanding, unless you wish to contribute additional code. 

## Files 
00_* = these are the core of the object tooling, and will be required with ANY usage of these tools 

01_* = debugging tools, these require the render_array from https://gist.github.com/cbrzeczysz/2583f1e4c71b566f005eaea036e8494d (Full credit to ciara) to work correctly

02_* = example files, due to the flexible nature of paradox scripting with variables, this can be used in a wide array of ways, 
and ill provide as many of those ways, as i make, in this repo

NOTE: there will be some logging code included in this git, it relies upon ciara's work. 

NOTE: the logging is incredibly disruptive due to the sheer amount of data these objects are likely to hold, 
in a future version, there will be a command to enable this.

## Initialisation

### dataframe__init__(trigger)
#### Requires:
* load_object (object token)
* object_archetype (object token)

#### Returns
* active datastruct_session

initialises the object ready for use, runs _object_schema trigger, sets default vars.

### [object_archetype]_object_schema
#### Requires:
* setup.

object_schema is used by dataframe__init__ to build the neccessary metadata for the effects/queries to work.

#### overview
##### object_type (required)
this variable is the object type, as there is only one object type right now this will always be token:dataframe, i will expand on this should i ever need anything more unique or complex. 
##### object_global_b
set this to 1 if you want it to be stored in the global. scope, you do not have to set it at all if you wish for it to remain in the current scope (ive only tested with the country scope, i have no concern about state scope, anything else, with risk, let me know)
##### object_schema (array)
this is an array of the tokens for the attribute names, e.g. token:posted_by for [OBJECT]_posted_by
##### object_schema_type (array)
this is an array which describes what kind of variable it is, int_type is the most common, but it also supports token_type (for meta coding) and bit_type (for boolean values, yes its an int shhh)

#### NOTE: object_schema and object_schema_type should be indentically sized. see any EXAMPLE/scripted_trigger/*_definitions.txt for live examples.

## Effect Commands

### dataframe_close
#### Requires:
* active datastruct_session

Clears all neccessary metadata and attributes (row data) (as theyre saved in the datastruct)
this will clear variables known as "active datastruct_session"

### clear_loaded_row
#### Requires:
* active datastruct_session

Clears only the currently loaded attributes (row data)

### dump_session_data
#### Requires:
* active datastruct_session

Prints out the currently loaded attributes (row data) to console and game.log

### add_row_to_dataframe
#### Requires:
* active datastruct_session

adds a new row to the end of your dataframe (e.g. if 6 long, will be placed in position 6)

### add_row_to_dataframe_head
#### Requires:
* active datastruct_session

adds a new row to the end of your dataframe (e.g. if 6 long, will be placed in position 0, everything else shifted up 1 index)

### read_dataframe_index
#### Requires:
* active datastruct_session
* dataframe_index (row numer)

this will load the specified row into the current scopes permanant variables (for easiest manipulation, use dataframe_close to clear these if thats the desired behaviour)

### update_dataframe_index
#### Requires:
* active datastruct_session
* dataframe_index (row numer)

this will take the current scopes permanant variables and loads them back into the dataframe in the correct positions, 

### clear_dataframe_index
#### Requires:
* active datastruct_session
* dataframe_index (row numer)

this will delete the current row from the dataframe record itself, you should only really do this if you are confident you will no longer need those vars (e.g. mechanic shutdown/annexed country etc.)

### update_dataframe_attr
#### Requires:
* active datastruct_session

### read_object_dataframe_attr
#### Requires:
* active datastruct_session

### delete_dataframe
#### Requires:
* active datastruct_session

this will delete the whole object, again, only use once you are condifent you no longer need it/ need to rebuild it from scratch

## Trigger Queries

### get_index_where_attr_is_v
#### Requires:
* active datastruct_session
* search_attr (token)
* search_attr_val (value(can be token/int/whatever))
#### Returns:
* ret_val (index where the query is true)
* trigger will fail if none are found. (any_of)

this will iterate through the rows, and check for the row where the search_attr = search_attr_val