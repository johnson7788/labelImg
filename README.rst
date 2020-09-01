LabelImg
========

.. image:: https://img.shields.io/pypi/v/labelimg.svg
        :target: https://pypi.python.org/pypi/labelimg

.. image:: https://img.shields.io/travis/tzutalin/labelImg.svg
        :target: https://travis-ci.org/tzutalin/labelImg

.. image:: /resources/icons/app.png
    :width: 200px
    :align: center

LabelImg is a graphical image annotation tool.

It is written in Python and uses Qt for its graphical interface.

Annotations are saved as XML files in PASCAL VOC format, the format used
by `ImageNet <http://www.image-net.org/>`__.  Besides, it also supports YOLO format

.. image:: https://raw.githubusercontent.com/tzutalin/labelImg/master/demo/demo3.jpg
     :alt: Demo Image

.. image:: https://raw.githubusercontent.com/tzutalin/labelImg/master/demo/demo.jpg
     :alt: Demo Image

`Watch a demo video <https://youtu.be/p0nR2YsCY_U>`__

Installation
------------------


Build from source
~~~~~~~~~~~~~~~~~

Linux/Ubuntu/Mac requires at least `Python
2.6 <https://www.python.org/getit/>`__ and has been tested with `PyQt
4.8 <https://www.riverbankcomputing.com/software/pyqt/intro>`__. However, `Python
3 or above <https://www.python.org/getit/>`__ and  `PyQt5 <https://pypi.org/project/PyQt5/>`__ are strongly recommended.


Ubuntu Linux
^^^^^^^^^^^^
Python 2 + Qt4

.. code:: shell

    sudo apt-get install pyqt4-dev-tools
    sudo pip install lxml
    make qt4py2
    python labelImg.py
    python labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]

Python 3 + Qt5 (Recommended)

.. code:: shell

    sudo apt-get install pyqt5-dev-tools
    sudo pip3 install -r requirements/requirements-linux-python3.txt
    make qt5py3
    python3 labelImg.py
    python3 labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]

macOS
^^^^^
Python 2 + Qt4

.. code:: shell

    brew install qt qt4
    brew install libxml2
    make qt4py2
    python labelImg.py
    python labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]

Python 3 + Qt5 (Recommended)

.. code:: shell

    brew install qt  # Install qt-5.x.x by Homebrew
    brew install libxml2

    or using pip

    pip3 install pyqt5 lxml # Install qt and lxml by pip

    cd labelImg
    make qt5py3
    python3 labelImg.py
    python3 labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]


Python 3 Virtualenv (Recommended)

Virtualenv can avoid a lot of the QT / Python version issues

.. code:: shell

    brew install python3
    pip3 install pipenv
    pipenv run pip install pyqt5==5.13.2 lxml
    pipenv run make qt5py3
    python3 labelImg.py
    [Optional] rm -rf build dist; python setup.py py2app -A;mv "dist/labelImg.app" /Applications

Note: The Last command gives you a nice .app file with a new SVG Icon in your /Applications folder. You can consider using the script: build-tools/build-for-macos.sh


Windows
^^^^^^^

Install `Python <https://www.python.org/downloads/windows/>`__,
`PyQt5 <https://www.riverbankcomputing.com/software/pyqt/download5>`__
and `install lxml <http://lxml.de/installation.html>`__.

Open cmd and go to the `labelImg <#labelimg>`__ directory

.. code:: shell

    pyrcc4 -o lib/resources.py resources.qrc
    For pyqt5, pyrcc5 -o libs/resources.py resources.qrc

    python labelImg.py
    python labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]

Windows + Anaconda
^^^^^^^^^^^^^^^^^^

Download and install `Anaconda <https://www.anaconda.com/download/#download>`__ (Python 3+)

Open the Anaconda Prompt and go to the `labelImg <#labelimg>`__ directory

.. code:: shell

    conda install pyqt=5
    conda install -c anaconda lxml
    pyrcc5 -o libs/resources.py resources.qrc
    python labelImg.py
    python labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]

Get from PyPI but only python3.0 or above
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
This is the simplest (one-command) install method on modern Linux distributions such as Ubuntu and Fedora.

.. code:: shell

    pip3 install labelImg
    labelImg
    labelImg [IMAGE_PATH] [PRE-DEFINED CLASS FILE]


Use Docker
~~~~~~~~~~~~~~~~~
.. code:: shell

    docker run -it \
    --user $(id -u) \
    -e DISPLAY=unix$DISPLAY \
    --workdir=$(pwd) \
    --volume="/home/$USER:/home/$USER" \
    --volume="/etc/group:/etc/group:ro" \
    --volume="/etc/passwd:/etc/passwd:ro" \
    --volume="/etc/shadow:/etc/shadow:ro" \
    --volume="/etc/sudoers.d:/etc/sudoers.d:ro" \
    -v /tmp/.X11-unix:/tmp/.X11-unix \
    tzutalin/py2qt4

    make qt4py2;./labelImg.py

You can pull the image which has all of the installed and required dependencies. `Watch a demo video <https://youtu.be/nw1GexJzbCI>`__


Usage
-----

Steps (PascalVOC)
~~~~~~~~~~~~~~~~~

1.按照上述说明进行构建和启动。
2.在菜单/文件中单击“更改默认保存的注释文件夹”
3.点击“打开目录”
4.点击“创建RectBox”
5.单击并释放鼠标左键，选择一个区域来标注矩形框
6.您可以使用鼠标右键拖动矩形框来复制或移动它

注释将保存到您指定的文件夹中。

您可以参考以下热键以加快工作流程。

Steps (YOLO)
~~~~~~~~~~~~

1.在“ data / predefined_classes.txt”中，定义将用于训练的的标签列表。

2.按照上述说明进行构建和启动。

3.在工具栏中的“保存”按钮下方，单击“ PascalVOC”按钮以切换为YOLO格式。

4.您可以使用Open / OpenDIR处理单个或多个图像。 完成单个图像后，单击“保存”。

YOLO格式的txt文件将以与您的图片相同的名称保存在同一文件夹中。 名为“ classes.txt”的文件也被保存到该文件夹。 “ classes.txt”定义了YOLO标签所引用的类名列表。

注意：

-标签列表在处理图像列表的过程中不得更改。 保存图像时，classes.txt也将被更新，而以前的注释将不被更新。

-保存为YOLO格式时，请勿使用“default class”功能，否则将不会被引用。

-当保存为YOLO格式时，“difficult”标志将被丢弃。

Create pre-defined classes
~~~~~~~~~~~~~~~~~~~~~~~~~~

你可以编辑
`data/predefined\_classes.txt <https://github.com/tzutalin/labelImg/blob/master/data/predefined_classes.txt>`__
去加载预先定义的类别

Hotkeys
~~~~~~~

+------------+--------------------------------------------+
| Ctrl + u   | 从目录加载所有图像                            |
+------------+--------------------------------------------+
| Ctrl + r   | 更改默认注释目标目录                          |
+------------+--------------------------------------------+
| Ctrl + s   | Save                                       |
+------------+--------------------------------------------+
| Ctrl + d   | 复制当前标签和矩形框                           |
+------------+--------------------------------------------+
| Space      | 将当前图像标记为已验证                         |
+------------+--------------------------------------------+
| w          | 创建一个矩形框                                |
+------------+--------------------------------------------+
| d          | Next image                                 |
+------------+--------------------------------------------+
| a          | Previous image                             |
+------------+--------------------------------------------+
| del        | Delete the selected rect box               |
+------------+--------------------------------------------+
| Ctrl++     | Zoom in                                    |
+------------+--------------------------------------------+
| Ctrl--     | Zoom out                                   |
+------------+--------------------------------------------+
| ↑→↓←       | 键盘箭头移动选定的矩形框                        |
+------------+--------------------------------------------+

**Verify Image:**

When pressing space, the user can flag the image as verified, a green background will appear.
This is used when creating a dataset automatically, the user can then through all the pictures and flag them instead of annotate them.

**Difficult:**

The difficult field is set to 1 indicates that the object has been annotated as "difficult", for example, an object which is clearly visible but difficult to recognize without substantial use of context.
According to your deep neural network implementation, you can include or exclude difficult objects during training.

How to reset the settings
~~~~~~~~~~~~~~~~~~~~~~~~~

In case there are issues with loading the classes, you can either:

1. From the top menu of the labelimg click on Menu/File/Reset All
2. Remove the `.labelImgSettings.pkl` from your home directory. In Linux and Mac you can do:
    `rm ~/.labelImgSettings.pkl`


How to contribute
~~~~~~~~~~~~~~~~~

Send a pull request

License
~~~~~~~
`Free software: MIT license <https://github.com/tzutalin/labelImg/blob/master/LICENSE>`_

Citation: Tzutalin. LabelImg. Git code (2015). https://github.com/tzutalin/labelImg

Related
~~~~~~~

1. `ImageNet Utils <https://github.com/tzutalin/ImageNet_Utils>`__ to
   download image, create a label text for machine learning, etc
2. `Use Docker to run labelImg <https://hub.docker.com/r/tzutalin/py2qt4>`__
3. `Generating the PASCAL VOC TFRecord files <https://github.com/tensorflow/models/blob/4f32535fe7040bb1e429ad0e3c948a492a89482d/research/object_detection/g3doc/preparing_inputs.md#generating-the-pascal-voc-tfrecord-files>`__
4. `App Icon based on Icon by Nick Roach (GPL) <https://www.elegantthemes.com/>`__
5. `Setup python development in vscode <https://tzutalin.blogspot.com/2019/04/set-up-visual-studio-code-for-python-in.html>`__
6. `The link of this project on iHub platform <https://code.ihub.org.cn/projects/260/repository/labelImg>`__


Stargazers over time
~~~~~~~~~~~~~~~~~~~~

.. image:: https://starchart.cc/tzutalin/labelImg.svg

