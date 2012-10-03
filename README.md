eplant
======

Easy `lxml.etree` planting.

Example:

    from lxml import etree
    import eplant

    plant = eplant.ElementPlant(
        default_namespace = 'http://default/',
        nsmap = {
            'foo': 'http://foo/',
            'bar': 'http://bar/',
        }
    )

    default, foo, bar = plant.namespaces('', 'foo', 'bar')

    doc = default.root(
        foo.title({bar.x: 'a'}, 'title text'),
        bar('small-body', 'body text'),
    )

    print(etree.tostring(doc, pretty_print=True))

produces the following XML:

    <root xmlns:foo="http://foo/" xmlns:bar="http://bar/" xmlns="http://default/">
      <foo:title bar:x="a">title text</foo:title>
      <bar:small-body>body text</bar:small-body>
    </root>
