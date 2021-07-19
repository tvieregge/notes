`g` in vim is used to apply to a command to each line in a range (defaults to whole file) like so
`:[range]g/pattern/cmd`

Before executing _cmd_, "`.`" is set to the current line.
It executes `cmd` as in command mode (`:`)

#### Examples
Delete all lines matching a pattern.
```
:g/pattern/d
```

Display context (5 lines) for all occurrences of a pattern, which some beautification
```
:g/pattern/z#.5|echo "=========="
```

Copy all lines matching a pattern to register 'a'.
```
qaq:g/pattern/y A
```
 _qaq is a trick to clear register a_
 
 Run a macro on matching lines (example assuming a macro recorded as 'q'):
```
:g/pattern/normal @q
```