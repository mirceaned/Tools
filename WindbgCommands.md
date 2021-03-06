```
Init

Install sosex (32 and 64 versions) and psscor4 (32 and 64 versions). 
It's a matter of copying the dlls in the 32 and 64 bits versions of the debugging tools.
.loadby sos clr # load sos, starting .Net 4.0
.load sosex # load sosex extension
.load psscor4 # load psscor extension (starting .Net 4.0)
.chain # display loaded modules
.reload /f  # force reload for all symbols 
.reload /f StatEngineProxy.dll  # reload symbol for specified dll
lm # display the status of loaded symbols
!sym noisy  # troubleshooting symbol loading steps (it shows the path used by windbg when probing for symbols and if a match was found)
lm v clr   # find out which CLR version is currently loaded
.logopen d:\log.txt # saves output to file
.logclose
 
 
Runtime commands

!dlk # report deadlocks (sosex)
!dumpstack # reports managed and unmanaged stack (sos)
!eestack # runs dumpstack on all threads
!threads # display all managed threads (sos)
~<thread id>s # switch to thread
!clrstack -a # display stack, locals and parameters for each method in the stack of the current thread, could be used for investigation with !do 
~* e!clrstack # display managed stack for all the threads 
~0 e!dso # dump stack objects for a thread (e.g. gui thread)
.kframes 0xFFF # increase the number of frames reported while doing kb
kb # displays the unmanaged stack for current thread
~* kb # displays the unmanaged stack for all threads
.dump /ma c:\temp.dmp # create dump file with windbg for later analysis
!analyze -v # finding more info from a crash dump (e.g. stack trace)
!syncblk # display the threads which are holding lock objects
!dso #dump stack object in current thread
!u <IP> # shows IL unassembly with C# code side by side, uses instruction pointer from an exception stack trace
!runaway # shows the cpu usage time for all the threads
.foreach (obj {!dumpheap -type TmpGUILib.TraceText.TextBuffer+LogEntry -short}) {.printf "${obj} %mu %mu\n", c+poi(${obj}+8),c+poi(${obj}+10)} # view latest log messages, useful for cases when we are missing diagnostics
~<finalizer thread>s; !clrstack # inspect finalizer thread in case of hangs when GC collect is in progress


Display data

dd # dump a double word - e.g. an int32 object
!do <address> # displays breakdown of object by fields, can be used recursively 
!da -details <address of array> # dumps array with details about objects
!dumpvc <MethodTable address> <Address> # display data about value types 
!dumpvc <Element MethodTable address> <Address> # display content of dictionaries
!mdt # sosex alternative to !do, provides hyperlinks


Memory usage

!dumpheap -stat # display heap stat, useful for tracking memory leaks, could be used for diffing snapshots (sos)
!dumpheap -type System.Collections.Hashtable+bucket[] # drill down on heap stats for a specific type
!gcroot 0x0000000022149a90 # finds root objects referencing the object at a specified address
!do 000000008153be10 # get info on the object referencing the suspected leaked one (starts from the bottom of the list from the dependency chain)
!heap -s # shows unmanaged heap stats


Exceptions

!pe <exception object> # print exception details
sxe -c "!clrstack; g" clr # break on clr exception and optionally execute command 
sxe -c "kb; g" eh # break on C++ exception and optionally execute command
sxe clr # break on clr exceptions
sxd clr # disable break on clr exceptions
sxe 0xe0434f4d # break on exceptions having the specified code (in this case clr ones)
!dae # display all exceptions (psscor)
```
