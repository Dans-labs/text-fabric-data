# Features (by category)

## Introduction
This is the key to the meaning of the features of the
[etcbc4c dataset](/ETCBC/hebrew/etcbc4c/home).

There are several
[types of objects](features/otype.md),
which specify what features such objects have.
Some :ref:`database features <database>` are shared by all object types.
We organize the object types as follows:
:ref:`sectional <sectional>`,
:ref:`word <word>`, and
:ref:`linguistic <linguistic>`.
See :doc:`otype <otype>` for a description of these types.

.. caution::
    At the moment, not all features have been described clearly enough.
    See :doc:`Features with cautions <0_cautions>`

=============================   =================================
:ref:`- database <database>`    generic features for all objects
:ref:`- sections <sectional>`   division in books, chapters, etc
:ref:`- word <word>`            all about the individual words
:ref:`- syntax <linguistic>`    phrases, clauses, etc
=============================   =================================

## Grid features

====================  =================  =================================================
:doc:`otype <otype>`  node type          ``book`` ``verse`` ``clause`` ``phrase`` ``word``
:doc:`oslots <oslots>` linked to slots    ``book`` ``verse`` ``clause`` ``phrase`` ``word``
:doc:`otext <otext>`   textapi   ``book`` ``verse`` ``clause`` ``phrase`` ``word``
====================  =================  =================================================

## Sectional features

==============================  ==============================  ===============================
:doc:`book <book>`              name of Bible book              ``Genesis`` ``Psalmi`` ``Amos``
:doc:`chapter <chapter>`        number if chapter within book   ``3``
:doc:`verse <verse>`            number of verse within chapter  ``4``
:doc:`label <label>`            passage indicator               ``AMOS 03,04``
:doc:`half_verse <half_verse>`  key for part within verse       ``A`` ``B`` ``C``
==============================  ==============================  ===============================

## Word features

=================================== ==============================================
:ref:`-- orthography <orthography>` several representations of the word occurrence
:ref:`-- lexical <lexical>`         lexical information about the word
:ref:`-- morphology <morphology>`   morphology classes of the word occurrence
:ref:`-- morphemes <morphemes>`     morphemes that are present in the word.
:ref:`-- statistics <statistics>`   frequency counts and occurrence ranks
=================================== ==============================================

## Orthography

===================================  =================  ===========  ==============  ===========
:doc:`g_cons <g_cons>`               word               consonantal  transliterated  ``>CR``
:doc:`g_cons_utf8 <g_cons_utf8>`     word               consonantal  hebrew          ``אשׁר``
:doc:`g_word <g_word>`               word               pointed      transliterated  ``>:ACER&``
:doc:`g_word_utf8 <g_word_utf8>`     word               pointed      hebrew          ``אֲשֶׁר``
:doc:`ketiv <ketiv>`                 word (ketiv)       consonantal  hebrew          ``אֲשֶׁר``
:doc:`g_qere_utf8 <g_qere_utf8>`     word (qere)        pointed      hebrew          ``אֲשֶׁר``
:doc:`trailer_utf8 <trailer_utf8>`   after-word         pointed      hebrew          ``׃ ׆̇``
:doc:`qtrailer_utf8 <trailer_utf8>`  after-word (qere)  pointed      hebrew          ``׃ ׆̇``
:doc:`phono <phono>`                 word               full         phonetic        ``dāvˈār``
:doc:`phono_sep <phono>`             after-word         full         phonetic        ``.``
===================================  =================  ===========  ==============  ===========

### Lexical

===============================  ==========  ===========  ==============  ========
:doc:`lex <lex>`                 word        consonantal  transliterated  ``>MR[``
:doc:`lex_utf8 <lex_utf8>`       word        consonantal  hebrew          ``אמר[``
:doc:`g_lex <g_lex>`             word        pointed      transliterated  ``>MER``
:doc:`g_lex_utf8 <g_lex_utf8>`   word        pointed      hebrew          ``אמֶר``
===============================  ==========  ===========  ==============  ========

==========================  ===============================  ======================
:doc:`language <language>`  language                         ``Hebrew`` ``Aramaic``
:doc:`sp <sp>`              part of speech                   ``verb`` ``subs``
:doc:`pdp <pdp>`            phrase dependent part of speech  ``verb`` ``subs``
:doc:`ls <ls>`              lexical set                      ``quot`` ``ques``
:doc:`nametype <nametype>`  type of named entity             ``pers`` ``topo``
==========================  ===============================  ======================

### Morphology

==============  =============  ================================
:doc:`gn <gn>`  gender         ``m`` ``f``
:doc:`nu <nu>`  number         ``sg`` ``pl`` ``du``
:doc:`ps <ps>`  person         ``p1`` ``p2`` ``p3``
:doc:`st <st>`  state          ``a`` ``c`` ``e``
:doc:`vs <vs>`  verbal stem    ``qal`` ``piel`` ``nif`` ``hif``
:doc:`vt <vt>`  verbal tense   ``perf`` ``impf`` ``wayq``
==============  =============  ================================

### Morphemes

================ ==================== ==============================  ==================  =========================
:doc:`nme <nme>` :doc:`g_nme <g_nme>` :doc:`g_nme_utf8 <g_nme_utf8>`  nominal ending      ``/`` ``/IJM`` ``/@H``
:doc:`pfm <pfm>` :doc:`g_pfm <g_pfm>` :doc:`g_pfm_utf8 <g_pfm_utf8>`  preformative        ``!!`` ``!J.I!`` ``!TI!``
:doc:`prs <prs>` :doc:`g_prs <g_prs>` :doc:`g_prs_utf8 <g_prs_utf8>`  pronominal suffix   ``+OW`` ``+IJ`` ``+HEM``
:doc:`uvf <uvf>` :doc:`g_uvf <g_uvf>` :doc:`g_uvf_utf8 <g_uvf_utf8>`  univalent final     ``~@H`` ``~IJ`` ``~OW``
:doc:`vbe <vbe>` :doc:`g_vbe <g_vbe>` :doc:`g_vbe_utf8 <g_vbe_utf8>`  verbal ending       ``[`` ``[W.`` ``[T.IJ``
:doc:`vbs <vbs>` :doc:`g_vbs <g_vbs>` :doc:`g_vbs_utf8 <g_vbs_utf8>`  root formation      ``]]`` ``]NI]`` ``]HA]``
================ ==================== ==============================  ==================  =========================

### Statistics

==========================  ==============================
:doc:`freq_lex <freq_lex>`  frequency of lexeme
:doc:`freq_occ <freq_occ>`  frequency of word occurrence
:doc:`rank_lex <rank_lex>`  rank of lexeme
:doc:`rank_occ <rank_occ>`  rank of word occurrence
==========================  ==============================

## Linguistic features

====================================  ==============
:ref:`-- sentence(-atom) <sentence>`  sentence level
:ref:`-- clause(-atom) <clause>`      clause level
:ref:`-- phrase(-atom) <phrase>`      phrase level
:ref:`-- generic <generic>`           generic
====================================  ==============

### Sentence(-atom) features

Nothing specific, just a generic `number` feature.

### Clause(-atom) features

================================  ===========================  ===================================
:doc:`typ <typ>`                  clause type                  ``AjCl`` ``WayX`` ``WXQt`` ``ZImX``
:doc:`kind <kind>`                rough clause type            ``VC`` ``NC`` ``WP``
:doc:`rela <rela>`                clause constituent relation  ``Adju`` ``Attr`` ``Coor``
:doc:`domain <domain>`            text type ??                 ``Q`` ``N`` ``D``
:doc:`txt <txt>`                  text type                    ``NQ`` ``NQQ`` ``QNQQ`` ``NQND``
:doc:`code <code>`                clause atom relation         ``200`` ``477`` ``999``
:doc:`is_root <is_root>`          ??
:doc:`tab <tab>`                  hierarchical tabulation      ``0`` ``3`` ``10`` ``29``
:doc:`pargr <pargr>`              paragraph number             ``1`` ``1.2`` ``2.3.4``
:doc:`instruction <instruction>`  instruction                  ``.q`` ``.d`` ``..`` ``ve``
================================  ===========================  ===================================

### Phrase(-atom) features

==========================  ====================  ======================================
:doc:`typ <typ>`            phrase type           ``VP`` ``NP`` ``PP`` ``AdjP`` ``AdvP``
:doc:`rela <rela>`          phrase atom relation  ``Appo`` ``Para`` ``Resu``
:doc:`function <function>`  phrase function       ``Pred`` ``Subj``
:doc:`det <det>`            determination         ``det`` ``und``
==========================  ====================  ======================================

## Generic features

==============================================  ====================================  =============================================
:doc:`number <number>`                          sequence number in context            ``123``
:doc:`dist <dist>`                              distance to mother                    ``-10`` ``0``  ``1`` ``8``
:doc:`dist_unit <dist_unit>`                    unit of measuring distance to mother  ``clause_atoms`` ``phrase_atoms`` ``words``
:doc:`mother_object_type <mother_object_type>`  object type of mother                 ``clause`` ``phrase`` ``subphrase`` ``word``
==============================================  ====================================  =============================================
