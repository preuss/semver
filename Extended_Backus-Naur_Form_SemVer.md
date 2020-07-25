# Special Semantic Version v2.1
This is the Extended Barckus Naur Form for the Special Semantic Version v2.1.  
It is compatible with SemVer 2.0 

# EBNF - Extended Barckus–Naur Form
This is the grammar for a valid SemVer version.

```
<valid semver> ::= <version core>
                 | <version core> "-" <pre-release>
                 | <version core> "+" <build>
                 | <version core> "-" <pre-release> "+" <build> ;

<version core> ::= <major> "." <minor> "." <patch> ;

<major> ::= <numeric identifier> ;

<minor> ::= <numeric identifier> ;

<patch> ::= <numeric identifier> ;

<pre-release> ::= <dot-separated pre-release identifiers> ;

<dot-separated pre-release identifiers> ::= <pre-release identifier>
                                          | <pre-release identifier> "." <dot-separated pre-release identifiers> ;

<build> ::= <dot-separated build identifiers> ;

<dot-separated build identifiers> ::= <build identifier>
                                    | <build identifier> "." <dot-separated build identifiers> ;

<pre-release identifier> ::= <alphanumeric identifier> ;

<build identifier> ::= <alphanumeric identifier> ;

<alphanumeric identifier> ::= <string> ;

<numeric identifier> ::= <integer> ;

<string> ::= <character>+ ;

<character> ::= <digit>
              | <non-digit> ;

<non-digit> ::= <letter>
              | <special character> ;
			  
<special character> ::= "-" ;

<integer> ::= <zero>
            | <positive digit> <digit>* ;

<digit> ::= <zero>
          | <positive digit> ;

<zero> ::= "0" ;

<positive digit> ::= [1-9] ;

<letter> ::= <ascii letter> ;

<ascii letter> ::= [a-z] 
                 | [A-Z] ;

```