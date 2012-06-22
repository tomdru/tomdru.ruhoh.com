---

title: xmldb Tutorial 
date: '2012-06-12'
description: Making an XPath query in the BDB XML database
categories: tutorial
tags: 
    - bdb
    - xml
    - xpath

layout: post

---

We'll use the example document `books.xml` from [http://www.w3schools.com/xquery/xquery_example.asp](http://www.w3schools.com/xquery/xquery_example.asp).


    In [1]: import clove.xmldb.XmlDbKit as XmlDbKit

    In [2]: db = XmlDbKit.make('dev')

    In [3]: db.env.list_documents()
    Out[3]: []

    In [4]: with open('/home/ubuntu/Dropbox/books.xml') as f:
       ...:     content = f.read()
       ...:     

We'll use `db.env.put_document` to add the XML content to the database for now, instead of using `db.create`, which is used for sifting out `quoteEvent` events, and which will not add anything if there are no `quoteEvent` tags.

    In [5]: db.env.put_document('document_uuid', content)

    In [6]: import clove.xmldb.XPathQuery as XPathQuery

    In [7]: query = XPathQuery.make('/bookstore/book')

    In [8]: db.query(query)
    Out[8]: 
    ['<book category="COOKING">\n  <title lang="en">Everyday Italian</title>\n  <author>Giada De Laurentiis</author>\n  <year>2005</year>\n  <price>30.00</price>\n</book>',
     '<book category="CHILDREN">\n  <title lang="en">Harry Potter</title>\n  <author>J K. Rowling</author>\n  <year>2005</year>\n  <price>29.99</price>\n</book>',
     '<book category="WEB">\n  <title lang="en">XQuery Kick Start</title>\n  <author>James McGovern</author>\n  <author>Per Bothner</author>\n  <author>Kurt Cagle</author>\n  <author>James Linn</author>\n  <author>Vaidyanathan Nagarajan</author>\n  <year>2003</year>\n  <price>49.99</price>\n</book>',
     '<book category="WEB">\n  <title lang="en">Learning XML</title>\n  <author>Erik T. Ray</author>\n  <year>2003</year>\n  <price>39.95</price>\n</book>']
