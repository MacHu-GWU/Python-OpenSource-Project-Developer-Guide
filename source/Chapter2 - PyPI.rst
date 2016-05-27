.. _pypi:

第二章 - 将你的扩展包在PyPI上发布
=================================

.. image:: _static/pypi-logo.jpg
   :height: 200px
   :width: 200px


第一步, 安装 pip
-------------------------------------------------------------------------------

.. image:: _static/pip-logo.png

`pip <https://pip.pypa.io/en/stable/>`_ 是Python社区官方的Package Control(包管理)工具, 功能非常强大。在正式发布到PyPI之前, 需要用pip测试在本地机器上安装。这样才能保证别人下载你发布的安装包也能够成功安装。

有关pip的安装, 请参考 `这篇文档 <https://github.com/MacHu-GWU/learn_pip-project>`_


第二步, 创建 ``setup.py`` 脚本
-------------------------------------------------------------------------------
``setup.py`` 脚本顾名思义是用于安装的。其中有许多参数需要我们去设置, 这些参数定义了各种各样的安装行为, 也为PyPI上你的项目提供了各种各样的描述性的信息, 例如版本号。固然我们可以为我们的每个项目手动设定各个参数, 但因为 ``setup.py`` 本身也是Python脚本, 所以我们可以通过定义几个重要变量, ``package_name`` 和 ``github_username``, 其他的重复性劳动就交给程序自动去做。`一个典型的setup.py文件可以参考这个模板 <https://github.com/MacHu-GWU/elementary_math-project/blob/master/setup.py>`_。

还记得上一章我们 :ref:`在介绍项目的Layout时 <create_repository>` 提到, 我们可以使用自动化脚本生成 ``setup.py`` 文件, 而不需要手动输入。我建议, 参考本例之后, 创建了你自己的 ``setup.py`` 文件之后, 也将其做成自动化脚本。使得每当你需要开发一个新项目时, 只需要改变几个关键的变量的值, 即可轻松使用。


有关 ``setup.py`` 的详细设置, 请参考这篇文档 :ref:`<setup_script>`


第三步, 创建 ``MANIFEST.in``, ``requirements.txt``, ``README.rst`` 文件
-------------------------------------------------------------------------------
``MANIFEST.in`` 文件可以告诉 ``setup.py`` 在使用 ``sdist`` 命令制作安装包时, 要包含哪些文件。例如有时候我们需要包含版权文件, 有时我们的程序需要依赖一些数据文件。
至于如何写 ``MANIFEST.in`` 文件, 可以参考 `本文档中的例子 <https://github.com/MacHu-GWU/elementary_math-project/blob/master/MANIFEST.in>`_, `也可以参考官方文档说明 <https://docs.python.org/2/distutils/sourcedist.html#manifest-template>`_。

``requirements.txt`` 文件指明了为了正确运行本项目, 需要安装哪些依赖的包。至于如何写 ``requirements.txt`` 文件, 可以参考 `官方文档说明 <https://pip.pypa.io/en/stable/user_guide/#requirements-files>`_。

``README.rst`` 文件是GitHub的项目首页的说明文档, 也可以作为PyPI首页的说明文档, 通常还作为文档网站的首页。所以此文件非常重要。你可以在这个文件中放入任何你想要的信息。为了方便起见, 我提供了 `一个例子 <https://github.com/MacHu-GWU/elementary_math-project/blob/master/README.rst>`_。**同样, 此文件也可以使用自动化脚本生成**。


.. _build_dist:

第四步, 制作你的安装包, 并在本地进行测试安装
-------------------------------------------------------------------------------
在命令行输入以下命令, Python将会自动生成两个文件夹 ``build`` 和 ``dist``。分别储存了编译过程中的临时文件, 和最终发布的安装包。

.. code-block:: console

	# 创建zip安装包
	$ python setup.py sdist

	# 创建全版本通用的wheel安装包
	$ python setup.py bdist_wheel --universal

我提供了一个 `Windows批处理脚本自动运行此过程 <https://github.com/MacHu-GWU/elementary_math-project/blob/master/build_dist.bat>`_。

制作完成之后, 你就可以先使用 ``$ pip uninstall elementary_math`` 清理已安装的版本, 然后使用 ``$ pip install elementary_math-0.0.1.zip`` 从刚才制作的安装包进行安装。如果安装成功, 则使用之前在开发过程中你的测试代码进行测试。若全部成功, 则说明你可以准备将其发布到PyPI上了。

注: 有关测试的部分请参考 `这篇文档 <https://github.com/MacHu-GWU/learn_pytest-project>`_。


.. _pypi_register:

第五步, 在PyPI注册你的项目信息
-------------------------------------------------------------------------------
注册你的项目信息是指, 创建一个PyPI的项目主页, 包含了一些介绍和你的项目的相关信息。我们以 `requests <https://pypi.python.org/pypi/requests>`_ 这一Python社区最流行的http扩展包(作者是Python社区顶级大牛, 他的项目值得每一个Python开发者作为教科书来学习, 无论是代码还是文档)为例, 看看PyPI的主页有哪些主要元素。


Title and Version
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``requests 2.10.0``, 这部分是你的项目名称和版本号。


Short Description
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
``Python HTTP for Humans.``, 这部分文本是你的项目的一句话短介绍。也是 ``setup.py`` 文件中 ``setup()`` 函数中 ``description`` 项中的值。


Long Description
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
一段长的介绍, 介绍你的扩展包的所有相关信息。建议这部分信息从 ``README.rst`` 文件中读取。

这部分用 `reStructuredText <http://docutils.sourceforge.net/rst.html>`_ 标记语言所写成。通常使用 ``readme.rst`` 文件中的内容, 同时也通常被作为github主页的页面。值得注意的是, **这部分内容中使用的是纯rst文件所支持的语法。并不支持sphinx中所支持的特殊语法。**


File (用户可下载的文件)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
在你执行了下一节中将要介绍的 **上传安装包至PyPI** 之后, 你上传的文件就会被放在这里。这部分的文件是, 当你使用 ``pip install package`` 命令是, 就会自动从这里下载安装包, 然后 ``pip`` 会自动完成 `build, install <https://docs.python.org/2/install/#splitting-the-job-up>`_, clean up的全过程。

同时用户还可以在PyPI的网页自己手动上传一些其他格式的安装文件, 比如: ``.whl``, ``.egg``, ``.exe`` (用于windows下的安装)。


MetaData (其他相关信息)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
这里存放的是你在 ``setup.py`` 文件中填写的例如: Author, Home Page, License。这部分可以在 ``setup.py`` 中定义, 也可以在PyPI网站界面进行手动填写。

了解其他的 metadata field `请戳这里 <https://docs.python.org/2/distutils/setupscript.html#additional-meta-data>`_


**当用户完成了setup.py文件的制作之后, 就可以将这些信息注册到PyPI了**。具体做法是在命令行中输入如下命令:

.. code-block:: console
	
	$ python setup.py register -r pypi

第一次注册时, 会需要填写你的PyPI账号密码, 然后系统会在你的操作系统用户根目录下生成一个.pypirc文件, 里面包含了你的身份信息。在同一台机器同一个账户, 以后就不会需要输入账号密码了。


.. _pypi_upload:

第六步, 将你的安装包上传至PyPI
-------------------------------------------------------------------------------

如果你有仔细阅读上一节的内容, 其实在 **File** 部分中所提到的一个默认的源代码包。(可以没有其他 ``.whl``, ``.exe`` 但一定会有的源码包)。使用下面的命令所上传的安装包是带有版本信息记录的, 只要你上传过一次, 就会在PyPI服务器上留下记录, 以同样的软件版本号无法再次上传。当开发流程熟悉稳定之后, 用户可以使用 ``upload`` 命令上传所有种类的安装包。但我推荐新手自己build安装包, 然后针对一个版本号在网页界面进行手动上传, 删除管理。

为防止忘记, 附上上传默认源码安装包的命令:

.. code-block:: console
	
	$ python setup.py sdist upload -r pypi

下面的命令能将你制作的安装包上传到PyPI上供其他用户下载和安装:

.. code-block:: console

	$ python setup.py sdist upload -r pypi

请注意, 进行上传操作前请确保你已经在本地 :ref:`测试过你要上传的安装包 <build_dist>`。因为当你上传过该版本的文件之后, PyPI服务器就会阻止你以同样的版本号再次上传。所以为了避免上传了有Bug的安装包的情况出现, 请先测试。在对开发流程熟悉之前, 建议新手自己Build安装包, 然后在网页界面手动上传, 管理。 

**下一篇**: :ref:`第三章 - 创建并部署你的文档网站 <doc>`, 