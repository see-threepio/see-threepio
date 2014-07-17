# see-threepio

see-threepio is a powerful, platform-agnostic solution to language localisation that leverages the ubiquity of JSON.

## format

    {
        "anErrorOccurred": "An error ~itemsInCart({count}) occurred",
        "itemsInCart(n)": "You have {count} ~pluralise({item}|{count}) in your cart",
        "pluralise(word|count)": "{word}~if(~=({number}|1)|s) ~ifElse(~>(~1|~2)|fruit|veggie)"
    }