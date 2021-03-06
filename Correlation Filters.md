***
* 最早将相关滤波用于目标跟踪的是MOSSE（2010）算法，它采用的是灰度特征，速度达到669fps，远远超出了其他算法，准确度一般，论文中还提到峰值旁瓣比（PSR），用来判断目标是否被遮挡或者跟踪失败，在以后的算法中也有用PSR来判断遮挡或者跟踪失败的，也有对PSR改进的算法，如果论文涉及的是遮挡问题的话一定绕不开PSR。  
* CSK（2012）在MOSSE的基础上引入了循环矩阵和核的概念，这是KCF的原型，但它用的是灰度特征，速度上320fps，精度上比MOSSE大大的提升，它主要是针对传统算法中采用稀疏采样造成样本冗余的问题提出的解决方案，从此循环矩阵和核技巧在相关滤波的目标跟踪领域大放异彩。  
* KCF（2014）和CSK是同一个作者，都是Henriques, KCF可以说是对CSK的完善，论文中对岭回归，循环矩阵、核技巧、快速检测等有着坚实的理论基础和完整的公式推导，这篇论文看起来完美无缺，KCF采用的HOG特征，代码中用的是fHOG，将单通道转换成了多通道，核函数有三种高斯核、线性核和多项式核，高斯核的精确度最高，线性核略低于高斯核，但速度上远高于高斯核。  
* CN（2014）是在CSK的基础上提出来的，它采用的是颜色特征（color names），不同语言中对颜色的描述是不一样的，英语中对颜色描述的11个单词，最接近人眼的视觉，论文中也用实验证明CN这种颜色空间相对于RGB、HSV、LAB等效果更好，为了提高运算速度，论文中还用了PCA将10维的特征降维到2维，并改进了模型跟踪方案。  
* DSST（2014）是基于MOSSE提出来的，主要针对的是尺度变化问题，文中用的是尺度相关滤波器，原理上和KCF相似，都是通过相关滤波器找到相关值最大的点对应的图像作为目标，DSST采用了33种不同尺度，相对时间上较慢，但是尺度估计的精度相对较高。  
* LCT（2015）在DSST的基础上增加了置信度滤波器，借鉴了TLD中的随机蕨分类器，它是针对长时间目标跟踪问题的，因此涉及到了遮挡问题，该算法用PSR来判断目标是否遮挡，遮挡后用随机蕨分类器重新定位目标，准确度相对于之前的算法大大提高，但是由于每帧都训练随机蕨分类器导致速度过慢。  
* SAMF（2014）是在KCF的基础上将CN特征和HOG特征串联，并且加入尺度估计，共有7种尺度变换，它与DSST尺度估计的主要区别就是，它将尺度估计和位置估计放在一起用于相关运算，取得最大值的点对应的图像即是位置最佳也是尺度最佳，而DDST是将位置估计和尺度估计分开进行，先求最佳的位置，在在此基础上求最佳的尺度。SAMF的另一个特点是对遮挡具有一定的抵抗能力，这说明好的特征才是目标跟踪的关键，也从侧面反映了目标跟踪的本质还是检测问题。  
* SRDCF（2015）是在DCF的基础上针对边界效应提出的解决方案，它加入了空间惩罚项，在效果上取得了突破性的进步，但空间惩罚项的加入破坏了岭回归方程的封闭解，只能用高斯-赛德尔迭代法求解，使得运算速度非常慢。  
* Staple(2016）也是HOG特征和颜色特征的结合，不过它是在响应阶段的融合，不是在特征阶段的融合，颜色特征是颜色直方图，不是CN，它可以看成是DSST算法和DAT（非相关滤波）算法的结合，它将滤波响应图和概率图以一定的比例结合，根据结合后的得分图来定位目标。Staple速度上能达到80fps满足实时性的要求，在准确度上和SRDCF相近。  
* 之后，用深度学习的特征代替普通特征提出了相关滤波算法，精度有一定的提高。  
* 再之后，深度学习的方法崛起，各种有关深度学习的目标跟踪算法也如雨后春笋，拔地而起。  
---
### 2010年开始发表在顶会顶刊上的使用correlation filter进行目标跟踪的论文 
1. Visual object tracking using adaptive orrelation filters. In CVPR, 2010. 
1. Exploiting the circulant structure of tracking-by-detection with kernels. In ECCV, 2012.
1. Accurate scale estimation for robust visual tracking. In BMVC,2014.
1. Fast visual tracking via dense spatio-temporal context learning. In ECCV, 2014.
1. Adaptive color attributes for real-time visual tracking. In CVPR, 2014.
1. High speed tracking with kernelized correlation filters. PAMI, 2015. 
1. Multi-store tracker (muster): A cognitive psychology inspired approach to object tracking. In CVPR,  2015.
1. Reliable patch trackers: Robust visual tracking by exploiting reliable patches. In CVPR,  2015. 
1. Real-time part-based visual tracking via adaptive correlation filters. In CVPR, 2015.
1. Long-term correlation tracking. In CVPR, 2015. 
1. Multi-Kernel Correlation Filter for Visual Tracking. In ICCV2015
1. Learning Spatially Regularized Correlation Filters for Visual Tracking. In ICCV2015    
1. Scalable Kernel Correlation Filter with Sparse Feature Integration. In ICCV2015 workshop
1. Joint Scale-Spatial Correlation Tracking with Adaptive Rotation Estimation.  In ICCV2015 workshop
1. Multi-Template Scale-Adaptive Kernelized Correlation Filters. In ICCV2015 workshop 
1. Convolutional Features for Correlation Filter Based Visual Tracking. In ICCV2015 workshop
1. Structural Correlation Filter for Robust Visual Tracking. In CVPR2016
1. Staple: Complementary Learners for Real-Time Tracking. In CVPR2016
1. Real-Time Visual Tracking: Promoting the Robustness of Correlation Filter Learning.In ECCV 2016.
1. Target Response Adaptation for Correlation Filter Tracking. ECCV2016
1. Beyond Correlation Filters: Learning Continuous Convolution Operators for Visual Tracking. ECCV2016
---
 * [相关滤波器（Correlation Filters）](https://blog.csdn.net/sgfmby1994/article/details/68490903)
