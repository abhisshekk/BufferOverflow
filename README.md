# BufferOverflow

### Section 3.4 - Running file a32.out and a64.out.
After running the makefile we get two binary files i.e., a32.out and a64.out.
After running the 2 binary files we get following output as shown in the snippet:

![image](https://user-images.githubusercontent.com/40964627/168496660-6259df45-4b81-49be-bb37-3b2fc7faf5b9.png)


### Section 4 - Stack.c working:
The stack.c is a C program that has a main function that reads 517 bytes from a file named ‘badfile’. It then copies the bytes read to a buffer of size 100. Here we observe that there is a problem of buffer overflow. 
To solve this problem, we need to put our code in the memory of the running program. So, we put our code in the ‘badfile’.
Now when the program reads the file, the code is placed in the str[] array. Now when the program copies str array to the target buffer our code gets stored in the stack. 
Now we need to make the program go to our code in the memory. So, using the buffer overflow we can override the return address field in the code. And when the function bof returns, it will directly go to the address where our code is.

### Section 5.1 - Using the following command as mentioned in snippet we can calculate the distance between buffer State address and location of the stored return address.

![image](https://user-images.githubusercontent.com/40964627/168496673-0cbaa304-47e3-4a78-9c5c-b97942b92492.png)

### Section 5.2 - Contents of exploit.py after modification is as follows:

![image](https://user-images.githubusercontent.com/40964627/168496684-1418e078-6363-4cea-a878-d4c756e39d61.png)

### Section 5.2 - Values for exploit.py were decided according to following observation:
Since shellcode needs to be there in the payload, I decided to put the start value and return value as follows:
Start = 517 – len(shellcode)
Ret = 0xffffcb78 + 220, because there might be some additional data pushed into the stack.
According to gdb result, the offset is set to 112 as the return address field starts from 112.


### Section 5.2 - Successful attack is performed as shown in following snippet.

![image](https://user-images.githubusercontent.com/40964627/168496704-f29c315b-e849-483b-af4a-9d277c84ccb0.png)

