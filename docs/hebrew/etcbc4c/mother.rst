Mother
######

Definition
==========
*mother* is a relation between objects, representing a linguistic relation of dependence.
In the ETCBC4 database, the mother relation exists between objects of many different kinds.

In the `mother notebook <https://shebanq.ancient-data.org/shebanq/static/docs/tools/shebanq/mother.html>`_
there is a count of the types that the mother relationship bridges::

    Mothers   of type clause              : 11684x
    Mothers   of type clause_atom         : 58002x
    Mothers   of type phrase              :  5164x
    Mothers   of type phrase_atom         :  9594x
    Mothers   of type subphrase           : 20556x
    Mothers   of type word                : 37008x
    Daughters of type clause              : 18580x
    Daughters of type clause_atom         : 89079x
    Daughters of type phrase              :   207x
    Daughters of type phrase_atom         : 13301x
    Daughters of type subphrase           : 55244x

More precisely, this is from where to where the mother relationships go::

    daughter = clause               and mother = clause              : 12462x
    daughter = clause               and mother = phrase              :  5167x
    daughter = clause               and mother = word                :   951x
    daughter = clause_atom          and mother = clause_atom         : 89079x
    daughter = phrase               and mother = clause              :     5x
    daughter = phrase               and mother = phrase              :   195x
    daughter = phrase               and mother = word                :     7x
    daughter = phrase_atom          and mother = phrase_atom         : 11717x
    daughter = phrase_atom          and mother = word                :  1584x
    daughter = subphrase            and mother = subphrase           : 20556x
    daughter = subphrase            and mother = word                : 34688x

**Caution:**
This description needs more body: what objects can be mothers, what daughters?
What is the linguistic meaning of mother in all those cases?
Are there formal characteristics indicating a mother relationship?
Examples needed!

Examples
--------

MQL Implementation
==================
In MQL, *mother* is not a feature, but it is possible to query with conditions involving the *mother*.

Example
-------
Here is a query that looks up occurrences of the word *swear* (``CB<``) if it occurs in a clause atom that
is the mother of a following clause which is a quotation (``txt = 'Q'``)::

    select all objects where
    [verse
        [clause_atom as c1
            [word focus lex = "CB<["
            ]
        ]
        ..
        [clause txt = 'Q'
            [clause_atom mother = c1.self
            ]
        ]
    ]

LAF-Fabric implementation
=========================
In the LAF representation of the ETCBC4 database, *mother* is a feature, annotated to edges between nodes.
The nodes correspond to the objects, and the edges to relationships between nodes.
The edges, labelled with *mother*, correpond to the *mother* relationship.

Example
-------
We count how many mothers nodes can have (it turns to be 0 or 1).
We walk through all nodes (``for c in NN()``) and per node we retrieve the mother nodes (``C.mother.v(c)``), and
we store the lengths (if non-zero) in a dictionary (``mother_len``)::

    mother_len = {}
    for c in NN():
        lms = list(C.mother.v(c))
        nms = len(lms)
        if nms: mother_len[c] = nms

This example is taken from the
`tree tool <https://shebanq.ancient-data.org/tools?goto=trees>`_.
