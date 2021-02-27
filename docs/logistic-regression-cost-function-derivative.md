---
layout: default
nav_order: 4
title: Logistic Regression cost Function Derivation Equation Development
---
## Appendix B:  Development of Cost Function Partial Derivative

The Cost function's partial derivatives are needed for the Gradient Descent calculation. The derivative equation is presented in Eq. 14, as the sum of Loss function derivatives

#### Eq. 14: Cost Function Derivative
$$\frac{\partial J(b,w)}{\partial w_i} =\sum_{i=1}^{m}\frac{\partial L(b,w)}{\partial w_i}$$


To simplify the equation let's look at one instance of the Loss function. It will be easy to sum the Losses later, so pluginig n L(b,w) gives:

#### Eq. 15: Loss Function Derivative

$$\frac{\partial L(b,w)}{\partial w_i} =\frac{\partial }{\partial w_i}(-y^{(i)}log (\hat{y}^{(i)})-(1-y^{(i)})log(1-\hat{y}^{(i)})$$




Now let's prepare the Loss function quation for deriavation by decomposing it like so:

#### Eq. 16a
$$\hat{y}=\sigma(z)$$

where:

#### Eq. 16b
$$\sigma(z) =\frac{1}{1+e^{-z}}$$

and:

#### Eq. 16c

$$z=b+w^Tx$$



Now we let's plug Eq. 16a to Eq. 15:

#### Eq. 17: Loss Function - substituting parameters by z

$$L(z)= -ylog \sigma(z) + (1-y)log(1- \sigma(z))
$$



Let's derivate Eq. 17 applyinh the derivatives chain rule:

#### Eq. 18: Loss Function Chain Derivatives

$$\frac{\partial }{\partial w_i}L(z)=\frac{\partial }{\partial \sigma(z)}L(z)\cdot\frac{\partial }  {\partial z}\sigma(z)\cdot\frac{\partial }  {\partial w_i}z
$$


Next, we will compute each of Eq 18 chained derivatives:



#### Eq. 19: Loss Function Chain Derivatives

$$\frac{\partial }{\partial w_i}L(z)=\frac{\partial }{\partial \sigma(z)}L(z)\cdot\frac{\partial }  {\partial z}\sigma(z)\cdot\frac{\partial }  {\partial w_i}z
$$

We will now compute each of Eq. 19's parts. Take the first part:

#### Eq. 20:
$$\frac{\partial }{\partial \sigma(z)}L(z) =\frac{\partial }{\partial \sigma(z)} (-ylog \sigma(z) + (1-y)log(1- \sigma(z))$$

Recall the well known natural log derivative:


#### Eq 21: Natural log derivative


$$\frac{\partial}{\partial x}log x=\frac{1}{x}$$


Plug that into the first partial derivative element of Eq. 20:

#### Eq 21: First part of the derivative chain

$$\frac{\partial }{\partial \sigma(z)}L(z)=\frac{\partial }{\partial \sigma(z)}(-y^{(i)}log(\sigma(z)+(1-y^{(i)})log(1-\sigma(z))=-\frac{y^{(i)}}{\sigma(z)}+\frac{1-y^{(i)}}{1-\sigma(z)}$$


For the 2nd part of the derivative chain, we'll use the reciprocal derivative rule:

#### Eq 19: The reciprocal derivative rule

$$(\frac{1}{f(x)})'=-\frac{f'(x)}{f^2(x)}
$$



Applying that rule on the seconds elemet of the chain gives:



### Eq 19: Second part of the derivative chain


$$\frac{\partial }  {\partial z}\sigma(z)=\frac{\partial }  {\partial z}\frac{1}{1+e^{-z}}=
-\frac{-e^{-z}}{(1+e^{-z})^2}=-\frac{1-(1+e^{-z})}{(1+e^{-z})^2}=-\sigma(z)^2+\sigma(z)=\sigma(z)(1-\sigma(z))$$


And lastly, solve the 3rd part of the derivatives chain:

#### Eq 20: Third part of the derivative chain

$$\frac{\partial }  {\partial w_i}z=x_i$$



re-Combining the 3 parts of the chain we get the Loss function for a single example:

#### Eq 21:  Recombining the 3 chained derivatives:

$$\frac{\partial }{\partial w_i}L=(-\frac{y^{(i)}}{\sigma(z)}+\frac{1-y^{(i)}}{1-\sigma(z)}) \cdot \sigma(z)(1-\sigma(z)) \cdot x^{(i)}=(\sigma(z)-y^{(i)})x^{(i)}=(\hat{y}^{(i)}-y^{(i)}$$


#### Eq 22:  Derivative of Loss Function

$$\frac{\partial }{\partial w_i}L(b,w)=(\sigma(z)-y^{(i)})x^{(i)}=(\hat{y}^{(i)}-y^{(i)}$$




Summing the Loss for all m examples, to get the Cost function derivatives:

#### Eq 23 a: Partial Derivative of Sum All Examples Losses:
$$\frac{\partial }{\partial w_i}J(b,w)=\frac{1}{m}\sum_{i=1}^{m}(\hat{y}^{(i)} -y^{(i)})x^{(i)} $$

Q.E.D
