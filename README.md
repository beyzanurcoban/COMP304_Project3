# COMP304_Project3

This is the third project of the COMP304 course (Fall'21) at Koç University.

## Contributors
Beyzanur Çoban\
Kerem Girenes

## Compiling

Use the following command to compile the program. 

```bash
gcc part1.c -o part1
```

## Executing

Use the following command to execute the program. The first argument will represent the disk that we look up for the\
page faults. The second argument will be the address list that we want to reach and find the corresponding physical memory location.
```bash
./part1 BACKING_STORE.bin addresses.txt
```

## Working Parts

We implemented the first part of the project. If you give the valid command line arguments, then it will produce an\
output. There is no error or segmentation fault in the code. 
