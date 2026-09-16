# Ex-3-RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC

# Date: 10-08-2026

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
```
expcd3.l
%{
#include "exp3cd.tab.h"
#include <stdio.h>
%}

%%

[0-9]+                  { return NUMBER; }
[a-zA-Z][a-zA-Z0-9]*    { return ID; }

"+"     { return '+'; }
"-"     { return '-'; }
"*"     { return '*'; }
"/"     { return '/'; }
"("     { return '('; }
")"     { return ')'; }

[ \t]   ;          /* ignore spaces */
\n      return 0;

.       return yytext[0];

%%

int yywrap()
{
    return 1;
}

expcd3.y
%{
#include <stdio.h>
#include <stdlib.h>

int yylex();
void yyerror(const char *s);

int valid = 1;
%}

%token NUMBER ID

%%

statement:
        expr
        {
            if(valid)
                printf("\nValid Arithmetic Expression\n");
        }
        ;

expr:
        expr '+' term
      | expr '-' term
      | term
      ;

term:
        term '*' factor
      | term '/' factor
      | factor
      ;

factor:
        '(' expr ')'
      | NUMBER
      | ID
      ;

%%

int main() {
    printf("Enter Expression:\n");
    
    if (yyparse() == 0) {
        printf("Valid Arithmetic Expression\n");
    }
    return 0;
}

void yyerror(char *s) {
    printf("Invalid Arithmetic Expression\n");
}
```

# OUTPUT

<img width="1484" height="1060" alt="image" src="https://github.com/user-attachments/assets/b1306b0e-b0e0-4eb1-ab45-4515947c8129" />


# RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
