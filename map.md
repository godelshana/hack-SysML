## Papers
ML Papers:

### Classification

[ImageNet Classification with Deep Convolutional Neural Networks](http://www.cs.toronto.edu/~fritz/absps/imagenet.pdf)(2010) ：用 deep convolutional neural network 在 2010 年的 ImageNet LSVRC 比赛上分类 1200百万高清(当时的)图片。使用的网络有6000万参数和65万神经元，引入了 dropout 来防止过拟合。


### Object Detection

[Faster R-CNN: Towards Real-Time Object Detection with Region Proposal Networks](https://arxiv.org/pdf/1506.01497.pdf)：提出了 Region Proposal Network (RPN)，和检测网络共享图片卷积特征，因此 region proposal 的代价非常小。


### Network Communication
[Flare: Flexible In-Network Allreduce](https://arxiv.org/pdf/2106.15565.pdf) 2021-6-29:  SwitchML 不灵活，他们设计了一个交换机：by using as a building block PsPIN, a RISC-V architecture implementing the sPIN programming model. 

In-Network Aggregation，[slides](https://www.usenix.org/system/files/nsdi21_slides_sapio.pdf), [Video](https://www.usenix.org/conference/nsdi21/presentation/sapio) [笔记](/network-communication/SwitchML.md) 18 年的

paper: [Scaling Distributed Machine Learning with In-Network Aggregation](https://www.usenix.org/system/files/nsdi21-sapio.pdf)

[NVIDIA SHARP](./network-communication/NVIDIA-Scalable-Hierarchical-Aggregation-and-Reduction-Protocol.md): 看起来跟上述开源方案的非常相似，对比见[这里](./network-communication/SwitchML.md#compare). 16 年就发论文了

[NetReduce: RDMA-Compatible In-Network Reduction for Distributed DNN Training Acceleration](https://arxiv.org/pdf/2009.09736.pdf) : 华为做的，需要硬件实现，好处是不需要修改网卡或交换机。


#### Gradient Compression

[GRACE: A Compressed Communication Framework for Distributed Machine Learning](https://sands.kaust.edu.sa/papers/grace.icdcs21.pdf) (2021) : s. We instantiate GRACE on TensorFlow and PyTorch, and implement 16 such methods.
Finally, we present a thorough quantitative evaluation with a variety of DNNs (convolutional and recurrent), datasets and system configurations. We show that the DNN architecture affects the relative performance among methods. Interestingly, depending on the underlying communication library and computational cost of compression / decompression, we demonstrate that some methods may be impractical. GRACE and the entire benchmarking suite are available as open-source.

[Deep Gradient Compression: Reducing the Communication Bandwidth for Distributed Training](https://arxiv.org/abs/1712.01887)(2017.12,2020-6-23 modify) :  In this paper, we find 99.9% of the gradient exchange in distributed SGD is redundant . 它就是在 GRACE 框架基础上开发的一类算法

[Code: GRACE: A Compressed Communication Framework for Distributed Machine Learning](https://github.com/sands-lab/grace):  is an unified framework for all sorts of compressed distributed training algorithms

### OPs in Network

#### Batch Normalization

[Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift](https://arxiv.org/abs/1502.03167)(2015): 用了 BN 后学习率可以调大，初始化过程更鲁棒。也有 regularization 作用，可以一定程度代替 drop out。 faster training and high performance 

[Norm matters: efficient and accurate normalization schemes in deep networks](https://arxiv.org/pdf/1803.01814.pdf)(2019 ): suggest several alternatives to the widely used L2 batch-norm, using normalization in L1 and L∞ space

Sys Papers:

### Compute Efficiency
[AdderNet: Do We Really Need Multiplications in Deep Learning](https://arxiv.org/abs/1912.13200v2)

### Memory Efficiency

[MONeT: Memory optimization for deep networks](https://openreview.net/pdf?id=bnY0jm4l59)(ICLR 2021) : 发在了 Learning Representation 上，说明不是系统的改进，是算法的改进
1. MONeT: Memory Optimization for Deep Networks：https://github.com/utsaslab/MONeT

Dynamic tensor rematerializatio(2020)
Pushing deep learning beyond the gpu memory limit via smart swapping. (2020)

Tensor-based gpu memory management for deep learning. (2020)

[ActNN: Reducing Training Memory Footprint via 2-Bit Activation Compressed Training](https://arxiv.org/pdf/2104.14129.pdf) (2021-7-6) [My notes](./papers/ActNN.md), [source code notes](ActNN-source-code.md)

[Low-Memory Neural Network Training: A Technical Report](https://arxiv.org/pdf/1904.10631.pdf)(2019-4-24)

[Visual Gifs to show gradient checkpointing](https://github.com/cybertronai/gradient-checkpointing)

Binaryconnect: Training deep neural networks with binary weights during propagations. (2015)

### Parallelism

[Efficient Large-Scale Language Model Training on GPU Clusters](https://arxiv.org/pdf/2104.04473.pdf) (2021.4): 主要介绍了继 Megatron-LM 之后，如何结合多种并行方式，让特定 batchsize 的大transformer 模型，高通吐地运行起来。[阅读笔记](papers/efficient-large-scale-language-model-training.md)

#### Data Parallel
[PyTorch Distributed: Experiences on Accelerating Data Parallel Training](https://arxiv.org/pdf/2006.15704.pdf)(2020.6.28) [My notes](./papers/PyTorch Distributed-Data Parallel Training.md)

[Automatic Cross-Replica Sharding of Weight Update in Data-Parallel Training](https://arxiv.org/abs/2004.13336)(2020-4-28) : 提出了 weights 的自动切分方法，通过高效的通信原语来同步，使用静态分析计算图的方法，应用于 ADAM 或 SGD

[GSPMD: General and Scalable Parallelization for ML Graphs](https://arxiv.org/pdf/2105.04663.pdf)(2021-5-10) (for transformers)



#### Pipeline Parallelism
[PipeDream: Generalized Pipeline Parallelism for DNN Training](https://cs.stanford.edu/~matei/papers/2019/sosp_pipedream.pdf)(SOSP'19)

[GPipe: Efficient training of giant neural networks using pipeline parallelism]()(NIPS 2019)

[PipeDream Source Code](https://github.com/msr-fiddle/pipedream)

[fairscale pipeline parallelism source code](https://github.com/facebookresearch/fairscale/tree/master/fairscale/nn/pipe)

[torochpipe](https://github.com/kakaobrain/torchgpipe)

#### Parallelization Strategies
[Beyond Data and Model Parallelism for Deep Neural Networks](https://arxiv.org/pdf/1807.05358.pdf)
> Defined a more comprehensive search space of parallelization strategies for DNNs called SOAP, which includes strategies to parallelize a DNN in the Sample, Operation, Attribute, and Parameter dimesions. Proposed FlexFlow, a deep learning framework that uses guided randomized search of the SOAP spaceto find a fast parallelization strategy for a specific parallel machine. To accelerate this search, FlexFlow introduces a novel execution simulator that can accurately predict a parallelizaiton strategy's performance.

### Quantization 

And the bit goes down: Revisiting the quantization of neural networks. (ICLR 2020)


### Network
[GradientFlow: Optimizing Network Performance for Distributed DNN Training on GPU Clusters](https://arxiv.org/pdf/1902.06855.pdf)(cs.DC 2019)

> Proposed a communication backend named GradientFlow for distributed DNN training. First we integrate ring-based all-reduce, mixed-precision training, and computation/communication overlap. Second, we propose lazy allreduce to improve network throughput by fusing multiple communication operations into a singe one, and design coarse-grained sparse communication to reduce network traffic by transmitting important gradient chunks.

### Resource Management

[Optimus on top of K8s](https://i.cs.hku.hk/~cwu/papers/yhpeng-eurosys18.pdf)

### Parameter Server
[Scaling Distributed Machine Learning with the Parameter Server](https://www.cs.cmu.edu/~muli/file/parameter_server_osdi14.pdf)(2013?)

## Course：
[CS294-AI-Sys](https://ucbrise.github.io/cs294-ai-sys-sp19/)(UC Berkely)

[笔记](./courses/ucberkely-cs294-ai-sys/)


里面提到的一些经典论文，找到人讨论效果更佳


###  [CS231n: Convolutional Neural Networks for Visual Recognition](http://cs231n.stanford.edu/)
>  This course is a deep dive into the details of deep learning architectures with a focus on learning end-to-end models for these tasks, particularly image classification. During the 10-week course, students will learn to implement and train their own neural networks and gain a detailed understanding of cutting-edge research in computer vision. Additionally, the final assignment will give them the opportunity to train and apply multi-million parameter networks on real-world vision problems of their choice. Through multiple hands-on assignments and the final course project, students will acquire the toolset for setting up deep learning tasks and practical engineering tricks for training and fine-tuning deep neural networks.
> 

### [CSE 599W: Systems for ML](http://dlsys.cs.washington.edu/schedule)
> System aspect of deep learning: faster training, efficient serving, lower
memory consumption

有不少结合TVM的部分，比如 Memory Optimization, Parallel Scheduing, 其中我感兴趣的部分：

#### [Introduction to Deep Learning](http://dlsys.cs.washington.edu/pdf/lecture1.pdf)
##### Evolution of ConvNets:

LeNet(1998)
Alexnet(2012)
GoogleLeNet(2014): Multi-indepent pass way (Sparse weight matrix)

Inception BN (2015): Batch normalization

Residual Net(2015): Residual pass way

Convolution = Spatial Locality + Sharing

ReLU: y = max(x, 0). 

Why ReLU?

* Cheap to compute
* It is roughly linear

Dropout Regularization: Randomly zero out neurons with probability 0.5

Why Dropout? Overfitting prevention.

Batch Normalization: Stabilize the Magnitude.

* Subtract mean
* Divide by standard deviation
* Output is invariant to input scale!
  - Scale input by a constant
  - Output of BN remains the same


Impact:
* Easy to tune learning rate . ?
* Less sensitive initialization. ?

#### [Lecture 1：Distributed Training and Communication Protocols](http://dlsys.cs.washington.edu/pdf/lecture11.pdf)

#### [Lecture 3: Overview of Deep Learning System](http://dlsys.cs.washington.edu/pdf/lecture3.pdf)
Computational Graph Optimization and Execution

Runtime Parallel Scheduing / Networks


#### [Lecture 5: GPU Programming](http://dlsys.cs.washington.edu/pdf/lecture5.pdf)

### https://ucbrise.github.io/cs294-ai-sys-sp19/
[AI-Sys Spring 2019](https://ucbrise.github.io/cs294-ai-sys-sp19/)(UC Berkeley)

## Books：
[Neural Networks and Deep Learning](http://neuralnetworksanddeeplearning.com/chap2.html)

### Deep Learning
[Deep Learning](https://www.deeplearningbook.org/): Ian Goodfellow and Yoshua Bengio and Aron Courville
> intended to help students and practitioners enter the field of machine learning in general and deep learning in particular. The online version of the book is now complete and will remain available online for free.

## OpenSource Frameworks And Libs
### [Pytorch]()
#### JIT

![](https://github.com/pytorch/tvm/blob/master/pt_execution.png?raw=true)

### [Tensorflow]()
[Tensorflow: a system for large-scale machine learning]()(OSDI 2016)

[Automatic differetiation in Pytorch]()(2017)

[Mesh-tensorflow: Deep learning for supercomputers]()(NIPS 2018)

### [Acme: A Research Framework for Distributed Reinforcement Learning](https://arxiv.org/pdf/2006.00979.pdf)(arXiv: June 1 2020)
> Agents are different scales of both complexity and computation -- including distributed versions.

让 RL 从单机版原型可以无痛扩展到多机分布式。
### [Launchpad]()

From Acme Paper:
> Roughly speaking, Launchpad provides a mechanism for creating a distributed program as a graph cnosisting of nodes and edges. Nodes exactly correspond to the modules -- represented as class instances as described above -- whereas the edges represent a client/server channel allowing communication between two modules. The key innovation of Launchpad is that it handles the creating of these edges in such a way that from perspective of any module there is no ditinction between a local and remote communication, e.g. for an actor retrieving parameters from a learner in both instances this just looks like a method call.

直观感觉是这些领域里需要一些基础的框架和库，去解决分布式通信，把问题抽象，和具体场景解耦出来，这样研究人员复用这些轮子。跟当年互联网领域 rpc 通信框架、最近几年的微服务里服务中心、服务主键等功能类似。

![](./imgs/acme-fig4-distrbuted-asynchronous-agent.png)

### Reverb(2020)
The dataset in RL can be backed by a low-level data storaeg system.
> It enables efficient insertion and routing of items and a flexible sampling mechanism that allows:FIFO, LIFO, unifrom, and weighted sampling schemes.


### [Weld](https://www.weld.rs/)(Standford)
Fast rust parallel code generation for data analytics frameworks. Developed at Standford University.
> Weld is a language and runtime for improving the performance of data-intensive applications. It optimizes across libraries and functions by expressing the core computations in libraries using a common intermediate repersentation, and optimizing across each framwork.
> Modern analytics applications combine multiple functions from different libraries and frameworks to build complex workflows.
> Weld's take on solving this problem is to lazily build up a computation for the entire workflow, and then optimizingn and evaluating it only when a result is needed.
 
看起来就是解决掉用不同的库和框架来构建复杂工作流时的效率问题。通过引入一层中间表达，然后再实现到不同的框架里来做联合优化。

Paper: [Weld: Rethinking the Interface Between Data-Intensive Applications.](https://arxiv.org/abs/1709.06416)
> To address this problem, we propose Weld, a new interface between data-intensive libraries that can optimize across disjoint libraries and functions. Weld can be integrated into existing frameworks such as Spark, TensorFlow, Pandas and NumPy without chaning their user-facing APIs.

Related research papers: [PipeDream: General Pipeline Parallelism for DNN Training](https://cs.stanford.edu/~matei/papers/2019/sosp_pipedream.pdf) (SOSP'19)

### Table Data Storage
[Reverb is an efficient and easy-to-use data storage and trasport system designed for machine learning research](https://github.com/deepmind/reverb)(DeepMind, 2021-4-22)

> Used an an experience replay system for distributed reinforcement learning algorithms

## Videos
[Flexible systems are the next frontier of machine learning](https://www.youtube.com/watch?v=Jnunp-EymJQ&list=WL&index=14) Stanford 邀请 Jeff Dean 和 Chris Re 探讨最新的进展(2019) [My Notes](./videos/Flexible-systems-are-the-next-frontiner-of-machine-learning.md)

## Hardware
[NVLink](./hardware/GPU/nvlink.md) vs PCiE

## Visualizing Neural Networks
[Deep Learning in your browser](https://cs.stanford.edu/people/karpathy/convnetjs/)
## Misc

[HPC-oriented Latency Numbers Every Programmer Should Know](https://gist.github.com/understeer/4d8ea07c18752989f6989deeb769b778)

[Curriculum Learning for Natural Language Understanding](https://aclanthology.org/2020.acl-main.542.pdf)()
[On The Power of Curriculum Learning in Training Deep Networks](https://arxiv.org/abs/1904.03626) (2019) : 传统的要求batch 的训练数据是均匀分布，而这个是模拟了人的学习过程：从简单的任务开始，逐步增加难度。解决了两个问题：1）根据训练难度排序数据集 2）计算逐步增加了难度的 一系列 mini-batches
