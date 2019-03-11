# SIGNAL language translator
University project for translation from subset of grammar of SIGNAL language to Assembly language.         
  
## Grammar
```
<signal-program> --> <program>
<program> --> PROGRAM <procedure-identifier> ; 
              <block>.
<block> --> <variable-declarations> 
            BEGIN 
              <statements-list> 
            END
<variable-declarations> --> VAR <declarations-list> | <empty>
<declarations-list> --> <declaration> <declarations-list> | <empty>
<declaration> --> <variable-identifier>:<attribute> ;
<attribute> --> INTEGER | FLOAT
<statements-list> --> <statement> <statements-list> | <empty>
<statement> --> WHILE <conditional-expression> DO 
                  <statements-list> 
                ENDWHILE ;
<conditional-expression> --> <expression><comparison-operator> <expression>
<comparison-operator> --> < | <= | = | <> | >= | >
<expression> --> <variable-identifier> | <unsigned-integer>
<variable-identifier> --> <identifier>
<procedure-identifier> --> <identifier>
<identifier> --> <letter><string>
<string> --> <letter><string> | <digit><string> | <empty>
<unsigned-integer> --> <digit><digits-string>
<digits-string> --> <digit><digits-string> | <empty>
<digit> --> 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
<letter> --> A | B | C | D | ... | Z
```

## Results
Input .sig file:
```
program tt1;

var v1: float;
    v2: integer;

begin
    while v1 = 42 do
    	(*nop*)
    endwhile;
end.
```

Output .asm file:
```assembly
TT1 SEGMENT
    V1  Dw ?, ?
    V2  DW ?

?loop0:
    MOV	AX, V1
    MOV	BX, 42
    CMP	AX, BX
    JNE	?loop0_end
    NOP
    JMP	?loop0
?loop0_end:
TT1 ENDS
```
