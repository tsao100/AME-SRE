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
  1. The int 21h will be called two times for each hot key pressed, therefore set new break point in the next instruction of int 21h: bp 9b1 al>53.
  1. When Ctrl+F1/Shift+F1 pressed Hiew breaked at 9b1, trace until the jump table. 
  1. Find the loaction of the jmp destination adress, change it to the adress of Ctrl+F1.

A live demo of the opertion: [Video](https://youtu.be/256guFYcyAA)


# Ture Basic Free - SRE

I learned the Ture Basic 2.01 in Taichung First Senior High School. During these years, I try to collect the Ture Basic interpreter for DOS  from internet. They are 1.0, 2.0, 2.01, 3.05, 3.05b.
The version 3.05b was locked with a nag message for everytime execution and for the code lines more than 250 lines. Althrough I have the unlock version 3.05, I still would like to crack it for free from nag message and unlimited code lines.

The required softwares or tools as listed below:
1. iDOS 2 for iPad or DOSBox in PC.
1. TR by Liu Taotao- I use the version 2.52.
1. Hacker's view HIEW.

For the nag message for everytime execution, use TR to tracea and IDA pro the change the function name meaningful/readable. Then try to think about how to change the opcode to by pass the nag message. Due the call ax, jump table everywhere in the exe file, it is very hard to understand the program flow, I doubt the exe file was intention to obfuscated, fianlly, I decide to change the opcode for one time execute and then recover it to by pass a key press of nag message.

A live demo of the opertion: [Video](https://youtu.be/256guFYcyAA)

