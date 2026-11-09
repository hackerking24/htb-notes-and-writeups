# 13. Binary & DLL Analysis

## Static analysis

`file binary
strings -n 8 binary
checksec --file=binary
rabin2 -I binary
readelf -a binary`

## Dynamic analysis

`ltrace ./binary
strace ./binary
gdb ./binary`

## DLL hijacking (Windows)

`rabin2 -i app.exe
# ProcMon: filter NAME NOT FOUND + .dll`