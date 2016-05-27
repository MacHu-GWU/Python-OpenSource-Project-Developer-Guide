.. _doc:

第三章 - 创建并部署你的文档网站
===============================

.. image:: _static/readthedocs-logo.png

sphinx是Python社区用于自动生成文档网站的工具。可以用来生成纯文档, 也可以自动从Python代码中提取文档。**本片文档不准备介绍sphinx的使用方法, 关于如何使用sphinx生成你的文档网站, 请自行查阅** `官方文档 <http://www.sphinx-doc.org/en/stable/>`_

第一步, 生成文档网站
-------------------------------------------------------------------------------

在使用 ``sphinx-quickstart`` 生成了基本的文档结构之后, 可以使用我提供的两个脚本 `创建 <https://github.com/MacHu-GWU/elementary_math-project/blob/master/build_doc.bat>`_ 和 `浏览 <https://github.com/MacHu-GWU/elementary_math-project/blob/master/view_doc.bat>`_ 你的文档网站。如果出现了 ``zzz_manual_install.py`` 相关的错误, 请参考 `什么是zzz_manual_install <https://github.com/MacHu-GWU/zzz_manual_install-project>`_

第二步, 部署你的文档网站
-------------------------------------------------------------------------------
在Python社区, 常用的三种部署文档网站的方法分别是:

1. 使用PyPI Host。
2. 使用ReadTheDocs。
3. 使用AWS S3。


使用PyPI Host
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在你的PyPI项目的后台界面的releases菜单中, 有一个 ``Choose File``, ``Upload Documentation`` 按钮, 可以让你把文档网站文件的压缩包上传到 http://pythonhosted.org。


使用ReadTheDocs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
相比其他两种方案, `ReadTheDocs <https://readthedocs.org/>`_ 的好处是什么呢?

1. 完全免费。 
2. 自动关联Github账户, 当有更新时, 自动更新网站。
3. 同时维护多个版本的文档。让使用老版本用户也能看到老版本的文档。
4. 可以关联 `Google Analytic <https://www.google.com/analytics/>`_, 追踪访问量。

如果使用自己的网站, 每当你有更新时, 你都要更新你的网页文件。而如果使用ReadTheDocs, 每当你的在Github上有更新时, ReadTheDocs会自动检测到更新, 并重新build所有页面。所以你所要做的就是在commit之前, 在本地使用 ``make_html.bat`` build一次网页, 确认无误之后, commit代码库到github即可。

**注意**: 如果你的包依赖其他第三方包, 那么就需要设置在ReadTheDocs的dashboard设置requirements.txt, 以及virtual environment。requirements.txt告诉ReadTheDocs在build的时候要安装哪些依赖的包, virtual env能配置出合适的虚拟环境。这是因为sphinx在build网页的时候, 要保证包里所有的模块都是可以被import的。这算是使用ReadTheDocs的一个复杂的地方。


.. _readthedocs_quickguide:

Readthedocs简明介绍
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
- 问: 我申请了Readthedocs账号, 第一件事要做什么?

从github导入你的项目。具体方法是: 

1. 登陆你的github, 进入你的github repository 
2. settings -> webhooks & service -> add Readthedocs
3. 回到Readthedocs, Import a project -> Import from github -> 找到你的项目 -> Create

- 问: 我已经导入了我的项目了, 那怎么让Readthedocs开始生成我的文档网站?

首先你要进行一些设置, 告诉Readthedocs一些信息: 

1. 进入你的Readthedocs project
2. 进入Admin菜单
3. 进入Setting菜单
4. 指定Programming language = Python
5. 进入Advance菜单
6. 如果你的包依赖其他第三方库, 请勾选: Install your project inside a virtualenv using setup.py install. 并指定requirement file, 通常为 ``requirements.txt``。这样在尝试Build网站时, readthedoc就会使用 ``pip`` 把 ``requirements.txt`` 中的包都安装了。
7. 如果你只想要保留最新的文档(通常需要保证你的库向下兼容), 请勾选: Single version
8. 在Python configuration file: 一栏中填写从项目目录到 Sphinx 的 ``conf.py`` 的路径, 在本例中是 ``source/conf.py``。这样Readthedocs才能找到你的文档放在哪里了。
9. 在 Python interpreter 中选择Python2/3。保持这个和你开发时测试所使用的一致。
10. 如果想要用Google Analytic, 填写 Analytics Code

然后回到readthedoc project页面, 进入Build菜单, 如果还没有开始自动Build, 则点击Build。如果发生Failed, 点击Failed查看错误信息。如果Passed, 恭喜你, 可以点击View Docs浏览你的文档了!


使用AWS S3
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
AWS的 `S3 <https://aws.amazon.com/s3/>`_ 服务提供了自动部署静态网站的服务。具体做法请参考 `官方文档 <http://docs.aws.amazon.com/AmazonS3/latest/dev/WebsiteHosting.html>`_。你所要做的只是将文档网站文件的压缩包上传到S3即可。


**至此, 你的源代码保管在GitHub, 扩展包发布在了PyPI, 支持 ``pip install ``安装, 并拥有了一个在线文档网站了。撒花, 撒花!**

.. image:: _static/sa-hua.gif


自动化测试与持续集成技术, 是保证你的项目高质量的关键。对于不复杂的项目, 这部分并不是必须的。但是要想在频繁的更新中同时保持代码的高治疗, 这是你必须要懂得的东西。

**下一篇**: :ref:`第四章 - 自动化测试与持续集成 <ci>`, 