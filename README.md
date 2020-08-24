Composer/Packagist version of EvalMath by Miles Kaufman
Copyright (C) 2005 Miles Kaufmann <http://www.twmagic.com/>
NAME
----
    EvalMath - safely evaluate math expressions
  
DESCRIPTION
-----------
    Use the EvalMath class when you want to evaluate mathematical expressions 
    from untrusted sources.  You can define your own variables and functions,
    which are stored in the object.  Try it, it's fun!
        
SYNOPSIS
--------
    `$m = new EvalMath;`
    
    `// basic evaluation:`
    `$result = $m->evaluate('2+2');`
    
    `// supports: order of operation; parentheses; negation; built-in functions`
    `$result = $m->evaluate('-8(5/2)^2*(1-sqrt(4))-8');`
    
    `// create your own variables`
    `$m->evaluate('a = e^(ln(pi))');`
    
    `// or functions`
    `$m->evaluate('f(x,y) = x^2 + y^2 - 2x*y + 1');`
    
    `// and then use them`
    `$result = $m->evaluate('3*f(42,a)');`

METHODS
-------
    `$m->evaluate($expr)`
        Evaluates the expression and returns the result.  If an error occurs,
        prints a warning and returns false.  If $expr is a function assignment,
        returns true on success.
    
    `$m->e($expr)`
        A synonym for $m->evaluate().
    
    `$m->vars()`
        Returns an associative array of all user-defined variables and values.
        
    `$m->funcs()`
        Returns an array of all user-defined functions.

PARAMETERS
----------
    `$m->suppress_errors`
        Set to true to turn off warnings when evaluating expressions

    `$m->last_error`
        If the last evaluation failed, contains a string describing the error.
        (Useful when suppress_errors is on).


Description of EvalMath library import into Moodle

Our changes:
* implicit multiplication (optionally) not allowed
* new custom calc emulation functions
* removed (optionally) e and pi constants - not used in calc
* removed sample files
* Fix a == FALSE that should have been === FALSE.
* added $expecting_op = true; for branch where a function with no operands is found to fix bug.
* moved pattern for func and var names into a static var
* made a function to test a string to see if it is a valid func or var name.
* localized strings
* added round, ceil and floor functions.
* EvalMath::EvalMath() changed to EvalMath::__construct() and there is a new EvalMath::EvalMath
  function to maintain backwards compatibility

To see all changes diff against version 1.1, available from:
http://www.phpclasses.org/browse/package/2695.html

skodak, Tim Hunt

Changes by Juan Pablo de Castro (MDL-14274):
* operators >,<,>=,<=,== added.
* function if[thenelse](condition, true_value, false_value)

Changes by Stefan Erlachner, Thomas Niedermaier (MDL-64414):
* add function or:
e.g. if (or(condition_1, condition_2, ... condition_n))
* add function and:
e.g. if (and(condition_1, condition_2, ... condition_n))
