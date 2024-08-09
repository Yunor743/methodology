
### SHELLCODE INJECTION
Shellcode injection is the most basic in-memory technique and has also been around the longest.
### REFLECTIVE DLL INJECTION
Attackers benefit from the ability to code in higher level languages like C/C++ instead of assembly.==
Classic reflective DLL injection, such as that used by Meterpreter, is easy for hunters to find. It leaves large RWX memory sections in the process, even when the meterpreter session is closed
### MEMORY MODULE
[Memory module](https://github.com/fancycode/MemoryModule) is another memory resident attacker technique. It is similar to Reflective DLL injection except the injector or loader is responsible for mapping the target DLL into memory instead of the DLL mapping itself. Essentially, the memory module loader re-implements the LoadLibrary function==, ==but it works on a buffer in memory instead of a file on disk.
### PROCESS HOLLOWING
### MODULE OVERWRITING
### GARGOYLE
[Gargoyle](https://jlospinoso.github.io/security/assembly/c/cpp/developing/software/2017/03/04/gargoyle-memory-analysis-evasion.html) is a proof of concept technique for memory resident malware that can evade detection from many security products. It accomplishes this feat by laying dormant with read-only page protections. It then periodically wakes up, using an asynchronous procedure call, and executes a ROP chain to mark its payload as executable before jumping to it. After the payload finishes executing, Gargoyle again masks its page permissions and goes back to sleep.
### SUSPENDED-THREAD-INJECTION
https://github.com/plackyhacker/Suspended-Thread-Injection
### Code Cave
- https://en.wikipedia.org/wiki/Code_cave
- https://stackoverflow.com/questions/787100/what-is-a-code-cave-and-is-there-any-legitimate-use-for-one
- https://www.youtube.com/watch?v=uvNq2r9U0uI
- https://www.youtube.com/watch?v=0NwlWaT9NEY
- https://unprotect.it/technique/code-cave/


---

sources:
- https://www.elastic.co/security-labs/hunting-memory