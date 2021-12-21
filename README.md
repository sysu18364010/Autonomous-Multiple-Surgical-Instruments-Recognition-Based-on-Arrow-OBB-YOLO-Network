# 使用说明
## 1 源代码来源
本项目代码是基于[该代码](https://github.com/ultralytics/yolov3/tree/archive)进行修改

## 2 代码解读
[tran.py](https://blog.csdn.net/weixin_43746266/article/details/117588089)

[model.py](https://blog.csdn.net/weixin_43746266/article/details/117617957)

## 3 该项目代码的使用
### 3.1 图片标注
1. 使用labelImg进行包围盒标注，得到xml文件
2. 将文件放入该项目对应的文件夹下
xml文件放在data/Annotation，图片文件放在data/JPEGImages，class_list.txt放在data下面
3. 运行1.1得到显示有包围盒的图片
4. 利用labeltool里面的landmark文件进行箭头标注，保存路径选择项目中的Arrow文件夹，先标尾点，再标头点，保证箭头落在包围盒内部
5. 标注完后，运行1.2进行标签生成，运行1.3进行数据划分
### 3.2 选出预设锚盒，修改cfg文件
1. 首先选择模型，tiny是比较小的，不是tiny的是比较大的【预设锚盒个数不同】
2. 根据锚盒尺寸，修改对应的cfg文件
tiny有两层yolo层，正常的有三层，每层预置3个锚盒，所以锚盒数=层数*3
需要修改的地方：每一个yolo及其上面的卷积层，classes类别个数，num锚盒数目，最后一层卷积层的数目=3 * (4 + 1 + 4 + 6)【 yolo 层输出包围盒x,y,w,h,置信度，箭头坐标(x1,y1,x2,y2)，类别概率6个，根据自己的参数进行修改】
![在这里插入图片描述](https://img-blog.csdnimg.cn/b347b9b7debe4f3091ac2d84ea970181.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5b-F5L-u5bGF5aOr,size_20,color_FFFFFF,t_70,g_se,x_16)
3. 修改yolo.names

### 3.3 修改其他文件
通过修改train.py选择保存路径，设置相应的权重
- 相应路径
![在这里插入图片描述](https://img-blog.csdnimg.cn/5434043945194fe48e390a91a432df3a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5b-F5L-u5bGF5aOr,size_20,color_FFFFFF,t_70,g_se,x_16)
- 优化算法的权重
![在这里插入图片描述](https://img-blog.csdnimg.cn/a0615977c00c496d84e5d46a30c2f8e6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5b-F5L-u5bGF5aOr,size_16,color_FFFFFF,t_70,g_se,x_16)
- 分阶段记录保存
![在这里插入图片描述](https://img-blog.csdnimg.cn/dffc339f885e4bb0b1199f81a0d1cbc7.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5b-F5L-u5bGF5aOr,size_20,color_FFFFFF,t_70,g_se,x_16)
通过修改dataset.py,确定加载的标签类型与路径
![在这里插入图片描述](https://img-blog.csdnimg.cn/03c8b687bf694ea88df6ab89677fa4a5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5b-F5L-u5bGF5aOr,size_20,color_FFFFFF,t_70,g_se,x_16)
通过修改utils.py，修改误差类型
![在这里插入图片描述](https://img-blog.csdnimg.cn/afc21f91c4964de3ade812a707a3f1ef.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5b-F5L-u5bGF5aOr,size_20,color_FFFFFF,t_70,g_se,x_16)
修改test.py，控制测试时候的输出
![在这里插入图片描述](https://img-blog.csdnimg.cn/f5a02354c8f144aea50fc246aee3067d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5b-F5L-u5bGF5aOr,size_20,color_FFFFFF,t_70,g_se,x_16)







