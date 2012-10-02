eplant
======

easy etree planting

You can plant an etree by subscribing it in terms of builtin python types.

    ('a tag name', [optional attrs dict], [optional children tags or text])

Some examples:

    ('tag', ) -> <tag/>
    ('tag', {'attr': 'value'}) -> <tag attr="value"/>
    ('tag', {'attr': 'value'}, 'text') -> <tag attr="value">text</tag>
    ('tag', ('child', )) -> <tag><child/></tag>
    ('tag',
      ('child', ),
      ('another_tag', 'text')) -> <tag><child/><another_tag>text</another_tag></tag>


---------
namespaces
---------

Of course xml without namespaces is unusable, so there is `eplant.namespace`
and `eplant.qname` primitives.

`eplant.namespace` — a class that represents a namespace and can be used to
emit tag and attribute(!) names. You can use attribute access or subscription
of `eplant.namespace` object to get some name in that namespace.

Real world example::

    from eplant import namespace, to_etree
    se = namespace('http://schemas.xmlsoap.org/soap/envelope/', 'se')
    mhe = namespace('http://my.header.ext/', 'mhe')

    def Envelope(body):
        plant = (se.Envelope,
                    (se.Header,
                        (mhe.From, {se.mustUnderstand: 'true'}, 'me'),
                    (se.Body, body)))
        return to_etree(plant)

--------
examples
--------

Simple usage::

    >>> from eplant import to_etree
    >>> from xml.etree.ElementTree import tostring
    >>> plant = ('SomeRootTag',
    ...             ('FirstChild', 'text'),
    ...             ('SecondChild', {'attr': 'value'}, 'text'))
    >>> tree = to_etree(plant)
    >>> tostring(tree)
    '<SomeRootTag><FirstChild>text</FirstChild><SecondChild attr="value">text</SecondChild></SomeRootTag>'
