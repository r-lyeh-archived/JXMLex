<pre>
JXMLex, revision 0
==================

JXMLex is an expressive and relatively small representation of JSON in XML, so data can be reused with XML tools.
JXMLex is based on JSONx and JXML (details at http://github.com/r-lyeh/JXML). 

Pros: JXMLex syntax provides more natural and expressive XPath queries by adding attributes and duplicating information.
Cons: JXMLex files are larger than their JXML counterparts.

Pros: JXMLex is a richer superset of JXML. JXML tools can still parse JXMLex files.
Cons: JXMLex attributes are lossy converted from JSON. Read @son attribute to retrieve original name instead.

TL;DR
=====

- Use JXML when a loss-less JSON representation is required (details at http://github.com/r-lyeh/JXML).
- Use JXML when size matters (details at http://github.com/r-lyeh/JXML).
- Use JXMLex when complex XPath statements are going to be made (see details below).
- Use JXMLex when ease of use and flexibility are mandatory (see details below).

Notes
=====

JXMLex syntax is subject to change.


Conversion guide
================

- Convert JSON to JXML by following conversion rules described at JXML reference document (details at http://github.com/r-lyeh/JXML).
- Then, for every XML target node that has a property name, add an attribute whereas propertyname="text()".
- Property name must be escaped to be compliant with XML attribute naming: all invalid characters are escaped to underscore characters.

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
      "ficoScore": "&gt; 640"
    }

The following output is the result of the transformed document to JXMLex.

    &lt;?xml version="1.0" encoding="UTF-8"?&gt;
    &lt;j son="o"&gt;
        &lt;j son="s:name" name_surname="John Smith"&gt;John Smith&lt;/j&gt;
        &lt;j son="o:address" address=""&gt;
            &lt;j son="s:streetAddress" streetAddress="21 2nd Street"&gt;21 2nd Street&lt;/j&gt;
            &lt;j son="s:city" city="New York"&gt;New York&lt;/j&gt;
            &lt;j son="s:state" state="NY"&gt;NY&lt;/j&gt;
            &lt;j son="n:postal-code" postal_code="10021"&gt;10021&lt;/j&gt;
        &lt;/j&gt;
        &lt;j son="a:IDs" IDs=""&gt;
            &lt;j son="s"&gt;2-111&lt;/j&gt;
            &lt;j son="s"&gt;2-222&lt;/j&gt;
        &lt;/j&gt;
        &lt;j son="0:additionalInfo" additionalInfo="" /&gt;
        &lt;j son="b:remote" remote="false"&gt;false&lt;/j&gt;
        &lt;j son="n:height" height="62.4"&gt;62.4&lt;/j&gt;
        &lt;j son="s:ficoScore" ficoScore="&amp;gt; 640"&gt;&amp;gt; 640&lt;/j&gt;
    &lt;/j&gt;

Credits
=======

- JXMLex was created by Mario "rlyeh" Rodriguez.
- JSONx is an IBM® standard format to represent JSON as XML.
</pre>
