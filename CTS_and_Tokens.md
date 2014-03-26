# Canonical Text Services & Tokenized Editions

CTS enables retrieval of passages of text based on canonical citation. Following the OHCO2 model of “text”, the citation-hierarchy of a text terminates in an ordered sequence of leaf-nodes, each of which uniquely identified. Leaf-nodes can contain mixed content. The defined reply to a CTS `GetPassage` request will deliver an XML fragment that includes a `<reply>…</reply>` element, which in turn contains XML that included all elements containing the requested leaf node, as defined by the citation scheme, as well as the contents of the leaf node, which may include elements under different namespaces.

Current implementations of CTS correctly deliver citations and citation-ranges, their containing elements, and their contents, even under complex situations where the range crosses hiearchical boundaries, _e.g._ `urn:cts:greekLit:tlg0012.tlg001.msA:1.600-2.10`.

Much of what we want to do with texts, however, happens at the content-level, below the level of citation, inside the contents of the leaf-nodes. Analysis of syntax, textual differences, alignment of texts and translations, stand-of indexing of named entities—all of these require identification at the _content level_, strings, words, and characters. The current implementation of CTS makes this a nearly insurmountable problem.

For example:

           <div n="1" type="chapter">
              <div n="6" type="verse">
                    <p>Ἰεσσαὶ δὲ ἐγέννησε τὸν <choice><abbr>δαδ</abbr><expan>Δαυὶδ</expan></choice> 
                    τὸν βασιλέα. <choice><abbr>δαδ</abbr><expan>Δαυὶδ</expan></choice> 
                    ὁ βασιλέυς δὲ. ἐγέννησε τὸν Σολομῶνα ἐκ τῆς τοῦ Οὐρίου· </p>
              </div>
           </div>

In this example, we could conceivably cite `urn:cts:greekLit:fuNTPL.matth.msCB25:Matthew.1.6@ἐγέννησε` to cite a single string. We could also cite `urn:cts:greekLit:fuNTPL.matth.msCB25:Matthew.1.6@δαδ[1]`, for the first instance of `δαδ`. But what about `urn:cts:greekLit:fuNTPL.matth.msCB25:Matthew.1.6@τὸν-Δαυὶδ`? We might expect any of the following responses:

        1. τὸν <choice><abbr>δαδ</abbr><expan>Δαυὶδ
        2. τὸν <choice><abbr>δαδ</abbr><expan>Δαυὶδ</expan>
        3. τὸν <choice><abbr>δαδ</abbr><expan>Δαυὶδ</expan></choice>
        4. τὸν Δαυὶδ

Of these (1) is no good, because it is not well-formed XML. (2) shows an attempt at being well-formed, but fails, since it did not catch all containing markup (the closing tag on `<choice></choice>`). (3) Is well-formed

## Translation Alignment

Some examples:

- [Aeneid 1.1 Latin](http://folio.furman.edu/citeservlet/texts?request=GetPassagePlus&urn=urn:cts:latinLit:phi0690.phi003.fuPers:1.1)
- [Aeneid 1.1-1.10 Latin](http://folio.furman.edu/citeservlet/texts?request=GetPassagePlus&urn=urn:cts:latinLit:phi0690.phi003.fuPers:1.1-1.10)
- [Aeneid 1.2-1.12 Latin](http://folio.furman.edu/citeservlet/texts?request=GetPassagePlus&urn=urn:cts:latinLit:phi0690.phi003.fuPers:1.1-1.12)
- [Aeneid 1.1 Unaligned English](http://folio.furman.edu/citeservlet/texts?request=GetPassagePlus&urn=urn:cts:latinLit:phi0690.phi003.fuEng:1.1)
- [Aeneid 1.8 Unaligned English](http://folio.furman.edu/citeservlet/texts?request=GetPassagePlus&urn=urn:cts:latinLit:phi0690.phi003.fuEng:1.8)
- [Aeneid 1.3 Unaligned English (broken link!)](http://folio.furman.edu/citeservlet/texts?request=GetPassagePlus&urn=urn:cts:latinLit:phi0690.phi003.fuEng:1.3)
- [Aeneid 1.1](http://folio.furman.edu/citeservlet/texts?request=GetPassagePlus&urn=urn:cts:latinLit:phi0690.phi003.fuPers:1.1)
