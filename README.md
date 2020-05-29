# DLL-Hijacking
DLL Hijacking
DLL Hijacking is a way for attackers to execute unexpected code on your machine. It means if an attacker tricks you into getting a file on your system (by social engineering, etc.)  that file could be executed when the user runs an application that is vulnerable to DLL Hijacking. To understand how it works, you must first understand two important concepts:
1.	What is a DLL
2.	What is the PATH variable in Windows?

What is a DLL?

Dynamic Link Libraries (DLL)s are like EXEs but they are not directly executable. They are like .so files in Linux/Unix. DLLs are MS's implementation of shared libraries. 
DLLs are so much like an EXE that the file format itself is the same. Both EXE and DLLs are based on the Portable Executable (PE) file format. DLLs can also contain COM components and .NET libraries.
What is the PATH variable in Windows?
Windows has something called ‘Environment Variables’. These are crucial paths and values that point the OS to important locations when there is a need to access essential information about the system. A subset of Environment Variables is the Path variable which points the system to EXE files. Adding a path to an EXE file allows users to access it from anywhere without having to switch to the actual directory.

Part ONE: To find a dll hijacking vulnerable application and analysis the optimal dll.
In my project I have use VLC media player to target the WININET.dll that is called by the VLC media player whenever it I executed. As you can see in the below figure the WININET.dll is first searched in the current working folder where it is not found.
![Image of procmon](https://github.com/AmanNegi144/DLL-Hijacking/blob/master/Images/procmon.png)
So, if we somehow place our malicious .dll file in this folder we can execute our file.

Part TWO: Using appropriate method to tricking user to create the malicious .dll file in the VLC default folder
I have chosen macro malware that is embedded inside a .doc file. As people are less cautious before opening a doc file.
I have hidden the hex code of the malicious dll in the comment section of the doc file.


![Image of hidden code](https://github.com/AmanNegi144/DLL-Hijacking/blob/master/Images/Hexcode_in_comments.png)


As you can see in the above figure the hidden code, its size is 5 KB.
The conversion of above hex code into a .dll file is done by the macro code shown below
 
It takes each byte of hex code in the comment section and write it into a file Name WININET.dll.
The malicious file on execution only open a calc.exe file to show the proof of concept.

PART THREE: Execution of the malware
On clicking the doc file, the WININET.dll file is created in the VLC directory. Check out the last file in the  figure.


![Image of dll generation](https://github.com/AmanNegi144/DLL-Hijacking/blob/master/Images/DLL_generation.png)
 
On execution of the VLC media player,both vlc media player and cacl.exe are executed.
![Image of calc execution](https://github.com/AmanNegi144/DLL-Hijacking/blob/master/Images/Execution_of_Calc.png)
