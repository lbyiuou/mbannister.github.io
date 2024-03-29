---
layout: default
title: "CS 62: Assignment 09"
mathjax: true
---

# Assignment 09: The BooOS operating system

## Design due on 4/3; Assignment due on 4/10

## Introduction

Until now, most of you will have only written Java programs that perform one task at a time. You have likely become quite accustomed to the assumption that your program will execute sequentially, in the order you specify, with one method executing at a time, as well as the comfortable assumption that a simple chunk of code like this will always execute from beginning to end without interruption or interference.

```java
int balance = getBalance();
balance += amount;
setBalance(balance);
```

Assuming that `getBalance( )` and `setBalance( )` are implemented as they should be, you can feel comfortable in a single-threaded program that nothing can really go wrong here; the old balance will be fetched and placed into the variable balance, an amount will be added to it, and the result will become the new balance. (There is one possible problem, which is the fact that `ints` have a maximum value and the balance will roll back to a negative number if it passes that maximum.) This chunk of code is simple, straightforward, and predictable.

We call Java programs that perform only one task at a time _single-threaded_. However, not all Java programs fall into this category. In Java, a thread consists of a run-time stack and a program counter (pointing to the current bytecode instruction that is to be executed). Java programs can have multiple, simultaneously-executing threads, meaning that they can have more than one run-time stack (one per thread) and more than one program counter (again, one per thread), though all the threads will share the same static memory and the same heap. (There is essentially no theoretical limit on how many threads you can run at a time, though there are practical limitations, such as the reality that run-time stacks are pre-allocated to a size that can be as large as a megabyte or two each.) The practical effect of this is that a program can carry on doing multiple, separate tasks simultaneously, with this simultaneity achieved by literally running the threads on separate processors, if you have at least as many processor cores as threads, or by time-slicing---rapidly switching between them, so that one processor can contribute to the work of more than one thread---if you have more threads than processors.

When first confronted with this notion, a reasonable question to ask is "Why would I want my program to be able to do more than one thing at a time?" There are a variety of reasons. A few of these reasons are:

- On a machine with multiple processors---something that has become the norm for personal computers and even many smartphones---more than one processor can execute parts of your program simultaneously. Current trends lead to a future where even personal computers may well have a very large number of processors; we'll want our programs to be able to make use of these. But a single Java thread can only keep a single processor busy! If you had four processors on a machine, 75% of your processing power would sit idle, even if there was theoretically work they could be doing.
- Even on a machine with a single processor, multiple threads, used judiciously, can be a valuable design aid, allowing us to take disparate tasks and separate them into threads, so that the code for each task does not have to be intertwined with code for the other. One place where this need arises is in programs with graphical user interfaces. For example, all of the UI-related code in a Java-based graphical user interface (using Java's Swing library) is required to run on the same thread, so long-running tasks must be run on a separate thread to allow the UI to remain responsive while those tasks proceed.
- A program that can be broken up into completely autonomous tasks that communicate only by passing messages back and forth can then be broken up into separate programs that run together as a distributed system on separate machines, with the messages sent over a network instead of just being copied from one memory location to another. This has some tremendous scalability benefits---if you have 1,000 machines and have enough work to keep all of them busy all the time, you can get your work done up to 1,000 times faster than you could on a single machine. Of course, you'll never really achieve the 1,000x speedup, since there is time spent creating, sending, and receiving messages — and quite possibly time spent by each machine waiting for another machine to do work that must be done before it can continue. But the speedup can still be dramatic, especially if you can get a lot of machines to work together on a problem that is easily divisible into individual, independent units of work. (And they don't all have to be your machines! [Folding@home](https://en.wikipedia.org/wiki/SETI@home), for example, asks people all over the world to donate their spare computing resources — times when their machines aren't doing anything else — to work on achieving a deeper understanding of diseases like Alzheimer's, Mad Cow, and Parkinson's. [SETI@home](https://en.wikipedia.org/wiki/SETI@home) is a similar project devoted to finding evidence of intelligent extra-terrestrial life.)

_Concurrency_, which is achieved in Java by using threads (and is achieved with a variety of mechanisms in other programming languages), has emerged as a central theme in programming language design and software engineering in recent years. This project begins your exploration of the topic of concurrency by asking you to write a multi-threaded Java program. In particular, we'll be exploring some of the concepts underlying _shared-state_ concurrency, where threads share objects as a way of communicating with one another. Our exploration will be done within the context of a simulation of a very rudimentary operating system.

## BooOS: Our operating system

One of the primary jobs of an operating system is to manage access to various resources. On a typical personal computer, these resources include the display, input devices such as the keyboard and mouse, memory, disk drives and other external storage, speakers, and network adapters. This access must be managed even in the face of concurrent attempts by multiple programs to use these resources. If one program is writing to a file, other programs may be prohibited from also writing to that same file; if more than one program is attempting to play a sound through the speakers, the sounds may be mixed and played together.

Our operating system for this assignment is called BooOS. BooOS doesn't manage all of the resources of a personal computer; it's little. Instead, it focuses on three things:

- __Files__, which store information and can be read or written.
- __Printers__, which print information in hard-copy form.
- __Programs__, which (for our purposes) read and write files and print to printers.

BooOS can run any number of programs simultaneously, each of which is a sequence of operations that are either file creations, file reads, file writes, line prints (printing one line of output to a printer), or calculations. Only one program is permitted to print to a printer at a time; similarly, no two programs can access the same file at the same time. File and printer operations are not instantaneous; they take time, and BooOS has the job of making sure that programs that attempt to access a file are suspended while another program is already accessing it.

There are __no__ fairness considerations in BooOS. Suppose Program A begins accessing the file X. While its access is proceeding, Program B attempts an access to the same file and is blocked; just after that, Program C also attempts an access to the same file and is blocked. When Program A's access completes, either Program B or Program C can be chosen to gain access to the file next. The same rule applies to printers. _This is the default behavior when you using locks in Java._

## The assignment: a BooOS simulator

In this project, you're being asked to write a BooOS simulator, which is capable of executing multiple simultaneous programs that consist of sequences of five operations: file creations, file reads, file writes, line prints, and sleeps (periods where the program is inactive). The sleeps simulate the calculations that a program might be performing in between file and printer accesses; for our simulator, though, we won't be concerned with what those calculations are or what values they produce.

Initially, the simulator reads an input file that consists of a set of programs to execute. All of the programs should begin immediately after the simulator finishes reading the last one.

For your simulator, assume that BooOS is running on a hardware platform that has the following characteristics. (These characteristics are slow, relative to realistic computer hardware, but serve to slow our simulation down to the point where we can see what it's doing along the way.)

- Creating a file, if it does not already exist, takes 300 milliseconds. If it does already exist, the attempt to create it fails silently.
- Reading from a file, once a program gains access to it, takes 150 milliseconds.
- Writing to a file, once a program gains access to it, takes 200 milliseconds.
- There is no limitation on the number of files that can exist at any given time.
- Files are sequences of characters, initially filled with spaces when they're first created.
- Printing a line of output to a printer, once a program gains access to it, takes at least 1000 milliseconds (with the actual duration determined by the length of the line).
- There is always exactly one printer connected to the machine.

Your simulator will store files in memory, rather than on disk. Printer output will be written to a text file, rather than printed to an actual printer.

The simulator is not required to print output to the console, but you might find it useful to print output whenever anything interesting happens (e.g., a program starts, a program ends, a program begins a read operation, a program finishes a read operation, and so on). _Programming tip: Eclipse will write a toString method for you! Look under the source menu_ Be aware that the `System.out.println()` method provides synchronized access to the console automatically; each call to `println()` blocks other threads from printing to the console until it's done. However, if you want to print a line of output to the console by using multiple calls to System.out.print, you may find that output from one thread will be interleaved with output from another; for this reason, it is better to build the entire line of output as a string, then print that string using one single call to `System.out.println()`.

## Input file format

An example of an input file for your simulator follows. The commented portions of the example below are not considered part of the input file; they're included here to explain the file's contents. Your parser may support comments, but is not required to.

```text
2                       // The number of programs
FirstProgram            // The name of the first program
CREATE File1 100        // Create a file called File1 of size 100 bytes
WRITE File1 0 C         // Write the character 'C' to byte 0 of the file File1
READ File1 10           // Read from position 10 in File1
SLEEP 200               // Sleep for 200 milliseconds
WRITE File1 10 F        // Write the character 'F' to byte 10 of the file File1
PRINT File1             // Print the contents of File1 to the printer on one line
END                     // End of FirstProgram
Program2                // The name of the second program
CREATE File2 10         // Create a file called File2 of size 10 bytes
WRITE File2 0 X         // Write the character 'X' to byte 0 of the file File2
SLEEP 300               // Sleep for 300 milliseconds
WRITE File2 1 Y         // Write the character 'Y' to byte 1 of the file File2
PRINT File2             // Print the contents of File2 to the printer on one line
SLEEP 500               // Sleep for 500 milliseconds
PRINT File1             // Print the contents of File1 to the printer on one line
END                     // End of SecondProgram
```

In general, the format of the input file is as follows.

- A number, on its own line, indicating how many programs will be running.
- For each program:
    - A single word, on its own line, indicating the name of the program. You can assume that all the program names will be unique.
    - A sequence of commands, one per line, taken from the following set:
        - `CREATE filename size` — where filename is a single word and size is a positive integer
        - `READ filename offset` — where filename is a single word and offset is a positive integer
        - `WRITE filename offset character` — where filename is a single word, offset is a positive integer, and character is a single character
        - `PRINT filename` — where filename is a single word
        - `SLEEP duration` — where duration is a positive integer
        - `END`
    - Each program ends with an `END` command, which is only permitted to appear at the end of a program.

You may assume that the input file is properly formatted according to these rules, though, of course, you may not assume that the input files we'll be testing the program with will look exactly like the example file shown above.

## More precise semantics of commands

The semantics of each command follow.

- `CREATE filename size`: Creates a new file called `filename` whose `size` is given by `size` (meaning that the file stores `size` characters). Initially, the file consists of spaces. If a file with this name already exists and is at least as big as `size` bytes, the command does nothing; if a file with this name already exists but is smaller than `size` bytes, the existing file is resized to be `size` bytes and spaces are used to fill in the new area. If creation is successful (either because a new file is being created or an existing file is being extended), block the currently-running program for 300 milliseconds.
- `READ filename offset`: Reads the character at the given offset from the file whose name is `filename`. Fails silently if no file with the name `filename` exists or if the offset is not within the bounds of the file. If the file exist (even if the offset is out of bounds), block the currently-running program for 150 milliseconds.
- `WRITE filename offset character`: Writes the character `character` into offset `offset` of the file whose name is `filename`. Fails silently if no file with the name `filename` exists or if the offset is not within the bounds of the file. If the file exists (even if the offset is out of bounds), block the currently-running program for 200 milliseconds.
- `PRINT filename`: Prints the contents of the file whose name is `filename` to the output file containing the printer's output. (The output of each `PRINT` command should be on its own line of the output file.) Fails silently if the file does not exist. If the file exists, block the currently-running program for 1000 milliseconds plus one millisecond per byte in the file. (So, for example, if the file has a length of 300 bytes, you'll block the currently-running program for 1300 milliseconds.) Note that printing a file requires locking both the printer and the file for the duration of the print operation.
- `SLEEP duration`: Blocks the currently-running program for `duration` milliseconds. This is used to simulate the program doing calculations that do not involve system resources like files and printers.
- `END`: Ends the program.

(You may be wondering why the `READ` command doesn't seem to have any real use, since there are no commands that take the character that was read and do anything with it. Remember, though, that the intent here is not to provide a programming language; it's just to simulate the interaction of multiple programs wanting to perform input and output to the same devices simultaneously. In such a context, it's less important what the operations are and more important when they occur relative to one another and how simultaneous operations affect one another.)

## Running your simulator

Your `main()` method should be written in a class called `Simulator`; all of your classes should be in a package `BooOS`. Your program should accept two command-line parameters: the name of the input file containing the programs it should execute, and the name of the output file to which printer output should be written. We should be able to run your program from the command line using the following command:

```bash
java Simulator input1.txt output1.txt
```

...and, of course, should be free to replace `input1.txt` with the name of any (properly formatted) input file we'd like to test your simulator with, and `output1.txt` with the name of any output file we'd like.

## Design requirements

This is an exploration of concurrency, so you'll need to use multiple threads in your solution. Furthermore, this is an exploration of shared-state concurrency, so you'll also need to have shared objects. I'm requiring the following basic design for your simulator:

- The main thread, when the simulator starts, should read the input file, then create and start one thread for each program that needs to be executed. It's fine to store the contents of the program in an `ArrayList<String>` and parse it as you execute it. (You can use a more complex solution, such as the [Command pattern](https://en.wikipedia.org/wiki/Command_pattern), if you prefer.)
- Start the threads one after another (use a for-loop), but don't start any of them until after you've read all of the programs.
- Files and the printer should be represented as shared objects. Note that you don't have to do anything special in Java to share objects; objects are shared by default, as all threads share the same heap. But you do need to ensure that all threads are accessing the same object for each file and the same object for the printer.
- Use a [HashMap](http://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html) to store the mapping between filenames and file objects, i.e., it is acting as your file system. If you have never used a `HashMap` before, read the JavaDocs and bring questions to class, office hours or mentor hours.
- Java synchronization and coordination primitives such as the `synchronized` keyword, `wait()`, and `notify()` should be used to coordinate activities between programs. You can use whichever combination of these primitives you think is appropriate to ensure that the simulation's threading-related guarantees are met. Be sure you're not just "sprinkling" the `synchronized` keyword throughout your program; use it when it's the right thing to use and avoid it when it's not.
- The current version of Java provides a library of useful concurrency-related classes (e.g., the `java.util.concurrent` library), but these classes are __strictly off-limits__ here; stick to the primitive operations like `synchronized`, `wait()`, and `notify()`.

## General rules and regulations

You may work with a partner for this assignment. Follow the naming convention we have used in lab when working with partners when submitting your assignment and remember the JSON file. You will be submitting your assignment in two parts: first a design, and second the completed project with a short write-up explaining how you implemented the project. Details about the write up will be posted shortly. For now work on the design and coding.

For the design you will be submitting incomplete implementations of the classes you will use in your assignment. The classes will need to include a description of their purpose, any classes they inherit from, decelerations for all public methods and JavaDocs for all public methods.

The Java library has many useful classes in it, and your classes may inherit from these classes. This can save you from writing a lot of code! Additionally, eclipse can auto-generate a lot of code for you! Look under the source menu. In this project I would like to encourage you to use both of these facilities.

You will submit your exported Eclipse project using the the usual method with the usual naming convention. Remember to include a JSON file for your project. For the design prefix your directory with `_design`.

## Rubric

Coming soon. Ask me if you have any questions.

## Acknowledgements

Originally written by [Alex Thornton](http://www.ics.uci.edu/~thornton), Fall 2007, based on an idea by [Raymond Klefstad](http://www.ics.uci.edu/~klefstad/).
