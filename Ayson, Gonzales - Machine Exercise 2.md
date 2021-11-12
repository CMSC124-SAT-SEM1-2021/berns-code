## Details
  Machine Exercise 2 - Lexer Function that returns the lexemes and their respective tokens from a text file. (Max - 9 characters per lexeme)
  
  Made by Lean Ayson and Bernard Gonzales
  
  Coded using C++

## Limitations
  The function was implemented provided that there will be three global variables declared. These are:
  
    - int index (default value 0);
    
    - char getC (default value '\0'); and
    
    - char lexarray[10] (default value all characters in the array is equal to '\0').
  
  Additionally, the library of `iostream` is needed.

## Code
```
#include <iostream>

using namespace std;

//declaration of global variables needed (limitations)
char getC = '\0';
char lexarray[] = {'\0', '\0', '\0', '\0', '\0', '\0', '\0', '\0', '\0', '\0'};
int index = 0;

//declaration of needed functions
int getChar(FILE* fp);
   void addChar();					//function to add characters to the lexeme array
   void lex();						//lexer function
   void printArray(string);		//function to print the lexeme array and reset it along with int index
string lookup();				//lookup for 'unknown' characters

//getChar()
int getChar(FILE* fp){
   getC = getc(fp);			//read a character
   if(getC != EOF){			//if not end of file
      if(isalpha(getC))		//then if character is a letter
         return 0;    
      else if(isdigit(getC))	//else if character is a digit
         return 1;
      else					//if character is 'unknown'
         return 2;
   }
   else						//end of file is reached
   return -1;
}

int main(){
   lex();						//call lex() function
}

void lex(){
   bool tuloy = true;			//declare boolean function whether to continue checking the next characters or not
   FILE *fp;					//file reader
   fp = fopen("input.txt", "r");//open the file
   if(fp == NULL)
      perror("Error opening file");
   else {
      cout << "LEXEME\t\tTOKEN\n---------------------------\n";//header
      while(tuloy){
         switch(getChar(fp)){
            case 0:									//if character is a letter
               if(index == 0){							//check if lexeme array is empty 
                  addChar();							//add character
                  break;
               }
               else if(isdigit(lexarray[0]))			//check if first character is a number
                  printArray("INT_LITERAL");
               if(index < 9)							//if lexeme array is full
                  addChar();
               break;
            case 1:									//if character is a number
               if(index < 9)							//if lexeme array is full
               addChar();
               break;
            case 2:									//if character is 'unknown'
               if(index != 0){							//if array is not empty then print lexeme
                  if(isdigit(lexarray[0]))			//check if first character is a number
                     printArray("INT_LITERAL");
                  else
                     printArray("IDENTIFIER");
               }
               if(lookup() == "INVALID"){         //if the 'unknown' character is invalid then stop reading the file
                  tuloy = false;
               break;
               }
               if(lookup() != "WHITESPACE"){			//if the 'unknown' character is not a whitespace
                  addChar();
                  printArray(lookup());
               }
               break;         //if the 'unknown' character is a whitespace then skip
            default:         //if end of file is reached then stop reading the file
               tuloy = false;
               break;
          }
      }
   }
   fclose(fp);					//close the text file
}

void addChar(){
   lexarray[index++] = getC;	//add character to the array
}


string lookup(){				//return lookup token for 'unknown' character
   switch(getC){
      case '+':
         return "ADD_OP";
      case '-':
         return "SUB_OP";
      case '*':
         return "MUL_OP";
      case '/':
         return "DIV_OP";
      case ',':
         return "SEP_OP";
      case '=':
         return "ASSIGN_OP";
      case ' ':				//whitespaces
      case '\t':
      case '\n':
      case '\v':
      case '\f':
      case '\r':
         return "WHITESPACE";
      default:				//invalid / foreign character
         return "INVALID";
   }
}

void printArray(string token){
   if(index < 8)
      cout << lexarray << "\t\t" << token << "\n";	//print the lexeme array and respective token
   else
      cout << lexarray << "\t" << token << "\n";		//extra for 'aligned' output 
   for(int x = 0; x < 10; x++){					//clear the lexeme array
      lexarray[x] = '\0';
   }
   index = 0;										//reset the index variable
}
```

## Sample Run
  When tried with this content of "input.txt":
```
v4r 12j+ej	-F*W/c=2,
3 HElo AWEFwe13c2e23e2c 12345 123456 1234567 12345678:3
```
  The output shows as
  
  ![ME2 Output](https://user-images.githubusercontent.com/90940695/141534298-50579fbe-3918-4d91-bc55-c37776939f74.PNG)
