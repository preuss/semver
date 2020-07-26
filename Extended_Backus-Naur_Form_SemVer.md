# Special Semantic Version v3.0
This is the Extended Barckus Naur Form for the Special Semantic Version v3.0.  

# EBNF - Extended Barckus–Naur Form
This is the grammar for a valid SemVer version.

```
<valid semver> ::= (<milestone prefix> <milestone> <milestone postfix)? <version core> ( <release prefix> <release> )? ( <build prefix> <build> )?
                 | <version core>
                 | <version core> <release prefix> <release>
                 | <version core> <build prefix> <build>
                 | <version core> <release prefix> <release> <build prefix> <build> ;

<milestone> ::= integer ;

<version core> ::= <major> ( <dot> <minor> ( <dot> <patch> )? )?

<major> ::= <numeric identifier> ;

<minor> ::= <numeric identifier> ;

<patch> ::= <numeric identifier> ;

<release> ::= <release identifier list> ;

<release identifier list> ::= <release identifier>
                            | <release identifier> <separator> <release identifier list> ;

<build> ::= <build identifier list> ;

<build identifier list> ::= <build identifier>
                          | <build identifier> <separator> <build identifier list>
						  ;

<separator> ::= <string> ;

<release identifier> ::= <alphanumeric identifier> ;

<build identifier> ::= "+"+ 
                     | <alphanumeric identifier> ;

<alphanumeric identifier> ::= <string> ;

<numeric identifier> ::= <integer> ;

<string> ::= <character>+ ;

<character> ::= <digit>
              | <letter>
              | <special character> 
			  ;

<special character> ::= "-" 
                      | "_" | "," | "`" | "´" | <dot>
                      | "$" | "£" | "€" | "¤" | "#" | "@" 
                      | "'" | "!" | "^" | "~" | "|" | ";"
                      | "{" | "}" | "[" | "]" | "(" | ")" 
                      ;

<milestone prefix> ::= "v" 
                     | "V" 
					 ;

<milestone postfix> ::= "," ;

<release prefix> ::= "-" ;

<build prefix> ::= "+" ;

<dot> ::= "." ;

# Describes that an integer is not prefixed with "0"
<integer> ::= <zero>
            | <positive digit> <digit>* 
			;

<digit> ::= <zero>
          | <positive digit> 
		  ;

<zero> ::= "0" ;

<positive digit> ::= [1-9] ;

<letter> ::= <ascii letter> ;

<ascii letter> ::= [a-z] 
                 | [A-Z] 
				 ;

```

## Example of legal version

- v3,1.22.55-SomeRelease.333432(example)+BuildInfo(2020-04-05)clock_1244
- 1.22.55-SomeRelease.333432(example)+BuildInfo(2020-04-05)clock_1244
- 1.22.55-SomeRelease.333432(example)
- 1.22.55+BuildInfo(2020-04-05)clock_1244
- 1.22.0+BuildInfo(2020-04-05)clock_1244
- 1.22+BuildInfo(2020-04-05)clock_1244
- 1.0+BuildInfo(2020-04-05)clock_1244
- 1+BuildInfo(2020-04-05)clock_1244

# Regular expression for SemVer

We are using https://regex101.com to test regex.

There are two. One with named groups for those systems that support them 

## PCRE (PHP)
This is the (PCRE [Perl Compatible Regular Expressions, i.e. Perl, PHP and R], Python and Go).

See: <https://regex101.com/r/VT89qd/1>

```
^(?:[vV](?P<milestone>0|[1-9]\d*)(?:,))?(?P<major>0|[1-9]\d*)(?:\.(?P<minor>(?:0|[1-9]\d*))(?:\.(?P<patch>0|[1-9]\d*))?)?(?:-(?P<release>(?:[_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+)(?:[_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+(?:[_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+))*))?(?:\+(?P<build>[+_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+(?:[+_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+[+_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+)*))?$
```

## ECMAScript (JavaScript)
And this one with numbered capture groups instead (so cg1 = milestone, cg2 = major, cg3 = minor, cg4 = patch, cg5 = release and cg6 = build) that is compatible with ECMA Script (JavaScript), PCRE (Perl Compatible Regular Expressions, i.e. Perl, PHP and R), Python and Go.

See: <https://regex101.com/r/rmSh6Y/1>

```
^(?:[vV]((?:0|[1-9]\d*))(?:,))?(0|[1-9]\d*)(?:.(0|[1-9]\d*)(?:.(0|[1-9]\d*))?)?(?:-((?:[_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+)(?:\.(?:[_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]*))*))?(?:\+([+_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+(?:[_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+[+_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+)*))?$
```

### Expanded Regex for PCRE (PHP)

```
^
	(?:
		[vV]
		(?P<milestone>
			0|[1-9]\d*
		)
		(?:,)
	)?
	(?P<major>
		0|[1-9]\d*
	)
	(?:\.
		(?P<minor>
			(?:0|[1-9]\d*)
		)
		(?:\.
			(?P<patch>
				0|[1-9]\d*
			)
		)?
	)?
	(?:-
		(?P<release>
			(?:
				[_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+
			)
			(?:
				[_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+
				(?:
					[_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+
				)
			)*
		)
	)?
	(?:\+
			(?P<build>
				[+_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+
				(?:
					[+_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+
					[+_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+
				)*
			)
	)?
$
```


### Expanded Regex for ECMA Script (JavaScript)

```
^
	(?:
		[vV]
		(
			(?:0|[1-9]\d*)
			
		)
		(?:,)
	)?
	(0|[1-9]\d*)
	(?:.
		(0|[1-9]\d*)
		(?:.
			(0|[1-9]\d*)
		)?
	)?
	(?:
		-
		(
			(?:[_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+)
			(?:\.
				(?:[_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]*)
			)*
		)
	)?
	(?:
		\+
		(
			[+_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+
			(?:
				[_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+
				[+_,`´.$£€¤#@'!^~;"{}[\]()0-9a-zA-Z-]+
			)*
		)
	)?
$
```
