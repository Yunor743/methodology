
**Hiding a process** has always being challenging for malware writers, and they found many ways to do so. The tip I’ll talk about is very basic, yet simple to write, but doesn’t work all the time. **This trick is known under the name “RunPE”** and has been used many time in malware industry, **especially in RATs** (Remote Administration Tools).

Basically, when a malware starts, it will **pick a victim** among the Windows processes (like explorer.exe) and **start a new instance** of it, in a **suspended state**. In that state it’s safe to modify and the malware will totally **clear it from its code**, extend the memory if needed, and **copy its own code inside**.

Then, the malware will do some magic to **adjust the address of entry point** as well as the base address and will **resume the process**.  
After being resumed, **the process shows being started from a file (explorer.exe) that has nothing to do anymore with what it actually does**.

> source : https://www.adlice.com/runpe-hide-code-behind-legit-process/

---

In order to create your own crypter you have to know some  
things: Crypters first functionality is to encrypt files to bypass Av's  
so if your Stub is detected by av's as a threat, your crypter won't be  
a “crypter” anymore because it will be detected.

> source : https://www.docdroid.net/GrvkCtu/make-your-fud-crypter-pdf#page=7

Some usefull RunPE
- [RunPE](https://github.com/Zer0Mem0ry/RunPE/blob/master/RunPE.cpp)

Open source crypter:
- [PE-Union](https://github.com/bytecode77/pe-union)
- [Lime-Crypter](https://github.com/NYAN-x-CAT/Lime-Crypter)
- [RustPacker](https://github.com/Nariod/RustPacker)

PE-Infection : http://www.rohitab.com/discuss/topic/41466-add-a-new-pe-section-code-inside-of-it/

Courses:
- https://fasterthanli.me/series/making-our-own-executable-packer

sources:
- https://www.hackingloops.com/crypters-tutorial-for-hackers-by-hackingloops/
- https://security.stackexchange.com/questions/42289/what-is-a-stub
- https://www.youtube.com/watch?v=TgYb3hwOAV4

More reading / TODO:
- https://www.reddit.com/r/rust/comments/15f4ijz/deleted_by_user/
- https://www.synercomm.com/blog/executing-shellcode-with-rust-aes-256-and-a-gnome-photo/
- https://xen0vas.github.io/antivirus-evasion-kaspersky-endpoint-security-bypass-using-a-fully-undetectable-cryptor/#
- https://github.com/n4sm/AD_1DA
- https://www.youtube.com/watch?v=hB5IYjEVgwE
- https://www.hackingloops.com/crypters-tutorial-for-hackers-by-hackingloops/
- https://www.youtube.com/watch?v=TgYb3hwOAV4&t=1s