# OntoFlex ported to Java from C#/.NET

[OntoFlex](http://artistech.com/ontoflex.html) is a windows based tool for ontology construction, maintenance, and foreign language document search.  It supports translation needs in dialects or languages where no machine translation (MT) resources exist.  It is meant to be tailorable in the field by Analyst/Translator pairs.   It has been designed to perform foreign language document “triage” ( separate out from a large group of documents those which should be fully translated based on the tactical situation at the time).  It uses an ontology of English terms and phrases with high quality translations into foreign languages to search the repository of foreign language documents.

The structure of the ontology is constructed as a hyperlinked, a-cyclic, directed graph.

The graph includes "Is-a", "Peer-to" and other links between terms and phrases.  The metadata in the ontology consists of links between terms and data associated with the links and terms/phrases.

## What works:
- Phrase Matching
- Word Matching
- Ranking
- File Reading
- Results Output

## What doesn't work:
- Chunk Matching
- GUI

## To Do:
- Web
- Hadoop
- Swing/UI
- CLI which can be called from external process

## Complile:  
`mvn clean install`

## Dependencies (Automatically Handled by Maven):
- [Tika Project 1.14](https://tika.apache.org/)
- [Commons Lang 3.5](https://commons.apache.org/proper/commons-lang/)
- [Commons IO 2.5](https://commons.apache.org/proper/commons-io/)
- [Commons Collections 4.1](https://commons.apache.org/proper/commons-collections/)
- [Jackson JSON 2.8.8](https://github.com/FasterXML/jackson)
- [Commons Beansutils 1.9.3](https://commons.apache.org/proper/commons-beansutils/)

### Tika Project
The Apache Tika™ toolkit detects and extracts metadata and text from over a thousand different file types (such as PPT, XLS, and PDF). All of these file types can be parsed through a single interface, making Tika useful for search engine indexing, content analysis, translation, and much more.

## Proof of Concept
- Swing/UI layout
- FX web browser for displaying results as HTML.
- CLI using a beanshell script for setting up a search.
