.. _prelude:

前言
===============================================================================

.. image:: _static/open-source-logo.jpg

Python语言作为一种通用的高级语言, 以最简单平滑的学习曲线, 以及几乎无所不能的强大功能, 在几乎所有的IT领域都有着广泛的应用。可依我看来, Python作为一个有着近30年历史的语言, 之所以能够这么流行, 可能要鬼用于而是世界上首屈一指活跃的开发者社区。在社区里, 有无数的第三方包, 涵盖了各行各业的不同领域。 使得无论你做什么, 几乎都能找到扩展包达到你的目的。 所以才有这么多的开发者热衷于Python。 而这一切, 都是完全免费开源的！这导致非常多的网络服务, 新技术, 都能在第一时间支持Python SDK和API。所以许多大公司对于Python的支持都非常友好。

既然Python的核心是第三方扩展包, 那你想不想自己写一个并发布呢? 是将自己的优秀成果开源出来供众开发者使用, 还是写一些可以经常复用的小工具供自己和同事使用, 都是一件很棒的事情。

我个人在前前后后做了10多个小作品, 并借鉴了许多Python社区大牛的项目, 总结出一套比较有效率, 重复性工作较少, 能保证高质量代码的工作流程, 从而有了本文档。

一个好的开源项目需要有下面几个部分


GitHub代码版本控制和云托管
-------------------------------------------------------------------------------

.. image:: https://img.shields.io/badge/GitHub-代码版本控制和云托管-E92525.svg

`GitHub <https://github.com/>`_ 是目前最流行的代码云托管服务, 支持开源和私有项目。无论是单人开发还是团队合作, 无论是纯IT项目还是其他以写文件为主要目标的项目, GitHub都是当下最优秀的解决方案。并且开发者所使用的许多云服务都能够和GitHub无缝结合。所以非常有必要学习使用GitHub管理你的项目。本文不准备详细介绍GitHub, 请读者自行找资料学习。


PyPI扩展包发布和云托管
-------------------------------------------------------------------------------

.. image:: https://img.shields.io/badge/PyPI-扩展包发布和云托管-E0C307.svg

既然是Python项目, 当然要发布在 `PyPI <https://pypi.python.org/pypi>`_ 上, 供大家下载和安装。**在这个大家耐心越来越差的时代, 只有下载和安装足够简单粗暴, 才能让用户更有心情去使用你的作品**。同时, PyPI是Python社区的官方第三方包索引网站, Python社区的官方包管理工具pip管理包的时候, 就是从PyPI上下载源码并编译安装的。只要你想要你的包能够通过网络被安装, 那么PyPI使你不二的选择。


ReadTheDoc or PyPI or AWS S3文档托管
-------------------------------------------------------------------------------

.. image:: https://img.shields.io/badge/ReadTheDoc_or_PyPI_or_AWS_S3-文档托管-0782E0.svg

许多时候, 隔了一段时间之后, 就连我们自己也读不懂我们自己的代码。**所以要让用户了解你的包能干什么, 以及怎么多快好省的干, 就需要有一份组织良好, 语言清晰, 例子众多的文档**。Python社区中有一个工具 `sphinx <http://www.sphinx-doc.org/en/stable/>`_, 可以让开发者能专注于内容, 轻易的生成漂亮的, 可搜索的, 组织结构良好的文档网站, 或是PDF。并且还能从代码的docstring中自动生成API文档。所以只要开发者遵从一定的代码风格, 并有良好的注释习惯, 那么生成文档并不是什么难事。

**问题来了, 大多数人没有维护一个网站的经验, 那要讲你的文档放在哪里呢**? 现在是云时代, 有多个服务允许你轻易的部署一个静态的文档网站(静态是指, 仅供阅读, 不提供复杂的互动性)。`ReadTheDoc <https://readthedocs.org/>`_ 是一个能在你每次提交代码到GitHub, 自动创建并部署你的文档网站的云服务。 而PyPI的release菜单中可以允许你上传sphinx所生成的文档网站的压缩包, 并帮你Host你的文档。`AWS S3 <https://aws.amazon.com/s3/>`_ 作为世界上最流行的云存储服务基础设施 (Dropbox以及许多视频网站都是使用的S3), 可以允许用户 `只需要将文件上传, 即可自动部署静态网站 <http://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html>`_。


Travis CI在线多操作系统多Python版本单元测试
-------------------------------------------------------------------------------

.. image:: https://img.shields.io/badge/Travis--CI-在线多操作系统多Python版本单元测试-3ECB1E.svg

Python之所以非常流行的另一个原因, 在于它的跨平台性。Python在Windows, MacOS, Linux甚至Embedded System上都有非常好的兼容性。但和其他语言相比, Python有两个不是100%兼容的Python2和Python3两个大版本, 以及多个主流的小版本Py26, Py27, Py33, Py34, Py35。目前社区中流行的项目, 大部分都已经全平台, 全版本兼容了。**但为了开发出符合这样要求的项目, 你需要对3个平台, 5个版本, 15个不同的环境进行测试。所以你需要有一套自动化测试解决方案**。`Travis-CI <https://travis-ci.org/>`_ 是一个为开源项目提供 `Continues Integration <https://en.wikipedia.org/wiki/Continuous_integration>`_ (`持续集成 <http://baike.baidu.com/view/5253255.htm>`_) 解决方案的云服务商。主要能在你每次提交代码到GitHub之后, 自动对多个操作系统环境, 以及多个Python版本进行测试, 并生成日志和报告。当然, `virtualenv的 <https://virtualenv.pypa.io/en/stable/>`_ 虚拟开发环境, `tox <https://tox.readthedocs.io/en/latest/>`_ 的多Python版本自动化测试, 以及 `pytest <http://pytest.org/latest/>`_ 单元测试框架, 都是你需要学习的内容, 都能很大程度上的简化你的开发和测试工作。请注意, Travis-CI支持 `pytest <http://pytest.org/latest/>`_, `nosetest <http://nose.readthedocs.io/en/latest/>`_, `unittest <https://docs.python.org/2.7/library/unittest.html>`_ 三个测试框架

**好了, 就让我们来学习, 这一整套的开发流程, 并从现在开始养成良好习惯, 复用你的代码, 让我们最简化这些复杂的流程, 将精力集中在创造性的开发上吧！**

注: 测试框架, 文档网站host, 都有多种选择, 本文中笔者的选择是个人经过比较试用后个人觉得最优的选择。你可以选择你喜欢的, 本文仅供参考。
