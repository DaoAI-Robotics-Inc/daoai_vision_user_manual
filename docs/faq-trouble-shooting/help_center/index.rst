如何使用 Help Center
===================

Help Center 网站： https://daoai.atlassian.net/servicedesk/customer/portals

.. image:: Images/1.png
    :align: center 

.. image:: Images/2.png
    :align: center 
|

*各种类别提交流程大致相同，下面以 提交Bug 流程作为例子*

*在 提交Bug 之前，请搜索 相关文档 以及搜索提交过的 相关请求，以避免提交重复或者已解决Bug*

搜索相关文档
~~~~~~~~~~~

打开Help Center网站，找到 搜索栏

.. image:: Images/9.png
    :align: center 
|

搜索 问题

.. image:: Images/10.png
    :align: center 
|

查看文档是否有解决方法，如果没有解决方法，再进行 Bug提交

.. image:: Images/11.png
    :align: center 
|

搜索相关请求
~~~~~~~~~~~

点击 右上角 “Requests”， 选择 “All”

.. image:: Images/12.png
    :align: center 
|

默认显示的是没有处理完的请求

.. image:: Images/13.png
    :align: center 
|

点击 “Status”，取消掉 “OPEN REQUESTS”

.. image:: Images/14.png
    :align: center 
|

此时显示的是 所有的请求

.. image:: Images/15.png
    :align: center 
|

点击 “Request contains”，输入 搜索关键词

.. image:: Images/16.png
    :align: center 
|

点击 搜索结果查看解决方案

.. image:: Images/17.png
    :align: center 
|

显示 Bug 已提交，无需再重复 提交Bug

.. image:: Images/18.png
    :align: center
|

提交 Bug
~~~~~~~~

打开Help Center网站， 点击 “Report a bug“

.. image:: Images/3.png
    :align: center
|

提交Bug 界面如下

.. image:: Images/4.png
    :align: center
|

在此处填写 标题 （简短的描述问题）

.. image:: Images/5.png
    :align: center
|

在输入 标题 之后，系统会自动根据关键字显示 相关文档

可以在提交Bug 之前查看相关问题是否解决问题，避免重复提交已解决问题

.. image:: Images/8.png
    :align: center
|

在此处填写 Bug 的详细介绍，请 **尽量详细** 的描述问题，逐步描述如何复现Bug

请包括： WeRobotics版本，SLC版本（如果问题与相机软件相关），现场工程师名字（如果有的话）

.. image:: Images/6.png
    :align: center
|

在此处添加 附件， 用于补充问题描述， 比如 截图，工作空间，视频 等

.. image:: Images/7.png
    :align: center
|

点击 “Send” 提交 Bug

*例子：* https://daoai.atlassian.net/servicedesk/customer/portal/6/DP-36

提交 产品功能需求
~~~~~~~~~~~~~~~~

打开Help Center网站， 点击 “Suggest improvement“

.. image:: Images/19.png
    :align: center
|

根据图片上的信息填写，请在 "Description" 里面详细描述 需要添加的功能 的介绍，用途和原因，以便我们更好的理解

.. image:: Images/20.png
    :align: center
|

*例子：* https://daoai.atlassian.net/servicedesk/customer/portal/6/DP-45?created=true

提交 项目支持需求
~~~~~~~~~~~~~~~~

打开Help Center网站， 点击 “Project support“

.. image:: Images/21.png
    :align: center
|

在 “Summary” 中填写 项目名和标题。格式为 【项目名】标题。比如: 【安道拓】下料小车Mod Finder检测不稳定。

在 “Description” 中添加 问题的 **详细描述** ，以及需要获得怎样的支持。请包括： WeRobotics版本，SLC版本（如果问题与相机软件相关），现场工程师名字（如果有的话）。请填写尝试过的解决办法。

在 “Attachment” 中上传 附件。如果与流程图相关，请上传 **完整的工作空间** 。添加 **视频** 以更好的展示问题和帮助我们复现。

在 “Labels” 中填写 项目名。如果该 项目名还没有创建的话请创建一个，这样会更好的帮助我们分类。比如： 安道拓

.. image:: Images/22.png
    :align: center
|

*例子：* https://daoai.atlassian.net/servicedesk/customer/portal/6/DP-47

收集数据
~~~~~~~

在现场的工程师需要在调试和实验过程中，尽量的保存更多的实验数据：可以在连接相机后勾选 **保存相机数据**，然后选择 **从编号文件**。这样设置之后，可以继续正常调试和实验，视觉会自动
把每次拍照的dcf、daf、dlf等相片文件保存在工控机本地。这样子的好处是在修改后的可以先进行虚拟实验，节省时间。

.. image:: Images/save_images.png
    :align: center
|

同时，如果在调试和实验中遇到了问题，可以把照片转移到其他的文件夹，以便管理。在重新调试时可以把有问题的数据先运行一次，检查调试结果是否到位，以此节省时间。

.. image:: Images/folders.png
    :align: center
|

问题反馈
~~~~~~~

结合上面 :ref:`收集数据` 文章，在遇到无法解决的问题，提交问题至研发。反馈时，应把问题解释清晰，合并数据，一起提交。

.. :attention::
    在遇到问题时，先独立思考：以前是否遇到过此问题或者相似的问题？是：查看问题中心，是否存在相关的解决方案或者文章；否：也可以查看问题中心，或者询问同行的工程师，是否遇到过类似的问题。

在问题无法解决并且没有相关文档提供有帮助的方案时，提交问题；

提交问题过后，思考是否能用其他的方法、备案或者功能去避开当下的问题，不应该在只苦苦等待，该积极寻找方案解决。

接下来我会用一个例子来讲述如何提交问题：

你在Verification的显示中发现，这个排序有问题：

.. image:: Images/order_wrong.png
    :align: center
|

不难发现，在上图的排序里，6和7的顺序反了。在此情况下，机器人先抓取工件6会使得工件7和工件9位置移动，从而没法正确抓取所有工件。

1. 问题的标题：
*************

标题尽量精简，所有的细节都应当在问题描述当中出现，而不是在标题上把问题都讲述了一遍。

这里我给一个标题的例子：

.. image:: Images/title.png
    :align: center
|

把当前出现问题的项目名称、软件、软件版本、问题的节点和简单点的描述了节点问题。这样子方便于任务卡片的管理；并且后续其他用户查找相关问题时可以快速找出关键字，从而减少问题的重复提交。

太详细或太短的标题都不建议使用，在其他用户遇到相关问题时，搜查关键字会出现太多结果、或者没有出现相关结果。

下面有一些反面例子：

.. image:: Images/bad_title.png
    :align: center
|

2. 问题描述
**********

    1）把发现问题的地方记录下来，如：在Verification节点发现排序的顺序不正确，6应该在7之后；

    2）把目前已尝试过的解决方案和结果大致总结一下，如：尝试修改Verification节点的置信度到 **HIGH**，结果仍旧一样；

    3）目前在无法解决该问题采取了什么方法暂时避开该问题，如：使用了Pick Sort节点暂时代替Verification节点；

3. 图片与视频
************

把问题出现的节点，或者报错信息截图，上传至卡片；尽量把整个屏幕截下来，包括节点参数和控制台输出，便于研发观察；如下图：

.. image:: Images/whole.png
    :align: center
|

把任何对于理解问题有帮助的视频上传到卡片，例如：现场机器人动态或者视觉运行的录屏等；若需要多个视频表达问题，请给视频作注释；如下图：

.. image:: Images/vid.png
    :align: center
|

卡片的回复与更新
**************

在获得卡片的提示、解决方案后，请尽快测试和验证，并在测试后把方案的测试结果更新到卡片上。若需要更多的解决方案，继续在卡片中的评论里留言，联系研发。

分享文件
~~~~~~~

如果不使用附件上传文件，使用第三方网盘。请 *不要使用百度网盘*，在一段时间时候百度网盘会清空文件。

请使用 OneDrive 分享文件，链接为：

https://daoairoboticsinc-my.sharepoint.com/:f:/g/personal/xchen_daoai_com/EvsyfWQXi4BKls0z3ttjkakBDzjVSNe9FUVaHzYghT5OKA?e=ekpd5j

使用方法：
首先在 Help Center 创建请求。在请求创建成功后，会自动生成一个 Reference。这个 Reference 是独特代表着这个新创建的 请求。

.. image:: Images/23.png
    :align: center
|

记住这个 Reference, 打开上面的 OneDrive 链接，创建一个文件夹，文件夹的名字为这个 reference

.. note::
    举个例子，如果要为 DP-59 的ticket上传文件，应该像下图创建文件夹

.. image:: Images/24.png
    :align: center
|

上传文件后，复制这个网页的链接，然后粘贴在创建的 请求 的评论下面。

.. image:: Images/25.png
    :align: center
|

.. image:: Images/26.png
    :align: center
|