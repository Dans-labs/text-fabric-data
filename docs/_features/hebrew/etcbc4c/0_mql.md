---
title: MQL
feat: false
---

# Text-Fabric versus SHEBANQ

The [ETCBC](http://www.godgeleerdheid.vu.nl/en/index.asp) provides two tools to work with its dataset of linguistic annotations
to the Hebrew Bible.

One is [SHEBANQ](https://shebanq.ancient-data.org) which provides a human readable view on the data on the basis of which researchers
can write queries. SHEBANQ is an **online** tool that offers to save such queries and show them next to the relevant chapters of the Bible.

SHEBANQ is best used for drawing attention of fellow researchers to interesting patterns in the Hebrew Bible.
It even provides visualizations of result sets, which can also be downloaded as `.csv` files.

Nevertheless, SHEBANQ falls short for those researchers that want to perform statistical analysis on the data.
These researchers need to preprocess the data in ways that an application author cannot anticipate.

The good news is that existence of the other tool,
[Text-Fabric](https://github.com/ETCBC/text-fabric/wiki).
This is an **offline** tool based on exactly the same data that powers SHEBANQ.
The programming researcher can use Text-Fabric as a preprocessing tool for transforming the complex ETCBC data into the formats that are suitable to
R, spreadsheets, or any format of choice.
Text-Fabric is open source, downloadable from [github](https://github.com/ETCBC/text-fabric),
and the data is downloadable from [text-fabric-data](https://igithub.com/ETCBC/text-fabric-data).

It can be installed on Mac OSX, Windows and Linux.
The recommended mode of working with the data is: programming in Python within a Jupyter Notebook.

# Tutorial

Text-Fabric is ideal if you interested in a certain phenomenon and you want to gather data about that phenomenon.
Take for example the following notebook:

* [tutorial](https://github.com/ETCBC/text-fabric/blob/master/docs/tutorial.ipynb)

This points the way to an explorative way of researching syntactical patterns, without knowing in advance how exactly
the data is organized.

# Text-Fabric versus MQL

The queries in SHEBANQ are based on MQL, the query language of
[Emdros](http://emdros.org).

As a concrete example where MQL becomes tedious and we feel the need to move to Text-Fabric,
we take the task to provide a `.csv` file with the occurrences of two Hebrew words for *there is* and *there is no(t)*.

## Approach 1

Here is a [public query in SHEBANQ](http://shebanq.ancient-data.org/hebrew/query?id=556) that asks for all occurrences.

As you can see, the query asks for these words in their context of enclosing objects such as phrase(atom) and clause(atom).
It is even possible to generate a neat `.csv` file from SHEBANQ with a lot of information, but as soon as you want to look up more information
about other parts of the context, e.g. phrases/clauses *next to* the words in question, SHEBANQ will let you down.

Then turn to Text-Fabric. If you have not yet installed it, you can look at this
[public notebook](http://nbviewer.ipython.org/github/etcbc/Text-fabric-nbs/blob/master/lingvar/yesh.ipynb),
where you see the
compilation of a csv file in (frozen) action. After installing Text-Fabric,
you can download this notebook and see it in real action on your own computer.

### Pitfalls of approach 1

There are pitfalls in approach 1.
If you have a query that pinpoints the textual phenomenon that you are after, and then wrap context objects around it,
there might be unexpected misses. For example, if you look for: 

    [phrase function = 'Pred' [word first lex = 'NTN[']]

and you want to collect the passage information as well, you want to say this:

    [book [chapter [verse [sentence
      [phrase function = 'Pred' [word first lex = 'NTN[']]
    ]]]]

then you miss the cases where a sentence spans more than one verse!

And if you want the other words or phrases in the same clause as the target phrase, you want something like:

    [book [chapter [verse [sentence
      [clause
        [phrase first]
        [phrase function = 'Pred' [word first lex = 'NTN[']]
        [phrase]*
        [phrase last]
       ]
    ]]]]

But what if the target phrase is itself the first one, or the last one, or both?
We need to distinguish cases:

    [book [chapter [verse [sentence
      [clause
        [phrase first and last function = 'Pred' [word first lex = 'NTN[']]
        or
        [phrase first function = 'Pred' [word first lex = 'NTN[']]
        [phrase]*
        [phrase last]
        or
        [phrase first]
        [phrase]*
        [phrase last function = 'Pred' [word first lex = 'NTN[']]
        or
        [phrase first]
        [phrase]*
        [phrase function = 'Pred' [word first lex = 'NTN[']]
        [phrase]*
        [phrase last]
       ]
    ]]]]

This is not pleasant and it is still wrong, because if the clause has gaps, and those gaps occur between phrases, than
any such clause will not be found by this query. We have to say this instead:

    [book [chapter [verse [sentence
      [clause
        [phrase first and last function = 'Pred' [word first lex = 'NTN[']]
        or
        [phrase first function = 'Pred' [word first lex = 'NTN[']]
        [[phrase][gap?]]*
        [phrase last]
        or
        [phrase first]
        [[phrase][gap?]]*
        [phrase last function = 'Pred' [word first lex = 'NTN[']]
        or
        [phrase first]
        [[phrase][gap?]]*
        [phrase function = 'Pred' [word first lex = 'NTN[']]
        [[phrase][gap?]]*
        [phrase last]
       ]
    ]]]]

And still we will miss results, because the target phrase may occur in a phrase that itself fills the gap inside another phrase.
These thing are not academic, they occur in the ETCBC data! In order to get them the size of this query will explode,
completely obscuring the intention of it.

A possible remedy is to simplify and just ask for:

    [clause
      [phrase function = 'Pred' [word first lex = 'NTN[']]
    ]

and then use another simple query to get the remaining material:

    [book [chapter [verse [sentence 
        [clause [phrase]]
    ]]]]

When you process the results of these queries you have to make an index of phrases in their clauses linked to the passages on the
basis of the second query, and use it when you process the results of the first query.

## Approach 2

As this is a fairly common use case, it is worthwhile to make this easy for you.
That is why Text-Fabric has the option to prepare and load data for the embedding relation bewteen objects, which is
accessible through the API functions `L.u(otype, node)` and `L.d(otype, node)`.

`L.u` gives the otype container of a node, e.g. `L.u('chapter', w)` gives the chapter to which word node `w` belongs.

`L.d` gives the list of contained nodes of a certain type, e.g. `L.u('subphrase', v)` gives the list of subphrases contained in verse node `v`.

So if you go back to the first query:

    [phrase function = 'Pred' [word first lex = 'NTN[']]

then you could process the result as follows (suppose you want to make a csv file of every result with passage info, verb info,
and a string of _ separated functions of all phrases in the clause).

Write the query down:

    ntn_sim_query = '''
        select all objects where
        [phrase function = Pred 
          [word focus first (language = Hebrew and (lex = 'NTN[' or lex = 'FJM[')) ]
        ]
    '''

Execute it and gather the results in a sheaf:

    sheaf_ntn_sim = Q.mql(ntn_sim_query)

Process the results:

    outf = outfile('test.csv')
    for ((phrase, ((word,),)),) in sheaf_ntn_sim.results():
        info = []
        verb_info = F.lex.v(word)
        clause = L.u('clause', phrase)
        book =  F.book.v(L.u('book', clause))
        chapter =  F.chapter.v(L.u('chapter', clause))
        verse =  F.chapter.v(L.u('verse', clause))
        for phr in L.d('phrase', clause):
            info.append(F.function.v(phr))
        outf.write('{} {}:{},{},{}\n'.format(
            book, chapter, verse,
            verb_info,
            '_'.join(info),
        ))
    outf.close()

See a more elaborate example in the [verbal valence tool](https://shebanq.ancient-data.org/tools?goto=valence) 

Once you got these tricks, the power is yours. Start by making small variations to this notebook, and then, as your programming skills get
sharpened, see how far you can get.

    
# Reproducible Computing

The whole point of Text-Fabric and SHEBANQ is that when you compute with hard, objective data, you also want
your results to have a firm status. In order to achieve that, you will need the scrutiny of your peers.
In SHEBANQ you can make the *queries* public so that everybody will be able to see the results that you now see.
In Text-Fabric you can make the *notebooks* public so that everybody can recompute the results you compute now.
