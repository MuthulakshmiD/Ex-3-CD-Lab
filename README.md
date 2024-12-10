# Ex-3-RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
# Date:
# AIM
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.
# PROGRAM
# EXEC.L
```
%{
#include "y.tab.h"
%}

%%

"=" { printf("\n Operator is EQUAL"); return '='; }
"+" { printf("\n Operator is PLUS"); return PLUS; }
"-" { printf("\n Operator is MINUS"); return MINUS; }
"/" { printf("\n Operator is DIVISION"); return DIVISION; }
"*" { printf("\n Operator is MULTIPLICATION"); return MULTIPLICATION; }
[a-zA-Z]*[0-9]* { printf("\n Identifier is %s", yytext); return ID; }
. { return yytext[0]; }
\n { return 0; }

%%

int yywrap() { return 1;
}
```
# EXEC.Y
```
%{
#include <stdio.h>
int yylex(void);
void yyerror(const char *s);
%}

%token ID PLUS MINUS MULTIPLICATION DIVISION

%%
statement: ID '=' expression { printf("\nValid arithmetic expression\n"); }
;

expression: expression PLUS ID
          | expression MINUS ID
          | expression MULTIPLICATION ID
          | expression DIVISION ID
          | ID
;
%%

int main() {
    printf("Enter input: ");
    yyparse();
    return 0;
}

```
# COMMAND:
```
lex exec.l 
yacc -d exec.y
gcc lex.yy.c y.tab.c -o parser
./parser
```
# OUTPUT
![image](https://github.com/user-attachments/assets/9f45f49f-17dd-432a-869c-ec4b3e0e9ff1)

# RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
