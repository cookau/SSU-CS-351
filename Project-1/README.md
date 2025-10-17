Which program is fastest? Is it always the fastest?

I calculated all the average times for all programs ran (-g, -O2 -g2, -O3 -march=native -g) with the parameters being MIN_BYTES=64, MAX_BYTES=256, NUM_BLOCKS=200000, NUM_TRIALS=5.
On average, alloca on -O3 -march=native -g was the fastest at 0.106 seconds. It was not always the fastest, as malloc had near identical times.

Which program is slowest? Is it always the slowest?

The slowest program on average was list on -g, running at a blazing 1.152 seconds. It seems like it is constantly the slowest. The next slowest time to it is 1.084 seconds, which is not much better.

Was there a trend in program execution time based on the size of data in each Node? If so, what, and why?

There is a trend in program execution time based on the size of each data node. When increased, the average time went up. Starting at MIN=10 MAX=10, all programs ran under 0.1 seconds. When increased to MIN=64 and MAX=256,
everything ran at a little over 0.1 seconds. When MIN=1024 and MAX=2048, everything took about 1 second to run.

Was there a trend in program execution time based on the length of the block chain?

Yes, when NUM_BLOCKS increased, all times across the board increased severely.

Consider heap breaks, what's noticeable? Does increasing the stack size affect the heap? Speculate on any similarities and differences in programs?

alloca stayed consistent the entire time, but everything else increased nearly 7x. No, increasing stack size does not affect the heap. All programs increased by about 7.5 times (besides alloca).

Considering either the malloc.cpp or alloca.cpp versions of the program, generate a diagram showing two Nodes. Include in the diagram the relationship of the head, tail, and Node next pointers. 
Show the size (in bytes) and structure of a Node that allocated six bytes of data. Include the bytes pointer, and indicate using an arrow which byte in the allocated memory it points to.
head -> nodeA(head) Size=6 Bytes (b0, b1, b2, b3, b4, b5) nodeA(tail) -> nodeB(head) Size=6 Bytes (b0, b1, b2, b3, b4, b5) nodeB(tail) -> tail

There's an overhead to allocating memory, initializing it, and eventually processing (in our case, hashing it). For each program, were any of these tasks the same? Which one(s) were different?

alloca uses alloca() to put memory into the stack. When using alloca(), you don’t use the heap, making it faster.
malloc uses malloc() to take memory from the heap. Using the heap makes it slower because malloc() now has to manage the heap and make sure it doesn’t run out of space.
I couldn’t tell you what list and new do, unfortunately.

As the size of data in a Node increases, does the significance of allocating the node increase or decrease?

When using small nodes, allocation costs are more important because you have to allocate the memory more often, versus when you have bigger nodes, you don’t have to allocate memory as much.
