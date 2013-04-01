JXMLex, revision 0
==================

JXMLex is an expressive and relatively small representation of JSON in XML, so data can be reused with XML tools.
JXMLex is based on JSONx and JXML (See http://github.com/r-lyeh/JXML for details). 

Pros: 
- JXMLex syntax provides more natural and expressive XPath queries by adding attributes and duplicating information.
- JXMLex is a richer superset of JXML. JXML tools can still parse JXMLex files.

Cons:
- JXMLex files are larger than their JXML counterparts.
- JXMLex attributes are a lossy conversion from JSON per se. If you need to retrieve original lossless name, then read @son attribute instead.

Conversion guide
================

- Convert XML to JXML by following conversion rules described at JXML reference document. See http://github.com/r-lyeh/JXML for details.
- Then, for every XML target node that has a property name, add an attribute whereas propertyname="text()".
- Property name must be escaped to be compliant with XML attribute naming.
- When escaping attribute names, all invalid characters are escaped to underscore characters.

JXMLex sample
=============

The following example document is a sample of the JSON structure.

    {
      "name/surname":"John Smith",
      "address": {
        "streetAddress": "21 2nd Street",
        "city": "New York",
        "state": "NY",
        "postal-code": 10021,
      },
      "IDs": [
        "2-111",
        "2-222"
      ],
      "additionalInfo": null,
      "remote": false,
      "height": 62.4,
      "ficoScore": "> 640"
    }

The following output is the result of the transformed document to JXML.

    <?xml version="1.0" encoding="UTF-8"?>
    <j son="o">
        <j son="s:name" name_surname="John Smith">John Smith</j>
        <j son="o:address" address="">
            <j son="s:streetAddress" streetAddress="21 2nd Street">21 2nd Street</j>
            <j son="s:city" city="New York">New York</j>
            <j son="s:state" state="NY">NY</j>
            <j son="n:postalCode" postal_code="10021">10021</j>
        </j>
        <j son="a:IDs" IDs="">
            <j son="s">2-111</j>
            <j son="s">2-222</j>
        </j>
        <j son="0:additionalInfo" additionalInfo="" />
        <j son="b:remote" remote="false">false</j>
        <j son="n:height" height="62.4">62.4</j>
        <j son="s:ficoScore" ficoScore="&gt; 640">&gt; 640</j>
    </j>

Credits
=======

- JXMLex was created by Mario "rlyeh" Rodriguez.
- JSONx is an IBM® standard format to represent JSON as XML.
