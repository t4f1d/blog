---
layout: post
title:  "Linear Support Vector Machine"
author: mus
categories: [Lecture, Machine Learning, AI ]
image: assets/images/post/2020/svm.jpg
tags: [Lecture, EN, Machine Learning, AI]
---

Support Vector Machine (SVM) is a machine learning algorithm which can be used for both regression or classification problem. 

It is an supervised algorithm in [Machine Learning]({{ '/machine-learning/' | relative_url }}) and mostly used in classification problems. Machine Learning is about computer learning from data how to make accurate predictions.

Formal problem setting and terminology, for example we are given the training data which usually denote as __input__ x<sub>1</sub>,...,x<sub>n</sub> and __label__ y<sub>1</sub>,...,y<sub>n</sub>. The aim is to compute a function _f_ (called __classifier__ or __predictor__) which predicting the unknown label _y_ of a new input _x_ . For example in k-nearest neighbor algoritm.

In SVM we plot data points as points in an __n-dimentional space__ (n being the number of feature that you have). The value of the feature be in the particular coordinate.


# Linear Classifiers
## Math Notation
The math notation for Machine Learning is very standard. we will give list the notation below
- Vectors __v__ ∈ ℝ<sup>d</sup> are thought of as column vectors and denoted with boldface lettters.
- Scalars s ∈ ℝ are denoted with normal letters
- Matrices _M_ ∈ ℝ<sup>mxn</sup> have _m_ rows and _n_ columns and are denoted with normal letters.
- Greek letters can refer to both scalars and vectors, but they are boldfaced if they denote vectors (__λ__ ∈ ℝ<sup>d</sup> vs. λ ∈ ℝ ).
- __0__ and __1__ are vectors in ℝ<sup>d</sup> with entries all zeros and ones, respectively.
- Transposition of a vector or matrix:
  - if __v__ is a column vector, then v<sup>T</sup> is a row vector
  - if _M_ ∈ ℝ<sup>mxn</sup> then _M<sup>T</sup>_ ∈ ℝ<sup>mxn</sup>
- Scalar product of two vectors __v__, __w__ ∈ ℝ<sup>d</sup> : __⟨v,w⟩__ := __v<sup>T</sup>w__
- Norm of a vector: ‖ __v__ ‖ := $$ \sqrt{⟨v,w⟩} = \sqrt{⟨v^T w⟩} $$.
- __v__ ≤ __w__ means ∀i = 1,...,d : __v__<sub>i</sub> ≤ __w__<sub>i</sub>
- The cardinality of a set _S_ is denoted as $$ \vert S \vert $$

### Projections
In linear algebra, the __scalar projection__ of a vector __v__ ∈ ℝ<sup>d</sup> onto vector __w__ ∈ ℝ<sup>d</sup> is the scalar projection $$ \Pi_w (v) = v^T \frac{w}{‖w‖} $$

![Scalar Projection](/assets/images/post/2020/dot-projection.jpg){:class="img-responsive text-center"}{:width="200px"} 


### Hyperplanes and Distances

Hyperplane can be considered as decision boundaries, that classify data points into classes in multi-dimentional space. Data point will be located on the either side of a hyperplane. A hyperplane is a generalization of a plane. In two dimension, it's a line. In three dimention, it's a plane. In more dimentions it will be a hyperplane. 

![Hyperplane](/assets/images/post/2020/hyperplane.jpg){:class="img-responsive text-center"}{:width="100%"} 

In the line, we usually define line as _y=ax+b_ . it will the same as on the hyperplane, we get $$ w^T x + b $$

An (affine) linear function is a function _f_ : ℝ<sup>d</sup> → ℝ of the form $$ f(x) = w^T x + b $$, where __w__ ∈ ℝ<sup>d</sup> (w ≠ 0) and b ∈ ℝ.

A __hyperplane__ is a subset H ⊂ ℝ<sup>d</sup> defined as $$ H := \{ x \in ℝ^d : f(x) = 0 \} $$

The preposition or properties of hyperplanes. Let H be a hyperplane defined by the affine-linear function $$ f(x) = w^T x + b $$
- the vector __w__ is __orthogonal__ to H, meaning that: for all x<sub>1</sub>, x<sub>2</sub> ∈ H. it holds $$ w^T (x_1 - x_2) = 0 $$
- the __signed distance__ of a point __x__ to H is given by $$ d(x,H) = \frac{1}{ \lVert w \rVert }(w^Tx+b)$$

### Finding the best Hyperplane
By looking at the data points and the result hyperplane, we can see the margin between the data with the hyperplane. This mean that __the optimal hyperplane will be the one with the biggest margin__, because the large margin will give a small deviation in the data points, and will not effect with the outcome of the model.

## Linear Classifiers
A classifier of the form $$ f(x) = w^T x + b $$ is called __linear classifier__.

### Adventages
- They easy to understand
- It works really well on clear margin seperation
- It is still effective on the big data, and also effective in cases where the number of dimensions is greater than the number of samples.
- It is fast

### Disadventages
- Suboptimal performance if true decision boundary is non-linear. it occure for very complex problems such as recognition problem and many others.

### Nearest Centroid Classifier
NCC is the linear classifier that classifies model that assigns to observations the label of the class of training samples whose the mean or (centroid) is closest to the observation.

The training data is compute as plus and minus centroid. by computing centroid for each using $$ c_{-} = \frac{1}{ \vert I_{-} \vert } \sum_{i \in I_{-}} x_i$$ for negative and $$ c_{+} = \frac{1}{ \vert I_{+} \vert } \sum_{i \in I_{+}} x_i$$ for positive.

The prediction is given new _x_ predict using $$ arg min_{y \in \{ - , +\}} ‖ x - c_y ‖ $$

Proof if the NCC is linear classifier $$ f(x) = w^T x + b $$ with $$ w:= 2(c_+ - c_-)$$ and $$ b := ‖c_-‖^2 - ‖c_+‖^2 $$

The decision boundary is $$ H = \{ x \in ℝ^d : \| x - c_- \| = \| x - c_+ \| \} $$

$$ \| x - c_- \|^2 = \| x - c_+ \|^2 $$

$$ \| x \|^2 - 2c_-^T x + \| c_- \|^2  = \| x \|^2 - 2c_+^T x + \| c_+ \|^2 $$

$$ 2(c_+ - c_-)^T x + ( \| c_- \|^2 - \| c_+ \|^2 )$$

$$ w:= 2(c_+ - c_-)$$ and $$ b := ‖c_-‖^2 - ‖c_+‖^2 $$

$$ w^T x + b = 0 $$

Thus it is proved that the NCC is a linear classifier.



# Linear Support Vector Machines
The properties of Linear SVMs is __fast__. It can be trained in _O(n d)_ . it also can be trained in a distributed manner (map-reduce). The second is the Linear SVMs is __simple__. it will easy on the geometrical interpretation. the third is __accurate__, in circa 50% of the data out there.

![SVM](/assets/images/post/2020/svm.jpg){:class="img-responsive text-center"}{:width="400px"} 

__State of the art__ in many application area, for example in _gene finding_ which is find in the DNA the positions that impact virtually all important inherited properties of human e.g. intelligence, height, visual appearence, etc.

There are two types of Linear SVM: Hard-margin linear SVMs and Soft-margin linear SVMs.

## Hard-Margin Linear SVM
The core idea of the Hard-margin Linear SVM is to make the hyperplane separates the data with the __largest margin__. So the goal is maximize the margin such that all data points lie outside of the margin.

How we can matematically do this, so we can tell the computer what the computer should do. We can start with denote the __margin by γ (gamma)__, then find the hyperplane parameters __w__ and _b_ that maximize the margin γ. But, also make sure that all positive data points lie on one side and all negative points on the other side.
- a point $$ x_i $$ with $$ y_i = +1 $$ lies on correct side of margin if $$ d(x_i,H) \geq +\gamma $$
- a point $$ x_i $$ with $$ y_i = -1 $$ lies on correct side of margin if $$ d(x_i,H) \leq -\gamma $$

Hence, we require for all points $$ x_i $$, is represented as $$ y_i \cdot d(x_i,H) \geq \gamma $$. So by using this equation, find the hyperplane _H_ with maximal margin γ such that (s.t.) for all training points $$ x_i $$ it holds: $$ y_i \cdot d(x_i,H) \geq \gamma $$

### Preliminary formulation of SVM : 
We recall the hyperplane _H_ is parametrized by __w__ and _b_ through: $$ H = \{ x : w^T x + b = 0 \} $$. and the previous proposition that $$ d(x,H) = \frac{1}{ \lVert w \rVert }(w^Tx+b)$$

$$ \underset{\gamma, b \in ℝ, w \in ℝ^d}{\max} \ \ \ \gamma $$  such that 

$$ y_i  \ ( w^T x + b ) \geq \| w \| \ \gamma , \ \ \forall i = 1,...,n$$


### Limitations of Hard-Margin SVMs
Any three points in the plane $$ ℝ^2 $$ (not lying on a line) can be "shattered" or separated by line (linear classifier). But there are configurations of four points which no hyperplane can shatter. 

Any n+1 points in ℝ<sup>n</sup> (not lying in a hyperplane) can be "shattered" by a hyperplane. But there are configurations of n+2 points which no hyperplane can shatter.

Another problem is that of outliers potentially corruption the SVM.

## Soft-Margin Linear SVM
The core ide of the soft margin is introduce for each input $$ x_i $$ a __slack varible__ $$ \xi \geq 0 $$ that allows for some (slight violations of the margin separation):

__Linear Soft-Margin SVM__

$$ \underset{\gamma, b \in ℝ, w \in ℝ^d, \xi_i,...\xi_n \geq 0 }{\max} \ \ \ \gamma  - \color{red}{  C \sum_{i=1}^{n} \xi_i  } $$ 

such that 

$$ y_i  \ ( w^T x + b ) \geq \| w \| \ \gamma - \color{red}{ \xi_i }, \ \ \forall i = 1,...,n$$


- Minimizes $$ C \sum_{i=1}^{n} \xi_i $$, to allow for "slight" violations of the margin.

- $$ C \sum_{i=1}^{n} \xi_i $$ is the total amount of violations of the training points lying inside the margin (measured in distances to the margin)

- _C > 0_ is a trade-off parameter (to be set in advance): the higher _C_, the more we penalize violations. __Higher C is harder SVM, and lower C is softer SVM__. When __C__ is small, classification mistakes are given less importance and focus is more on maximizing the margin. When __C__ is large, the focus is more on avoiding misclassification at the expense of keeping the margin small.

# Why the name 'Support Vector Machine'?
Since the margin is calculated by taking into account only spesific data points, __support vectors__ are data points that closer to or inside the tube of the hyperplaneand influence with the orientation and the position of the hyperplane.

Assume we denote the optimal arguments from the previous equation by $$ \gamma^* \ and \ w^* $$.

The definition, All vector $$ x_i $$ with $$ y_i \cdot d(x_i,H(\gamma^*, b^*)) \leq \gamma^* $$ (i.e., lying inside the tube) are called `support vectors`. The SVM depends only on the support vectors: all other points can be removed from the training data (no impact on classifier)

![Support Vector](/assets/images/post/2020/supportvector.jpg){:class="img-responsive text-center"}{:width="400px"} 

The support vectors are imaginary or real data points that are considered landmark points to determine the shape and orientation of the margin. The objective of the SVM is to find the optimal separating hyperplane that maximizes the margin of the training data.

# Conclusion
- Linear Support Vector Machines (SVMs) motivated grometrically by the image on the title.
- Mathematical formalization of the image is

$$ \underset{\gamma, b \in ℝ, w \in ℝ^d}{\max} \ \ \ \gamma $$ 

such that 

$$ y_i  \ ( w^T x + b ) \geq \| w \| \ \gamma , \ \ \forall i = 1,...,n$$

- This idea for Soft Margin SVM is based on a simple premise: allow SVM to make a certain number of mistakes and keep margin as wide as possible so that other points can still be classified correctly. This can be done simply by modifying the objective of SVM.














