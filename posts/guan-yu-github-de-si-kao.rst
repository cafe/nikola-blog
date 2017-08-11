.. title: 关于GitHub的使用思考
.. slug: guan-yu-github-de-shi-yong-si-kao
.. date: 2016-08-23 11:41:45 UTC+08:00
.. tags: github
.. category: tools
.. link: 
.. description: 
.. type: text
.. author: YONG

之前一直对使用GitHub存放博客(静态网站)很痴迷, 后来又发现Gist的好处, 最近又开始频繁使用普通的Repo来存放一些东西. GitHub光是文字记录功能的产品不止这几样, 比如评论和Wiki等等. 这就让我开始思考, 到底哪些东西适合用对应的哪一项功能来完成或是存放.

.. TEASER_END

先说GitHub Pages. 这个除了展示静态的网页(网站)之外并没有什么神奇的功能 - GitLab也可以, 只是在国内访问受限. 既然是网页, 除了文字图片等核心的东西之外, 还有不少与网页装饰相关的边角料. 而且更新也并不直观便捷, 需要使用Git上传. 所以每次写东西都是先放在自己硬盘里, 等攒上一些东西后一并更新. 我觉得这种展示方式是面向大众的, 适合表达一些自己的一些感想, 观点, 以及需要在必要时展示给别人的demo等等. 另外一种情况需要用到GitHub Pages, 即涉及到LaTeX数学公式的情况. GitHub不支持对README文本文档中的公式进行MathJax渲染, 因此需要GitHub Pages中实现(Nikola就支持). 另外GitHub Pages支持category, tags等功能, 也是比较方便的地方.

再说说Repository. 它是整个GitHub的核心, GitHub Pages虽然表面花哨, 其实也是基于Repo的. 为什么GitHub吸引我, 很大的一个原因就是它对各种文本文档的渲染支持, 比如 .md, .rst, .org 等. 正是由于这个原因, 很多方面可以直接代替GitHub Pages的功能. 比如一些工具设置步骤, 问题的解决方案等, 都可以写在 .org 文档里, GitHub直接就要以看到渲染后的结果, 不用Git客户端, 编辑也很方便快捷, 几乎算是"所见即所得". 而且比起GitHub Pages更简洁, 只用储存有用的干货, 与美观相关的修饰全都用不着. 缺点是目前不支持LaTeX公式渲染(但可以用反斜杠插入希腊字母), 因此涉及数学公式表达的还是得靠GitHub Pages. 现在越来越喜欢用Repo来管理和记录自己喜欢的一切东西, 比如日志, 目录, Task, List, 心得, 教程, 图片等等, 因为是Git, 所以自带历史版本信息, 比起传统的微博, QQ空间之类的要方便不少, 而且可以在任何时候用Git工具备份到自己本地电脑上, 着实好用. 以后Repo里就存放各种和技术相关的东西, 不再麻烦地使用GitHub Pages了.

备注: 个人偏好 .org 格式, 因为它风格统一, 不会有不同的标准. 而GitHub支持的 .md 与 .rst 可能与其它的标准不兼容. 而且 .org 支持语法高亮(.rst好像GitHub并不支持), 且其它功能如插入图片等都没有问题.

Gist适合写一些代码小片断, 且免费用户也可以将Gist设为Secret. 缺点是当Gist一多, 又没有好的归类, 就不太容易找. 因此现在我更喜欢用Repo来专门存放修改各种code snippets.

Wiki和评论也是很好的文档记录工具, 也有很多使用的trick(插入图片也可以用引用评论中图片的方式实现). 但因为不能直接用Git工具管理和备份, 因此我觉得并不如Repo实在, 所以自己用得就比较少.