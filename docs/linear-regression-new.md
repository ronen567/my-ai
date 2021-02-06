---
layout: default
nav_order: 1
title: inear Regression NEW!!
---

# An Intro to Supervised Learning, Linear Regression and Gradient Descent

The essence of machine learning is the predictor. When speaking of predictors, the first question should normally be - which type of predicors to use. The curenntly commonly used predictort of Supervised Learning is **Logistic Regression**. Logistic Regression will be presented with details on a post which follows. Still this post is about the **Linear Predictor**. Though not commonly used for Supervised Learning, being a relatively simple model, it might be a good point to start with, and gain familiarity with some of the predictors' principles.

Eq. 1 presnets the Linear Prediction formula.

### Eq. 1: Linear Prediction 

$$y\approx \hat{y}=b+\sum_{j=1}^{n}w_jx_j$$


Eq.1 presents $$\hat{y}$$ which estimates y, by a linear combination of the input set (AKA input features ),$$X={x_i}$S i= 1 to n, where b and  {w_i}, i=1:n are the predictor's coeffcients.


Let's illustrate a linear prediction scenario. We start with a simple case, where n=1. 


### Table 1:  Apartments price prediction - single feature


|``x`-Floor |`y`- Price (M $)|
|:----------|:---------------|
|0          | 0.4            |
|1          | 0.7            |
|2          | 1.1            |
|3          | 1.4            |
|4          | 1.65           |        

Floor number by itself is not sufficient for apartment price prediction, still we use it just as illustration. for the is ofcoursenot 

With n=1 Eq.1 reduces to:

### Eq. 2: Linear Prediction, n=1 

$$y\approx \hat{y}=b+w_1x_1$$

Let's see the graphical presentation of this 1D linear predictor.



### Figure 1: Linear Prediction - 1D

![Linear Predictiopn 1d](../assets/images/linear-regression/linear_1d_prediction.png)



Figure 1 illustrates a linear model for the appartment prices. According to the graph, the  model indeed fits the data points, though to prove model's validity,  much more than 5 example datapoints are needed. Here we use less points. for the sake of simplicity. Later on, we will increase the number of points, AKA examples.


Now let's increase the predictor's dimenssions to 2. Now we'll have 2 features which determine the apartments' prices: Floor and Number of rooms, as listed in Table 2.


### Table 2:  Apartments price prediction - 2 feature

|`x1`-Number of bedrooms|`x2`-Floor|`y`- Price (M $)|
|:----------------------|:---------|:---------------|
| 5                     | 0        | 1.5            |
| 4                     | 1        | 0.5            |
| 5                     | 2        | 1              |
| 6                     | 3        | 1.2            |
| 6                     | 4        | 1.5            |

Needless to note again that these 2 features are not enought to predict apartments pricess, but we still use a simplified example, as an illustration example.


Now let's see the graphical presentation of this 2 features setup.
linear predictor.


### Figure 2: Linear Prediction - 2D

![Linear Predictiopn 2d](../assets/mages/linear-regression/predicted_prices_2d_gif.gif)








The Linear Model, as expressed by Eq. 2, is charactarized by the parameters b and w_1, where b is the offset of the line at $$\hat(y)=0$$, and w_1 is the line's slope.





Next question to be asked here is, how should the predictor's coefficients be caluclated. Goal of this post is to show the matematical development leading to finding the predictor's coeffcients..

Before we delve into the develpoment of the mathematical formulas, let's start with illustrating the context which the prediction operation relates to.




The scenario this post considers, it of a Spervised Learning, at which the predictor is calculated during the Training Phase. 
So here we go.

To demonstrate the assignment of a predictor, let's sketch a problem which should be solved with a Supervised Machine Learning. ?Just to note -the problem is very much simplified, for the sake of 
Note that the context thIn this post, we intriduce the Linear Predictor, 
When speking of Machine Learning, then



Here's an intro which with a simple Supervised Machine Learning Regression example, continues to the presentation of the Linear Regression predictor, and then show how to solve for the predictor's coefficients with Gradient Descent algorithm. It folows the intro to Machine Learnng.


Let’s begin with an example problem: It is required make a Machine Learning Predictor which determines house pricing, based on 3 features:
1. Number of bedrooms
2. Zip code
3. Floor
as listed in Table 1. 

Note - obviously those 3 features are not enough to predict houses prices, but for the sake of simplicity, let's assume they are.

Table 1, consists of 4 training labeled data entries, aka examples, each labeled with the known corresponding price.



#### Table 1:  House price prediction - Labeled data


|`x1`-Number of bedrooms|`x3`-Floor|`y`- Price|
|:----------------------|:------------------|:----------|:---------|
| 3                     |0        | 179000   |
| 5                     |1        | 210000   |
| 7                     |2        | 250000   |
| 8                     |3        | 260000   |
| 9                   


Following now, is table 2, which consists of regular features data- 4 entries. The house price should be estimated for those, based on data features.


#### Table 2: House Price Prediction - Regular Data

| x1 -Number of bedrooms| x3 - Zip code     | x3 -Floor| y - Price|
|:----------------------|:------------------|:---------|:---------|
| 3                     |34321              | 3        |  ?       |
| 5                     |64322              | 5        |  ?       |
| 1                     |23241              | 4        |  ?       |
| 4                     |83422              | 2        |  ?       |


Our challenge is the following:

1. Select a prediction model
2. Train the model with the labeled examples, (table 1), so that this model will later be able to estimate normal data (Table 2).

### Select a prediction model
Let’s start with the first challenge, and determine the model. 
In this post, for the sake of simplicity, we chose the "Linear Regression" model. Note that however the currently most common prediction model used is "Logistic Regression", examining the simpler "Linear Regression" first, will be a foundation for the other more complicated algorithms. Still, you may skip this post and jump directly to "Logistic Regression" which will be presented in the post which follows.

With that said, let's start!

Linear Regression is a model which approximates y by $$\hat(y}$$, which is a linear function of the input x,  as expressed in Eq 1.

#### Eq. 1: Linear Prediction 

$$y\approx \hat{y}=b+\sum_{j=1}^{n}w_jx_j$$

Where:
$${x_j}$$ are the input's features, e.g. columns of tables 1 and 2.
$$n$$ is the dimension of the input features.
$$ b and {w_j}$$ are the estimator coefficients.


Now having the Linear Regression selected, the challenge is find the coefficients' values. This should be done during the Trainingphase.

Note that I deliberately keep the notation of the free coefficient, (aka bias), as {b}, rather then {w_0}. Reason - this is a common notation in many papers and books.
Rest of this post presents the mathematical development, which leads to finding formula for the predictor's coeficients values.



Eq 1 expresses  an n dimensional input model. A multi dimensional problem is hard to sketch graphically, not to say impossible. For the sake of simplicity, and without losing generality, let’s reduce the dimensionality of features to 1. Now it will be easier to sketch and illustrate the problem and the solution.

For the sake of simplicity, let's reduce the dimension $$n$$ of the predictor's Eq. 1 to $$n=1$$, making it a 2 dimensional problem. Results would be valid to any n, but with 2-3 dimensions, we can presnt the data graphically.

So Eq. 1 reduces to Eq. 2.  

#### Eq. 2: Line Approximation

$$ \hat{y} ={ b}+w_1{x}$$

Figure 1, illustrates the line approximity: We are looking for the line offset $$b$$ and slope $$w_1$$ which optimize the approximation of the line to the dara point. To make that optimization, we will define a cost function which expresses the distance between the model and the points it aims to model, and chose the coefficients which minimize that cost.

#### Figure 3: Line Approximation 

![Linear Approximation](../assets/images/linearApproximation.jpg)



The cost, denoted by $$J(w,b)$$ is presented in Eq. 3, where the cost function is chosen to be the sum of squared euclidiean distances between the line and data points, aka squared errors. 

#### Eq. 4: Cost function -Squared Errors

$$J(w,b)=\frac{1}{m}\sum_{i=1}^{m}(\hat{y}^i-y^i)^2$$

Figure 4 illustrates graphically the euclidiean distance between approximate and actual value $$d=\hat{y}-y$$.

#### Figure 5: Approximation Distance
![Approximation Distance](../assets/images/approximation/point_to_aprox_line_dist.png)



BTW, optionally other cost functions could be chosen, e.g.minimizing the absolute difference between coordinates, see Eq. 5.

#### Eq. 5: Cost function using absolute coordinates differences

$$J(w,b)=\frac{1}{m}\sum_{i=1}^{m}\left | \hat{y}^i-y^i \right |$$


Cost expression as in Eq. 5, is dependent on squared distances, thus increases more as error grows, and is commonly used.


Let's substutute  \hat{y}^i by b^i+w_1x^i in Eq. 4, and get Eq. 6:

#### Eq. 6: Cost function for line approximation

$$J(w,b)=\frac{1}{m}\sum_{i=1}^{m}(b^i+w_1x^i-y^i)^2$$


Plotting Eq 6, which is a quadric equation, will result in a surface, such as  illustrated in figure 7:

#### Figure 7:  Plot illustration of  $$J(b,w)$$:


![Approximation Surface](../assets/images/approximationSurface.jpg)



#### Question: 
Which are the coefficients {b, w1} which minimize Eq.6? 
#### Answer: 
Take a look at Figure 7! The cost function minimum is at the bottom of the curve. We need {b, w1} which correspond to this point.


and solve for b and w1.

Here:


#### Eq. 7: Cost function derivative wrt b

$$\\\frac{\partial J(b,w)}{\partial  b}=\\\frac{\partial(\frac{1}{2m}\sum_{i=1}^{m}(b+w_1x^i-y^i)^2)}{\partial b}=$$

$$\\\frac{1}{2m}*\sum_{i=1}^{m}\frac{\partial(b+w_1x^i-y^i)^2}{\partial b}=$$

$$\\\frac{1}{m}\sum_{i=1}^{m}(b+w_1x^i-y^i)= \\\mathbf{\frac{1}{m}\sum_{i=1}^{m}(\hat(y^i)-y^i)}$$

#### Eq. 8:  Cost function derivative wrt w1

$$\\\frac{\partial J(b,w)}{\partial w1}=\\\frac{\partial(\frac{1}{2m}\sum_{i=1}^{m}(b+w_1x^i-y^i)^2)}{\partial  w1}=$$

$$\\\frac{1}{2m}*\sum_{i=1}^{m}\frac{\partial(b+w_1x^i-y^i)^2}{\partial  w1}=$$

$$\\\frac{1}{m}\sum_{i=1}^{m}(b+w_1x^i-y^i)*x^i=\\\mathbf{\frac{1}{m}\sum_{i=1}^{m}(\hat(y^i)-y^i)*x^i}$$


As mentioned before, we are interested in the minima where derivatives are 0s. Here are our 2 equations:

#### Eq. 9:  Cost Function Partial Derivatives

a:

$$0 = \frac{1}{m}\sum_{i=1}^{m}(\hat(y^i)-y^i)$$

b:

$$0 = \frac{1}{m}\sum_{i=1}^{m}(\hat(y^i)-y^i)*x^i$$



#### Question: 
How should Eq 9 and in our specific case , Eq. 10 should be solved for b and w1?
#### Answer: 
We can consider of 2 optional solutions:
1. Analytical Solution
2. An iterative numerical solution - Gradient Descent

#### Analytical Solution 
The analytical solution is straightforward solution: It is required to solve n+1 linear equations for n+1 unknown parameters. 
Let's demonstrate the the sIn our example where n=1, we have 2 equations, Eq. 10 a and b, with 2 unknown parameters to find: $$b$$ and $$w_1$$.

Let's demonstrate the solution  for n=1:
We take Eq. 9a, subsitute the line equation. Consider that $$x^i$$ and $$y^i$$ are constants - $$x^i$$ is ith training input data, while $$y^i$$ is the correspondig label.
So Eq. 9a, after rearranging the constants reduces to:

#### Eq. 10a:
$$\\A*b + B*w_1 = C$$
Where A and B are known constants.
Similariliy Eq. 9b can be reduced to:
#### Eq. 10b:
$$\\D*b + E*w_1 = E$$

Let's rewrite it in a matrix format:

#### Eq. 11:
$$\\\begin{bmatrix}
\mathbf{} A& B\\ 
D & E
\end{bmatrix}\begin{bmatrix}
b\\w_1 
\end{bmatrix}=\begin{bmatrix}
C\\E
\end{bmatrix}$$


Let's solve this. For convinience let's denote:
#### Eq. 12:

$$M=\begin{bmatrix}
\mathbf{} A& B\\ 
D & E
\end{bmatrix}$$

Substitute Eq. 12 into Eq. 11:


#### Eq. 13:

$$M\begin{bmatrix}
b\\w_1 
\end{bmatrix}=\begin{bmatrix}
C\\ E
\end{bmatrix}$$

Solve it for $$\begin{bmatrix}
b\\w_1 
\end{bmatrix}$$:

$$\begin{bmatrix}
b\\w_1 
\end{bmatrix}=(M^TM)^{-1}M^T\begin{bmatrix}
C\\E
\end{bmatrix}$$



And that's it, quite a simple solution. We needed to inverse a 2*2 matrix for solution, which is not much. Why only 2*2? Because number of features where n=1. But what if we had much more features, say n=1000, or more? In that case inverse could be too complicated.
That's where the other solution comes in - the Gradient Descent solution.


#### Gradient Descent Solution

Gradient Descent is an iterative algorithm for finding a local minimum. Eq. 13 presents the Gradient Descent formula for our example's cost function J(b, w1)


#### Eq. 13: Gradient Descent
a:  Gradient Descent with gradient to the {w_2} direction:
$$\\w_1:=w_1-\alpha \frac{\partial J(b,w_1) }{\partial w_1}$$

b. Gradient Descent with gradient to the {b} direction:
$$\\b:=b-\alpha \frac{\partial J(b,w_1) }{\partial b}$$


#### How is Eq 13 calculated?
Here are the algorithm's cooking recipe: 
1. Select arbitrary initial values for the calculated values. Here let's say: w_1=TEMP_W, b=TEMP_b.
2. Substiture TEMP_W and TEMP_b in 13 a and b. Now new w_1 and b are calculated. Iteration 1 done!
3. Substitute new values in Eq. 13, and repeat to produce new {b} and {w_1}
4. Repeat step 3 until convergence, i.e. whenn iteration result wrt to previous iteration is below threshold: if $$abs(w_1[k]-w_1[k-]) < \Delta, stop$$

The algorithm steps in the opposite direction of the gradient until convergence, as the gradient, multiplied by a constant $$\alpha$$ is decremented from previous value.
The algorithm converges at the minima, where all partial derivatives are 0.


Let's illustrate the algorithm to make it intuitively clear:

Figure 8 illustrates the iterative process and its convergence: 
Figure 8.a shows the first iteration, which starts with an aribtrary selected value of $$w_1$$ , $w_1[0]=1 in our example. The gradient is quite steep here.
Figure 8.b shows 4 iterations, still far from convergence, but gradient are less steep.
Figure 8.c shows 14 iterations, which converge as expected at $$\alpha \frac{\partial J(b,w1) }{\partial b}=0$$.

#### Figure 8: Gradient Descent: Gradient of a single parameter

a. After One Iteration

![gradient_descent_1_iteration](../assets/images/gradient_descent/gradient_descent_1_iteration.png)

b. After Four Iterations

![gradient_descent_4_iterations](../assets/images/gradient_descent/gradient_descent_4_iterations.png)


c. After Fourteen Iterationss

![gradient_descent_14_iteration](../assets/images/gradient_descent/gradient_descent_14_iteration.png)


Let's talk about $$/alpha$$, the step size.

Looking at Figure 8, it looks like the smaller the step size $$/alpha$$ is, the slower convergence goes. And also vice versa - one might assume that the larger $$/alpha$$ is, the fastest it will converge. Wrong assumption!
A too large step-size may result with oscilations. Look at Figure 9.

Figre 9: Gradient Descent Oscilation

![gradient_descent_14_iteration](../assets/images/gradient_descent/gradient_descent_oscilations.png)


Conclusion - step size should be carefully selected, and may be needed to tune during caluclations.

We have reviwed the 2 methods to solve for the estimator's coefficients: The Analytic Solution method and Gradient Descent.The Analytic Solutoin involves inverting a matrix of size n+1*n+1 where n equal number of features. The Gradient Descent requires selection of step size $$//alpha$$, and migh, in some cases, converge to a local minima, rather to the global.

So, we're done with this post, which discussed Linear Regression, from problem (house prices) to solution. 
Next we'll discuss Logistic Regression, which is the currently most popular predictionmodel used.





























a  where it is needed to solve  in our example of line approximation. Look at Eq 10




the point where $$J(b,w)$$ is minimal
To find the cTo minima of the cost function, is the point where derivative of order one is zero. 



dimensions, the cost function equals to the sum of squared distances between the example points labels, aka training data points, to the approximated values  $$en the example points labels, aka training data points, to the approximated values  $$$$ the example points labels, aka training data points, to the approximated values  $$values  $$$$lues  $$\hat{y^i}.$$


So, we're done with this post, which discussed Linear Regression, from problem (house prices) to solution. 
Next we'll discuss Logistic Regression, which is the currently most popular predictionmodel used.
================================

This can be plot using a 2 dimensions lgraph. Here’s such a graph:


Let’s plot 
 The n=1



 model, illustrated in the figure below.




So, the training data set consists of m labeled examples, each denoted as $$x^{i}, i=1 to m$$ is the input data and it is labeled by $$y^{i} $$, the corresponding label, is the expected decision of the predictor.$$(x^{i}, y^{i})$$, where $$x^{i}, i=1 to m$$ is the input data and it is labeled by $$y^{i} $$, the corresponding label, is the expected decision of the predictor.

So, for simplicity, we start with a 1D set of input points X, and can present it on a 2D graph, as shown in figure 3.

Figure 3: Linear Approximation







Looking at Figure 3, we can see that a linear approximation fits the training examples points well.
The line equation is $$^{\hat{y}}=wx+b$$, so now we need to calculate w and b that give the best approximation. We do that by defining a cost function J(w,b). Then we find w and b which minimize the cost function.
 We chose it to be the some of the squared errors:

$$J(w,b)=\frac{1}{m}\sum_{i=1}^{m}(\hat{y}^i-y^i)^2$$

Aim is to find w and b, such that minimize the cost function:
$$$$\\ \min_{w,b}J(w,b)$$

$$J(w,b)$$ is a 2 quadric function of 2 parameters. The 2D Graph below illustrates the surface defined by an equation of this type:





To find the best line equation, we should select a cost function, which minimizing 





Figure 1 describes the  Supervised Learning system, be it a regression or classification prediction.


Figure 1: Supervised Learning





The system runs in 3 stages, as presented in Figure 2.
Training - At which the predictor coefficient are calculated
Testing - At which the predictor performance is evaluated,
Prediction - The predictor calculates output Y based on input X

Figure 2: Supervised Learning - 3 stages




Here we will delve to the calculation of predictor’s coefficient. The analytical solution is straight forward and easy, but with a large number of features, it may be computationally too heavy to inverse huge matrixes.
Gradient Descent is a very common algorithm used, low computation complication on one hand, but sensitive to selection of $$/alpha$$ and may have issues such as local minima convergence on the other hand.


So, we're done with this post, which discussed Linear Regression, from problem (house prices) to solution. 
Next we'll discuss Logistic Regression, which is the currently most popular predictionmodel used.





