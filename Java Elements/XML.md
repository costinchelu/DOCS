## DTD vs. XMLSchema

XML Schema utilize an XML-based syntax, whereas DTDs (Document Type Definition) have a unique syntax held over from SGML (Standard Generalized Markup Language) DTDs. Although DTDs are often criticized because of this need to learn a new syntax, the syntax itself is quite terse. The opposite is true for XML Schema, which are verbose, but also make use of tags and XML so that authors of XML should find the syntax of XML Schema less intimidating.

## What is XPath

- defines a "path" into an XML document (navigate through elements and attributes in an XML document)
- fundamental part of XSLT, XQuery

## What is XSLT

- extensible stylesheet language transformations
- applies templates to XML data
- written using XML syntax
- it can transform XML data into other type of documents (data)
- can perform operations directly on the data

 ## What is XQuery
 
 - XQuery is to XML what SQL is to databases

## SAX vs. DOM

**SAX (Simple API for XML)**: Is a stream-based processor. You only have a tiny part in memory at any time and you "sniff" the XML stream by implementing callback code for events like tagStarted() etc. It uses almost no memory, but you can't do "DOM" stuff, like use XPath or traverse trees.
- Event based parser (Sequence of events).
- SAX parses the file as it reads it, i.e. parses node by node.
- No memory constraints as it does not store the XML content in the memory.
- SAX is read only i.e. can’t insert or delete the node.
- Use SAX parser when memory content is large.
- SAX reads the XML file from top to bottom and backward navigation is not possible.
- Faster at run time.

**DOM (Document Object Model)**: You load the whole thing into memory. You can blow memory with even medium sized documents. But you can use XPath and traverse the tree etc.
- Tree model parser (Object based) (Tree of nodes).
- DOM loads the file into the memory and then parse- the file.
- Has memory constraints since it loads the whole XML file before parsing.
- DOM is read and write (can insert or delete nodes).
- If the XML content is small, then prefer DOM parser.
- Backward and forward search is possible for searching the tags and evaluation of the information inside the tags. So this gives the ease of navigation.
- Slower at run time.

## What is XML Namespace

XML Namespaces provide a method to avoid element name conflicts. Name conflicts in XML can easily be avoided using a name prefix.

```xml
<root xmlns:h="http://www.w3.org/TR/html4/"
xmlns:f="https://www.w3schools.com/furniture">
    
<h:table>
  <h:tr>
    <h:td>Apples</h:td>
    <h:td>Bananas</h:td>
  </h:tr>
</h:table>

<f:table>
  <f:name>African Coffee Table</f:name>
  <f:width>80</f:width>
  <f:length>120</f:length>
</f:table>
```
