# Deltacode

### About:
`deltacode` is a simple command line utility that leverages the power of 
[scancode-toolkit](https://github.com/nexB/scancode-toolkit) to determine file-level 
differences between two codebases. 

### How to use:
In order to calculate these differences (i.e. 'deltas'), the user must have two individual
scancode scan files, with the `--info` scan option at minimum.

For example:
```
$ pip install scancode-toolkit
$ scancode --info ~/postgresql-9.6/ ~/psql-9.6-fileinfo.json
$ scancode --info ~/postgresql-10.0/ ~/psql-10.0-fileinfo.json
```

Once you have the two codebase scans, simply install/configure deltacode, and run it 
on the two scans:
```
$ source configure
(deltacode) $ deltacode --help

Usage: deltacode [OPTIONS]

  This script identifies the changes that need to be made to the 'old' scan
  file (-o or -old) in order to generate the 'new' scan file (-n or -new).
  The results are written to a .csv file (-c or -csv-file) or a .json file
  (-j or -json-file) at a user-designated location.  If no file option is
  selected, the JSON results are printed to the console.

Options:
  -h, --help            Show this message and exit.
  -n, --new PATH        Identify the path to the "new" scan file  [required]
  -o, --old PATH        Identify the path to the "old" scan file  [required]
  -c, --csv-file PATH   Identify the path to the .csv output file
  -j, --json-file PATH  Identify the path to the .json output file

(deltacode) $ deltacode -n ~/psql-10.0-fileinfo.json -o ~/psql-9.6-fileinfo.json -j ~/psql-10.0-psql-9.6.5-delta.json
```

### Notes:
* `deltacode` also collects statistical information, like # of files and other percentages. Currently, this output is not present in the `csv` output
* json output will be consumable by other utilities. There will also be a json -> csv converter in the future as well. 

### Future TODOs/additions:
* Use `license` information from scan to determine deltas as well (As opposed to strictly fileinfo)
* Use `copyright` information from scan to determine deltas
