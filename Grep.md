## Example lines

### Search a `man` page

Use option `-e` -

`man rsync|grep -e -P`

### Find TODOs in git repos

`grep -RIn TODO httpie/*`

### Exclude anything that does not include this

`grep -v com.apple`

### Return only lines that exactly match

`grep -w 'URL'`

### Find process ID with `pgrep`

`pgrep nameofapp` - print process ID.

`pgrep -l nameofapp` - print process ID and name of process.
