# Week4: Memory

## 1. Hexadecimal
- Hexadecimal Values: 0 1 2 3 4 5 6 7 8 9 A B C D E F

  ie. 14 = 0E = 0 * 16^1 + 15*16^0
      10 = 16 = 1 * 16^1 + 0*16^0
      255 = FF = 16 * 16^1 + 16*16^0
 - Why do we use hexadecimal in computer science?

    255 (decimal) = FF (hexadecimal) = 1111 1111 (bynary)
    1 hexadecimal = 4 binary digits (0 or 1) 4x4 possibilities
  
  - To warn you are using an Hexadecimal number and not a decimal number use: **0x**
    
    For example the color code used for RGB
    Black, the absense of all colors is = #000000
    While white is #FFFFFF
    
## 2. Address
Print the address of a variable in hexadecimal

    int n = 50;
    printf("%p\n", &n);

Now this will return the contents of the address (this case 50)

    int n = 50;
    printf("%i\n", *&n);

## 3. Pointers
Declaring a pointer:

    int n = 50;
    int *p = &n;
    printf("%p\n", p);

Returning its value:

    int n = 50;
    int *p = &n;
    printf("%i\n", *p);

Pointers take 8 bytes of Memory and they store adresses (point to there)

## 5. Strings
    > string s = "Hi!";

s[0] = 'H' -&-> 0x123 

s[1] = 'I' -&-> 0x124

s[2] = '!' -&-> 0x125 

s[3] = '\0'-&-> 0x126 

They are stored continuously one byte apart because every char takes one byte.

&s = 0x123 (the address of s is on the first char)

<img src="https://user-images.githubusercontent.com/43222644/125205721-15773500-e25a-11eb-9372-d8e2d1bf3300.png" alt="drawing" width="200"/>

- Strings do not exist as a DataType in C. Instead, we can use char *s that is a pointer that points to a char address

      char *s = "Hi!";
      printf("%c\", *s);
      printf("%c\", *(s+1)); /pointer arithmetic

It will print H I (adds a byte)

Up until now CS50 have been using string as a datatype because it has definef in a typedef:
> typedef char *string;

## 6. Malloc
How to copy a string?

    #include <stdio.h>
    #include <stdlib.h> //where malloc is
    
    int main(void)
    {
       char *s = "Hi!";
       char *t = malloc(strlen(s) + 1); /add 1 to store the ending null /0
       for (int i = 0; n = strlen(s); i<=n; i++)
        {
          t[i] = s[i]
        }

        return;
        
     }
     
NULL != '\0'
NULL is for pointers (Null pointer, the absense of an address)
'\0' is for characters

    strcpy(t,s); // (copies the string (destination, origin))
    
If you use malloc you have the onus to desalocate the memory

    free(t);

## 7. Valgrind
It is a code that can be used to detect errors in the memory (if you touch memory that shouldn't)

Example of a code that has an error on allocating 3 bytes instead 4 for the string:
<img src="https://user-images.githubusercontent.com/43222644/125373652-e9dc7380-e35b-11eb-9006-f2a4ce2d4926.png" alt="drawing" width="200"/>

    valgrind ./program.c
    
Line 10 is invalid write bc you touched a part of memory that wasnt allocated:
![image](https://user-images.githubusercontent.com/43222644/125373959-64a58e80-e35c-11eb-8764-489fbc1a89b3.png)
Line 11 is invalid read bc you ask to printout a string that contains a memory problem
![image](https://user-images.githubusercontent.com/43222644/125374021-81da5d00-e35c-11eb-8f7c-3f18a2d804cd.png)
Memory Leak because you didn't free the memory
![image](https://user-images.githubusercontent.com/43222644/125374073-9fa7c200-e35c-11eb-921a-e13b634ab3e3.png)

Fixing the code:

<img src="https://user-images.githubusercontent.com/43222644/125374360-396f6f00-e35d-11eb-92a2-32452d804123.png" alt="drawing" width="200"/>

Success!

![image](https://user-images.githubusercontent.com/43222644/125374395-4e4c0280-e35d-11eb-8341-7ebc43c6c863.png)


## 8. Binky (More over pointers)
You should always initalize your pointers. Cause they are pointing to "garbage values" originally.
The reference the ponter points is called **pointee**, to allocate values to thar you dereference ne the pointer,

    int *x;
    int *y;

    x = malloc(sizeof(int));
    x = y; //they will point to the same address
    
    *x = 42;
    *y = 13;
    
## 9. Memory Layout
    Machine Code
    Global Variables
    Heap [malloc]
    Stack [functions]
    
StackOverflow is when you called so many functions that it touches the Heap Memory

## 10. Mario Pyramid Recursive

This will cause a segmentation fault because it starts to stack too many funciont til the heap:
<img src="https://user-images.githubusercontent.com/43222644/125377013-9c173980-e362-11eb-9b0f-ca40dd89172f.png" alt="drawing" width="200"/>

You need to add:

    if(h==0)
    {
      return;
    }
Keep it in mind that recursion has this limit on calling a certain number of functions while loops (iterations) dont.

Another problem is Buffering: Error when you go past the memory allocated for an array or it gets too fast to the end of it.

## 11. Scanf
    int x;
    printf("x: ");
    scanf("%i", &x);
    printf(
    iscanf)
    
 ## 12. Files I/O
 Until now we have been using the memory. When you use files you can save files longterm.
 
    int main(void)
    {
      FILE *file = fopen("phonebook.csv","a"); //FILE is a datatype and "a" means open it on append mode add info row by row
      if (file == NULL)
      {
        return 1;
      }
      
     char = *name = get_string = ("Name: ");
     char = *number = get_string = ("Number: ");
     
     fprintf(file, "%s, %s\n", name, number);
     fclose(file);
    }
    
Copy files Program
        
    #include <stdint.h>
    #include <stdio.h>
    #include <stdlib.h>

    typedef uint8_t BYTE;

    int main(int argc, char *argv[])
    {
    // Ensure proper usage
    if (argc != 3)
    {
        fprintf(stderr, "Usage: copy SOURCE DESTINATION\n");
        return 1;
    }

    // open input file
    FILE *source = fopen(argv[1], "r");
    if (source == NULL)
    {
        printf("Could not open %s.\n", argv[1]);
        return 1;
    }

    // Open output file
    FILE *destination = fopen(argv[2], "w");
    if (destination == NULL)
    {
        fclose(source);
        printf("Could not create %s.\n", argv[2]);
        return 1;
    }

    // Copy source to destination, one BYTE at a time
    BYTE buffer;
    while (fread(&buffer, sizeof(BYTE), 1, source))
    {
        fwrite(&buffer, sizeof(BYTE), 1, destination);
    }

    // Close files
    fclose(source);
    fclose(destination);
    return 0;
    }

## 13. Typedef

    typedef char* string;
    typedef unsigned char byte;
    typedef struct car
    {
      int year;
      make char[10];
      plate char[7];
      color char[10];
    }
    car_t;
    
    int main(void)
    {
      struct car my_car;
      car_t my_car;
    }
