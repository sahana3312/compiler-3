# compiler-3
# Ex. No : 3	
# RECOGNITION OF A VALID ARITHMETIC EXPRESSION THAT USES
## Register Number :212225040356
## Date :05.09.26 

## AIM   
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.

## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.

## PROGRAM

### arth.l
```


%{
#include <stdio.h>
#include "y.tab.h"
%}

%%

"="                     { printf("\n Operator is EQUAL"); return '='; }
"+"                     { printf("\n Operator is PLUS"); return PLUS; }
"-"                     { printf("\n Operator is MINUS"); return MINUS; }
"*"                     { printf("\n Operator is MULTIPLICATION"); return MULTIPLICATION; }
"/"                     { printf("\n Operator is DIVISION"); return DIVISION; }
"("                     { printf("\n Parenthesis is OPEN"); return '('; }
")"                     { printf("\n Parenthesis is CLOSE"); return ')'; }
[a-zA-Z][a-zA-Z0-9]*    { printf("\n Identifier is %s", yytext); return ID; }
[0-9]+                  { printf("\n Number is %s", yytext); return NUMBER; }
[ \t]                   { /* ignore whitespace */ }
\n                      { return 0; }
.                       { return yytext[0]; }

%%

int yywrap() {
    return 1;
}
```
### arth.y
```
%{
#include <stdio.h>
#include <stdlib.h>

int yylex(void);
void yyerror(const char *s);
%}

%token ID NUMBER
%token PLUS MINUS MULTIPLICATION DIVISION

%left PLUS MINUS
%left MULTIPLICATION DIVISION

%%

statement: ID '=' E {
    printf("\n\nValid arithmetic expression\n");
    return 0;
}
;

E: E PLUS E
 | E MINUS E
 | E MULTIPLICATION E
 | E DIVISION E
 | '(' E ')'
 | ID
 | NUMBER
 ;

%%

void yyerror(const char *s) {
    printf("\n\nInvalid arithmetic expression\n");
}

int main() {
    printf("Enter an arithmetic expression: ");
    yyparse();
    return 0;
}

```

## OUTPUT 
<img width="1337" height="517" alt="image" src="https://github.com/user-attachments/assets/65d9b3a5-2563-46bc-8414-03043149f04d" />


## RESULT
 YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
