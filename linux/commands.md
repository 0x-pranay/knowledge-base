- `find -name '*.js' -not -path './node_modules/*'`

To list out all files excluding node_modules in a codebase

- `find -name '*.js' -not -path './node_modules/*' | xargs wc -l`

To list out all files and number of lines in each file. 



### Generate airtable record id and copy to clipboard

`airtable-uuid | tr -d "\n" | xclip -sel clip`



## GTile

- Move between monitors  - `Super + Shift + Arrows`

  
