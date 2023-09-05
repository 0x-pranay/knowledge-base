Kill all processes related to `pgAdmin4`. 
`pkill -f pgadmin4`

The `pkill` command sends a signal to all processes whose command name or arguments match the given pattern, in this case, "pgadmin4". The `-f` option tells `pkill` to match against the entire command line rather than just the process name.

