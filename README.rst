Requests-HTML: HTML人性化解析™
=======================================
该库旨在尽可能简单直观地解析HTML（例如，抓取网页）。

当使用这个库时，你会自动获得：

- CSS选择器（也称为jQuery风格，感谢PyQuery）。
- XPath选择器，对于这个微弱的内核来说。
- 模拟用户代理（像一个真正的Web浏览器）。
- 自动跟踪重定向。
- 连接池和cookie持久性。
- 您了解并喜爱的请求体验，具有魔法解析能力。

还有一些不错的功能包括：

- 减少页面和元素的导出。


用法
=====

使用 Requests 向'python.org'发出GET请求：

.. code-block:: pycon

    >>> from requests_html import session
    >>> r = session.get('https://python.org/')

将页面上所有链接（包含绝对和相对路径）组成列表后返回（锚点除外）:

.. code-block:: pycon

    >>> r.html.links
    {'/users/membership/', '/about/gettingstarted/', 'http://feedproxy.google.com/~r/PythonInsider/~3/zVC80sq9s00/python-364-is-now-available.html', '/about/success/', 'http://flask.pocoo.org/', 'http://www.djangoproject.com/', '/blogs/', ... '/psf-landing/', 'https://wiki.python.org/moin/PythonBooks'}

将页面上所有链接（统一成绝对路径形式）组成列表后返回（锚点除外）：

.. code-block:: pycon

    >>> r.html.absolute_links
    {'http://feedproxy.google.com/~r/PythonInsider/~3/zVC80sq9s00/python-364-is-now-available.html', 'https://www.python.org/downloads/mac-osx/', 'http://flask.pocoo.org/', 'https://www.python.org/docs.python.org/3/tutorial/', 'http://www.djangoproject.com/', 'https://wiki.python.org/moin/BeginnersGuide', 'https://www.python.org/about/success/', 'http://twitter.com/ThePSF', 'https://www.python.org/events/python-user-group/634/', ..., 'https://wiki.python.org/moin/PythonBooks'}

使用CSS选择器选择一个元素：

.. code-block:: pycon

    >>> about = r.html.find('#about', first=True)

抓取元素的文字内容：

.. code-block:: pycon

    >>> print(about.text)
    About
    Applications
    Quotes
    Getting Started
    Help
    Python Brochure

将元素属性以键值对形式组成字典后返回:

.. code-block:: pycon

    >>> about.attrs
    {'id': 'about', 'class': 'tier-1 element-1  ', 'aria-haspopup': 'true'}

将元素内的指定元素组成列表后返回：

.. code-block:: pycon

    >>> about.find('a')
    [<Element 'a' href='/about/' title='' class=''>, <Element 'a' href='/about/apps/' title=''>, <Element 'a' href='/about/quotes/' title=''>, <Element 'a' href='/about/gettingstarted/' title=''>, <Element 'a' href='/about/help/' title=''>, <Element 'a' href='http://brochure.getpython.info/' title=''>]

将元素渲染为Markdown

.. code-block:: pycon

    >>> print(about.markdown)

    * [About](/about/)

      * [Applications](/about/apps/)
      * [Quotes](/about/quotes/)
      * [Getting Started](/about/gettingstarted/)
      * [Help](/about/help/)
      * [Python Brochure](http://brochure.getpython.info/)

搜索页面上的文字：

.. code-block:: pycon

    >>> r.html.search('Python is a {} language')[0]
    programming

更复杂的CSS选择器例子（从Chrome浏览器开发工具复制）:

.. code-block:: pycon

    >>> r = session.get('https://github.com/')
    >>> sel = 'body > div.application-main > div.jumbotron.jumbotron-codelines > div > div > div.col-md-7.text-center.text-md-left > p'

    >>> print(r.html.find(sel, first=True).text)
    GitHub is a development platform inspired by the way you work. From open source to business, you can host and review code, manage projects, and build software alongside millions of other developers.

也支持XPath：

.. code-block:: pycon

   >>> r.html.xpath('a')
   [<Element 'a' class='btn' href='https://help.github.com/articles/supported-browsers'>]

安装
============

.. code-block:: shell

    $ pipenv install requests-html
    ✨🍰✨

