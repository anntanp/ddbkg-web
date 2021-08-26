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
      ?work rdf:type fabio:Work .
      ?work dcterms:creator ?author .
      ?author foaf:name ?author_name FILTER regex(str(?author_name), "Schiller", "i") .
      ?work dcterms:title ?title .
    }
    ```
  {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&query=PREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0A++++PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0A++++PREFIX+gnd%3A+%3Chttp%3A%2F%2Fd-nb.info%2Fgnd%2F%3E%0D%0A++++PREFIX+gndo%3A+%3Chttp%3A%2F%2Fd-nb.info%2Fstandards%2Felementset%2Fgnd%23%3E%0D%0A++++PREFIX+fabio%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Ffabio%2F%3E%0D%0A++++PREFIX+frbr%3A+%3Chttp%3A%2F%2Fpurl.org%2Fvocab%2Ffrbr%2Fcore%23%3E%0D%0A++++PREFIX+foaf%3A+%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0A++++PREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A++++%0D%0A++++SELECT+DISTINCT+%3Ftitle+%3Fwork+%3Fauthor%0D%0A++++WHERE+%7B%0D%0A++++++%3Fwork+rdf%3Atype+fabio%3AWork+.%0D%0A++++++%3Fwork+dcterms%3Acreator+%3Fauthor+.%0D%0A++++++%3Fauthor+foaf%3Aname+%3Fauthor_name+FILTER+regex%28str%28%3Fauthor_name%29%2C+%22Schiller%22%2C+%22i%22%29+.%0D%0A++++++%3Fwork+dcterms%3Atitle+%3Ftitle+.%0D%0A++++++++++++%7D&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}
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
      ?ddbitem dcterms:title ?title FILTER regex(str(?title), "Räuber", "i") .
    }
    ```
  {{< cta cta_text="Run 👉" cta_link="http://10.10.4.10:8890/sparql?default-graph-uri=&query=PREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0APREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0APREFIX+gnd%3A+%3Chttp%3A%2F%2Fd-nb.info%2Fgnd%2F%3E%0D%0APREFIX+gndo%3A+%3Chttp%3A%2F%2Fd-nb.info%2Fstandards%2Felementset%2Fgnd%23%3E%0D%0APREFIX+fabio%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Ffabio%2F%3E%0D%0APREFIX+frbr%3A+%3Chttp%3A%2F%2Fpurl.org%2Fvocab%2Ffrbr%2Fcore%23%3E%0D%0APREFIX+foaf%3A+%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0APREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A++++%0D%0ASELECT+DISTINCT+%3Fddbitem+%3Ftitle+%3Fauthor%0D%0AWHERE+%7B%0D%0A++%3Fddbitem+rdf%3Atype+fabio%3AAnalogItem+.%0D%0A++%3Fddbitem+dcterms%3Acreator+%3Fauthor+FILTER+%28%0D%0A+++++%21EXISTS+%7B%0D%0A+++++++%3Fddbitem+dcterms%3AisPartOf+%3Fparent%0D%0A+++++%7D%0D%0A++%29%0D%0A++%3Fauthor+foaf%3Aname+%3Fauthor_name+FILTER+regex%28str%28%3Fauthor_name%29%2C+%22Schiller%22%2C+%22i%22%29+.%0D%0A++%3Fddbitem+dcterms%3Atitle+%3Ftitle+FILTER+regex%28str%28%3Ftitle%29%2C+%22R.*uber%22%2C+%22i%22%29+.%0D%0A%7D&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}
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
            FILTER regex(str(?title), "Die Räuber", "i") .
      ?ddbitem dcterms:type ?type ;
            fabio:hasReproduction ?di .
      ?di fabio:isExemplarOf ?epub .        
    }
    ```
   {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/sparql?default-graph-uri=&query=++++PREFIX+rdf%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F1999%2F02%2F22-rdf-syntax-ns%23%3E%0D%0A++++PREFIX+rdfs%3A+%3Chttp%3A%2F%2Fwww.w3.org%2F2000%2F01%2Frdf-schema%23%3E%0D%0A++++PREFIX+gnd%3A+%3Chttp%3A%2F%2Fd-nb.info%2Fgnd%2F%3E%0D%0A++++PREFIX+gndo%3A+%3Chttp%3A%2F%2Fd-nb.info%2Fstandards%2Felementset%2Fgnd%23%3E%0D%0A++++PREFIX+fabio%3A+%3Chttp%3A%2F%2Fpurl.org%2Fspar%2Ffabio%2F%3E%0D%0A++++PREFIX+frbr%3A+%3Chttp%3A%2F%2Fpurl.org%2Fvocab%2Ffrbr%2Fcore%23%3E%0D%0A++++PREFIX+foaf%3A+%3Chttp%3A%2F%2Fxmlns.com%2Ffoaf%2F0.1%2F%3E%0D%0A++++PREFIX+dcterms%3A+%3Chttp%3A%2F%2Fpurl.org%2Fdc%2Fterms%2F%3E%0D%0A++++%0D%0A++++++++SELECT+DISTINCT+%3Ftitle+%3Fddbitem+%3Ftype+%3Fepub%0D%0A++++++++WHERE+%7B%0D%0A++++++++++%3Fwork+rdf%3Atype+fabio%3AWork+%3B%0D%0A++++++++++++++++fabio%3AhasRealization+%3Fexpression+.%0D%0A++++++++++%3Fexpression+fabio%3AhasRepresentation+%3Fddbitem+%3B%0D%0A++++++++++++++++dcterms%3Atitle+%3Ftitle+%0D%0A++++++++++++++++FILTER+regex%28str%28%3Ftitle%29%2C+%22Die+R.*uber%22%2C+%22i%22%29+.%0D%0A++++++++++%3Fddbitem+dcterms%3Atype+%3Ftype+%3B%0D%0A++++++++++++++++fabio%3AhasReproduction+%3Fdi+.%0D%0A++++++++++%3Fdi+fabio%3AisExemplarOf+%3Fepub+.++++++++%0D%0A%7D&format=text%2Fhtml&should-sponge=&timeout=0&signal_void=on" >}}
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
      ?author foaf:name ?author_name FILTER (regex(str(?author_name), "Thomas Mann", "i") || regex(str(?author_name), "Mann, Thomas", "i")).
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
      ?author foaf:name ?author_name FILTER (regex(str(?author_name), "Johann Wolfgang von Goethe", "i") || regex(str(?author_name), "Goethe, Johann Wolfgang von", "i")) .
      ?expression dcterms:title ?title FILTER regex(str(?title), "Faust", "i") .
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

<!---
### CQ6
  - How many books were published by publishers located in Leipzig?
    ```

    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/" >}}
    {{% staticref "https://ise-fizkarlsruhe.github.io/ddbkg/cq/cq06.html" "newtab" %}}Download Results{{% /staticref %}}

### CQ7
  - 
    ```

    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/" >}}
    {{% staticref "https://ise-fizkarlsruhe.github.io/ddbkg/cq/cq07.html" "newtab" %}}Download Results{{% /staticref %}}

### CQ8
  - 
    ```

    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/" >}}
    {{% staticref "https://ise-fizkarlsruhe.github.io/ddbkg/cq/cq08.html" "newtab" %}}Download Results{{% /staticref %}}

### CQ9
  - 
    ```

    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/" >}}
    {{% staticref "https://ise-fizkarlsruhe.github.io/ddbkg/cq/cq09.html" "newtab" %}}Download Results{{% /staticref %}}

### CQ10
  - 
    ```

    ```
    {{< cta cta_text="Run 👉" cta_link="https://ddbkg.fiz-karlsruhe.de/" >}}
    {{% staticref "https://ise-fizkarlsruhe.github.io/ddbkg/cq/cq10.html" "newtab" %}}Download Results{{% /staticref %}}

--->
<!---
Previous CQ2
```
    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX gnd: <http://d-nb.info/gnd/>
    PREFIX gndo: <http://d-nb.info/standards/elementset/gnd#>
    PREFIX fabio: <http://purl.org/spar/fabio/>
    PREFIX frbr: <http://purl.org/vocab/frbr/core#>
    PREFIX foaf: <http://xmlns.com/foaf/0.1/>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    
    SELECT DISTINCT ?ddbitem ?title ?work ?author
    WHERE {
      ?work rdf:type fabio:Work .
      ?work dcterms:creator ?author .
      ?work fabio:hasPortrayal ?ddbitem .
      ?author foaf:name ?author_name FILTER regex(str(?author_name), "Schiller", "i") .
      ?work dcterms:title ?title FILTER regex(str(?title), "R.*uber", "i") .
            }
    ```
    
    CQ5
    ```
    PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX gnd: <http://d-nb.info/gnd/>
    PREFIX gndo: <http://d-nb.info/standards/elementset/gnd#>
    PREFIX fabio: <http://purl.org/spar/fabio/>
    PREFIX frbr: <http://purl.org/vocab/frbr/core#>
    PREFIX foaf: <http://xmlns.com/foaf/0.1/>
    PREFIX dcterms: <http://purl.org/dc/terms/>
    
    SELECT ?langcode (COUNT (?langcode) as ?translations)
    WHERE {
      ?expression dcterms:creator ?author .
      ?expression fabio:hasRepresentation ?ddbitem
      ?author foaf:name ?author_name FILTER (regex(str(?author_name), "Johann Wolfgang von Goethe", "i") || regex(str(?author_name), "Goethe, Johann Wolfgang von", "i")) .
      ?expression dcterms:title ?title FILTER regex(str(?title), "Faust", "i") .
      ?expression dcterms:language ?lang .
      ?lang rdfs:label ?langcode .
    } GROUP BY ?langcode
    ```
--->
