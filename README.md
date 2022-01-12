# COMP304_Project3

This is the third project of the COMP304 course (Fall'21) at Koç University.

## Contributors
Beyzanur Çoban\
Kerem Girenes

## Compiling

Use the following command to compile the program. 

### Part 1:
```bash
gcc part1.c -o part1
```

### Part 2:
```bash
gcc part2.c -o part2
```

## Executing

Use the following command to execute the program. The first argument will represent the disk that we look up for the
page faults. The second argument will be the address list that we want to reach and find the corresponding physical memory location. The bit after the -p flag specifies page replacement policies (1 for LRU, 0 for FIFO)

### Part 1:
```bash
./part1 BACKING_STORE.bin addresses.txt
```

### Part 2 FIFO:
```bash
./part2 BACKING_STORE.bin addresses.txt -p 0
```

### Part 2 LRU:
```bash
./part2 BACKING_STORE.bin addresses.txt -p 1
```

## Working Parts

We implemented the both parts of the project. If you give the valid command line arguments, then it will produce an
output. There is no error or segmentation fault in the code. 

## Brief Discussion on Implementation

In the first part, for the search on tlb, we go through each entry in the tlb table. To add to tlb, we implemented a FIFO algorithm. 
It uses circular indexing and writes the new entry to the place of the oldest entry in the table. Our Offset Mask and Page Mask are 10 bits of 1.
To get the offset of the logical address, we bit-wise mask with Offset Mask. To get the logical page, we first shift it to the right by
Offset Bits which is 10. Then we bit-wise mask it with Page Mask. Then, we search the tlb for this logical page, and store it in our physical page. If physical page is -1, we know its logical page was not in TLB, so it is a page fault. In that case, we assign our physical page to the last free page, then prepare the next free page as by incrementing free page by 1. If that free page is out of bounds, we circle back. We then enter to the pagetable our physical page at the logical page index. Lastly, we copy our page's content from backing store and place it in physical frame content. After this, we also add the physical and logical pages to the TLB.

In the second part, in addition to part1, we did the following. We defined a page frame count as 256 as given. Our memory size was now page frame count times the page size. In addition, we added a clock for our LRU implementation. We also included a page frame register array for LRU. We now get from the user an -p flag with either 0 or 1 that is stored in lru selected integer, so we can execute operations by either LRU or FIFO. Searching the TLB is the same, however we changed add to tlb function to support the LRU replacement policy in addition to FIFO. If LRU is selected, we go through the page frame register and find the least recently used page to replace. This time, in main, even if we have a TLB hit, we advanced the clock and updated that page's register with its last use time. And now if we have a TLB miss, if LRU is selected, we replace the least recently used page.
