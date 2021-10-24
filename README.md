# AME-SRE

Every thing started form the trip to find the authorization code
By reading of "Hacker Disassembling Uncovered by Kris Kaspersky (ed) ISBN:1931769222", I start to discover the code of ame.exp in AME 2.1 for AutoCAD Release 12.

First of all, the required softwares or tools as listed below:
1. Oracle VM VirtualBox with debugger enabled.
1. IDA pro.
1. Hacker's view.
1. Pharlap 386 Dos extender 4.1.

In the Oracle VM VirtualBox, I built a VM with:
  1. DOS 6.22, AutoCAD R12 with AME 2.1;
  1. MASM 6.1;
  1. Hacker's view.;
  1. Pharlap 386 Dos extender 4.1;
  1. Metaware High C 386;

To excute the task of finding authorization code, I have learned or tried:
  1. x86 Assembly language with DOS and BIOS call.
  1. AutoCAD Developement System (ADS) in Metaware High C language.
  1. IDA Pro and FLIRT, FLAIR.
  1. Oracle VM VirtualBox debugger.

Collect the information:
When the Model menu in AutoCAD R12 is triggerred with "Solbox", for example, the authorization code will be checked. User will be asked for a valid authorization code, if it is not authorized yet. Such program flow, in ADS, will call the ads_getstring function. For the AME authorization code found by google search, it is formed by 8 HEX number, "AutoCAD R12 for Windows, S/N: 110-10524473, AME Authorization code: 631CBEB9; AutoCAD R12 for DOS, S/N: 110-10304111, AME Authorization code: 6AA602B0; AutoCAD R12 for DOS, S/N: 117-10058907, AME Authorization code: F258421D; AutoCAD R11 for DOS, S/N: 110-10007686, AME Authorization code: D44151A1". To convert the Hex string to Hex number the function sscanf with format string "%lx" will be called. AutoCAD R12 is 32bit code by using the 386 DOS extender. To debug the AME.exp in VM/DOSBox in DOS environment is very diffcult, due to the 640 KB low memory limit or not a real computer, I am not sure. I tried the dxdebug, 386debug watcom debug and Oracle VM VirtualBox debugger, Oracle VM VirtualBox debugger is the better one can meet the SRE opertion. By IDA pro FLIRT, described below, to located and figure out what's going on when the invalid authorization code is entered. The assembly code for calculate the authorization code is also found. 

Since the calculation of the authorization code is revealed, I try to decompiled it with Ghidra, then write the keygen in C language, failed due to I am not familiar with the asm and C relationship. Then I try to write it in assembly language, assemble and link with Phar lap DOS extender 4.1, and successfully build the keygen executable. In order to build independent executable from run386.exe, I check the R12 acad.exe and discover its composition is "16bitEXE + 32bitEXP". Fortunately, the trial for link my keygen.exp with the 16bitEXE get success.

Before discover the disambled code in IDA pro, it's better to recognize the disambled code function name by FLIRT. And before apply FLIRT, the linked library of AME.exp needs to be prepared by using flair, I found flair 7.0 in the downloaded IDA pro 7.0. In the installed folder of AutoCADR12\ADS\DOCS, there are text files to tell me the ADS, .exp can be done with the MSC, High C, Watcom C, etc. I tried the ADS.lib library file fisrt and fortunately get succeed. And, of course, ADS.lib should be linked with metaware High C.

A live demo of the opertion: [Video](https://youtu.be/256guFYcyAA)

# Hiew - SRE

I install the iDOS 2 in my iPad mini 4. And discovered that Ctrl+F1 was occupied by the Keyboard mapper function which was the 16/32 bit togle hot key in HIEW, therefore, I try to trace the assembly code of Hiew 6.11 to change the Hot key as Shift+F1. 

First of all, the required softwares or tools as listed below:
1. iDOS 2 for iPad or DOSBox in PC.
1. TR by Liu Taotao- I use the version 2.52.
1. Hacker's view HIEW 6.11. Version 6.50, 6.86 are also traced and change the Hot key as Shift+F1.

The procedure is:

  1. Check if the file was packed: Yes, packed by Pklite Pro, which will be unextractable.
  1. Due to the file is unextractable, there would be no automatic unpacker, use TR to manually unpack, see the live demo below for detail.
  1. Use TR to trace the OP code to find the very instruction control the hot key.
  1. From the trial, the break point can be set after the keyboard interrupt int 21h ah=08.
  1. The int 21h will be called two times for each hot key pressed, therefore set new break point in the next instruction of int 21h: "bp 9b1 al>53" for example.
  1. When Ctrl+F1/Shift+F1 pressed Hiew breaked at 9b1, trace until the jump table. 
  1. Find the loaction of the jmp destination adress, change it to the address of Ctrl+F1.

A live demo of the opertion: [Video](https://youtu.be/256guFYcyAA)


# Ture Basic Free - SRE

I learned the Ture Basic 2.01 in Taichung First Senior High School. During these years, I try to collect the Ture Basic interpreter for DOS  from internet. They are 1.0, 2.0, 2.01, 3.05, 3.05b.
The version 3.05b was locked with a nag message for everytime execution and for the code lines more than 250 lines. Althrough I have the unlock version 3.05, I still would like to crack it for free from nag message and unlimited code lines.

The required softwares or tools as listed below:
1. iDOS 2 for iPad or DOSBox in PC.
1. TR by Liu Taotao- I use the version 2.52.
1. Hacker's view HIEW.
1. IDA Pro.

For the nag message for everytime execution, use TR to trace and IDA pro to change the function name meaningful/readable. Then try to think about how to change the opcode to by pass the nag message. Due the call ax, jump table everywhere in the exe file, it is very hard to understand the program flow, I thought the exe file was intention to obfuscated, fianlly, I decide to change the opcode, which will receive a Enter key, for one time execution and then recover it to by pass a Enter key press of the nag message.
For the unlimited code lines, I use the TR LOGS technique to recored the execution CS:IP flow after the SAVE command. First I make a 250 lines code to save and get a successful execution CS:IP flow. Second I add one more line, 251 lines in total, to save and get a fail execution CS:IP flow. Thrid, I compare those two LOGS file, then discovered there is a number "FA 00" saved in the exe file which will limit the code lines. Fourth, change the "FA 00" to "FF 7F" to get 32767 lines to unlocked the 250 code lines limitation.

A live demo of the opertion: [Video](https://youtu.be/256guFYcyAA)

