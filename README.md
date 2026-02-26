# Paradox-Object-Tools
a package of hoi effects/triggers and other configuration info, to enable to usage of psuedo-objects in paradox coding, primarily used and tested in HOI4


## Files 
00_* = these are the core of the object tooling, and will be required with ANY usage of these tools 

01_* = debugging tools, these require the render_array from https://gist.github.com/cbrzeczysz/2583f1e4c71b566f005eaea036e8494d (Full credit to ciara) to work correctly

02_* = example files, due to the flexible nature of paradox scripting with variables, this can be used in a wide array of ways, 
and ill provide as many of those ways, as i make, in this repo

NOTE: there will be some logging code included in this git, it relies upon ciara's work. 

NOTE: the logging is incredibly disruptive due to the sheer amount of data these objects are likely to hold, 
in a future version, there will be a command to enable this.

## Initialisation

### dataframe__init__

## Effect Commands

### dataframe_close

### datatype_close 

### clear_loaded_row

### dump_session_data

### add_row_to_dataframe

### add_row_to_dataframe_head

### read_dataframe_index

### read_object_dataframe_attr

### update_dataframe_index

### update_dataframe_attr

### delete_dataframe

### clear_dataframe_index

## Effect Queries

### get_index_where_attr_is_v

