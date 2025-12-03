
## Highlights

### Chapter 12: System and Process Information

In this chapter we look at ways of accessing a variety of system and process information. The primary focus of the chapter is the `/proc` filesystem.

In older UNIX implementations, there was typically no easy way to introspectively analyze (or change) attributes of the kernel, to answer questions such as the following:
- How many process are running on the system and who ownes them?
- What files does a process have open?
- And other questions

Some older UNIX implementations solved this problem by allowing privileged programs to delve into data structure in kernel memory. However this approach suffered various problems. In paritcular, it requires knowledge of the data structures of the kernel, and these may change between different kernel versions, requiring these programs to be rewritten.

To provide easier access to kernel information, many modern UNIX implementations provide a `proc` virtual file system. This file system resides under the `\proc` directory and contains various files that expose kernel information, allowing process to conveniently read that information anche change it in some cases, using normal file I/O system calls.

The file system is said to be virtual because the files and subdirectories that it contains don't reside on a disk. Instead, the kernel creates them "on the fly" as processes access them.