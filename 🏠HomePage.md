```dataview 
table 
  file.folder as "Folder"
, file.path as Path
, file.tags as "Tags"
, file.ctime as "Create_Timestamp"
, file.mtime as "Update_Timestamp"

from "/" 

sort file.mtime  desc

```

