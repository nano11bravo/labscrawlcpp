#labscrawl-cpp

##Dependencies
labscrawl-cpp is dependent on **Boost 1.53 or above**. It requires access to the libraries:
* boost asio
* boost filesystem
* boost regex
* boost thread
* boost program_options
* boost system

labscrawl-cpp was originally written/compiled on Ubuntu 12/Slackware 14 with g++-4.8.1 installed. It was written using VIM. I used GNU make to automate my builds. Later, I change it to compile on Windows using MSVC14 (Visual C++ 14 with Visual Studio 15 Community Edition). Builds were performed using Boost.Build. I switched to using Visual Studio Code with the C/C++ extension package.

##Usage
You can build the software by opening the `Jamroot` file and changing the `<include>`/`<library-path>` values to point to your boost folder. Make sure the main boost directory is on your PATH; typing `b2` will compile the code and place an executable in the `bin\` directory.

The following should be able to run the spider:
    
    ./labscrawl [options] --url=<url> --directory=<directory>

If you have any issues, you might need to change your `LD_LIBRARY_PATH` to point to your GCC lib/ path and Boost's /lib path.

## Purpose
The hope is that, given a URL, the code will eventually extract additional URLs from the resultant HTML. From those URLs, more pages will be extracted. This process should continue until all unique URLs are visited (this could take a while). Additionally, URLs referring to certain types of resources (movies, images, etc.) will be downloaded to a local file.

## Possible Extensions
These are tasks that could be interesting:

* Handle HTTPS.
* Create NCurses interface with progress bars.
* Create a GUI with progress bars.
* Allow rendering and parsing JavaScript-driven pages.
* URL pattern detection for "guessing" unlinked resources.
* robots.txt support
* persistent database for long-term caching
 
## Motivation
When I tell people I wrote a multi-theaded web spider in C++, they usually just stare at me blankly for a moment and then ask me, "...why?". I tell them I wanted to write a semi-realistic C++ application that did a little more than just process files or write to the console. Anybody could write this app in Python or C# in a day or two; where's the challenge there?

It's amazing that you can go through an entire 4-year, decent college program and almost never hit a database or the Internet. That said, I worked miracles in C++ when I was in college and I'm a little more than "familiar" with the language and STL. But *really* knowing a language means knowing the tools, conventions and processes involved in getting working software out the door and I lack that. The aim of this project, therefore, is to familiarize myself with said tools, conventions and processes.

When I started this project, C++11 was *mostly* adopted and still had to be turned on with compiler flags. I really wanted to get to know all the new latest language features and libraries, so add that to the checklist. I have aspirations to someday learn some basic QT or OpenGL code and this application will act as a good starting point.

## What I've Learned So Far
Already, I have learned a lot about writing realistic C++ applications. It has made me more appreciative of how hard it can be to write large scale software in such a low-level language. Amongst the things I have learned, here is a short list:

* make files are a lot of work.
* separate compilation allows pushing off linking until the last second.
* Boost's unit testing framework is pretty awesome, but relies on macros (boo!).
* working with Git on the command-line isn't that bad.
* Boost's asio library is a very low-level abstraction of the underlyiung socket libraries.
* argument checking in C++ is annoying and creating custom exceptions is even more annoying.
* it is hard to tell when to return `std::string` vs. `const char *`.
* I find myself reaching for Boost more often than I thought I would.
* having implementation (.cpp) in a separate file than the declaration (.hpp) takes longer and requires more memorization.
* almost never use `using namespace xyz;` (using directive); limit yourself to using declarations within functions.
* template members must be implemented in the header files (since export doesn't work).
* inline functions must be implemented in the header files, too.
* prefer taking a templated destination iterator over a collection to populate.
* always check whether a constructor takes a value or a reference type.
* when you can't figure out the cause of a segmentation fault, use gdb.
* the `iostream` library is extremely powerful and flexible at the same time.
* `fstream` only accepts `char *` for file names (accepts strings in C++11).
* `fstream` doesn't recognize `~` and other special path indicators. No exceptions thrown.
* prior to C++ 11, default function template arguments weren't allowed.
* template member functions lead to ugly syntax, in many cases.
* Boost and C++11's `function` template simplifies working with threads.
* C++11's regex doesn't support named capture groups.
* C++11's `bind` can't easily be negated. Boost's `bind` could be proceeded by `!`. Use lambdas.
* inheriting from types in the `<functional>` header is painful. Use `ptr_fun`, etc. when possible.
* because `std::exception`\`s `what` method returns `char const *`, returning the results of `c_str` on a locally built error string is a bug. The message must be built within the ctor.
* there may be some value in creating simple wrapper classes around primitive types to make sure they are given the same treatment as user-defined types within ctors.
* Boost's `bind` function can save from creating lots of little functor classes.
* Polymorphism can rarely be used with references; pointers work more naturally.
* There's not a convenient formatting for ctors with lots of parameters or long initializer lists.
* Don't pass variables to a lambda by reference when it will be running in a separate thread!
* C++11 threads call `terminate` when deconstructed, unless joined or detached.
* an editor that lets you have the .hpp and .cpp files open side-by-side is useful.
* make files are composed of specific commands, making it unfriendly for multiple platforms.
* I switched to Boost.Build which hides platform-/compiler-specific details and is a lot less typing.
* boost has `sync_queue` and `sync_priority_queue` - boost needs a better way to advertise what it can do.
* apparently `DELETE` causes compile issues in MSVC (probably a non-standard MACRO).
