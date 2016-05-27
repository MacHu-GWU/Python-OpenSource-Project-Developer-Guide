.. _github:

第一章 - 使用GitHub管理你的开源Python项目
=========================================

.. image:: _static/github-logo.jpg

为了说明的方便, 我们假设我们要开发一个叫做 ``elementary_math`` (小学数学) 的Python扩展包。下文中提到 ``package_name`` (扩展包的名字) 就用 ``elementary_math`` 代替。本文档提供了一个 `示例的GitHub项目 <https://github.com/MacHu-GWU/elementary_math-project>`_ 实现了本文中所说的一切。``elementary_math`` 实现了最简单的加减乘除函数 (仅供说明使用)。

注: 根据官方 `Python Style Guide <https://www.python.org/dev/peps/pep-0008/#package-and-module-names>`_, 包名称须全部小写, 并只允许用下划线。

第一步, 创建一个 `GitHub <https://github.com/>`_ 账户
-------------------------------------------------------------------------------
这部分就不详细介绍了, 请自行创建。而GitHub的具体使用, 可以参考 `这篇文档 <https://github.com/MacHu-GWU/learn_git-project/blob/master/Document/01-What-Is-Git-and-GitHub.rst>`_ 中的资料。


.. _create_repository:

第二步, 创建一个repository(代码库)
-------------------------------------------------------------------------------
创建代码库非常简单, 可以使用网页界面, 在Windows和MacOS下也可以下载GitHub客户端来创建; 而在Linux系统中则可以使用第三方Git客户端软件, 例如SmartGit, 具体方法可以参考 `这篇文档 <https://github.com/MacHu-GWU/learn_git-project/blob/master/Document/03-Use-SmartGit-With-GitHub-In-Ubuntu.rst>`_。**建议使用网页版本, 或GitHub客户端创建**。 因为这样在创建的时候能选择自动生成一个为Python特殊设计的 ``.gitignore`` 文件, 能够帮助你在commit代码时, 忽略掉一些无用的编译文件, 临时文件, 虚拟环境文件等。

一个Python扩展包项目的GitHub repository name建议是 ``package_name-project``, 即 ``elementary_math-project``, 那么你的项目的GitHub Url则会是 ``https://github.com/github-username/elementary_math-project``。之所以加上project的后缀是为了帮助开发者在文件系统中将项目目录, 和包的代码目录区分开。

接下来, 我们来简单规划一下这个项目的文件目录结构(Layout)。一个组织良好的Python扩展包项目的Layout看起来应该是这样的:

.. code-block:: python

	<project_name-project>   # 项目名称
	# 以下是文件夹
	|--- .git                # git版本控制的数据包
	|--- <package_name>      # 你开发的扩展包的名字, 是一个目录。 你的Python代码都在这里了。
	|--- build               # setup.py 生成的build文件以及sphinx生成的html网站。
	|--- dist                # setup.py 生成的distribute文件。
	|--- source              # documentation网站的reStructuredText文本。
	|--- example             # 你的包的使用方法的一些代码例子。(可选)
	|--- tests               # pytest单元测试文件 (可选)。
	# 以下是文件
	|--- .gitattributes      # github的配置文件。
	|--- .gitignore          # github提交时需要忽略的文件。
	|--- LICENSE.txt         # 版权信息文件。
	|--- requirements.txt    # 该项目所依赖的其他包的信息, 当pip用PyPI在线安装时可能会自动安装的包。
	|--- MANIFEST.in         # PyPI上传安装包时候的发布文件信息。
	|--- setup.cfg           # setup的额外配置信息 (可选)。
	|--- setup.py            # 用于安装的核心脚本。
	|--- README.rst          # 或README.md; github, pypi项目主页说明文档。为了保持Linux系统中的兼容性, 文件名需大写。
	|--- Makefile            # sphinx用于的命令行脚本文件, 由sphinx-quickstart命令自动生成。
	|--- make.bat            # sphinx用于生成网站的批处理文件, 由sphinx-quickstart命令自动生成。
	|--- release_history.rst # 版本更新的详细信息 (可选)。

另外地, 出于个人开发方便起见, 我使用了一些自动化脚本能够简化需要频繁进行的繁琐操作。在这里我只做简要说明, 目前就不进行详细介绍了。

.. code-block:: python

	<project_name>
	|--- install-win.bat   # 在Windows中, 一键安装package, 替换已安装的版本
	|--- install-macos.sh  # 在MacOS中, 一键安装package, 替换已安装的版本
	|--- install-linux.sh  # 在Linux中, 一键安装package, 替换已安装的版本
	|--- build_dist.bat    # 用于一键生成安装包, 在执行 pypi upload 命令前先使用, 然后用pip命令, 尝试从源码安装, 看是否安装成功。
	|--- pypi_register.bat # 用于一键上传package信息到PyPI。
	|--- pypi_upload.bat   # 用于一键发布当前版本到PyPI。
	|--- build_doc.bat     # 用于一键Build文档。其中包括了, 重新安装package到本地, 执行 create_doctree.py, 执行 make.bat。
	|--- view_doc.bat      # 用于一键打开build好的文档网站主页。
	|--- create_doctree.py # 用于生成 module and index 的源文档的Python脚本。
	|--- .travis.yml       # 用于持续集成的travis-ci云服务的配置文件。

笔者制作了所有这些文件的模板 (`可以在这里下载 <https://github.com/MacHu-GWU/elementary_math-project>`_, 在automate-scripts目录下), 并写了一个脚本 `_generate_automate_scripts.py <https://github.com/MacHu-GWU/elementary_math-project/blob/master/automate-scripts/_generate_automate_scripts.py>`_, 只要你输入你的package_name和github_username以及你的主力开发Python版本的名称, 即可一键生成所有文件, 你只需要将其拷贝到前面所提到的Layout中的位置即可。


接下来, 你需要做的事情就是专注于开发, 写出漂亮, 干净, 无Bug, 全平台, 全Python版本兼容的代码。这其中有两个难点:

1. 写出全Python版本兼容的代码, 你可以参考: http://python-future.org/compatible_idioms.html
2. 写出跨平台的代码, 两个值得注意的点是: 1. Windows的文件路径使用 ``\``, 而MacOS和Linux使用 ``/``。2. site-packages目录不同。除此之外请尽量避免系统级操作。

**下一篇**: :ref:`第二章 - 将你的扩展包在PyPI上发布 <pypi>`, 