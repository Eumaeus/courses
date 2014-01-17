# Canonical Text Services & Tokenized Editions

CTS enables retrieval of passages of text based on canonical citation. Following the OHCO2 model of “text”, the citation-hierarchy of a text terminates in an ordered sequence of leaf-nodes, each of which uniquely identified. Leaf-nodes can contain mixed content. The defined reply to a CTS `GetPassage` request will deliver an XML fragment that includes a `<reply>…</reply>` element, which in turn contains XML that included all elements containing the requested leaf node, as defined by the citation scheme, as well as the contents of the leaf node, which may include elements under different namespaces.
        <dissssss="book" n="1">

Current implementations of CTS correctly deliver citations and citation-ranges, their containing elements, and their contents, even under complex situations where the range crosses hiearchical boundaries, _e.g._ `urn:cts:greekLit:tlg0012.tlg001.msA:1.200-2.10`.

Much of what we want to do with texts, however, happens at the content-level, below the level of citation, inside the contents of the leaf-nodes. Analysis of syntax, textual differences, alignment of texts and translations, stand-of indexing of named entities—all of these require identification at the _content level_, strings, words, and characters. The current implementation of CTS makes this a nearly insurmountable problem.

For example:

           <div n="6" type="verse">
                    <p>Ἰεσσαὶ δὲ ἐγέννησε τὸν <choice><abbr>δαδ</abbr><expan>Δαυὶδ</expan></choice> 
                    τὸν βασιλέα. <choice><abbr>δαδ</abbr><expan>Δαυὶδ</expan></choice> 
                    ὁ βασιλέυς δὲ. ἐγέννησε τὸν Σολομῶνα ἐκ
                    τῆς τοῦ Οὐρίου· </p>
           </div>

In this...
