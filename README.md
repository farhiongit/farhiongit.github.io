# My Favourite Things

Let's go straight to the point: I'm an old school IT engineer.
Therefore, I've got my fixed ideas.

## My favourite code

Hereafter are few tools and implementations of famous algorithms of my own.

- tools are here to show that the C language can be extended to provide software component similar to those available with "modern" languages.
- algorithms are here for fun and personal studies.

Everything is on [Github](https://github.com/farhiongit).

### Tools

#### Pool of threads for parallel programming on CPU

This is the common pattern of asynchronous programming ported to C language for parallel programming.

This comprehensive C standard implementation of [thread pool](https://github.com/farhiongit/c_thread_pool) goes beyond the classical API "create, add tasks, wait, destroy":

- dynamic creation of tasks, useful in divide and conquer algorithms for instance ;
- automatic deallocation and reallocation of threads (and their resources) with regard to the rate of submitted tasks ;
- monitoring feature ;
- management of virtual tasks (invoking asynchronous system calls).

#### Channels for exchanging messages between threads

This is another common pattern of asynchronous programming ported to C language for synchronisation of threads.

This [module](https://github.com/farhiongit/message-in-the-bottle) implements the [communicating sequential processes](https://en.wikipedia.org/wiki/Communicating_sequential_processes) model first described by from Tony Hoare's in 1978 and that can also be found in Go or Rust to name a few: several threads communicate and synchronise by exchanging messages of any type.

The interface is easy to use: open the channel between threads, send messages on one side, wait for and receive messages on the other side, close the channel.

Messages sent in the channel are strongly typed with some kind of templates (from an idea of [Randy Gaul](https://randygaul.github.io/)).

#### Dates and times without wasting time

The C standard time handling API (time.h) is very low level and difficult to understand and to use. The object `struct tm` follows unusual and subtle conventions, is counter-intuitive and needs translation to concepts as simple as days, months and years to name a few. The use of functions such as `mktime`, `localtime` is not straight forward.

Nevertheless, it gets everything needed to handle UTC, local time (as chosen by the user) and other time zones properly, and to alternate between those referentials (actually and fortunately, Berkerley in BSD, and later GNU in glibc, added an extra (but unfinished and useless), field `tm_zone` to `struct tm` that can be hijacked to handled every timezone.)

[better_times](https://github.com/farhiongit/better_times) allows to manage UTC, local time and time zones conveniently in C, with a correct handling of daylight saving time. It offers a complete set of functions for definition and calculation on date and time, based on the usual structure `struct tm` of `<time.h>`.

#### Light C standard timers

POSIX defines timers with `timer_create` and `timer_settime`.

The C standard defines timers with `timerfd_create` and `timerfd_settime`.

[timer.h](https://github.com/farhiongit/c_thread_pool/blob/master/timer.h) is a simpler user-interface that permits to define timers within a single process (but possibly several threads).

#### Maps, sets and lists

This is a never-seen-before implementation of a [map library](https://github.com/farhiongit/c_thread_pool/blob/master/map.h) that can manage maps, sets, ordered and unordered lists :

    - It uses only 7 functions: create, destroy, insert, traverse, forward and backward (and remove elements), find a key (and remove it) and count.
    - All functions are MT-safe (which is not true for most implementations of maps).

#### Templates (maps, sets and lists)

Generic programming is a great paradigm that is not limited to object oriented languages.

Functional languages make use of them as well.

And Randy Gaul has shown can this can be [applied to C](http://cecilsunkure.blogspot.com/2012/08/generic-programming-in-c.html).

I turned his ideas into [template containers for C](https://github.com/farhiongit/Ctemplates).

This is therefore another implementation of containers with is strongly typed, in C.

#### log4t and trace

[trace](https://github.com/farhiongit/c_thread_pool/blob/master/trace.h) permits to log all calls to a function without changing the code.

[log4t] is a korn-shell script that catches the standard input, standard output and standard error of a process and log them to files, augmented with timestamp, without changing the code of the process and without recompiling. Worth to be seen.

#### h2md

This small [script](https://github.com/farhiongit/c_thread_pool/blob/master/h2md) converts a C header file (from the standard input stream) into a markdown file (to the standard output stream).

For instance, [README_map.md](https://github.com/farhiongit/c_thread_pool/blob/master/README_map.md) was generated from [map.h](https://github.com/farhiongit/c_thread_pool/blob/master/map.h).
This guarantees that documentation is in line with the code.

### Algorithms

#### game of life

The [game of unlimited life](https://github.com/farhiongit/hashlife). Let cells evolve in an (almost) infinite space for an (almost) infinite time.

The code implements in C language the Hash-life algorithm proposed by R. Gosper in 1984 to explore the evolution of the Conway's Game Of Life.
With a user-friendly programming interface.

#### Aho Corasick

Make the famous Aho Corasick algorithm [easy to use](https://github.com/farhiongit/aho-corasick-1975) for C.

It faithfully and accurately sticks, step by step, to the pseudo-code given in the original (and exquisite) paper of 1975 from Aho and Corasick: "Efficient string matching: An aid to bibliographic search"

But this implementation comes with few enhancements:

- it is generic in the sense that it works for any kind of alphabet of any type and number of signs (and not limited to 256 and not only for `char`) ;
- the list of signs to search for is not statically fixed and can grow dynamically and indefinitely, even while searching for already registered words.

#### Exact cover search with the Knuth's Dancing links algorithm

Make the famous Knuth's Dancing links algorithm [easy to use](https://github.com/farhiongit/dancing-links) for C.

Can be used to solve Sudoku grids for instance.

## My favourite languages

### C

The spirit of C (Rationale for International Standard) brings several advantages :

- Trust the programmer (`malloc` is not dangerous when you write `free` at the same time ; when there is a leak, you know it's you, and you know you can fix it).
- Don’t prevent the programmer from doing what needs to be done (everything can be done with it, and not more : no need to use maps everywhere).
- Keep the language small and simple (it's easy to learn and conceptually kept to the smallest set ; not much to learn).
- Provide only one way to do an operation (it is imperative, and only imperative ; what you learn is not much, and is what you need, not more).
- Make it fast (when it is slow, you know it's you).

That is why C is a great language.

### Korn-shell

Korn-shell is similar to bash (as a predecessor) but it is much faster even though bash brings facilities for interactive shell, as well as more advanced coprocesses exchanging messages.

It's powerful and its awkward syntax is so funny !

## My favourite resources and books

I've read a few IT books. Not that much.

Considering new languages, those struggling to reach the top of the [TIOBE-index](https://www.tiobe.com/tiobe-index/), every thing is on the web rather than in books.

Therefore, I'm more into books that focus on concepts that technical aspects:

- The C language - K&R
- Introduction to Programming Using SML - Hansen, Michael - 1999
- The Annotated Turing - Petzold, Charles - 2008
- Facts and Fallacies of Software Engineering - Glass, Robert L. - 2002
- Smalltalk 80: The Language - Goldberg, Adele and Robson, David - 1989

### OOP

I started to learn object-oriented programming with an early version of [C++ Annotations](http://www.icce.rug.nl/documents/cplusplus/) by Frank B. Brokken.
It is clear and focuses on concepts rather than recipes.

Smalltalk is a purely object-oriented conceptual language. Pharo is a good implementation of a variant of Smalltalk.

### Functional programming

SML and Haskell are purely functional languages. So they are great to learn the concepts (a.k.a "everything is recursive") of functional programming without the burden of more general languages.

### Generic programming

The book "Modern C++ Design: Generic Programming and Design Patterns Applied" by Alexandrescu, Andrei, 2001 is a very good introduction to generic programming.

Haskell also permits generic programming.

### Multi-thread programming

The book "Programming with POSIX Threads" by Butenhof, David R., 1997, explains clearly the concepts and patterns of asynchronous programming with threads.

Multithreading is now integrated in the C standard, as a subset of the POSIX threads.

## My favourite links

- WG14, the international working group for the programming language C.
  https://www.open-std.org/jtc1/sc22/wg14/www/wg14_document_log.htm

Thanks for reading !

-------
*frr*

