pywk
====

Python awk-like line processing tool

```
usage:
    pywk PRE BODY POST
    pywk BODY
    pywk -h | --help

BODY is executed with the variable 'line' bound to each input line.

The following awk-like variables are available:
  _1, _2, ... for parts of the line split by the field separator FS
  _0 for the whole line
  NF for the number of fields and _NF for the last field
  NR for the number of records
The variable _ is the list of [line, _1, _2, ...], useful for slicing.
The function p prints its arguments joined by the output field separator OFS.
To simplify writing complex statements, ';;' is replaced by newline.

Awk-like patterns of /regex/ { } or python expression { } form can be used.
Append a '?' to the body to see the expansion for debugging.

Examples:
  # print line number, number of :-separated fields, and the first and last one:
  pywk 'FS=":"' 'print NR, FS, _1, _FS' ''
  # print the 1st, and 3rd to 7th field:
  pywk 'p(_1, *_[3:8])'
  # reverse every other line
  pywk 'if NR % 2: print line;;else: print "".join(reversed(line))'
  # print lines missing x or with more x:s than y:s
  pywk '! /x/ { p(line) }  line.count("x") > line.count("y") { p(line) }'
```
