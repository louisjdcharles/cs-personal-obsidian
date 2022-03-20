# The Integrating Factor
For the Linear First Order ODE:
$$\dv{y}{x} + P(x)y = Q(x)$$
You can multiply through by the function $I(x)$ such that $I'(x) = I(x)P(x)$
$$I(x) \dv{y}{x} + I(x)P(x)y = I(x)Q(x)$$
meaning
$$I(x) \dv{y}{x} + I'(x)y = I(x)Q(x)$$
Using the product rule for differentiation, this is equal to
$$\dv{x} (I(x)y) = I(x)Q(x)$$
Integrating both sides with respect to x:
$$y = \frac 1 {I(x)} \int I(x) Q(x) \,\dd x$$
The function that satisfies the condition $I'(x) = I(x)P(x)$ is
$$I(x) = e^{\int P(x) \, \dd x}$$

## Example
$$\text{Solve } \cos x \dv{y}{x} -2y \sin x = 3 \text{ for } -\frac \pi 2 \lt x \lt \frac \pi 2$$
$$\text{given that } y=1 \text{ when } x= 0$$
![](https://i.imgur.com/jVY2jzb.png)