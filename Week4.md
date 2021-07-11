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




