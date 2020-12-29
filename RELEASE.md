# Release note for Alpha Two

The purpose of the Alpha Two is to fix the stability of the network in internal mode. (See [Purpose of the Alpha Network](Purpose_of_the_Alpha_network.md).

The release contains the same functionality as the Alpha One release, except that The Alpha Two is now more stable then Alpha One and the debugging capabilities has been improved. Three bugs have been fixed.

 

1. The project has been split into a number of submodules which enables improved release process and test flow and quality control.

2. The LoggerService system has been improved which enables easier debugger and tracing of such as assert and exception handling.

   Both the Error and Exception handling is now tagged with the task-name and which makes it possible to for the task owner to take action or just to bailout and stop the program.

3. In the case of a segmentation fault the core program (tagionwave) now dumps the calls stack (backtrace) into a file.

4. A new tool has been added (callstack) which enables to printout the callstack-file in a human readable format.  

5. Bugfixes: Least used algorithm and more bugs in scrapping of Events, Rounds and Witness has now been fixed. 
