---
# Title, summary, and page position.
linktitle: Examples
summary: Example SPARQL Queries based on a few competency questions.
weight: 2
icon: book
icon_pack: fas

# Page metadata.
title: Competency Questions and sample SPARQL Queries
date: "2021-08-25T00:00:00Z"
type: book  # Do not modify.
---
### CQ1
  - Look for all works of author "Schiller"
    ```
    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX gnd: <http://d-nb.info/gnd/>
    PREFIX gndo: <http://d-nb.info/standards/elementset/gnd#>
    PREFIX fabio: <http://purl.org/spar/fabio/>
    PREFIX frbr: <http://purl.org/vocab/frbr/core#>
    PREFIX foaf: <http://xmlns.com/foaf/0.1/>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    
    SELECT DISTINCT ?title ?work ?author
    WHERE {
      ?work rdf:type fabio:Work ;
        dcterms:title ?title ;
        dcterms:creator ?author .
      ?author foaf:name ?author_name FILTER regex(?author_name, "Schiller", "i") .
    }
    ```
  {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&query=PREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+gnd%3A+%3Chttp%3A%2F%2Fd-nb.info%2Fgnd%2F%3E%0D%0APREFIX+gndo%3A+%3Chttp%3A%2F%2Fd-nb.info%2Fstandards%2Felementset%2Fgnd%23%3E%0D%0APREFIX+fabio%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Ffabio%2F%3E%0D%0APREFIX+frbr%3A+%3Chttp%3A%2F%2Fpurl.org%2Fvocab%2Ffrbr%2Fcore%23%3E%0D%0APREFIX+foaf%3A+%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A++++%0D%0ASELECT+DISTINCT+%3Ftitle+%3Fwork+%3Fauthor%0D%0AWHERE+%7B%0D%0A++%3Fwork+rdf%3Atype+fabio%3AWork+%3B%0D%0A++++dcterms%3Atitle+%3Ftitle+%3B%0D%0A++++dcterms%3Acreator+%3Fauthor+.%0D%0A++%3Fauthor+foaf%3Aname+%3Fauthor_name+FILTER+regex%28%3Fauthor_name%2C+%22Schiller%22%2C+%22i%22%29+.%0D%0A%7D&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}
  {{% staticref "https://ise-fizkarlsruhe.github.io/ddbkg/cq/cq01.html" "newtab" %}}Download Results{{% /staticref %}}

----
### CQ2   
  - Look for all items created by "Schiller" with title "Räuber", exclude partial objects.
    ```
    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX gnd: <http://d-nb.info/gnd/>
    PREFIX gndo: <http://d-nb.info/standards/elementset/gnd#>
    PREFIX fabio: <http://purl.org/spar/fabio/>
    PREFIX frbr: <http://purl.org/vocab/frbr/core#>
    PREFIX foaf: <http://xmlns.com/foaf/0.1/>
    PREFIX dcterms: <http://purl.org/dc/terms/>
        
    SELECT DISTINCT ?ddbitem ?title ?author
    WHERE {
      ?ddbitem rdf:type fabio:AnalogItem .
      ?ddbitem dcterms:creator ?author FILTER (
         !EXISTS {
           ?ddbitem dcterms:isPartOf ?parent
         }
      )
      ?author foaf:name ?author_name FILTER regex(str(?author_name), "Schiller", "i") .
      ?ddbitem dcterms:title ?title FILTER regex(?title, "Räuber", "i") .
    }
    ```
  {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&query=PREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+gnd%3A+%3Chttp%3A%2F%2Fd-nb.info%2Fgnd%2F%3E%0D%0APREFIX+gndo%3A+%3Chttp%3A%2F%2Fd-nb.info%2Fstandards%2Felementset%2Fgnd%23%3E%0D%0APREFIX+fabio%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Ffabio%2F%3E%0D%0APREFIX+frbr%3A+%3Chttp%3A%2F%2Fpurl.org%2Fvocab%2Ffrbr%2Fcore%23%3E%0D%0APREFIX+foaf%3A+%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A++++++++%0D%0ASELECT+DISTINCT+%3Fddbitem+%3Ftitle+%3Fauthor%0D%0AWHERE+%7B%0D%0A++%3Fddbitem+rdf%3Atype+fabio%3AAnalogItem+%3B%0D%0A++++dcterms%3Acreator+%3Fauthor+FILTER+%28%0D%0A+++++%21EXISTS+%7B%0D%0A+++++++%3Fddbitem+dcterms%3AisPartOf+%3Fparent%0D%0A+++++%7D%0D%0A++%29%0D%0A++%3Fauthor+foaf%3Aname+%3Fauthor_name+FILTER+regex%28str%28%3Fauthor_name%29%2C+%22Schiller%22%2C+%22i%22%29+.%0D%0A++%3Fddbitem+dcterms%3Atitle+%3Ftitle+FILTER+regex%28%3Ftitle%2C+%22Räuber%22%2C+%22i%22%29+.%0D%0A%7D%0D%0A&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}
  {{% staticref "https://ise-fizkarlsruhe.github.io/ddbkg/cq/cq02.html" "newtab" %}}Download Results{{% /staticref %}}

---
### CQ3

  - Look for digitized copies of "Die Räuber"
    ```
    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX gnd: <http://d-nb.info/gnd/>
    PREFIX gndo: <http://d-nb.info/standards/elementset/gnd#>
    PREFIX fabio: <http://purl.org/spar/fabio/>
    PREFIX frbr: <http://purl.org/vocab/frbr/core#>
    PREFIX foaf: <http://xmlns.com/foaf/0.1/>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    
    SELECT DISTINCT ?title ?ddbitem ?type ?epub
    WHERE {
      ?work rdf:type fabio:Work ;
            fabio:hasRealization ?expression .
      ?expression fabio:hasRepresentation ?ddbitem ;
            dcterms:title ?title 
            FILTER regex(?title, "Die Räuber", "i") .
      ?ddbitem dcterms:type ?type ;
            fabio:hasReproduction ?di .
      ?di fabio:isExemplarOf ?epub .        
    }
    ```
   {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&query=PREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+gnd%3A+%3Chttp%3A%2F%2Fd-nb.info%2Fgnd%2F%3E%0D%0APREFIX+gndo%3A+%3Chttp%3A%2F%2Fd-nb.info%2Fstandards%2Felementset%2Fgnd%23%3E%0D%0APREFIX+fabio%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Ffabio%2F%3E%0D%0APREFIX+frbr%3A+%3Chttp%3A%2F%2Fpurl.org%2Fvocab%2Ffrbr%2Fcore%23%3E%0D%0APREFIX+foaf%3A+%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A++++%0D%0ASELECT+DISTINCT+%3Ftitle+%3Fddbitem+%3Ftype+%3Fepub%0D%0AWHERE+%7B%0D%0A++%3Fwork+rdf%3Atype+fabio%3AWork+%3B%0D%0A++++++++fabio%3AhasRealization+%3Fexpression+.%0D%0A++%3Fexpression+fabio%3AhasRepresentation+%3Fddbitem+%3B%0D%0A++++++++dcterms%3Atitle+%3Ftitle+%0D%0A++++++++FILTER+regex%28%3Ftitle%2C+%22Die+Räuber%22%2C+%22i%22%29+.%0D%0A++%3Fddbitem+dcterms%3Atype+%3Ftype+%3B%0D%0A++++++++fabio%3AhasReproduction+%3Fdi+.%0D%0A++%3Fdi+fabio%3AisExemplarOf+%3Fepub+.++++++++%0D%0A%7D&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}
   {{% staticref "https://ise-fizkarlsruhe.github.io/ddbkg/cq/cq03.html" "newtab" %}}Download Results{{% /staticref %}}

---

### CQ4
  - What are the works of Thomas Mann and the DDB primary objects associated with them?
    ```
    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX gnd: <http://d-nb.info/gnd/>
    PREFIX gndo: <http://d-nb.info/standards/elementset/gnd#>
    PREFIX fabio: <http://purl.org/spar/fabio/>
    PREFIX frbr: <http://purl.org/vocab/frbr/core#>
    PREFIX foaf: <http://xmlns.com/foaf/0.1/>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    
    SELECT DISTINCT ?title ?ddbitem
    WHERE {
      ?work rdf:type fabio:Work .
      ?work fabio:hasPortrayal ?ddbitem FILTER (
         !EXISTS {
           ?ddbitem dcterms:isPartOf ?parent
         }
      ) .
      ?work dcterms:creator ?author .
      ?author foaf:name ?author_name FILTER (regex(?author_name, "Thomas Mann", "i") || regex(?author_name, "Mann, Thomas", "i")).
      ?work dcterms:title ?title .
    }
    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&query=PREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0A++++PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0A++++PREFIX+gnd%3A+%3Chttp%3A%2F%2Fd-nb.info%2Fgnd%2F%3E%0D%0A++++PREFIX+gndo%3A+%3Chttp%3A%2F%2Fd-nb.info%2Fstandards%2Felementset%2Fgnd%23%3E%0D%0A++++PREFIX+fabio%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Ffabio%2F%3E%0D%0A++++PREFIX+frbr%3A+%3Chttp%3A%2F%2Fpurl.org%2Fvocab%2Ffrbr%2Fcore%23%3E%0D%0A++++PREFIX+foaf%3A+%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0A++++PREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A++++%0D%0A++++SELECT+DISTINCT+%3Ftitle+%3Fddbitem%0D%0A++++WHERE+%7B%0D%0A++++++%3Fwork+rdf%3Atype+fabio%3AWork+.%0D%0A++++++%3Fwork+fabio%3AhasPortrayal+%3Fddbitem+FILTER+%28%0D%0A+++++++++%21EXISTS+%7B%0D%0A+++++++++++%3Fddbitem+dcterms%3AisPartOf+%3Fparent%0D%0A+++++++++%7D%0D%0A++++++%29+.%0D%0A++++++%3Fwork+dcterms%3Acreator+%3Fauthor+.%0D%0A++++++%3Fauthor+foaf%3Aname+%3Fauthor_name+FILTER+%28regex%28str%28%3Fauthor_name%29%2C+%22Thomas+Mann%22%2C+%22i%22%29+%7C%7C+regex%28str%28%3Fauthor_name%29%2C+%22Mann%2C+Thomas%22%2C+%22i%22%29%29.%0D%0A++++++%3Fwork+dcterms%3Atitle+%3Ftitle+.%0D%0A++++%7D&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}
    {{% staticref "https://ise-fizkarlsruhe.github.io/ddbkg/cq/cq04.html" "newtab" %}}Download Results{{% /staticref %}}

---

### CQ5
  - Which languages was Johann Wolfgang von Goethe's Faust was translated into and how many objects exist per translations?
    ```
    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX gnd: <http://d-nb.info/gnd/>
    PREFIX gndo: <http://d-nb.info/standards/elementset/gnd#>
    PREFIX fabio: <http://purl.org/spar/fabio/>
    PREFIX frbr: <http://purl.org/vocab/frbr/core#>
    PREFIX foaf: <http://xmlns.com/foaf/0.1/>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    
    SELECT DISTINCT ?lang (COUNT (?lang) as ?items)
    WHERE {
      ?expression dcterms:creator ?author .
      ?author foaf:name ?author_name FILTER (regex(?author_name, "Johann Wolfgang von Goethe", "i") || regex(str(?author_name), "Goethe, Johann Wolfgang von", "i")) .
      ?expression dcterms:title ?title FILTER regex(?title, "Faust", "i") .
      ?expression dcterms:language ?lang .
      ?expression fabio:hasRepresentation ?ddbitem FILTER (
         !EXISTS {
           ?ddbitem dcterms:isPartOf ?parent
         }
      ) .
    } GROUP BY ?lang
    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&query=PREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+gnd%3A+%3Chttp%3A%2F%2Fd-nb.info%2Fgnd%2F%3E%0D%0APREFIX+gndo%3A+%3Chttp%3A%2F%2Fd-nb.info%2Fstandards%2Felementset%2Fgnd%23%3E%0D%0APREFIX+fabio%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Ffabio%2F%3E%0D%0APREFIX+frbr%3A+%3Chttp%3A%2F%2Fpurl.org%2Fvocab%2Ffrbr%2Fcore%23%3E%0D%0APREFIX+foaf%3A+%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A++++%0D%0ASELECT+DISTINCT+%3Flang+%28COUNT+%28%3Flang%29+as+%3Fitems%29%0D%0AWHERE+%7B%0D%0A++%3Fexpression+dcterms%3Acreator+%3Fauthor+.%0D%0A++%3Fauthor+foaf%3Aname+%3Fauthor_name+FILTER+%28regex%28str%28%3Fauthor_name%29%2C+%22Johann+Wolfgang+von+Goethe%22%2C+%22i%22%29+%7C%7C+regex%28str%28%3Fauthor_name%29%2C+%22Goethe%2C+Johann+Wolfgang+von%22%2C+%22i%22%29%29+.%0D%0A++%3Fexpression+dcterms%3Atitle+%3Ftitle+FILTER+regex%28str%28%3Ftitle%29%2C+%22Faust%22%2C+%22i%22%29+.%0D%0A++%3Fexpression+dcterms%3Alanguage+%3Flang+.%0D%0A++%3Fexpression+fabio%3AhasRepresentation+%3Fddbitem+FILTER+%28%0D%0A+++++%21EXISTS+%7B%0D%0A+++++++%3Fddbitem+dcterms%3AisPartOf+%3Fparent%0D%0A+++++%7D%0D%0A++%29+.%0D%0A%7D+GROUP+BY+%3Flang&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}
    {{% staticref "https://ise-fizkarlsruhe.github.io/ddbkg/cq/cq05.html" "newtab" %}}Download Results{{% /staticref %}}

---

### CQ6
  - Look for all notable works of Friedrich Schiller as listed in DBPedia that are available in the DDB.
    ```
    PREFIX dct: <http://purl.org/dc/terms/>
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX dbc: <http://dbpedia.org/resource/Category:>
    PREFIX dbo: <http://dbpedia.org/ontology/>
    PREFIX fabio: <http://purl.org/spar/fabio/>
    PREFIX foaf: <http://xmlns.com/foaf/0.1/>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    PREFIX wdt: <http://www.wikidata.org/prop/direct/>
    PREFIX schema: <http://www.schema.org/>
    PREFIX frbr: <http://purl.org/vocab/frbr/core#>
    
    SELECT DISTINCT ?workLabel ?ddbitem ?digitized ?owner ?ownerName ?thumbnail WHERE {  
        SERVICE <http://dbpedia.org/sparql> {
          ?s rdfs:label "Friedrich Schiller"@de .
          ?s dbo:notableWork ?notableWork .
          ?notableWork rdfs:label ?workLabel FILTER (LANG(?workLabel)="de") .      
       }
       ?ddbitem rdf:type fabio:AnalogItem FILTER (
         !EXISTS {
           ?ddbitem dcterms:isPartOf ?parent
         }
      )
       ?ddbitem dcterms:title ?title FILTER regex(?title, ?workLabel, "i") .
       ?ddbitem fabio:hasReproduction ?digitizedItem .
       ?digitizedItem fabio:isExemplarOf ?digitized .
       ?digitized frbr:owner ?owner .
       optional { ?owner foaf:name ?ownerName }
       optional { ?digitizedItem schema:thumbnail ?thumbnail }
    }

    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&query=PREFIX+dct%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0APREFIX+skos%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0APREFIX+dbc%3A+%3Chttp%3A%2F%2Fdbpedia.org%2Fresource%2FCategory%3A%3E%0D%0APREFIX+dbo%3A+%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0APREFIX+fabio%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Ffabio%2F%3E%0D%0APREFIX+foaf%3A+%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0APREFIX+wdt%3A+%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%0D%0APREFIX+schema%3A+%3Chttp%3A%2F%2Fwww.schema.org%2F%3E%0D%0APREFIX+frbr%3A+%3Chttp%3A%2F%2Fpurl.org%2Fvocab%2Ffrbr%2Fcore%23%3E%0D%0A++++%0D%0ASELECT+DISTINCT+%3FworkLabel+%3Fddbitem+%3Fdigitized+%3Fowner+%3FownerName+%3Fthumbnail+WHERE+%7B++%0D%0A++++SERVICE+%3Chttp%3A%2F%2Fdbpedia.org%2Fsparql%3E+%7B%0D%0A++++++%3Fs+rdfs%3Alabel+%22Friedrich+Schiller%22%40de+.%0D%0A++++++%3Fs+dbo%3AnotableWork+%3FnotableWork+.%0D%0A++++++%3FnotableWork+rdfs%3Alabel+%3FworkLabel+FILTER+%28LANG%28%3FworkLabel%29%3D%22de%22%29+.++++++%0D%0A+++%7D%0D%0A+++%3Fddbitem+rdf%3Atype+fabio%3AAnalogItem+FILTER+%28%0D%0A+++++%21EXISTS+%7B%0D%0A+++++++%3Fddbitem+dcterms%3AisPartOf+%3Fparent%0D%0A+++++%7D%0D%0A++%29%0D%0A+++%3Fddbitem+dcterms%3Atitle+%3Ftitle+FILTER+regex%28%3Ftitle%2C+%3FworkLabel%2C+%22i%22%29+.%0D%0A+++%3Fddbitem+fabio%3AhasReproduction+%3FdigitizedItem+.%0D%0A+++%3FdigitizedItem+fabio%3AisExemplarOf+%3Fdigitized+.%0D%0A+++%3Fdigitized+frbr%3Aowner+%3Fowner+.%0D%0A+++optional+%7B+%3Fowner+foaf%3Aname+%3FownerName+%7D%0D%0A+++optional+%7B+%3FdigitizedItem+schema%3Athumbnail+%3Fthumbnail+%7D%0D%0A%7D&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}

---
    
### CQ7
  - What are the notable works ([wdt:p800](https://www.wikidata.org/wiki/Property:P800)) according to Wikidata?
    ```
    PREFIX dct: <http://purl.org/dc/terms/>
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX dbc: <http://dbpedia.org/resource/Category:>
    PREFIX dbo: <http://dbpedia.org/ontology/>
    PREFIX fabio: <http://purl.org/spar/fabio/>
    PREFIX foaf: <http://xmlns.com/foaf/0.1/>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    PREFIX wdt: <http://www.wikidata.org/prop/direct/>
    PREFIX wd: <http://www.wikidata.org/entity/>
    PREFIX schema: <http://www.schema.org/>
    PREFIX frbr: <http://purl.org/vocab/frbr/core#>
        
    SELECT DISTINCT ?workLabel ?ownerName ?ddbitem ?digitized ?thumbnail WHERE {  
        SERVICE <https://query.wikidata.org/sparql> {
          wd:Q22670 wdt:P800 ?notableWork . #Friedrich Schiller
          ?notableWork rdfs:label ?workLabel FILTER (LANG(?workLabel)="de") .      
       }
       ?ddbitem rdf:type fabio:AnalogItem FILTER (
         !EXISTS {
           ?ddbitem dcterms:isPartOf ?parent
         }
      )
       ?ddbitem dcterms:title ?title FILTER regex(?title, ?workLabel, "i") .
       ?ddbitem fabio:hasReproduction ?digitizedItem .
       ?digitizedItem fabio:isExemplarOf ?digitized .
       ?digitized frbr:owner ?owner .
       optional { ?owner foaf:name ?ownerName }
       optional { ?digitizedItem schema:thumbnail ?thumbnail }
    }
    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&qtxt=PREFIX+dct%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0APREFIX+skos%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0APREFIX+dbc%3A+%3Chttp%3A%2F%2Fdbpedia.org%2Fresource%2FCategory%3A%3E%0D%0APREFIX+dbo%3A+%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0APREFIX+fabio%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Ffabio%2F%3E%0D%0APREFIX+foaf%3A+%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0APREFIX+wdt%3A+%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%0D%0APREFIX+wd%3A+%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%0D%0APREFIX+schema%3A+%3Chttp%3A%2F%2Fwww.schema.org%2F%3E%0D%0APREFIX+frbr%3A+%3Chttp%3A%2F%2Fpurl.org%2Fvocab%2Ffrbr%2Fcore%23%3E%0D%0A++++%0D%0ASELECT+DISTINCT+%3FworkLabel+%3FownerName+%3Fddbitem+%3Fdigitized+%3Fthumbnail+WHERE+%7B++%0D%0A++++SERVICE+%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E+%7B%0D%0A++++++wd%3AQ22670+wdt%3AP800+%3FnotableWork+.+%23Friedrich+Schiller%0D%0A++++++%3FnotableWork+rdfs%3Alabel+%3FworkLabel+FILTER+%28LANG%28%3FworkLabel%29%3D%22de%22%29+.++++++%0D%0A+++%7D%0D%0A+++%3Fddbitem+rdf%3Atype+fabio%3AAnalogItem+FILTER+%28%0D%0A+++++%21EXISTS+%7B%0D%0A+++++++%3Fddbitem+dcterms%3AisPartOf+%3Fparent%0D%0A+++++%7D%0D%0A++%29%0D%0A+++%3Fddbitem+dcterms%3Atitle+%3Ftitle+FILTER+regex%28%3Ftitle%2C+%3FworkLabel%2C+%22i%22%29+.%0D%0A+++%3Fddbitem+fabio%3AhasReproduction+%3FdigitizedItem+.%0D%0A+++%3FdigitizedItem+fabio%3AisExemplarOf+%3Fdigitized+.%0D%0A+++%3Fdigitized+frbr%3Aowner+%3Fowner+.%0D%0A+++optional+%7B+%3Fowner+foaf%3Aname+%3FownerName+%7D%0D%0A+++optional+%7B+%3FdigitizedItem+schema%3Athumbnail+%3Fthumbnail+%7D%0D%0A%7D&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}
    {{% staticref "https://ise-fizkarlsruhe.github.io/ddbkg/cq/sunburst.html" "newtab" %}}Download Results{{% /staticref %}}

---

### CQ8
  - Have there been stage performances of Friedrich Schiller's works plays? (with [Linked Stage Graph](https://codingdavinci.de/de/projekte/linked-stage-graph) lookup)
    ```
    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX fabio: <http://purl.org/spar/fabio/>
    PREFIX frbr: <http://purl.org/vocab/frbr/core#>
    PREFIX foaf: <http://xmlns.com/foaf/0.1/>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    
    SELECT DISTINCT ?title ?lsgUri ?date ?desc (COUNT(?image) AS ?images)
    WHERE {
       ?ddbitem a fabio:Work ;
         dcterms:title ?title ;
         dcterms:creator ?author .
       ?author foaf:name ?author_name 
       FILTER regex(?author_name, "Schiller, Friedrich", "i") .
    
       SERVICE <https://slod.fiz-karlsruhe.de/sparql> {
          ?lsgUri dcterms:title ?lsgTitle ;
             foaf:depiction ?image ;  
             dcterms:date ?date ;
             dcterms:description ?desc .
       }
       
      FILTER regex(?lsgTitle, ?title, "i") .
    
    }
    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&qtxt=PREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+fabio%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Ffabio%2F%3E%0D%0APREFIX+frbr%3A+%3Chttp%3A%2F%2Fpurl.org%2Fvocab%2Ffrbr%2Fcore%23%3E%0D%0APREFIX+foaf%3A+%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A%0D%0ASELECT+DISTINCT+%3Ftitle+%3FlsgUri+%3Fdate+%3Fdesc+%28COUNT%28%3Fimage%29+AS+%3Fimages%29%0D%0AWHERE+%7B%0D%0A+++%3Fddbitem+a+fabio%3AWork+%3B%0D%0A+++++dcterms%3Atitle+%3Ftitle+%3B%0D%0A+++++dcterms%3Acreator+%3Fauthor+.%0D%0A+++%3Fauthor+foaf%3Aname+%3Fauthor_name+%0D%0A+++FILTER+regex%28%3Fauthor_name%2C+%22Schiller%2C+Friedrich%22%2C+%22i%22%29+.%0D%0A%0D%0A+++SERVICE+%3Chttps%3A%2F%2Fslod.fiz-karlsruhe.de%2Fsparql%3E+%7B%0D%0A++++++%3FlsgUri+dcterms%3Atitle+%3FlsgTitle+%3B%0D%0A+++++++++foaf%3Adepiction+%3Fimage+%3B++%0D%0A+++++++++dcterms%3Adate+%3Fdate+%3B%0D%0A+++++++++dcterms%3Adescription+%3Fdesc+.%0D%0A+++%7D%0D%0A+++%0D%0A++FILTER+regex%28%3FlsgTitle%2C+%3Ftitle%2C+%22i%22%29+.%0D%0A%0D%0A%7D&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}
    {{% staticref "https://ise-fizkarlsruhe.github.io/ddbkg/cq/lsg.html" "newtab" %}}Download Results{{% /staticref %}}

---

### CQ9
  - Look for Schiller's Jeanne D'Arc (with [Wikidata](https://www.wikidata.org/wiki/Wikidata:Main_Page) lookup)
    ```
    PREFIX dct: <http://purl.org/dc/terms/>
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX fabio: <http://purl.org/spar/fabio/>
    PREFIX foaf: <http://xmlns.com/foaf/0.1/>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    PREFIX wdt: <http://www.wikidata.org/prop/direct/>
    PREFIX wd: <http://www.wikidata.org/entity/>
        
    SELECT DISTINCT ?altName  ?author_name ?title ?ddbitem WHERE {  
        SERVICE <https://query.wikidata.org/sparql> {
          wd:Q7226 skos:altLabel ?altName FILTER(lang(?altName)="de").
       }
       ?ddbitem dcterms:title ?title FILTER regex(?title, SUBSTR(?altName,1,12), "i") .
       ?ddbitem dcterms:creator ?author .
       ?author foaf:name ?author_name FILTER regex(?author_name, "Friedrich Schiller", "i") .
    }
    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&qtxt=PREFIX+dct%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A++++PREFIX+skos%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0A++++PREFIX+fabio%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Ffabio%2F%3E%0D%0A++++PREFIX+foaf%3A+%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0A++++PREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A++++PREFIX+wdt%3A+%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%0D%0A++++PREFIX+wd%3A+%3Chttp%3A%2F%2Fwww.wikidata.org%2Fentity%2F%3E%0D%0A++++++++%0D%0A++++SELECT+DISTINCT+%3FaltName++%3Fauthor_name+%3Ftitle+%3Fddbitem+WHERE+%7B++%0D%0A++++++++SERVICE+%3Chttps%3A%2F%2Fquery.wikidata.org%2Fsparql%3E+%7B%0D%0A++++++++++wd%3AQ7226+skos%3AaltLabel+%3FaltName+FILTER%28lang%28%3FaltName%29%3D%22de%22%29.%0D%0A+++++++%7D%0D%0A+++++++%3Fddbitem+dcterms%3Atitle+%3Ftitle+FILTER+regex%28%3Ftitle%2C+SUBSTR%28%3FaltName%2C1%2C12%29%2C+%22i%22%29+.%0D%0A+++++++%3Fddbitem+dcterms%3Acreator+%3Fauthor+.%0D%0A+++++++%3Fauthor+foaf%3Aname+%3Fauthor_name+FILTER+regex%28%3Fauthor_name%2C+%22Friedrich+Schiller%22%2C+%22i%22%29+.%0D%0A++++%7D&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}

---

### CQ10
  - Look for items by other authors belonging to the same literary movement as Friedrich Schiller (with [DBPedia](https://www.dbpedia.org) lookup)
    ```
    PREFIX dct: <http://purl.org/dc/terms/>
    PREFIX skos: <http://www.w3.org/2004/02/skos/core#>
    PREFIX dbc: <http://dbpedia.org/resource/Category:>
    PREFIX dbo: <http://dbpedia.org/ontology/>
    PREFIX fabio: <http://purl.org/spar/fabio/>
    PREFIX foaf: <http://xmlns.com/foaf/0.1/>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    PREFIX wdt: <http://www.wikidata.org/prop/direct/>
    PREFIX schema: <http://www.schema.org/>
    PREFIX frbr: <http://purl.org/vocab/frbr/core#>
        
    SELECT DISTINCT ?otherAuthors ?title ?ddbitem WHERE {  
        SERVICE <http://dbpedia.org/sparql> {
          ?s rdfs:label "Friedrich Schiller"@de .
          ?s dbo:movement ?movement .
          ?other dbo:movement ?othermovement .
          ?other rdfs:label ?otherAuthors FILTER (LANG(?otherAuthors)="de") .
          FILTER ((?movement = ?othermovement) AND (?other != ?s))
       }
    
       ?ddbitem rdf:type fabio:AnalogItem FILTER (
         !EXISTS {
           ?ddbitem dcterms:isPartOf ?parent
         }
      )
       ?ddbitem dcterms:title ?title ;
          dcterms:creator ?creator .
       ?creator a foaf:Person ;
          foaf:lastName ?lastName ;
          foaf:givenName ?firstName .
       BIND (CONCAT(?firstName, " ", ?lastName) AS ?ddbName ).
       FILTER regex(?ddbName, ?otherAuthors, "i")
    }
    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&qtxt=PREFIX+dct%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0APREFIX+skos%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2004%2F02%2Fskos%2Fcore%23%3E%0D%0APREFIX+dbc%3A+%3Chttp%3A%2F%2Fdbpedia.org%2Fresource%2FCategory%3A%3E%0D%0APREFIX+dbo%3A+%3Chttp%3A%2F%2Fdbpedia.org%2Fontology%2F%3E%0D%0APREFIX+fabio%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Ffabio%2F%3E%0D%0APREFIX+foaf%3A+%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0APREFIX+wdt%3A+%3Chttp%3A%2F%2Fwww.wikidata.org%2Fprop%2Fdirect%2F%3E%0D%0APREFIX+schema%3A+%3Chttp%3A%2F%2Fwww.schema.org%2F%3E%0D%0APREFIX+frbr%3A+%3Chttp%3A%2F%2Fpurl.org%2Fvocab%2Ffrbr%2Fcore%23%3E%0D%0A++++%0D%0ASELECT+DISTINCT+%3FotherAuthors+%3Ftitle+%3Fddbitem+WHERE+%7B++%0D%0A++++SERVICE+%3Chttp%3A%2F%2Fdbpedia.org%2Fsparql%3E+%7B%0D%0A++++++%3Fs+rdfs%3Alabel+%22Friedrich+Schiller%22%40de+.%0D%0A++++++%3Fs+dbo%3Amovement+%3Fmovement+.%0D%0A++++++%3Fother+dbo%3Amovement+%3Fothermovement+.%0D%0A++++++%3Fother+rdfs%3Alabel+%3FotherAuthors+FILTER+%28LANG%28%3FotherAuthors%29%3D%22de%22%29+.%0D%0A++++++FILTER+%28%28%3Fmovement+%3D+%3Fothermovement%29+AND+%28%3Fother+%21%3D+%3Fs%29%29%0D%0A+++%7D%0D%0A%0D%0A+++%3Fddbitem+rdf%3Atype+fabio%3AAnalogItem+FILTER+%28%0D%0A+++++%21EXISTS+%7B%0D%0A+++++++%3Fddbitem+dcterms%3AisPartOf+%3Fparent%0D%0A+++++%7D%0D%0A++%29%0D%0A+++%3Fddbitem+dcterms%3Atitle+%3Ftitle+%3B%0D%0A++++++dcterms%3Acreator+%3Fcreator+.%0D%0A+++%3Fcreator+a+foaf%3APerson+%3B%0D%0A++++++foaf%3AlastName+%3FlastName+%3B%0D%0A++++++foaf%3AgivenName+%3FfirstName+.%0D%0A+++BIND+%28CONCAT%28%3FfirstName%2C+%22+%22%2C+%3FlastName%29+AS+%3FddbName+%29.%0D%0A+++FILTER+regex%28%3FddbName%2C+%3FotherAuthors%2C+%22i%22%29%0D%0A%7D&format=text%2Fx-html%2Btr&should-sponge=&timeout=0&signal_void=on" >}}

