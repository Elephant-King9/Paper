**A Gentle Introduction to Graph Neural Networks**[[博客](https://distill.pub/2021/gnn-intro/)]

# 1  什么是图

## 1.1 图相关的任务

- 图层面
  - 对图进行分类，判断有没有两个环
  - ![image-20250609145525473](/Users/sitianyi/Paper/Base_Model/GNN/assets/pics/A Gentle Introduction to Graph Neural Networks/image-20250609145525473.png)
- 顶点层面
  - 假设确定两个定点A,B，对其余节点进行分类，判断是属于A还是属于B
  - ![image-20250609145619583](/Users/sitianyi/Paper/Base_Model/GNN/assets/pics/A Gentle Introduction to Graph Neural Networks/image-20250609145619583.png)
- 边层面
  - 对图像进行建模，每一条边代表不同的人之间目前的状态，判断人与人之间的状态
  - ![image-20250609145722695](/Users/sitianyi/Paper/Base_Model/GNN/assets/pics/A Gentle Introduction to Graph Neural Networks/image-20250609145722695.png)

## 1.2 图的信息表示

图分为四种信息

- 顶点属性
- 边属性
- 全局信息
- 顶点与顶点的连接性

![image-20250609150240645](/Users/sitianyi/Paper/Base_Model/GNN/assets/pics/A Gentle Introduction to Graph Neural Networks/image-20250609150240645.png)

顶点和边都适用标量保存

顶点和顶点的连接性使用标量对表示

全局信息用标量表示

图中的所有标量都可以转化为向量

# 2 GNN

## 2.1 单层GNN表示

将全局向量，定带向量，边向量分别放进不同的MLP中更新数据，

![image-20250609151022031](/Users/sitianyi/Paper/Base_Model/GNN/assets/pics/A Gentle Introduction to Graph Neural Networks/image-20250609151022031.png)

## 2.2 对于顶点层面的问题

假设顶点层面的问题是个二分类问题

### 假设已经有当前节点向量

我们只需要将每个顶点的向量接一个全链接层转化为二分类就可以了

![image-20250609151227040](/Users/sitianyi/Paper/Base_Model/GNN/assets/pics/A Gentle Introduction to Graph Neural Networks/image-20250609151227040.png)

### 假设没有当前节点向量

使用pooling根据周围的所有节点进行推断

![image-20250609151534206](/Users/sitianyi/Paper/Base_Model/GNN/assets/pics/A Gentle Introduction to Graph Neural Networks/image-20250609151534206.png)

## 2.3 最简单的GNN网络

![image-20250609151829611](/Users/sitianyi/Paper/Base_Model/GNN/assets/pics/A Gentle Introduction to Graph Neural Networks/image-20250609151829611.png)

### 问题

在MLP部分，边、顶点、全局分别经过三个不同的MLP，其中顶点与顶点的联系等图中的信息并没有被考虑，可能会导致捕获到图中的信息并不完全

### 解决方法

![image-20250609152649921](/Users/sitianyi/Paper/Base_Model/GNN/assets/pics/A Gentle Introduction to Graph Neural Networks/image-20250609152649921.png)

同理，顶点可以同时将相邻的边的向量也进行组合，边也可以结合相邻顶点的信息

![image-20250609153141455](/Users/sitianyi/Paper/Base_Model/GNN/assets/pics/A Gentle Introduction to Graph Neural Networks/image-20250609153141455.png)

## 2.4 全局信息的作用

 当图非常稀疏的时候，可能节点A和节点B之间的信息需要很多层才能建立联系

全局信息的作用是作为一个超级节点，相当于一个节点既和所有边相联又和所有顶点相联，这样就可以保证在层数较低的情况下能交互到所有的信息

![image-20250609153606399](/Users/sitianyi/Paper/Base_Model/GNN/assets/pics/A Gentle Introduction to Graph Neural Networks/image-20250609153606399.png)

