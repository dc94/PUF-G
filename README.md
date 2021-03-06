# PUF-G: A CAD Framework for Automated Assessment of Provable Learnability from Formal PUF Representations

The (simplified) syntactical representation (grammar) of the proposed language in our PUF-G framework is described below.

TOP::               MODULE TOP 
                    | MODULE
                    
MODULE::            begin PRIMITIVE ( INPUT_DEF )
                        STATEMENTS
                        OUTPUT_DEF
                    end PRIMITIVE
                    
PRIMITIVE::         PUF_PRIMITIVE | BASIC_PRIMITIVE

PUF_PRIMITIVE::     APUF | XORAPUF | FFAPUF | FFXORAPUF | DAPUF
                  | MUXPUF | IPUF | ROPUF | COMPOSEPUF 

BASIC_PRIMITIVE::   ARBITER | MUX_2x1 | SWITCH_2x2 | DELAY-CHAIN
                  | FF-DELAY-CHAIN | RING_OSC 

INPUT_DEF::         DATA_TYPE TUPLE DELIMITER INPUT_DEF
                  | DATA_TYPE TUPLE | //no-input

OUTPUT_DEF::        return ( INPUT_DEF ) DELIMITER | //no-output

PRIMITIVE_CALL::    PRIMITIVE ( VARIABLES )

TUPLE:              < VARIABLES > | STRING | NUMBER

VARIABLES::         TUPLE DELIMITER VARIABLES | TUPLE | //null

STRING::            [a-zA-Z_][a-zA-Z0-9_]*

NUMBER::            [1-9][0-9]*

DELIMITER::         ; | ,  //semi-colon or comma

STATEMENTS::        STATEMENT STATEMENTS | STATEMENT

STATEMENT::         ASSIGNMENT | IFELSE_STATEMENT
                  | SERIAL_STATEMENT | PARALLEL_STATEMENT

ASSIGNMENT::        STRING = EXPRESSION DELIMITER
                  | TUPLE = PRIMITIVE_CALL DELIMITER
                  | DELIMITER    //null-statement

EXPRESSION::        EXPRESSION ARITHMETIC_OPERATOR EXPRESSION
                  | EXPRESSION LOGICAL_OPERATOR EXPRESSION
                  | ( EXPRESSION ) | not EXPRESSION | STRING | NUMBER

ARITHMETIC_OPERATOR::/ | * | + | - | %

LOGICAL_OPERATOR::  and | or | xor | == | != | <= | >= | < | >

IFELSE_STATEMENT::  if EXPRESSION then STATEMENTS end if
                  | if EXPRESSION then STATEMENTS end if
                    else STATEMENTS end if
                  | if EXPRESSION then STATEMENTS end if
                    ELSEIF_STATEMENTS
                    else STATEMENTS end if

ELSEIF_STATEMENTS:: else if EXPRESSION then STATEMENTS end if
                    ELSEIF_STATEMENTS
                  | else if EXPRESSION then STATEMENTS end if

SERIAL_STATEMENT::  serial ASSIGNMENT to EXPRESSION do
                        STATEMENTS
                    end serial

PARALLEL_STATEMENT::parallel ASSIGNMENT to EXPRESSION do
                        STATEMENTS
                    end parallel
