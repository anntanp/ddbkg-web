---
# Title, summary, and page position.
linktitle: Audio (MO + ACO)
summary: Alignment of DDB-EDM to MO and ACO
weight: 1
icon: book
icon_pack: fas

# Page metadata.
title: Audio Ontologies in the DDB
date: "2022-03-07T00:00:00Z"
type: book  # Do not modify.
---
## Introduction
The vast collection of the German Digital Company (DDB) includes objects that the UNESCO cultural heritage (CH) hierarchy (Ronchi, 2011) classified as intangible. Examples of intangible objects include musical works, natural heritage, oral traditions, to name a few. These are often digitized as audio or video.

Audio content in the DDB can be found across several sectors: audio books from libraries, interviews of significant German personalities from research institutions, commercial jingles from archives, recordings of animal sounds from natural museums and music from gramophone records often found in multimedia libraries. The audio files can be classified into two broad  (2) categories:

1.  **Work** - audio files containing intellectual or artistic content, such as Music, and Ebooks. 
     
2.  **Non-Work** - audio files without intellectual or artistic content, such as as bird songs, and machinery sounds.

The types of audio files are encoded in the [dc:type](http://purl.org/dc/elements/1.1/type) or [edm:hasType](http://www.europeana.eu/schemas/edm/hasType) data properties.  Below is the list of these terms and the number of objects associated with them. Note that the 

{{< gdocs src="https://docs.google.com/spreadsheets/d/1_iN1W2Xo5WyYIQ3sgfDOcOeBvgZ_MkaBsL-7JTCKiUU/edit?usp=sharing" >}}

To determine whether the audio file is a *Work* or *Non-Work*, the values encoded by the data property [dc:subject](http://purl.org/dc/elements/1.1/subject) are inspected. There are approximately 3,700 unique terms relating to the object's subject or topic, however, only terms with frequency counts in the thousands were used. These terms are as follows: 

1.  Work - *Lied* (Song), *Duett* (Duet), *Arie* (Arias), *Oper* (Opera), *Erzählende Literatur* (Audio Books), *Werbesendung* (Ads)
2.  Non-Work - *Tierstimme* (Animal Sounds), *Tonaufname* (Sound Recording)

## Ontologies
To be able to represent the semantics of these diverse objects, the selection of the target ontologies is based on the following considerations: interoperability, suitability to the domain, and the application profile.

In the case of audio books, adapting a FRBR-aligned ontology facilitates interoperability, by considering them as  expressions of their respective literary works. The same holds true for any musical composition and its text; for instance, a recording of Carl Orff's Carmina Burana is considered an expression of the 13*th* century manuscript containing a collection of poems it was based on.

### FaBiO
Although, [FaBiO](https://sparontologies.github.io/fabio/current/fabio.html) (Peroni et al., 2012), as a FRBR-aligned bibliographic ontology, provides subclasses relating to musical works [fabio:Song](https://sparontologies.github.io/fabio/current/fabio.html#d4e5392), [fabio:MusicalComposition](https://sparontologies.github.io/fabio/current/fabio.html#d4e4227) and their expression [fabio:AudioDocument](https://sparontologies.github.io/fabio/current/fabio.html#d4e2145), these subclasses cannot represent the full range of audio content described above (Figure [1](#docs-audio-fig1)). 

{{< figure src="https://ise-fizkarlsruhe.github.io/ddbkg/images/audio-in-fabio.jpg" caption="FaBiO Classes for Audio Files" numbered="true" id="docs-audio-fig1" >}}.

### Music Ontology (MO)
[MO](http://musicontology.com/specification/) (Raimond et al., 2007) aims to model the semantics of music production workflows and their editorial metadata. FRBR plays a central role in the definition of its classes. Parallels can be drawn between the super-classes of MO ([mo:MusicalWork](http://musicontology.com/specification/#term-MusicalWork), [mo:MusicalExpression](http://musicontology.com/specification/#term-MusicalExpression), [mo:MusicalManifestation](http://musicontology.com/specification/#term-MusicalManifestation), and [mo:MusicalItem](http://musicontology.com/specification/#term-MusicalItem) and the 4 conceptual layers of FRBR. Since the original intention of the authors is to model the different workflows, events are central to this ontology. Entities that are usually found as attributes of a [frbr:Endeavor](https://vocab.org/frbr/core#term-Endeavour) sub-class require intermediate events to link them to that endeavor: the attribution of an *mo:MusicalArtist* (Agent) to its [mo:MusicalWork](http://musicontology.com/specification/#term-MusicalWork)) requires an instance of the [mo:Composition](http://musicontology.com/specification/#term-Composition) event, in contrast to the widely-adopted convention of linking agents directly to the [frbr:Work](https://vocab.org/frbr/core#term-Work).

{{< figure src="https://ise-fizkarlsruhe.github.io/ddbkg/images/audio-in-mo.jpg" caption="MO Classes for Audio Files" numbered="true" id="docs-audio-fig2" >}}.


### Audio Commons Ontology (ACO)
As mentioned, not all audio content in the DDB possess intellectual or artistic content. Examples of these are natural sounds and field recordings. An ontology that  provides classes and properties to allow representations of non-musical audio content exists in [ACO](https://w3id.org/ac-ontology/aco#AudioExpression) (Ceriani et al., 2018). Being an upper-level ontology for audio content, the authors' initial intention is to provide interoperability across repositories on the Web. The FRBR-aligned classes of ACO are generalizations of MO classes. However, a FRBR Work sub-class specific to ACO was not defined, since it does not generalize to all types of sounds. Similarly to MO, events also play an central role in ACO.

## Alignment
The decision to forego the usage of [owl:Event](http://motools.sourceforge.net/event/event.html#term_Event) sub-classes, namely, [mo:Composition](http://musicontology.com/specification/#term-Composition), [mo:Performance](http://musicontology.com/specification/#term-Performance), and [mo:Recording](http://musicontology.com/specification/#term-Recording), can be explained by the application profile and dataset of the DDB. The intention to publish metadata describing the CHOs for the purpose of retrieval and exploration means that details of events that are relevant for music or sound production are rarely included in the data provided by participating institutions. For instance, the description of a gramophone record includes the names of the composer, performer/s and publisher. However, details of the performance of this specific record which is crucial when modeling a music production workflow is not available. If event-centric modeling is followed, the additional entities representing events such as [mo:Composition](http://musicontology.com/specification/#term-Composition) or [mo:Performance](http://musicontology.com/specification/#term-Performance) will serve no purpose, since the relationship between entities of the endeavor and the event will always be 1:1. Thus, the attributes that may be attached to the event can be defined as object or data properties of the involved endeavor entities. As a result, the generic property [dcterms:contributor]() is used in lieu of [mo:performer](http://musicontology.com/specification/#term-performer), since the latter strictly defines the domain to be of class [mo:Performance](http://musicontology.com/specification/#term-Performance), an event which is not utilized in the alignment.

##### Simplified (Music)
{{< figure src="https://ise-fizkarlsruhe.github.io/ddbkg/images/ddbedm-to-mo-aco.jpg" caption="Alignment to Target Ontologies (simplified)" numbered="true" id="docs-audio-fig3" >}}.


### Detailed (Music)
Figure [3](#docs-audio-fig3) illustrates the alignment with object and data properties. From the source data encoded in [xml](https://www.deutsche-digitale-bibliothek.de/item/xml/ILNOJIJWFWN3WFHQBS6RXI4QJ3BOXZVV), the resulting alignment is shown in this [turtle file](https://ise-fizkarlsruhe.github.io/ddbkg/data/sample-music.ttl).

{{< figure src="https://ise-fizkarlsruhe.github.io/ddbkg/images/mo-aco-detailed-music.jpg" caption="Alignment to Target Ontologies of Musical Audio Content (detailed)" numbered="true" id="docs-audio-fig4" >}}.


### Detailed (Non-Musical)
{{< figure src="https://ise-fizkarlsruhe.github.io/ddbkg/images/mo-aco-detailed-birdsong.jpg" caption="Alignment to Target Ontologies of Non-Musical Audio Content (detailed)" numbered="true" id="docs-audio-fig3" >}}.

## References:
[1] Ceriani, M., Fazekas, G.: Audio Commons Ontology: A Data Model for an AudioContent Ecosystem. In: SEMWEB (2018)

[2] Peroni, S., Shotton, D.: FaBiO and CiTO: Ontologies for describing bibliographicresources and citations. Journal of Web Semantics17, 33–43 (12 2012)

[3] Raimond, Y., Abdallah, S., Sandler, M., Giasson, F.: The Music Ontology. In: ISMR.vol. 422 (09 2007)

[4] Ronchi, A.M.: eCulture: Cultural Content in the Digital Age. Springer, Berlin, Hei-delberg (2009)
