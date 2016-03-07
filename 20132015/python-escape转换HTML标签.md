title: python escape转换HTML标签
categories:
  - Python
date: 2013-11-11 06:12:52
tags:
  - Python
---

```
_escape_map = {ord('&'): '&amp;', ord('<'): '&lt;', ord('>'): '&gt;'}
_escape_map_full = {ord('&'): '&amp;', ord('<'): '&lt;', ord('>'): '&gt;',
                    ord('"'): '&quot;', ord('\''): '&#x27;'}
# NB: this is a candidate for a bytes/string polymorphic interface
def escape(s, quote=True):
    """
    Replace special characters "&", "<" and ">" to HTML-safe sequences.
    If the optional flag quote is true (the default), the quotation mark
    characters, both double quote (") and single quote (') characters are also
    translated.
    """
    if quote:
        return s.translate(_escape_map_full)
    return s.translate(_escape_map)
```
参考来源：http://www.paobuke.com/develop/pbk1297.html