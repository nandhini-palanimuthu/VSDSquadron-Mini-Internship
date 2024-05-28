# VSDSquadron-Mini-Internship
TASK1

 Install RISC-V toolchain and the installation is done.

Then the task was to complile the c program which calculates the sum from 1 to n.For this the command to open is "gedit sum1ton.c".
And after the code is written for sum of integers we need to compile it and the following commands were used to accomplish the same.After the compilation the sum value will be printed as shown below.The command to display the output is "./a.out".

![WhatsApp Image 2024-05-28 at 7 20 56 PM](https://github.com/nandhini-palanimuthu/VSDSquadron-Mini-Internship/assets/170846569/32c13486-2811-4d56-86c3-d7f7414742a8)

Then compile the same code with RISC-V compiler. For that we need to open the code in terminal itself.Command to open is "cat sum1ton.c".
After that the following command is used to create .o file as shown below.

![WhatsApp Image 2024-05-28 at 7 20 26 PM](https://github.com/nandhini-palanimuthu/VSDSquadron-Mini-Internship/assets/170846569/9ac9502c-0e2b-4956-94ec-e4ff7e819274)

Then to open the assembly level instructions for the above written c code we use the following command

In this code lets search for the "main".

if we subtract 101b0-10184 it is 11 so there are 11 instructions in this above assembly code in the "main".

To reduce the number of instructions we add"|less" along with the above command which generates less assembly code instructions in this we are mainly concerned about main so to search we use "/main" and this is how it looks.

![WhatsApp Image 2024-05-28 at 7 19 55 PM](https://github.com/nandhini-palanimuthu/VSDSquadron-Mini-Internship/assets/170846569/e9e4471b-f893-4089-806b-67b626ef4b77)
The number of instructions hasn't changed because it was a simple program.
