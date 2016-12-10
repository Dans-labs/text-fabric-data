Frequency-occurrence `freq_occ`
-------------------------------------------------------------------------------
The frequency of a word occurrence, measured as the number of occurrences in the whole Hebrew Bible.

This feature is present on objects of type *word*.

What is counted is the consonantal representation of the words, without accents.

.. note::
    This feature does not distinguish between homonyms, i.e. it counts representations and lexeme distinctions
    are not taken into account.

**Hint:**
The measures *frequency* and *rank* have been computed for *lexemes* and *occurrences*.
    
This feature has been added to the database in a later stage as package called `lexicon`.

You can use it in SHEBANQ queries.

If you want to use it in LAF-Fabric, you have to load `lexicon` as *annox*.
Consult the [LAF-Fabric API reference on annoxes](http://laf-fabric.readthedocs.io/en/latest/texts/API-reference.html#extra-annotation-packages).

See also:
 
* [freq_lex](freq_lex)
* [rank_lex](rank_lex)
* [freq_occ](freq_occ)
* [rank_occ](rank_occ)

