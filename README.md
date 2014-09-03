# see-threepio

see-threepio is a powerful, platform-agnostic solution to language localisation that leverages the ubiquity of JSON.

[## Example](http://see-threepio.github.io/see-threepio-js/)

## Goals

See-Threepio aims to solve many issues inherent in localising strings.

To achieve this, See-Threepio employs an expression language that allows for much greater control
over how translations can be made.

## Languages:

[Javascript](https://github.com/see-threepio/see-threepio-js)

## Terminology
* term - a key value pair, where the key is the name of the term, and the value is an expression.
* expression - the functional part of a term. Can be a simple as a string, or more complex.
* function - base functions supported by the language.

## Term
All 'terms' are essentially functions with 0 - N named parameters.

## Example format

    {
        "anErrorOccurred": "An error occurred",
        "itemsInCart(count)": "You have {count} ~pluralise(item|{count}) in your cart",
        "pluralise(word|number)": "{word}|~?(~=({number}|1)|s))"
    }

## The expression format

In See-Threepio, everything is a bareword, with a few exceptions:

* braces ```{}``` are used to mark placeholders.
* the tilde ```~``` is used to reference a function or term.
    * After a tilde reference, parenthesis ```()``` may be used to pass parameters.
        * Parameters are pipe ```|``` separated.

So, the following terms just result in plain strings:

    {
        "helloWorld":"Hello world",
        "symbols":"Here are a few symbols, they won't do anything special!"
    }

These terms contain placeholders:

    {
        "hello(userName)":"Hello {userName}",
        "multipleParameters(first|second|third)":"Any order is fine, such as {third}, {first}, then {second}"
    }

Note the pipe ```|``` symbol being used to separate the parameters in ```multipleParameters```

These terms use other terms:

    {
        "world":"world",
        "helloWorld":"hello ~world"
    }

These terms call shipped functions, and complex terms:

    {
        "pluralize(word|count)": "{word}~?(~=({count}|1)||s)",
        "apples":"~pluralize(apples)"
    }