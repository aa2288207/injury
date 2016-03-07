title: lxml 解析 xml 经典 源自stackoverflow
tags:
  - lxml
  - xpath
categories:
  - Python
date: 2014-07-11 09:28:15
---

    <span class="kwd" style="color: #00008b;">from</span><span class="pln"> lxml </span><span class="kwd" style="color: #00008b;">import</span><span class="pln"> etree
    data </span><span class="pun">=</span><span class="str" style="color: #800000;">"""
     &lt;svg
        xmlns:dc="</span><span class="pln">http</span><span class="pun">:</span><span class="com" style="color: #808080;">//purl.org/dc/elements/1.1/"</span><span class="pln">
        xmlns</span><span class="pun">:</span><span class="pln">cc</span><span class="pun">=</span><span class="str" style="color: #800000;">"http://web.resource.org/cc/"</span><span class="pln">
        xmlns</span><span class="pun">:</span><span class="pln">rdf</span><span class="pun">=</span><span class="str" style="color: #800000;">"http://www.w3.org/1999/02/22-rdf-syntax-ns#"</span><span class="pln">
        xmlns</span><span class="pun">:</span><span class="pln">svg</span><span class="pun">=</span><span class="str" style="color: #800000;">"http://www.w3.org/2000/svg"</span><span class="pln">
        xmlns</span><span class="pun">=</span><span class="str" style="color: #800000;">"http://www.w3.org/2000/svg"</span><span class="pln">
        xmlns</span><span class="pun">:</span><span class="pln">xlink</span><span class="pun">=</span><span class="str" style="color: #800000;">"http://www.w3.org/1999/xlink"</span><span class="pln">
        xmlns</span><span class="pun">:</span><span class="pln">sodipodi</span><span class="pun">=</span><span class="str" style="color: #800000;">"http://sodipodi.sourceforge.net/DTD/sodipodi-0.dtd"</span><span class="pln">
        xmlns</span><span class="pun">:</span><span class="pln">inkscape</span><span class="pun">=</span><span class="str" style="color: #800000;">"http://www.inkscape.org/namespaces/inkscape"</span><span class="pln">
        width</span><span class="pun">=</span><span class="str" style="color: #800000;">"50"</span><span class="pln">
        height</span><span class="pun">=</span><span class="str" style="color: #800000;">"25"</span><span class="pln">
        id</span><span class="pun">=</span><span class="str" style="color: #800000;">"svg2"</span><span class="pln">
        sodipodi</span><span class="pun">:</span><span class="pln">version</span><span class="pun">=</span><span class="str" style="color: #800000;">"0.32"</span><span class="pln">
        inkscape</span><span class="pun">:</span><span class="pln">version</span><span class="pun">=</span><span class="str" style="color: #800000;">"0.45.1"</span><span class="pln">
        version</span><span class="pun">=</span><span class="str" style="color: #800000;">"1.0"</span><span class="pln">
        sodipodi</span><span class="pun">:</span><span class="pln">docbase</span><span class="pun">=</span><span class="str" style="color: #800000;">"/home/tcooksey/Projects/qt-4.4/demos/embedded/embeddedsvgviewer/files"</span><span class="pln">
        sodipodi</span><span class="pun">:</span><span class="pln">docname</span><span class="pun">=</span><span class="str" style="color: #800000;">"v-slider-handle.svg"</span><span class="pln">
        inkscape</span><span class="pun">:</span><span class="pln">output_extension</span><span class="pun">=</span><span class="str" style="color: #800000;">"org.inkscape.output.svg.inkscape"</span><span class="pun">&gt;</span><span class="pun">&lt;</span><span class="pln">text
           xml</span><span class="pun">:</span><span class="pln">space</span><span class="pun">=</span><span class="str" style="color: #800000;">"preserve"</span><span class="pln">
           style</span><span class="pun">=</span><span class="str" style="color: #800000;">"font-size:14.19380379px;font-style:normal;font-variant:normal;font-weight:normal;font-stretch:normal;text-align:start;line-height:125%;writing-mode:lr-tb;text-anchor:start;fill:#000000;fill-opacity:1;stroke:none;font-family:DejaVu Sans Mono;-inkscape-font-specification:DejaVu Sans Mono"</span><span class="pln">
           x</span><span class="pun">=</span><span class="str" style="color: #800000;">"109.38555"</span><span class="pln">
           y</span><span class="pun">=</span><span class="str" style="color: #800000;">"407.02847"</span><span class="pln">
           id</span><span class="pun">=</span><span class="str" style="color: #800000;">"libcode-00"</span><span class="pln">
           sodipodi</span><span class="pun">:</span><span class="pln">linespacing</span><span class="pun">=</span><span class="str" style="color: #800000;">"125%"</span><span class="pln">
           inkscape</span><span class="pun">:</span><span class="pln">label</span><span class="pun">=</span><span class="str" style="color: #800000;">"#text4638"</span><span class="pun">&gt;&lt;</span><span class="pln">tspan
             sodipodi</span><span class="pun">:</span><span class="pln">role</span><span class="pun">=</span><span class="str" style="color: #800000;">"line"</span><span class="pln">
             id</span><span class="pun">=</span><span class="str" style="color: #800000;">"tspan4640"</span><span class="pln">
             x</span><span class="pun">=</span><span class="str" style="color: #800000;">"109.38555"</span><span class="pln">
             y</span><span class="pun">=</span><span class="str" style="color: #800000;">"407.02847"</span><span class="pun">&gt;</span><span class="lit" style="color: #800000;">12345678</span><span class="pun">&lt;</span><span class="str" style="color: #800000;">/tspan&gt;&lt;/</span><span class="pln">text</span><span class="pun">&gt;</span><span class="pun">&lt;/</span><span class="pln">svg</span><span class="pun">&gt;</span><span class="str" style="color: #800000;">"""

    nsmap = {
        'sodipodi': 'http://sodipodi.sourceforge.net/DTD/sodipodi-0.dtd',
        'cc': 'http://web.resource.org/cc/',
        'svg': 'http://www.w3.org/2000/svg',
        'dc': 'http://purl.org/dc/elements/1.1/',
        'xlink': 'http://www.w3.org/1999/xlink',
        'rdf': 'http://www.w3.org/1999/02/22-rdf-syntax-ns#',
        'inkscape': 'http://www.inkscape.org/namespaces/inkscape'
        }

    data = etree.XML(data)

    # All svg text elements
    &gt;&gt;&gt; data.xpath('//svg:text',namespaces=nsmap)
    [&lt;Element {http://www.w3.org/2000/svg}text at b7cfc9dc&gt;]
    # All svg text elements with id="</span><span class="pln">libcode</span><span class="pun">-</span><span class="lit" style="color: #800000;">00</span><span class="str" style="color: #800000;">"
    &gt;&gt;&gt; data.xpath('//svg:text[@id="</span><span class="pln">libcode</span><span class="pun">-</span><span class="lit" style="color: #800000;">00</span><span class="str" style="color: #800000;">"]',namespaces=nsmap)
    [&lt;Element {http://www.w3.org/2000/svg}text at b7cfc9dc&gt;]
    # TSPAN child elements of text elements with id="</span><span class="pln">libcode</span><span class="pun">-</span><span class="lit" style="color: #800000;">00</span><span class="str" style="color: #800000;">"
    &gt;&gt;&gt; data.xpath('//svg:text[@id="</span><span class="pln">libcode</span><span class="pun">-</span><span class="lit" style="color: #800000;">00</span><span class="str" style="color: #800000;">"]/svg:tspan',namespaces=nsmap)
    [&lt;Element {http://www.w3.org/2000/svg}tspan at b7cfc964&gt;]
    # All text elements with id starting with "</span><span class="pln">libcode</span><span class="str" style="color: #800000;">"
    &gt;&gt;&gt; data.xpath('//svg:text[fn:startswith(@id,"</span><span class="pln">libcode</span><span class="str" style="color: #800000;">")]',namespaces=nsmap)
    [&lt;Element {http://www.w3.org/2000/svg}text at b7cfcc34&gt;]
    # Iterate text elements, access tspan child
    &gt;&gt;&gt; for elem in data.xpath('//svg:text[fn:startswith(@id,"</span><span class="pln">libcode</span><span class="str" style="color: #800000;">")]',namespaces=nsmap):
    ...     tp = elem.xpath('./svg:tspan',namespaces=nsmap)[0]
    ...     tp.text = "</span><span class="kwd" style="color: #00008b;">new</span><span class="pln"> text</span><span class="str" style="color: #800000;">"

    open("</span><span class="pln">newfile</span><span class="pun">.</span><span class="pln">svg</span><span class="str" style="color: #800000;">","</span><span class="pln">w</span><span class="str" style="color: #800000;">").write(etree.tostring(data))

    参考地址：[http://stackoverflow.com/questions/2359317/how-to-find-elements-by-id-field-in-svg-file-using-python/2359880#2359880](http://stackoverflow.com/questions/2359317/how-to-find-elements-by-id-field-in-svg-file-using-python/2359880#2359880)</span>