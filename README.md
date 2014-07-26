# see-threepio

see-threepio is a powerful, platform-agnostic solution to language localisation that leverages the ubiquity of JSON.

## Terminology
* term - base expression, as simple as a string
* imports - external sources (outside of file) i.e FQDN, local file

## Term
All 'terms' are essentially functions with 0 - N named parameters.

## Imports
Translations can be built up from any number of sources via imports.  The expression
precedence is determined by the last imported.

An example import tree with import precedence for overlapping terms:

    - base
    - myOtherSource
    - application
      -> en imports:[base, application]
            precedence:[en, application, base]
        -> en_AU imports:[en]
            precedence:[en_AU, en, application, base]
        -> en_US imports:[en]
            precedence:[en_US, en, application, base]
      -> zh imports:[base, application]
            precedence:[zh, application, base]
        -> zh_CN imports:[zh, myOtherSource]
            precedence:[zh_CH, myOtherSource, zh, application, base]
        -> zh_HK imports:[zh]
            precedence:[zh, application, base]


## Example format

    {
        "imports":[
            "http://somecdn.org/somelanguage.json"
        ],
        "terms":{
            "anErrorOccurred": "An error occurred",
            "itemsInCart(n)": "You have {count} ~pluralise(item|{count}) in your cart",
            "pluralise(word|number)": "{word}|~if(~=({number}|1)|s))"
        }
    }
