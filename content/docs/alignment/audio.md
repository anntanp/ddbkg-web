---
# Title, summary, and page position.
linktitle: Audio (MO + ACO)
summary: Alignment of DDB-EDM to MO and ACO
weight: 30
icon: book
icon_pack: fas

# Page metadata.
title: Audio Ontologies in the DDB
date: "2022-03-07T00:00:00Z"
type: book  # Do not modify.
---
## 1. Introduction
The vast collection of the German Digital Company (DDB) includes objects that the UNESCO cultural heritage (CH) hierarchy (Ronchi, 2011) classified as intangible. Examples of intangible objects include musical works, natural heritage, oral traditions, to name a few. These are often digitized as audio or video.

Audio content in the DDB can be found across several sectors: audio books from libraries, interviews of significant German personalities from research institutions, commercial jingles from archives, recordings of animal sounds from natural museums and music from gramophone records often found in multimedia libraries. The audio files can be classified into two broad  (2) categories:

1.  **Work** - audio files containing intellectual or artistic content, such as Music, and Ebooks. 
     
2.  **Non-Work** - audio files without intellectual or artistic content, such as as bird songs, and machinery sounds.

The types of audio files are encoded in the [dc:type](http://purl.org/dc/elements/1.1/type) or [edm:hasType](http://www.europeana.eu/schemas/edm/hasType) data properties.  Below is the list of these terms and the number of objects associated with them. Note that the 

{{< gdocs src="https://docs.google.com/spreadsheets/d/1_iN1W2Xo5WyYIQ3sgfDOcOeBvgZ_MkaBsL-7JTCKiUU/edit?usp=sharing" >}}

To determine whether the audio file is a *Work* or *Non-Work*, the values encoded by the data property [dc:subject](http://purl.org/dc/elements/1.1/subject) are inspected. There are approximately 3,700 unique terms relating to the object's subject or topic, however, only terms with frequency counts in the thousands were used. These terms are as follows: 

1.  Work - *Lied* (Song), *Duett* (Duet), *Arie* (Arias), *Oper* (Opera), *Erzählende Literatur* (Audio Books), *Werbesendung* (Ads)
2.  Non-Work - *Tierstimme* (Animal Sounds), *Tonaufname* (Sound Recording)

--- 

## 2. Ontologies
To be able to represent the semantics of these diverse objects, the selection of the target ontologies is based on the following considerations: interoperability, suitability to the domain, and the application profile.

In the case of audio books, adapting a FRBR-aligned ontology facilitates interoperability, by considering them as  expressions of their respective literary works. The same holds true for any musical composition and its text; for instance, a recording of Carl Orff's Carmina Burana is considered an expression of the 13*th* century manuscript containing a collection of poems it was based on.

### 2.1 FaBiO
Although, [FaBiO](https://sparontologies.github.io/fabio/current/fabio.html) (Peroni et al., 2012), as a FRBR-aligned bibliographic ontology, provides subclasses relating to musical works [fabio:Song](https://sparontologies.github.io/fabio/current/fabio.html#d4e5392), [fabio:MusicalComposition](https://sparontologies.github.io/fabio/current/fabio.html#d4e4227) and their expression [fabio:AudioDocument](https://sparontologies.github.io/fabio/current/fabio.html#d4e2145), these subclasses cannot represent the full range of audio content described above (Figure [1](#docs-audio-fig1)). 

{{< figure src="https://ise-fizkarlsruhe.github.io/ddbkg/images/audio-in-fabio.jpg" caption="FaBiO Classes for Audio Files" numbered="true" id="docs-audio-fig1" >}}

### 2.2 Music Ontology (MO)
[MO](http://musicontology.com/specification/) (Raimond et al., 2007) aims to model the semantics of music production workflows and their editorial metadata. FRBR plays a central role in the definition of its classes. Parallels can be drawn between the super-classes of MO ([mo:MusicalWork](http://musicontology.com/specification/#term-MusicalWork), [mo:MusicalExpression](http://musicontology.com/specification/#term-MusicalExpression), [mo:MusicalManifestation](http://musicontology.com/specification/#term-MusicalManifestation), and [mo:MusicalItem](http://musicontology.com/specification/#term-MusicalItem) and the 4 conceptual layers of FRBR. Since the original intention of the authors is to model the different workflows, events are central to this ontology. Entities that are usually found as attributes of a [frbr:Endeavor](https://vocab.org/frbr/core#term-Endeavour) sub-class require intermediate events to link them to that endeavor: the attribution of an *mo:MusicalArtist* (Agent) to its [mo:MusicalWork](http://musicontology.com/specification/#term-MusicalWork)) requires an instance of the [mo:Composition](http://musicontology.com/specification/#term-Composition) event (fig [2](#docs-audio-fig2)), in contrast to the widely-adopted convention of linking agents directly to the [frbr:Work](https://vocab.org/frbr/core#term-Work).

{{< figure src="https://ise-fizkarlsruhe.github.io/ddbkg/images/audio-in-mo.jpg" caption="MO Classes for Audio Files" numbered="true" id="docs-audio-fig2" >}}


### 2.3 Audio Commons Ontology (ACO)
As mentioned, not all audio content in the DDB possess intellectual or artistic content. Examples of these are natural sounds and field recordings. An ontology that  provides classes and properties to allow representations of non-musical audio content exists in [ACO](https://w3id.org/ac-ontology/aco#AudioExpression) (Ceriani et al., 2018). Being an upper-level ontology for audio content, the authors' initial intention is to provide interoperability across repositories on the Web. The FRBR-aligned classes of ACO are generalizations of MO classes. However, a FRBR Work sub-class specific to ACO was not defined, since it does not generalize to all types of sounds. Similarly to MO, events also play an central role in ACO.

---

## 3. Alignment
The decision to forego the usage of [owl:Event](http://motools.sourceforge.net/event/event.html#term_Event) sub-classes, namely, [mo:Composition](http://musicontology.com/specification/#term-Composition), [mo:Performance](http://musicontology.com/specification/#term-Performance), and [mo:Recording](http://musicontology.com/specification/#term-Recording), can be explained by the application profile and dataset of the DDB. The intention to publish metadata describing the CHOs for the purpose of retrieval and exploration means that details of events that are relevant for music or sound production are rarely included in the data provided by participating institutions. For instance, the description of a gramophone record includes the names of the composer, performer/s and publisher. However, details of the performance of this specific record which is crucial when modeling a music production workflow is not available. If event-centric modeling is followed, the additional entities representing events such as [mo:Composition](http://musicontology.com/specification/#term-Composition) or [mo:Performance](http://musicontology.com/specification/#term-Performance) will serve no purpose, since the relationship between entities of the endeavor and the event will always be 1:1. Thus, the attributes that may be attached to the event can be defined as object or data properties of the involved endeavor entities. As a result, the generic property [dcterms:contributor]() is used in lieu of [mo:performer](http://musicontology.com/specification/#term-performer), since the latter strictly defines the domain to be of class [mo:Performance](http://musicontology.com/specification/#term-Performance), an event which is not utilized in the alignment.

##### 3.1 Simplified (Music)
An overview of the alignment from DDB-EDM to MO and ACO is shown in Figure [3](#docs-audio-fig3). The [DDB object](https://www.deutsche-digitale-bibliothek.de/item/ILNOJIJWFWN3WFHQBS6RXI4QJ3BOXZVV) in this example is a gramophone record of "[Old Folks at Home](https://en.wikipedia.org/wiki/Old_Folks_at_Home)" by [Stephen Foster](https://en.wikipedia.org/wiki/Old_Folks_at_Home).
{{< figure src="https://ise-fizkarlsruhe.github.io/ddbkg/images/ddbedm-to-mo-aco.jpg" caption="Alignment to Target Ontologies (simplified)" numbered="true" id="docs-audio-fig3" >}}


### 3.2 Detailed (Music)
Figure [4](#docs-audio-fig3) illustrates the alignment with object and data properties. From the source data encoded in [xml](https://www.deutsche-digitale-bibliothek.de/item/xml/ILNOJIJWFWN3WFHQBS6RXI4QJ3BOXZVV), the resulting alignment is shown in this [turtle file](https://ise-fizkarlsruhe.github.io/ddbkg/data/sample-music.ttl).

{{< figure src="https://ise-fizkarlsruhe.github.io/ddbkg/images/mo-aco-detailed-music.jpg" caption="Alignment to Target Ontologies of Musical Audio Content (detailed)" numbered="true" id="docs-audio-fig4" >}}


### 3.3 Detailed (Non-Musical)
Figure [5](#docs-audio-fig5) illustrates the alignment of a non-musical audio object, e.g. [birdsong](https://www.deutsche-digitale-bibliothek.de/item/JI53FTTP6AQMEJEYJE3OMX3NROJPGQAP). From the source data encoded in [xml](https://www.deutsche-digitale-bibliothek.de/item/xml/JI53FTTP6AQMEJEYJE3OMX3NROJPGQAP), the resulting alignment is shown in this [turtle file](https://ise-fizkarlsruhe.github.io/ddbkg/data/sample-birdsong.ttl).

{{< figure src="https://ise-fizkarlsruhe.github.io/ddbkg/images/mo-aco-detailed-birdsong.jpg" caption="Alignment to Target Ontologies of Non-Musical Audio Content (detailed)" numbered="true" id="docs-audio-fig5" >}}

---
## 4. SPARQL Endpoint
A total of 40,611 (see Google Sheets [2](#docs-audio-sheet2)) audio objects from the DDB are included in the [DDB-KG](https://ddbkg.fiz-karslruhe.de:42003/sparql) SPARQL endpoint. Using the [DDB REST API](https://labs.deutsche-digitale-bibliothek.de/app/ddbapi/), a list of object IDs corresponding to the audio objects are retrieved. After which, Python libraries to parse the DDB XML files ([Element Tree](https://docs.python.org/3/library/xml.etree.elementtree.html)) and to generate the RDF triples ([RDFLib](https://github.com/RDFLib/rdflib)). Competency questions and their corresponding SPARQL queries are provided in [section 4.2]({{< relref "/docs/examples/#audio" >}}) below.

### 4.1 Dataset
The top source of audio objects belong to the museum sector, closely followed by multimedia libraries and archives. There are 3,848,605 triples with 192,683 entities. A detailed list of entity types and their properties are shown in Google Sheets [2](#docs-audio-sheet2). 
 
{{< gdocs src="https://docs.google.com/spreadsheets/d/1_iN1W2Xo5WyYIQ3sgfDOcOeBvgZ_MkaBsL-7JTCKiUU/edit#gid=2067206494" id="docs-audio-sheet2" >}}

---
### 4.2 Competency Questions and SPARQL Queries
#### CQ1
- Which audio objects have musical content?
    ```
    PREFIX mo: <http://purl.org/ontology/mo/>
        
    SELECT DISTINCT ?ddbitem ?item WHERE {  
       ?ddbobj rdf:type mo:MusicalItem ;
           dcterms:title ?title ;
           owl:sameAs ?ddbitem FILTER regex(?ddbitem, "deutsche-digitale-bibliothek", "i")
    }
    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&qtxt=++++PREFIX+mo%3A+%3Chttp%3A%2F%2Fpurl.org%2Fontology%2Fmo%2F%3E%0D%0A++++PREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A++++++++%0D%0A++++SELECT+DISTINCT+%3Fddbitem+%3Ftitle+WHERE+%7B++%0D%0A+++++++%3Fddbobj+rdf%3Atype+mo%3AMusicalItem+%3B%0D%0A+++++++++++dcterms%3Atitle+%3Ftitle+%3B%0D%0A+++++++++++owl%3AsameAs+%3Fddbitem+FILTER+regex%28%3Fddbitem%2C+%22deutsche-digitale-bibliothek%22%2C+%22i%22%29%0D%0A++++%7D&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}

#### CQ2
- How many objects in the DDB are recordings of Arias?
    ```
    PREFIX mo: <http://purl.org/ontology/mo/>
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX fabio: <http://purl.org/spar/fabio/>
        
    SELECT DISTINCT COUNT(?ddbobj) WHERE {  
       ?ddbobj rdf:type mo:MusicalItem ;
           fabio:hasSubjectTerm ?subject .
       ?subject skos:prefLabel ?subject_label FILTER regex(?subject_label, "arie", "i")
    }
    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&qtxt=++++PREFIX+mo%3A+%3Chttp%3A%2F%2Fpurl.org%2Fontology%2Fmo%2F%3E%0D%0A++++PREFIX+skos%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0A++++PREFIX+fabio%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Ffabio%2F%3E%0D%0A++++++++%0D%0A++++SELECT+DISTINCT+COUNT%28%3Fddbobj%29+WHERE+%7B++%0D%0A+++++++%3Fddbobj+rdf%3Atype+mo%3AMusicalItem+%3B%0D%0A+++++++++++fabio%3AhasSubjectTerm+%3Fsubject+.%0D%0A+++++++%3Fsubject+skos%3AprefLabel+%3Fsubject_label+FILTER+regex%28%3Fsubject_label%2C+%22arie%22%2C+%22i%22%29%0D%0A++++%7D&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}

#### CQ3
- How many objects in the DDB are recordings of animal sounds?
    ```
    PREFIX aco: <https://w3id.org/ac-ontology/aco#>
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX fabio: <http://purl.org/spar/fabio/>
        
    SELECT DISTINCT COUNT(?ddbobj) WHERE {  
       ?ddbobj rdf:type aco:AudioItem;
           fabio:hasSubjectTerm ?subject .
       ?subject skos:prefLabel ?subject_label FILTER regex(?subject_label, "tierstimme", "i")
    }
    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&qtxt=++++PREFIX+aco%3A+%3Chttps%3A%2F%2Fw3id.org%2Fac-ontology%2Faco%23%3E%0D%0A++++PREFIX+skos%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0A++++PREFIX+fabio%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Ffabio%2F%3E%0D%0A++++++++%0D%0A++++SELECT+DISTINCT+COUNT%28%3Fddbobj%29+WHERE+%7B++%0D%0A+++++++%3Fddbobj+rdf%3Atype+aco%3AAudioItem%3B%0D%0A+++++++++++fabio%3AhasSubjectTerm+%3Fsubject+.%0D%0A+++++++%3Fsubject+skos%3AprefLabel+%3Fsubject_label+FILTER+regex%28%3Fsubject_label%2C+%22tierstimme%22%2C+%22i%22%29%0D%0A++++%7D%0D%0A&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}

#### CQ4
- Are there audio books in the DDB?
    ```
    PREFIX aco: <https://w3id.org/ac-ontology/aco#>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX fabio: <http://purl.org/spar/fabio/>
        
    SELECT DISTINCT ?ddbitem ?title WHERE {  
       ?ddbobj rdf:type aco:AudioItem;
           dcterms:title ?title ;
           dcterms:type ?obj_type ;
           owl:sameAs ?ddbitem FILTER regex(?ddbitem, "deutsche-digitale-bibliothek", "i") .
       ?obj_type skos:prefLabel ?type_label FILTER regex(?type_label, "monografie", "i")
    }
    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&qtxt=++++PREFIX+aco%3A+%3Chttps%3A%2F%2Fw3id.org%2Fac-ontology%2Faco%23%3E%0D%0A++++PREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A++++PREFIX+skos%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0A++++PREFIX+fabio%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Ffabio%2F%3E%0D%0A++++++++%0D%0A++++SELECT+DISTINCT+%3Fddbitem+%3Ftitle+WHERE+%7B++%0D%0A+++++++%3Fddbobj+rdf%3Atype+aco%3AAudioItem%3B%0D%0A+++++++++++dcterms%3Atitle+%3Ftitle+%3B%0D%0A+++++++++++dcterms%3Atype+%3Fobj_type+%3B%0D%0A+++++++++++owl%3AsameAs+%3Fddbitem+FILTER+regex%28%3Fddbitem%2C+%22deutsche-digitale-bibliothek%22%2C+%22i%22%29+.%0D%0A+++++++%3Fobj_type+skos%3AprefLabel+%3Ftype_label+FILTER+regex%28%3Ftype_label%2C+%22monografie%22%2C+%22i%22%29%0D%0A++++%7D%0D%0A&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}

#### CQ5
- Are there recordings of arias from Puccini's Tosca?
    ```
    PREFIX mo: <http://purl.org/ontology/mo/>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

    SELECT DISTINCT ?ddbitem ?title WHERE {  
       ?ddbobj rdf:type mo:MusicalItem ;
           dcterms:creator ?creator ;
           dcterms:title ?title FILTER regex (?title, "tosca", "i") .
       ?ddbobj owl:sameAs ?ddbitem FILTER regex(?ddbitem, "deutsche-digitale-bibliothek", "i") .
       ?creator foaf:name ?creator_name FILTER regex(?creator_name, "puccini", "i") .
    }
    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&qtxt=PREFIX+mo%3A+%3Chttp%3A%2F%2Fpurl.org%2Fontology%2Fmo%2F%3E%0D%0A++++PREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A++++PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0A%0D%0A++++SELECT+DISTINCT+%3Fddbitem+%3Ftitle+WHERE+%7B++%0D%0A+++++++%3Fddbobj+rdf%3Atype+mo%3AMusicalItem+%3B%0D%0A+++++++++++dcterms%3Acreator+%3Fcreator+%3B%0D%0A+++++++++++dcterms%3Atitle+%3Ftitle+FILTER+regex+%28%3Ftitle%2C+%22tosca%22%2C+%22i%22%29+.%0D%0A+++++++%3Fddbobj+owl%3AsameAs+%3Fddbitem+FILTER+regex%28%3Fddbitem%2C+%22deutsche-digitale-bibliothek%22%2C+%22i%22%29+.%0D%0A+++++++%3Fcreator+foaf%3Aname+%3Fcreator_name+FILTER+regex%28%3Fcreator_name%2C+%22puccini%22%2C+%22i%22%29+.%0D%0A++++%7D&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}

#### CQ6
- How many objects were provided by museums and who are these providers?
    ```
    PREFIX mo: <http://purl.org/ontology/mo/>
    PREFIX aco: <https://w3id.org/ac-ontology/aco#>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX prov: <http://www.w3.org/ns/prov#>
    PREFIX foaf: <http://xmlns.com/foaf/0.1/>

    SELECT DISTINCT ?provider_name (COUNT(?ddbobj) as ?NumObjects) WHERE {  
       VALUES (?type) { (mo:MusicalItem) (aco:AudioItem) } 
       ?ddbobj prov:wasDerivedFrom ?dataset .
       ?dataset prov:wasAttributedTo ?provider .
       ?provider dcterms:type ?sparte ;
           foaf:name ?provider_name .
      FILTER regex(?sparte, "sparte006") 
    } GROUP BY ?provider_name
    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&qtxt=++++PREFIX+mo%3A+%3Chttp%3A%2F%2Fpurl.org%2Fontology%2Fmo%2F%3E%0D%0A++++PREFIX+aco%3A+%3Chttps%3A%2F%2Fw3id.org%2Fac-ontology%2Faco%23%3E%0D%0A++++PREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A++++PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0A++++PREFIX+prov%3A+%3Chttp%3A%2F%2Fwww.w3.org%2Fns%2Fprov%23%3E%0D%0A++++PREFIX+foaf%3A+%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0A%0D%0A++++SELECT+DISTINCT+%3Fprovider_name+%28COUNT%28%3Fddbobj%29+as+%3FNumObjects%29+WHERE+%7B++%0D%0A+++++++VALUES+%28%3Ftype%29+%7B+%28mo%3AMusicalItem%29+%28aco%3AAudioItem%29+%7D+%0D%0A+++++++%3Fddbobj+prov%3AwasDerivedFrom+%3Fdataset+.%0D%0A+++++++%3Fdataset+prov%3AwasAttributedTo+%3Fprovider+.%0D%0A+++++++%3Fprovider+dcterms%3Atype+%3Fsparte+%3B%0D%0A+++++++++++foaf%3Aname+%3Fprovider_name+.%0D%0A++++++FILTER+regex%28%3Fsparte%2C+%22sparte006%22%29+%0D%0A++++%7D+GROUP+BY+%3Fprovider_name%0D%0A&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}


---
## References
[1] Ceriani, M., Fazekas, G.: Audio Commons Ontology: A Data Model for an AudioContent Ecosystem. In: SEMWEB (2018)

[2] Peroni, S., Shotton, D.: FaBiO and CiTO: Ontologies for describing bibliographicresources and citations. Journal of Web Semantics17, 33–43 (12 2012)

[3] Raimond, Y., Abdallah, S., Sandler, M., Giasson, F.: The Music Ontology. In: ISMR.vol. 422 (09 2007)

[4] Ronchi, A.M.: eCulture: Cultural Content in the Digital Age. Springer, Berlin, Hei-delberg (2009)
