.. title: Matlab 3D Plot
.. slug: matlab-3d-plot
.. date: 2016-05-25 20:02:10 UTC+08:00
.. tags: matlab
.. category: programming
.. link: 
.. description: 
.. type: text
.. author: YONG

之前我一直是MMA的忠实用户, 因为它symbolic运算强大且精确. 也从来没有实际感受过它和其它计算系统之间的速度差别. 我之前有一组数据是连着跑了一天一夜, 因为MMA有着天然的内存泄漏问题, 为了防止它把我电脑的16G内存全吃掉后卡死, 我必须将它运行的中间结果都打印出来, 每次吃完内存后就重启MMA释放内存, 从中断的地方接着运行. 前天又想算一组误差数据, 本以为天亮后计算结果就会出来, 可是并没有, 当我到了实验室还仍然是Running的状态. 这让我愤怒地转向了Julia, 边自学边上阵, 大半天加一晚上把程序弄到了Julia里来, 到今天已经能正常地得出结果了. 

.. TEASER_END

Julia使用感受: 很快, 真的很快, 真真真的太TM快了. MMA上一跑就要至少一天还没跑出结果的东西, Julia居然一分钟内就把结果给了我. 简真像加了特技一样. 不知道是不是因为MMA编程技术太烂的原因. 本来还搜索了Julia并行计算的内容, 想着怎么捣鼓一下, 结果完全没用上. 数据出来了, 不过几经周折发现Julia画图是个短板. 继续用回MMA, 40几M的数据文档一加载就是接近十分钟, 画完图整个MMA就跟死了一样. 好吧, 又是我不专业的锅. 没办法, Matlab走起. 终于扯到正题, 我本来只是想写点matlab 3d画图命令做备忘之用, 不留神一提笔就把整个事情的由来也唠叨了一回. 

作图要求: 两个向量分别是x, y轴数据, 一个矩阵的内容为z数据.

尝试结论: 因为数据比较大且不规则, surf结果太丑, 没有好的配色, scatter3直接把电脑整假死了, mesh结果比较令人满意.

数据:

.. code:: matlab

    L=0.05:0.05:50.0;
    sigma=0.05:0.05:pi/(0.05*0.05);
    value=dlmread('C:\\home\\Dropbox\\juliastuff\\result.txt');
    % value(value==0)=NaN % omit 0 values
    mesh(sigma,L,value)
    xlabel('\sigma'),ylabel('L'),zlabel('\epsilon')
    axis([0.0 pi/(0.05*0.05) 0.0 50.0 0.0 8e-3])
    
注:

1. 数据导入参考 `Import Numeric Data from Text Files <http://www.mathworks.com/help/matlab/import_export/import-numeric-data-from-a-text-file.html>`_
2. matlab貌似矩阵是列主序的, 幸好L和sigma的长度不一样, mesh报错才发现. 参考 `Row-major order <https://en.wikipedia.org/wiki/Row-major_order>`_
3. 3D 作图参考 `Plotting 3D Surfaces <http://math.loyola.edu/~loberbro/matlab/html/Plot3Dsurfaces.html>`_
4. 在mesh命令之前, 因为本数据中0都表示无效, 可以用 value(value==0)=NaN 使最终的图里不显示0
5. 其它几种但此例中效果不理想的作图: surf(sigma,L,value), contour(sigma,L,value), 以及 scatter3:

   .. code:: matlab

       Lrep=repmat(L,1,25132);
       sigmarep=repmat(sigma,1,1000);
       valuerep=reshape(value',1,1000*25132);
       scatter3(Lrep,sigmarep,valuerep)

画图搞定, 继续搞Julia.

