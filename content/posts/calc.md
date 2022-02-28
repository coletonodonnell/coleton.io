---
author: "Coleton O'Donnell"
title: "Calculus Notes"
date: "2022-02-01"
description: "These are all my notes while learning Calculus. This is a living document and reflects my adventure learning Calculus."
tags: ["math", "calculus"]
math: true
---
# Calculus Notes

## Preface

The Calculus I and II topics follows the [AP Calculus BC course on Khan Academy.](https://www.khanacademy.org/math/ap-calculus-bc) Most problems/solutions are taken from the quizzes, videos, and examples and as such are taught better than they are here. A small amount are ones I came up with to illustrate my point and some additional notes are outside the initial scope of AP Calculus BC but are useful for more advanced math which at the time of writing I am interested in. These are "living" notes, I update them as I learn and as a result may change, be reformatted, or be inaccurate at times. As of writing, I am not done with AP Calculus BC, so I am still writing notes for these topics. I aim to be as accurate as possible but I am a student of Calculus and am not qualified to teach Calculus. These notes are in no way supplements for any actual material and instead are just for reference, **please** use them as such. You will *in no way* gain any deep understanding of the topics discussed here by reading solely these notes. Most important thing that I can impart from these notes though is not the material, but some advice: don't give up in Calculus, people hype it up to be way harder than it actually is. It is self-teachable, it is understandable, and **it is fun. Math is fun.** Calculus will come easier to you if you treat it like a game full of puzzles. Might be a boring game initially, but a game nonetheless. If I, in my seemingly never ending stupidity, can do it: so can you. To quote Silvanus Thompson:

> “What one fool can do, another can.”  
~ Ancient Simian Proverb.  

All math rendering is [done with $\KaTeX$.](https://katex.org/)

### Prerequisites: 

- Understand everything found [here](https://www.khanacademy.org/math/ap-calculus-bc/bc-limits-new/ap-bc-about/a/ap-calc-prerequisites).
- Understand what a [limit is.](https://www.khanacademy.org/math/ap-calculus-bc/bc-limits-new)
- Understand [basic logic and set notation](https://en.wikipedia.org/wiki/List_of_logic_symbols) for some part of these notes.

### Recommended Texts and Resources for Calculus:

#### Texts/Courses

- [AP Calculus BC/Calculus I and II on Khan Academy](https://www.khanacademy.org/math/ap-calculus-bc)
- [MIT 18.01 Single Variable Calculus (Calc I and II)](https://www.youtube.com/watch?v=7K1sB05pE0A&list=PL590CCC2BC5AF3BC1)
- [MIT 18.02 Multivariable Calculus (Calc III)](https://www.youtube.com/watch?v=PxCxlsl_YwY&list=PL4C4C8A7D06566F38)
- [Stewart, James. Calculus: Early Transcendentals. 8th ed., Cengage Learning, 2016](https://www.amazon.com/Calculus-Early-Transcendentals-James-Stewart/dp/1285741552)
- [Thompson, Silvanus P., and Martin Gardner. Calculus Made Easy. St. Martin's Press, 1998](https://www.amazon.com/Calculus-Made-Easy-Silvanus-Thompson/dp/0312185480)

#### Playlists

- [3Blue1Brown's "Essence of Calculus" (Big Ideas in Calculus)](https://www.youtube.com/watch?v=WUvTyaaNkzM&list=PL0-GT3co4r2wlh6UHTUeQsrf3mlS2lk6x)
- [3Blue1Brown's "Differential equations, a tourists guide" (Cool things about Differential Equations but by no means a guide)](https://www.youtube.com/watch?v=p_di4Zn4wz4&list=PLZHQObOWTQDNPOjrT6KVlfJuKtYTftqH6)
- [blackpenredpen's Calculus 1 Tutorials](https://www.youtube.com/c/blackpenredpen/playlists?view=50&sort=dd&shelf_id=5)
- [blackpenredpen's Calculus 2 Tutorials](https://www.youtube.com/c/blackpenredpen/playlists?view=50&sort=dd&shelf_id=6)
- [blackpenredpen's Differential Equations Tutorials](https://www.youtube.com/c/blackpenredpen/playlists?view=50&sort=dd&shelf_id=7)
- [The Organic Chemistry Tutor's Calculus Videos](https://www.youtube.com/watch?v=GiCojsAWRj0&list=PL0o_zxa4K1BWYThyV4T2Allw6zY0jEumv)

#### Problem Sets

- [100 Integral Problems (w/o solutions)](https://people.math.sc.edu/girardi/m142/integration/100problems.pdf)
- [MIT 18.01 Course Home, Check the "Worked Example" Sections](https://ocw.mit.edu/courses/mathematics/18-01sc-single-variable-calculus-fall-2010/1.-differentiation/part-a-definition-and-basic-rules/session-1-introduction-to-derivatives)

## The Derivative
> Change is the law of life. And those who look only to the past or present are certain to miss the future.  
~ John F. Kennedy, Address in the Assembly Hall at the Paulskirche in Frankfurt  

### Definition of a Derivative

The derivative of a function called $f(x)$ (f of x) is called $f'(x)$ (f prime of x.) For any given $x$ input for $f(x)$, $f'(x)$ will equal the slope of the tangent line passing through $f(x)$ at point $x$. In other words, the derivative measures instantaneous change at a point. For these notes we will use both the Leibniz and Lagrange notation to denote the action of finding or representing the derivative. Lagrange is the notation we used above, while Leibniz is notation represented by:
$$\displaystyle \frac{d}{dx}$$ 

Which is read as "The derivative ($d$) of the following thing as respect to $x$ ($dx$)." If we are finding the derivative of $y$ as respect to $x$ we would write this as:
$$\displaystyle \frac{dy}{dx}$$

#### Derivative of a Function

$$\displaystyle \frac{d}{dx} f(x)= \lim_{\Delta x \rightarrow 0} \frac{f(x+\Delta x) - f(x)}{\Delta x}$$

This can be read as "the derivative of $f(x)$ as respect to $x$ is equal to the limit of the function $f(x + \Delta x)$ subtracted by $f(x)$ all divided by $\Delta x$ as $\Delta x$ approaches 0."

##### Example for the function $f(x) = x^2$

For the function $f(x) = x^2$

$$\displaystyle \frac{d}{dx} f(x) = \lim_{\Delta x \rightarrow 0} \frac{f(x+\Delta x) - f(x)}{\Delta x} = \lim_{\Delta x \rightarrow 0} \frac{(x+\Delta x)^2 - x^2}{\Delta x} =$$ 
$$\lim_{\Delta x \rightarrow 0} \frac{x^2 +2(\Delta x)(x) + \Delta x^2 -x^2}{\Delta x} = \lim_{\Delta x \rightarrow 0} \frac{2(\Delta x)(x) + \Delta x^2}{\Delta x} = \lim_{\Delta x \rightarrow 0} 2x + \Delta x = 2x$$ 

As we can see, as the limit of $\Delta x$ approaches 0, we can substitute 0 for $\Delta x$, thus giving us the final result $\frac{d}{dx} f(x) = 2x$

#### Derivative of a Point

$$\displaystyle \frac{d}{dx} f(c) = \lim_{x \rightarrow c} \frac{f(x)-f(c)}{x-c}$$

##### Example for the function $f(x) = x^2$ at $x = 2$

$$\displaystyle \frac{d}{dx} f(c) = \lim_{x \rightarrow c} \frac{f(x)-f(c)}{x-c} = \lim_{x \rightarrow c} \frac{x^2 -4}{x-2} = \lim_{x \rightarrow c} \frac{(x+2)(x-2)}{x-2} = \lim_{x \rightarrow c} x + 2 = 2 + 2 = 4$$

#### Differentiability

A point is differentiable if it is continuous at that point, this fact can be represented by the following rule:

$$\displaystyle f(c) = \lim_{x \rightarrow c} f(x) \text{ and }\exists~\displaystyle \lim_{x \rightarrow c} \frac{f(x)-f(c)}{x-c}$$ 

### Useful Derivatives to Memorize

- $\displaystyle \frac{d}{dx} \cos x = -\sin x$

- $\displaystyle \frac{d}{dx} \sin x = \cos x$

- $\displaystyle \frac{d}{dx} \tan x = \frac{d}{dx} \frac{\sin x}{\cos x} = \frac{\cos^2x + \sin^2x}{\cos^2 x} = \frac{1}{\sin^2 x} = \sec^2 x = \tan^2 x + 1$

- $\displaystyle \frac{d}{dx}\cot x= \frac{d}{dx}\frac{\cos x}{\sin x} = \frac{-(\sin^2x + \cos^2 x)}{\sin^2x}=-\frac{1}{\sin^2x} = -\csc^2 x$

- $\displaystyle \frac{d}{dx} \sec x = \frac{d}{dx} \frac{1}{\cos x} = \frac{\sin x}{\cos^2 x} = \frac{\sin x}{\cos x }\times \frac{1}{\cos x} = \tan x \times \sec x$

- $\displaystyle \frac{d}{dx} \csc x = \frac{d}{dx} \frac{1}{\sin x} = -\frac{\cos x}{\sin^2 x} = -\frac{\cos x}{\sin x} \times \frac{1}{\sin x} = -\cot x \times \csc x$

- $\displaystyle \frac{d}{dx} \sin^{-1}x = \frac{1}{\sqrt{1-x^2}}$
- $\displaystyle\frac{d}{dx} \cos^{-1}x = -\frac{1}{\sqrt{1-x^2}}$

- $\displaystyle \frac{d}{dx} \tan^{-1} x = \frac{1}{x^2+1}$

- $\displaystyle \frac{d}{dx} e^x = e^x$

- $\displaystyle\frac{d}{dx} \ln x = \frac{1}{x}$

- $\displaystyle \frac{d}{dx} a^x, a>0 = \frac{d}{dx} (e^{\ln a})^x = \ln a \times (e^{\ln a})^x = (\ln a)a^x$

- $$\displaystyle \frac{d}{dx} \log_ax, a \ne 1 = \frac{d}{dx} \frac{\ln x}{\ln a} = \frac{d}{dx} [\frac{1}{\ln a} \ln x] = \frac{1}{\ln a} \frac{d}{dx}[\ln x] = \frac{1}{\ln a} \times \frac{1}{x} = \frac{1}{(\ln a)x}$$

### Derivative Rules

#### Power Rule

$$\frac{d}{dx} x^n = nx^{n-1}$$

##### Example for the function $f(x) = x^2$

$$\frac{d}{dx}x^2=2x^{2-1}=2x$$

Along with this, learning exponent rules is important as well:

##### Exponent Rules

- $x^a+x^a = 2x^a$
- $x^a + x^b = x^a + x^b$
- $\displaystyle (x^a)^b = x^{a \times b}$
- $\frac{x^a}{x^b} = x^{a-b}$
- $x^a \times x ^b = x^{a+b}$
- $x^{-n} = \frac{1}{x^n}$
- $x^\frac{a}{b}= \sqrt[b]{x^a}$

#### Constant Rule

$$\displaystyle \frac{d}{dx} k = 0$$

#### Constant Multiple Rule

$$\displaystyle \frac{d}{dx}[k f(x)] = k \frac{d}{dx}[f(x)]$$

##### Example for the function $f(x) = 2x^2$

$\frac{d}{dx}[2x^2] = 2\frac{d}{dx}[x^2]=2 \times 2x^{2-1} = 4x$

#### Sum and Difference Rule

$$\displaystyle \frac{d}{dx}[f(x) \pm g(x)] = \frac{d}{dx}[f(x)] \pm \frac{d}{dx}[g(x)]$$

##### Example for $f(x) - g(x)$ when $f(x) = x^3$ and $g(x) = x^2$

$\frac{d}{dx}[f(x) - g(x)] = \frac{d}{dx}[f(x)] - \frac{d}{dx}[g(x)] = \frac{d}{dx}[x^3] - \frac{d}{dx}[x^2] = 3x^{3-1} - 2x^{2-1} = 3x^2 - 2x$

##### Example for the function $f(x) = 5x^4 + x^3 + 5$

$\frac{d}{dx}[f(x)] = \frac{d}{dx}[5x^4 + x^3 + 5] = \frac{d}{dx}[5x^4] + \frac{d}{dx}[x^3] + \frac{d}{dx}[5]= 5\frac{d}{dx}[x^4] + \frac{d}{dx}[x^3] + 0 = 5 \times 3x^{4-1} + 3x^{2-1} = 15x^3 +3x^2$

#### Product Rule

$$\displaystyle \frac{d}{dx}[f(x)g(x)] = g(x)\frac{d}{dx}[f(x)] + f(x)\frac{d}{dx}[g(x)]$$

##### Example for $f(x)g(x)$ when $f(x) = x^2$ and $g(x) = \sin x$

$\frac{d}{dx}[f(x)(g(x)] = g(x)\frac{d}{dx}[f(x)] + f(x)\frac{d}{dx}[g(x)] = \sin x \frac{d}{dx}[f(x)] + x^2\frac{d}{dx}[g(x)] = 2x \sin x + x^2 \cos x$

#### Quotient Rule

$$\displaystyle \frac{d}{dx}[\frac{f(x)}{g(x)}] = \frac{g(x)\frac{d}{dx}[f(x)] - f(x)\frac{d}{dx}[g(x)]}{[g(x)]^2}$$

##### Example for $\frac{f(x)}{g(x)}$ when $f(x) = x^2$ and $g(x) = \cos x$

$\frac{d}{dx}[\frac{f(x)}{g(x)}] = \frac{g(x)\frac{d}{dx}[f(x)] - f(x)\frac{d}{dx}[g(x)]}{[g(x)]^2} = \frac{\cos x \frac{d}{dx}[x^2]-x^2\frac{d}{dx}[\cos x]}{\cos^2x} = \frac{2x\cos x -x^2(-\sin x)}{\cos^2x} = \frac{2x\cos x +x^2\sin x}{\cos^2x}$

#### Chain Rule

I will write this in both Leibniz and Lagrange notation as I think it can be hard to visualize:

$$\displaystyle \frac{d}{dx}[f(g(x))] = f'(g(x)) \times g'(x)$$

$$\displaystyle \frac{d}{dx}[f(g(x))] = \frac{df(g(x))}{dx} = \frac{d[f(g(x))]}{d[g(x)]}\times \frac{d[g(x)]}{dx}$$

This basically means that the derivative of a composite function is equal to the derivative of the outer function $f(x)$ as respect to the inner function $g(x)$ multiplied by the derivative of the inner function $g(x)$. To really understand this, we must look at an example:

##### Example for $h(x)$ when $h(x) = (\sin x)^2$

When approaching this problem, we see that the outer function is $f(x) = x^2$ and the inner is $g(x) = \sin x$, so what is the derivative of $f(x)$? Well we already know this it is $2x$. Replace $x$ with the inner function and we're golden. $2 \sin x$. It is that simple, we are finding the derivative of $x^2$ as respect to $\sin x$. Once we have this, we multiply $2 \sin x$ by the derivative of $\sin x$, $\cos x$. Seeing this worked out:

$\frac{dh}{dx} = \frac{df}{dg} \times \frac{dg}{dx} = \frac{d[(\sin x)^2]}{d\sin x} \times \frac{d \sin x}{dx} = 2 \sin x \times \cos x$

### Implicit Differentiation

Now that we understand all of rules (most notably the Chain Rule) we can differentiate an equation with two variables. We do this by taking the derivative of both sides, and assume that one of the variables is a function of another variable ($y$ is a function of $x$.) This is not multivariable calculus, as in multivariable calculus the variables are not functions of each other. Here is a worked example that helps illustrate Implicit Differentiation:

#### Example for the expression $x^2 + y^2 = 1$, find $\frac{dy}{dx}$

As we know, this is the equation for the unit circle, but what would be the derivative for this equation? The issue here is that this isn't really a function, for (most) $x$ values, there are **two** $y$ values, that is a big no no for our definition of a function. Here is how this is solvable utilizing Implicit Differentiation:
- **Given**

$x^2 + y^2 = 1$

- **Find Derivative of Each Side**

$\frac{d}{dx}[x^2 + y^2] = \frac{d}{dx}[1]$

- **Sum Rule**

$\frac{d}{dx}[x^2] + \frac{d}{dx}[y^2] = \frac{d}{dx}[1]$

- **Constant Rule**

$\frac{d}{dx}[x^2] + \frac{d}{dx}[y^2] = 0$

- **Power Rule**

$2x^{2-1} + \frac{d}{dx}[y^2] = 0$

- **Chain Rule, finding the derivative of $y^2$ as respect to $y$**

$2x^{2-1} + \frac{d[y^2]}{dy} \times \frac{dy}{dx} = 0$

- **Simplify**

$2x + 2y \times \frac{dy}{dx} = 0$

Now that we have solved the derivative of $y^2$ as respect to $y$, we need to finish this instance of the Chain Rule by solving the derivative of $y$ as respect to $x$. This is what can be viewed as our "unknown" like in Algebra, we are now going to solve for $\frac{dy}{dx}$:

$2x -2x + 2y \times \frac{dy}{dx} = 0-2x$
$\frac{2y \times \frac{dy}{dx}}{2y} = \frac{-2x}{2y}$
$\frac{dy}{dx}=-\frac{2x}{2y}$
$\frac{dy}{dx}=-\frac{x}{y}$

The derivative of $y$ as respect to $x$ is $-\frac{x}{y}$. What is interesting about this is that for any given $x$ and $y$ value, we can find the slope of the tangent line passing through our $(x,y)$ point on the Unit Circle, which is pretty useful.

#### Example for the expression $x^2 + xy + y^3 = 0$, find $\frac{dy}{dx}$

- **Given**

$x^2 + xy + y^3 = 0$

- **Find Derivative of Each Side**

$\frac{d}{dx}[x^2 + xy + y^3] = \frac{d}{dx}[0]$

- **Constant Rule**

$\frac{d}{dx}[x^2 + xy + y^3] = 0$

- **Sum Rule**

$\frac{d}{dx}[x^2] + \frac{d}{dx}[xy] + \frac{d}{dx}[y^3] = 0$

- **Power Rule**

$2x^{2-1} + \frac{d}{dx}[xy] + \frac{d}{dx}[y^3] = 0$

- **Product Rule**

$2x + y\frac{d}{dx}\[x\] + \frac{d}{dx}[y]x + \frac{d}{dx}[y^3] = 0$

- **Power Rule**

$2x + yx^{1-1} + \frac{d}{dx}[y]x + \frac{d}{dx}[y^3] = 0$

- **Chain Rule**

$2x + y + \frac{d[y]}{dy} \times \frac{dy}{dx} \times x + \frac{d}{dx}[y^3] = 0$

- **Power Rule**

$2x + y + y^{1-1} \times \frac{dy}{dx} \times x + \frac{d}{dx}[y^3] = 0$

- **Chain Rule**

$2x + y + \frac{dy}{dx} \times x + \frac{d[y^3]}{dy}\times\frac{dy}{dx} = 0$

- **Power Rule**

$2x + y + \frac{dy}{dx} \times x + y3^{3-1} \times\frac{dy}{dx} = 0$

- **Factor**

$2x + y + \frac{dy}{dx}(y3^{2} + x) = 0$

- **Solve for $\frac{dy}{dx}$**

$2x -2x + y -y + \frac{dy}{dx}(3y^{2} + x) = 0 - 2x - y$

$\frac{dy}{dx}(3y^{2} + x) = -(2x + y)$

$\frac{\frac{dy}{dx}(3x^{2} + x)}{(3x^{2} + x)} = \frac{-(2x + y)}{(3y^{2} + x)}$
**Solved**
$\frac{dy}{dx}=-\frac{(2x + y)}{(x+3y^{2})}$

### Second Derivative

A second derivative is a derivative of a derivative. It is pretty self explanatory. It is denoted as:
$$\frac{d^2}{dx^2} \text{ or } f"(x)$$
Which is pretty logical considering what it means:
$\displaystyle \frac{d^2y}{dx^2} = \frac{d}{dx}[\frac{d}{dx}[y]]$ 

#### Example for the function $f(x) = \frac{6}{x^2}$

- **Given**

$\frac{6}{x^2}=6x^{-2}$

- **Power Rule**

$\frac{d}{dx}[6x^{-2}] = 6 \times -2x^{-3}$

- **Simplify**

$\frac{d}{dx}[6x^{-2}] = -12x^{-3}$

Now, we find the second derivative:
- **Given**

$\frac{d^2}{dx^2}[6x^{-2}] = \frac{d}{dx}[-12x^{-3}]$

- **Power Rule**

$\frac{d^2}{dx^2}[6x^{-2}] = -12\times -3x^{-4}$

- **Simplify**

$\frac{d^2}{dx^2}[6x^{-2}] = 36x^{-4}$

The second derivative, $\frac{d^2}{dx^2}$, of $6x^{-2}$ is $36x^{-4}$.

#### Example for expression $y^2 - x^2 =4$

- **Given**

$y^2-x^2=4$

- **Take the Derivative of Both Sides (Implicit Differentiation)**

$\frac{d}{dx}[y^2-x^2]=\frac{d}{dx}[4]$

- **Difference Rule**

$\frac{d}{dx}[y^2] - \frac{d}{dx}[x^2] = 0$

- **Chain Rule**

$\frac{dy}{dx} \times \frac{d}{dy}[y^2] - \frac{d}{dx}[x^2] = 0$

- **Power Rule**

$\frac{dy}{dx} \times 2y - 2x = 0$

- **Solve for $\frac{dy}{dx}$**:
$\frac{dy}{dx} \times 2y - 2x + 2x= 0 + 2x$
$\frac{\frac{dy}{dx} \times 2y}{2y} = \frac{2x}{2y}$
$\frac{dy}{dx} = \frac{2x}{2y}$
$\frac{dy}{dx} = \frac{x}{y}$

**Solve for $\frac{d^2y}{dx^2}$:**
- **Given**

$\frac{dy}{dx} = \frac{x}{y}$

- **Find $\frac{d}{dx}$**

$\frac{d}{dx}[\frac{dy}{dx}] = \frac{d}{dx}[\frac{x}{y}]$

- **Simplify**

$\frac{d^y2}{dx^2} = \frac{d}{dx}[xy^{-1}]$

- **Product Rule**

$\frac{d^2y}{dx^2} = \frac{d}{dx}\[x\]y^{-1}+\frac{d}{dx}[y^{-1}]x$

- **Power Rule:**

$\frac{d^2y}{dx^2} = 1y^{-1}+\frac{d}{dx}[y^{-1}]x$

- **Chain Rule**

$\frac{d^2y}{dx^2} = \frac{1}{y}+\frac{dy}{dy}[y^{-1}] \times \frac{dy}{dx}\times x$

- **Power Rule**

$\frac{d^2y}{dx^2} = \frac{1}{y}+-1y^{-2}\times \frac{dy}{dx}\times x$

- **Substitute $\frac{dy}{dx}$**

$\frac{d^2y}{dx^2} = \frac{1}{y}-\frac{1}{y^2}\times \frac{x}{y}\times x$

- **Simplify:**

$\frac{d^2y}{dx^2} = \frac{1}{y}-\frac{x^2}{y^3}$

The second derivative, $\frac{d^2y}{dx^2}$, of $y^2 - x^2 =4$ is $\frac{1}{y}-\frac{x^2}{y^3}$.

### Applications of Derivatives

#### Straight Line Motion

Given a particle that can move left or right on the $x$-axis defined as $x(t), t \ge 0$, what is the velocity, speed, and acceleration of that particle? Well $v(t) =x'(t)$ is our velocity, speed is the magnitude/absolute value of $v(t)$, or $s(t) =|v(t)|$ , and acceleration is equal to $a(t) = v'(t) = x"(t)$. If $v(t) > 0$ then we're moving forward, if $v(t) < 0$ then we're moving backward, and if $v(t) = 0$ then we are neither moving forwards or backwards. To determine speed we must use both $v(t)$ and $a(t)$, if $v(t) > 0$ and $a(t) > 0$ then our speed is increasing, if $v(t) < 0$ and $a(t) < 0$ then our speed is also increasing. If $v(t) = 0$, then it is neither increasing or decreasing. Otherwise, the speed is decreasing. 

#### Local Linearity

Local Linearity means that for a graph that is differentiable, if you zoom in close enough at a point, the graph will begin to look linear and that slope of that linear line will equal that of the derivative at that point. Local Linearity allows us to approximate the value for a point on a curve using the derivative of the function at a different point. This is best explained with an example. Say that we wanted to find out, approximately, what the value of $\sqrt{4.25}$ is when you don't have a calculator. This is obviously a rare circumstance but this is the case here. The issue is, this isn't really easy to solve without a calculator. What we do know is what the value of $\sqrt 4$ is, that is simple it is just $2$. With this knowledge, we can take the derivative of the function $f(x) = \sqrt x$ at the point $x = 4$, and we will get the slope of the tangent line passing through $f(4)$. Why is this important? Because the tangent, although not perfect, is quite close to the curve of $f(x)$.  To find out our approximate value we can use the following formula where $x$ is equal to the point we already know the value for and $a$ is the value we are trying to approximate:

$$f(x) + f'(x)(a-x)$$

Using this formula for our problem will reveal the solution:

$f(4) + f'(4)(4.25 - 4)$
$2 + \frac{0.25}{4}$
$2 + 0.0625$
$2.0625$

As we can see $\sqrt {4.25} \approx 2.0625$. Does this hold up? Well the actual value for $\sqrt{4.25}$ is more accurately $2.0615528$. I'd say that our approximate value is good enough for most use cases. As we can see Local Linearity is an incredibly powerful tool for estimating values of a function.

#### L'Hôpital's rule

L'Hôpital's rule is another powerful application of the derivative that relates to the limit. The limit relates to the derivative, and much in the same way the derivative also relates to the limit. Heck, limits are used in the definition of a derivative so it makes sense that the derivative can be inversely used with limits. L'Hôpital's rule states that for the differentiable functions $f(x)$ and $g(x)$:

$$\displaystyle \text{if } \lim_{x \rightarrow c} f(x) = \lim_{x \rightarrow c} g(x) = 0 \text{ or}\pm\infin \land g'(x) \ne 0 \land \displaystyle \exists~\lim_{x \rightarrow c} \frac{f'(x)}{g'(x)} \Rightarrow \displaystyle \lim_{x \rightarrow c} \frac{f(x)}{g(x)} = \lim_{x \rightarrow c} \frac{f'(x)}{g'(x)}$$

### Analyzing Functions Using Derivatives

#### Mean Value Theorem

The Mean Value Theorem states that  $f \in C[a, b] \iff f \in C^1(a, b) \Rightarrow \exists~c, c \in (a, b) \text { and } f'(c) = \frac{f(b) - f(a)}{b-a}$. This makes intuitive sense, we are basically saying that if $f$ is continuous between $a$ and $b$ inclusive and that $f$ is differentiable between $a$ and $b$ exclusive, at some value called $c$ (there can be multiple $c$ values) between $a$ and $b$ exclusive, that the derivative at that point, or the slope of the tangent line, is equal to the average rate of change between the two points $a$ and $b$. Lets see this in action:

##### Example for the function $f(x) = \sqrt{4x-3}$  for $f$ on the interval $1 \le x \le 3$

Given the function $f(x) = \sqrt{4x - 3}$, find the point $c$ that satisfies the Mean Value Theorem for $f$ on the interval $1 \le x \le 3$. This means that $c \in (1, 3)$. First, we must find the derivative of $f(x)$ which is equal to $f'(x) = \frac{2}{\sqrt{4x-3}}$. Now, we must find the average rate of change between $x = 1$ and $x = 3$ for our function $f(x)$:

$\frac{\Delta y}{\Delta x} = \frac{f(b) - f(a)}{b - a} = \frac{f(3) - f(1)}{3-1} = \frac{\sqrt{4\times 3 - 3} - \sqrt{4 \times 1 -3}}{2} = \frac{3-1}{2}=\frac{2}{2}=1$

This means that we must find the point $c$ which equals the rate of change $1$. Now, we just substitute $1$ for $f'(x)$: 

$1 = \frac{2}{\sqrt{4c -3}}$

$\sqrt{4c - 3} = 2$

$4c - 3 = 4$

$4c = 4 + 3$

$4c = 7$

$c = \frac{7}{4}$

This means that to satisfy $f'(c) = 1$, the point $c = \frac{7}{4}$.

#### Extreme Value Theorem

The Extreme Value Theorem states that $\text{if }f \in C[a, b] \Rightarrow \exists~c, d \in [a, b] \text{ such that }f(c) \le f(x) \le f(d) ~\forall x \in [a, b]$. In other words, if a function doesn't break away at any point (eg. continuous) there is guaranteed to be two values for the function that are greater than or equal to every other point and smaller than or equal to every other point, respectively.

#### Critical Points

Critical points are points on the graph where the derivative at that point is equal to zero or it is undefined. In other words:

$$\exists~c \text{ such that } f'(c) = 0 \text{ or undefined}$$

##### Example for $g(x) = \sin(3x), \text{ for } 0 \le x \le \pi$

- **Find the derivative of $g(x)$**

$g'(x) = \frac{d}{dx}[\sin(3x)]$

- **Chain Rule**

$g'(x) = \frac{d}{\sin x}[\sin(3x)] \times \frac{d}{dx}[3x]$

- **Take the derivative of $\sin(3x)$ with respect to $\sin x$**

$g'(x) = \cos(3x) \times \frac{d}{dx}[3x]$

- **Take the derivative of $3x$ with respect to $x$**

$g'(x) = 3\cos(3x)$

We know that $\cos$ is defined for all values of $x$, so we don't have to search for any undefined points. So now we just search for when our derivative is equal to $0$:

- **Set $g'(x) = 0$**

$0 = 3 \cos (3x)$

- **Solve for $x$**

$\frac{0}{3} = \frac{3 \cos(3x)}{3}$

$0 = \cos(3x)$

$\cos^{-1}0 = \cos^-1(\cos(3x))$

$3x = \pi n + \frac{\pi}{2} \text{ for all } n \in \Z$ 

$x = \frac{\pi n}{3} + \frac{\pi}{6} \text{ for all } n \in \Z$

Remember that our range for this example is $0 \le x \le \pi$, so we can take any value for this expression above such that $\frac{\pi n}{3} + \frac{\pi}{6} \le \pi$, which our values of $n$ that satisfy this are:
$n = 0, 1, 2$

So the critical points are:

$x_0 = \frac{\pi}{6}$

$x_1 = \frac{\pi}{2}$

$x_2 = \frac{5\pi}{6}$

#### Finding the Increasing and Decreasing Intervals for a Function

For a function $f(x)$, the intervals at which $f$ is increasing are when $f'(x) >0$ and decreasing when $f'(x) < 0$. If a function is decreasing to the left of $0$ and to the right of $0$, it will be decreasing through $0$, the same is true for increasing. We can apply the principle of critical points to help locate these intervals.

##### Example for $f(x) = x^3+3x^2−9x+7$

First we must find $f'(x)$, which is equal to $3x^2 + 6x -9$. So we have to find $f'(x) > 0$ and $f'(x) < 0$, we can do this using critical points. Critical points are when the derivative is zero or undefined, and if the derivative is at $0$ the rate of change is also $0$, meaning that it is either going to stay $0$ or will change positive or negative. Lets factor this expression and see what our $0$s are:

$3x^2 + 6x -9$

$3(x^2 + 2x - 3)$

$3(x + 3)(x - 1)$

Now that we have factored our expression, we can see what our Critical Points are, $x = -3$ and $x = 1$. So, we need to find what the function does at these intervals:

- $x < - 3$
- $-3 < x < 1$
- $x > 1$

Well for our first interval $x < -3$ we just need to evaluate what $f'(-4)$ is. Then, for our second interval $-3 < x < 1$ we need to evaluate $f'(0)$. Finally, for our third interval $x > 1$ we need to evaluate $f'(2)$:

- $x< 3$: $f'(-4)$

$f'(-4)=3(-4)^2 + 6(-4)- 9 = 15$, this is a positive $x$ value, thus $x$ is increasing at the interval $x < 3$.

- $-3 < x < 1$: $f'(0)$

$f'(0) = 3(0)^2+6(0) - 9 = -9$, this is a negative $x$ value, thus $x$ is decreasing at the interval $-3 < x < 1$.

- $x > 1$: $f'(2)$

$f'(1) = 4(1)^2 + 6(1) - 9 = 19$, this is a positive $x$ value, thus $x$ is increasing at the interval $x > 1$.

#### First Derivative Test

In the section above, we determined a method to locate the intervals using critical points. We will combine these two principles in what is known as the First Derivative Test to locate **relative** extrema. These extrema are our relative maximum and our relative minimum. Relative maximum and relative minimum are different from global maximum and minimum because those are the absolute largest and absolute smallest values for out function over an interval. Our relative maximum is defined as:

$$f(c) \text{ is a relative maximum iff } f(c) \ge f(x) \text{ for all } x \in (c-h, c+h) \text{ for } h > 0$$

Similarly, relative minimum is defined as:

$$f(c) \text{ is a relative minimum iff } f(c) \le f(x) \text{ for all } x \in (c-h, c+h) \text{ for } h > 0$$

Now that we have our definitions, we can think about what it is saying. Basically, for a relative maximum to be a relative maximum it has to be larger than or equal to every $x$ value in some non-zero interval. This also means that from the left of $f(c)$ the derivative has to be positive and from the right of $f(c)$ the derivative has to be negative. We can think of this as "swapping" from positive to negative once we get past $f(c)$. Inversely, for a relative minimum to be a relative minimum it has to be smaller than or equal to every $x$ value in some non-zero interval. This would mean the opposite from our relative maximum, this means that from the left of $f(c)$, the derivative has to be negative and from the right of $f(c)$, the derivative has to be positive. Again, we can think of this as "swapping" from negative to positive once we get past $f(c)$. Putting this all together we can determine using our derivatives that a point is a relative maximum if $f'$ goes from $f' > 0$ to $f' < 0$ and a point is a relative minimum if $f'$ goes from $f'<0$ to $f'>0$. For it to "swap" like that it would have to pass through $0$ or be undefined at a certain point, logically. This is where our critical points come in. If the derivative to the left of a critical point is greater than zero and the derivative to the right of a critical point is less than zero, then it is a relative maximum point. Inversely, if the derivative to the left of a point is less than zero and the derivative to the right of a critical point is greater than zero, then it is a relative minimum point.  

##### Example for $f(x) = x^3 - x^4$

First we take the derivative, which equals $f'(x) = 3x^2-4x^3$. We can factor to $f'(x) = x^2(3-4x)$. Now we can find our critical points:

$0 = x^2(3-4x)$

We can separate this into $x^2 = 0 \text{ or } 3 - 4x = 0$. Solving both:

$x^2 = 0$

$x = 0$

$3-4x = 0$

$3 = 4x$

$x = \frac{3}{4}$

Our two critical points are at $0$ and $\frac{3}{4}$. So, we can look to the left and the right of our critical points to reveal what they are relative to the graph. 

- Left of $0$: $f'(-1) = 3(-1)^2 - 4(-1)^3 = 3 + 4 = 7$
- Right of $0$, Left of $\frac{3}{4}$: $f'(\frac{1}{2}) = 3(\frac{1}{2})^2 - 4(\frac{1}{2})^3 = \frac{3}{4} - \frac{1}{2} = \frac{1}{4}$  
- Right of $\frac{3}{4}$: $f'(1) = 3(1)^2-4(1)^3=3-4=-1$

So to the left of $0$, we are increasing, to the right of $0$ we are increasing, to the left of $\frac{3}{4}$ we are increasing and to the right of $\frac{3}{4}$ we are decreasing. This means that $0$ is neither a relative maximum or relative minimum and that $\frac{3}{4}$ is a relative maximum. 

#### Absolute Extrema

##### Extrema in a Closed Interval

As we learned from the Extreme Value Theorem, we know that for any continuous closed interval, a function is guaranteed to have a maximum value and a minimum value. This is known as the **absolute** extrema, or an absolute maximum and absolute minimum. So, although for any given relative extrema there are, a continuous function on a closed interval is guaranteed to have absolute extrema. The absolute maximum or the absolute minimum can either be the end points of the closed interval or the critical points inside those close points.

###### Example for $f(x) = 8 \ln x - x^2 \text{ for } x \in [1, 4]$

Given the function $f(x) = 8 \ln x - x^2$, find the absolute extrema. 

Well the absolute extrema can either be the end points or the critical points, eg. $1, 4...c$. We don't know our critical points yet so lets do that. First, lets find calculate the derivative as $f'(x) = \frac{8}{x} -2x$, with this, let's set $f'(x)=0$:

$0 = \frac{8}{x}-2x$

$2x = \frac{8}{x}$

$2x^2=8$

$x^2=4$

$x = \pm2$

Because $-2$ is outside of our interval, we can eliminate it as a critical point, we can also eliminate the only part where $f'(x) = \text{ undefined}$ as that is only at $0$ which too is outside of our interval. So we are left with

$c = 2$

So, to locate our absolute extrema, we insert our points into our original function:

$f(1) = 8\ln 1 - 1^2=-1$

$f(2) = 8 \ln 2 - 2^2 \approx 1.545$

$f(4)= 8 \ln 4 - 4^2 \approx -4.910$

So, we can see that our absolute maximum for this interval of the function $f(x)$ is $x=2$ and the absolute minimum for this interval of the function $f(x)$ is $x = 4$.

##### Extrema Globally (Entire Domain) 

Just like extrema in a close interval, extrema can also exist globally. Some functions don't have a global extremum on their **entire** domain. To find global extrema, this is much the same way as the First Derivative Test, but in this case we are locating a critical point, say $c \text{ such that } (-\infin, c)$ is increasing or decreasing and $(c, \infin)$ is increasing or decreasing. Note that if the first is increasing the second has to be decreasing for it to be a maximum, and inversely if the first is decreasing the second has to be increasing for it to be a minimum. Let's see this in action.

###### Example for $f(x) = x^2 \ln x$ for $x > 0$

Given the function $f(x) = x^2\ln x$ for $x > 0$, locate the global extrema.

First, let's determine the derivative as $f'(x) = 2x\ln x + x$. We have a restriction that $x > 0$, because $\ln x$ does not apply for negative values.

$0 = 2x \ln x + x$

$2x + \ln x = - x$

$\ln x = - \frac{1}{2}$

$x = e^{-\frac{1}{2}} = \frac{1}{\sqrt e}$

So now that we have our critical point, we can look to see what happens to $f'(x)$ around our critical point:

$f'(0.5) = 2 \times 0.5 \ln (0.5) + 0.5 \approx 0.693 + 0.5 \approx -0.193$

$f'(1) = 2 \times 1 \ln (1) + 1 = 1$

So to the left of our critical point, we are decreasing from the left and increasing from the right, which means that this is an absolute global maximum point of the function $f(x)$. Pretty neat. 

#### Concavity

Concavity is a result of our extrema, a graph will form a bit of a "concave" around these points. In the case of maximums they form a downwards concave $\cap$ and in the case of minimums they form an upwards concave $\cup$. They are defined using the following rough rules:

Concave Downwards:

Slope Is Decreasing at an interval, thus $f'(x)$ is decreasing at that interval, and thus $f"(x) < 0$ at that interval.

Concave Upwards

Slope is Increasing at an interval, thus $f'(x)$ is increasing at that interval, and thus $f"(x)$ > 0 at that interval.

##### Analyzing Concavity Using Algebra

It is possible to analyze concavity without the need to graph, we do this by utilizing the second derivative of a function. If we can find the critical points of the second derivative, we can locate where we have concaves.

###### Example for $f(x) = -x^4 +6x^2 -2x -3$

Given the function $f(x) = -x^4 + 6x^2 -2x -3$ locate the intervals at which there are either upward or downward concaves. To do this lets locate the second derivative:

$f'(x) = -4x^3 + 12x - 2$

$f"(x) = -12x^2 +12$

Now we locate our critical points:

$0 = -12x^2 + 12$

$-12x^2 = -12$

$x^2 = 1$

$x = \sqrt 1$

$x = \pm 1$

Now that we have our critical points we can locate the intervals:

- $(- \infin, -1): f"(-2) = -12(-2)^2+12 = -36,f"(x) < 0 \Rightarrow \cap$

- $(-1, 1): f"(0) = -12(0)^2 + 12 = 12, f"(x) > 0 \Rightarrow \cup$

- $(1, \infin): f"(2) = -12(2)^2 + 12 = -36, f"(x) < 0 \Rightarrow \cap$

#### Inflection Points

Building off of what he have learned about Concavity, we have seen what happens at a critical point, the slope switches from positive to negative or vise versa. Now that we understand Concavity, we will notice that there exists points that "switch" from say a downward concave to a upward concave. These "switches" for the $f(x)$ are the extrema of the graph $f'(x)$, meaning that the switch from these concaves happen at the critical point of $f"(x)$. If $f"(x)$ switches from negative to positive, it switches from a $\cap$ to $\cup$. If $f"(x)$ instead switches from a positive to a negative, it switches from $\cup$ to $\cap$.

##### Finding Inflection Points Using Algebra

The principle of finding inflection points is identical to that of finding concavity using the second derivative, if we can locate the critical points of the second derivative, and it switches signs like the example in "Analyzing Concavity Using Algebra." The points in the example, $f"(-2)$, $f"(0)$, and $f"(2)$ are our Inflection Points.

#### Second Derivative Test

Putting together all we have learned about the mean value theorem, the extreme value theorem, critical points, increasing and decreasing intervals for a function, the extrema, concavity and finally inflection points has brought us here, the Second Derivative test. This test states:

$$\text{if } f'(x) = 0 \land \exists~ f"(c) \Rightarrow \begin{cases} f(c) = \text{local maximum} & \text{if } f"(c) < 0 \\\ f(c) = \text{local minimum} & \text{if } f"(c) > 0 \\\ \text{inconclusive} & \text{if } f"(c) = 0 \end{cases}$$

## The Integral
> So, naturalists observe, a flea  
Has smaller fleas that on him prey;  
And these have smaller still to bite 'em,  
And so proceed *ad infinitum.*  
~ Jonathan Swift, *On Poetry: a Rhapsody*  

### Definite Integrals

#### Definition of Summation

Summation is adding a series of numbers. Summation is given with the capital Sigma notation:
$$\displaystyle \sum_{i=m}^n i$$

Where $i$ is the index of summation, $m$ is the lower bound of summation, and $n$ is the upper bound of summation. The $i=m$ basically means that $i$ starts at $m$, and the $n$ means that the summation ends when $i=n$. To the left of the Sigma is the lone $i$, which indicates what we are summing, in this case we are just summing $i$. Here is an example summation for $i^2$ between 1 and 100:

$$\displaystyle \sum_{i=1}^{100} i^2 = 1^2 + 2^2 + 3^3...99^2 + 100^2$$ 

#### An Integral

The idea of an integral is finding the area under a graph and it relates to what is known as **infinitesimally** small quantities, or quantities that are closer to zero than any other real number, but also aren't 0. This may sound foreign so I encourage you to watch this video by 3Blue1Brown entitled: ["Integration and the fundamental theorem of calculus".](https://youtu.be/rfG8ce4nNh0) I'd recommend watching the *entire* series as well as it is quite a beautiful and easy way to understand the core principles of Calculus. With this understanding, we can jump right into a "Riemann integral" and its definition:

$$\displaystyle \int_a^b f(x)~dx = \lim_{n \rightarrow \infin} \sum_{i=1}^n \Delta x f(x_i)$$

This is read as "the limit as $n$ approaches infinity of the sum of the function $f$ with $x$ sub $i$ times delta $x$ sub $i$ from $i$ equal $1$ to $n$ is equal to the integral over $[a, b]$ of $f(x)$." We can think of the integral sign much like the summation sign, but instead of taking the sum of a discrete number of things we are instead taking the sum of an infinite number of infinitely thin things.

#### Accumulation of Change and Net Change

A definite integral can help express the accumulation and net change. If we envision a tank filling with water at a constant rate, what would be the volume for any given time $t$? Well we could represent this as $\text{Volume} = \text{Time } \times \text{ Rate}$. So if we are filling up our tank at a constant rate of $5\frac{\text{L}}{\text{min}}$, then after $2$ minutes, the volume would be $10~\text{L}$. This is fine and good, but lets re-frame this some. If we were instead to graph the rate per unit of time, we'd get a function like $r(t) = 5$, or rate per time. In this case, this would just be a constant horizontal line at $y=5$. How would we figure out the volume using this? Well, much like a rectangle we would multiply the height under the graph (which is always the rate) in this case $5 \frac{\text{L}}{\text{min}}$ and then the width, which is time. If our time is again $2$ minutes, we'd be finding the area underneath the graph if we multiplied by the height and the width, $10~\text{L}$. Now imagine that the rate at which we are filling up our tank is instead not constant, and it varies. We could model our new rate by using the equation: $r_2(t)=6 \sin(0.3t)$. How could we use the above method using area to determine this graph as well? Well this is where integrals come into play, say we wanted to find the volume after 7 minutes, we'd say:

$\displaystyle \int_0^6 r_2~dt \approx 24.5~\text{L}$

So that is neat, and I didn't show how to that was calculated there as that is outside the scope of this section. Instead, we are here to appreciate what this means, it means that from the 0 minutes to 6 minutes, the tank had a **net change** of $24.5~\text{L}$. Why do I say net change? Because technically speaking, we don't know how much water is in the tank before we started filling it, say it could of already been $7~\text{L}$ full. An Integral helps us see the accumulation of change over a period of time, thus we are studying the net change between the intervals. We are not asking how much water is in the tank, we are asking between two periods of time what was the new change of water?

#### Riemann Sums

Riemann Sums are a foundational component of Integral Calculus, in fact a definition for the integral is derived from the Riemann Sum. Say that we are trying to find the area underneath the graph, it'd make logical sense to split it up into smaller rectangular bits, like from that 3blue1brown video.

##### Subdivisions/Partitions

As is the main focus with Reimann Sums, Subdivisions or Partitions (we will call them Subdivisions from now on) are incredibly important. Subdivisions are intervals that relate to a space underneath the graph that can be measured. The main take away is to remember that subdivisions can be uniform (every subdivision is the same width) or nonuniform (some subdivisions aren't the same width as the others.) The more subdivisions we have, the more accurate our approximation for the area will be.

##### Left Vs. Right Riemann Sums

The first thing to understand about Reimann Sums is that there are a lot of way of configuring these partitions. For instance, when we make these rectangles on our graph, do we set the left point of the rectangle to equal $(x, f(x))$ or do we set the right? If a left point of each rectangle is resting on the graph of our function, then it is a Left Riemann Sum, if the right point of each rectangle is resting on the graph of our function, then it is a Right Riemann Sum. As a result for each of our graphs we could be overestimating or underestimating the value for the area underneath the graph. This is because depending on where place our sums (either left or right) they can either over shoot the graph or undershoot the graph. A general rule of thumb is:

- If the graph is increasing at the interval, it will be an underestimate for a Left Reimann sum, and an overestimate for a Right Reimann Sum.
- If the graph is decreasing at that interval, it will be an underestimate for a Right Reimann sum, and an overestimate for a Left Reimann Sum.

##### Midpoint and Trapezoidal Reimann Sums

Reimann Sums don't only have to be based on the left or right point of the "rectangle." In fact, they don't have to be rectangles at all. Given a subdivision as an interval such as $[-1, 0]$, instead of taking the Riemann sum at $-1$ (left) or $0$ (right,) lets instead take it at $-\frac{1}{2}$. This is what a Midpoint Reimann Sum is, it is merely setting the height of the subdivision to be the mid point of an interval.

Trapezoidal Reimann sums are as they are described, trapezoids, where the heights are the end points of the interval, so if your subdivision is from $[-1, 2]$, the heights would be $f(-1), f(2)$ respectively and the area would be found with $A= \frac{f(-1) + f(2)}{2}\Delta x$. Logically then, a summation of multiple Trapezoidal Reimann Sums, would look something like this:

$$S = \frac{f(n_0) +f(n_1)}{2} \Delta x + \frac{f(n_1) + f(n_2)}{2}\Delta x + ... +\frac{f(n_{z-1} + f(n_z))}{2}\Delta x$$

Which, we can then simplify this by factoring out $\frac{\Delta x}{2}$

$$S = \frac{\Delta x}{2}(f(n_0) + 2f(n_1) + 2f(n_2) + ... 2f(n_{z-1}) + f(n_z))$$

##### Representing Riemann Sums with Summation Notation

Let $\Delta x$ equal the width of each subdivision, so for the interval $[a,b]$, we can find equal widths with $\Delta x = \frac{b-a}{n}$, where $n$ is the number of subdivisions. Let $x_i$ equal the right endpoint of each subdivision, thus we can find each right point with $x_i = a + \Delta x \times i$. Thus we can find the height of each subdivision for the function $f(x)$ with $f(x_i)$, and the area would be the height of each subdivision multiplied by the width: $f(x_i) \times \Delta x$. So, putting this all together with Summation Notation, we can find the area underneath a graph for either a Left, Right, or Midpoint Riemann sum with the following equations:

- Left Riemann sum

$$\displaystyle \sum_{i = 0}^{n-1} f(x_i)\Delta x $$

- Right Riemann sum

$$\displaystyle \sum_{i=1}^{n}f(x_i)\Delta x $$

- Midpoint Riemann sum

$$\displaystyle \sum_{i=0}^{n-1} f(a+\frac{\Delta x}{2} + i)\Delta x$$

#### Definite Integral as the Limit of a Riemann Sum

Looking back at our definition of the definite integral as discussed earlier, it is defined as:

$$\displaystyle \int_a^b f(x)~dx = \lim_{n \rightarrow \infin} \sum_{i=1}^n \Delta x f(x_i)$$

This is a very nice definition now that we understand what a Riemann is. With this, we can also define what the width of each subdivision equals, $\Delta x$, as well as each right point is, $x_i$:

$$\Delta x = \frac{b - a}{n} \text{ and } x_i = a + \Delta x \times i$$

##### Find the Riemann Sum From a Definite Integral
Imagine we have the definite integral:
$$\displaystyle \int_{\pi}^{2\pi} \cos(x)~dx$$

And we are asked to find the limit of the Riemann sum from the integral. The limit of the Riemann sum is denoted as:
$$\displaystyle \lim_{n \rightarrow \infin} \sum_{i=1}^n \Delta x f(x_i)$$

So we are going to solve for $\Delta x$ and $x_i$:

$$\Delta x = \frac{b-a}{n}$$

$$\Delta x = \frac{2\pi - \pi}{n}$$

$$\Delta x = \frac{\pi}{n}$$

With this we can solve $x_i$:

$$x_i = a + \Delta x \times i$$

$$x_i = \pi + \frac{\pi}{n} \times i$$

$$x_i = \pi + \frac{\pi i}{n}$$

Therefore:

$$\displaystyle \int_{\pi}^{2\pi} \cos(x)~dx = \lim_{n \rightarrow \infin} \sum_{i=1}^n \frac{\pi}{n} f(\pi + \frac{\pi i}{n})$$

##### Find the Definite Integral from a Riemann Sum
This is a bit trickier than the previous problem. Imagine we have the Riemann Sum:
$$\displaystyle \lim_{n \rightarrow \infin} \sum_{i=1}^n \sqrt{4 + \frac{5i}{n}} \times \frac{5}{n}$$

And we are asked to find the definite integral from the limit of the Riemann sum. The definite integral is denoted as:
$$\displaystyle \int_a^b f(x)~dx$$
We must find $f(x)$ and $a$ and $b$. First locate the fraction that does not contain $i$, this is $\Delta x$, you should see a similar fraction inside the $f(x)$, but have an $i$. You will notice there is no $f(x)$, this is because the actual definition for $f(x)$ has been given. This is known as the "integrand" and in this case it is $\sqrt{x}$. The $a$ value is $4$, as denoted inside the integrand. So to find $b$, we add $a$ to the numerator of $\Delta x$, which gives us $9$. So, putting this all together we can make our integral:

$$\displaystyle \int_4^9 \sqrt{x} ~dx$$

#### Definite Integral Rules
##### Sum/Difference Property
$$\displaystyle \int_a^b [f(x) \pm g(x)]~dx = \int_a^b f(x)~dx \pm \int_a^b g(x)~dx$$
##### Constant Multiple Property

Where $k$ is any constant:

$$\displaystyle \int_a^b k\times f(x) ~dx = k \int_a^b f(x)~dx$$

##### Reverse Interval Property

$$\displaystyle \int_a^b f(x)~dx = -\int_b^af(x)~dx$$

##### Zero-Length Interval Property

$$\displaystyle \int_a^a f(x)~dx=0$$

##### Adding Intervals Property

$$\displaystyle \int_a^b f(x)~dx + \int_b^cf(x)~dx = \int_a^cf(x)~dx$$

##### Estimation Property

$$\displaystyle \int_a^b f(x)~dx \le \int_a^b g(x)~dx \iff f(x) \le g(x) \in [a,b]$$

##### Absolute Value Property

$$\displaystyle \left|\int^b_a f(x)~dx\right| \le \int_a^b |f(x)|~dx$$

### Indefinite Integrals

#### Definition

Consider the relationship of these two functions:

$$F(x)=x^2$$

$$f(x)=2x$$

$F'(x) =f(x)$, so $f$ is the derivative of $F$. Inversely, $F$ is the **antiderivative** of $f$. An Indefinite Integral is the reverse of a derivative, it is the antiderivative, and is denoted with: $\displaystyle \int$. It can be seen that it looks a lot like a definite integral, but it lacks an $a$ or $b$ to define the scope of intervals. Appreciate for a moment what this accomplishes for us and really think about the relationship we have just established. To find a derivative is a task that has set steps, steps of which are reversible. Remind yourself too what this means for the study of change. We have established now a relationship between something that helps us find instantaneous change, the derivative, and now something that helps us find the accumulation of change, the antiderivative. Calculus is easy to be thought of as an arbitrary set of rules but truly it has a diversity of applications. The **antiderivative** is just as important as the **derivative.** It is just as **fundamental.** You will see why shortly. 

So, the derivative of $x^2$ is $2x$, so the antiderivative of $2x$ would be $x^2$, no? Sort of. The issue is that the derivative of $x^2 + 1$ is $2x$, and so is $x^2 + 2$. So to remedy to this we introduce the "constant." The antiderivative of $2x$ is $x^2 +C$. Where C is any constant. So:
$$\displaystyle \int 2x ~dx = x^2 + C$$

##### Examples

* $\displaystyle \int 3z^2 + 5 ~dz = z^3 +5z + C$
* $\displaystyle \int 18x^2 +10 x ~ dx = 6x^3 + 5x^2 + C$
* $\displaystyle \int -56 \sin(7x -5) ~ dx = 8 \cos (7x-5) + C$

#### The Reverse Power Rule

$$\displaystyle \int x^n ~dx = \frac{x^{n+1}}{n+1} + C \text{ for } n \ne -1$$

* $\displaystyle \int x^5 ~dx  = \frac{x^{5+1}}{5+1} + C = \frac{x^6}{6} + C$
* $\displaystyle \int 5x^{-2}  ~ dx= 5\int x^{-2} ~dx = 5(\frac{x^{-2+1}}{-2+1} + C) = 5(\frac{x^{-1}}{-1} + C) = 5x^{-1} + C$
  * Note: We didn't write $C$ as $5C$ after distributing because $C$ represents some arbitrary constant.

#### Using the Reverse Power Rule

* $\displaystyle \int (3x^5 -x^3 + 6)~dx = \frac{3}{6}x^6-\frac{1}{4}x^4+6x+C=\frac{x^6}{2}-\frac{x^4}{4}+6x+C$
* $\displaystyle \int (-9x^2+9x+2)~dx = -\frac{9}{3}x^3+\frac{9}{2}x^2+2x+C=-3x^3+\frac{9}{2}x^2+2x+C$

#### Common Indefinite Integrals

* $\displaystyle \int \frac{1}{x} ~dx = \ln{|x|} +C$
* $\displaystyle \int \sin x ~dx = -\cos x + C$
* $\displaystyle \int \cos x ~dx = \sin x + C$
* $\displaystyle \int \tan x ~dx = \ln|\sec x| + C$
* $\displaystyle \int e^x ~dx = e^x + C$

#### The Fundamental Theorem of Calculus

##### FTC 1

$$\displaystyle \frac{d}{dx}\int_a^xf(x)~dx=f(x)$$

##### FTC 2

$$\displaystyle \int_\textcolor{cyan}{a}^\textcolor{purple}{b}f(x)~dx=F(\textcolor{purple}{b})-F(\textcolor{cyan}{a}), \text{ where } F(x) = \int~f(x)~dx$$

### Techniques for Evaluating Definite and Indefinite Integrals  

#### Applying the Fundamental Theorem of Calculus To Solve Definite Integrals

Imagine we are trying to solve the definite integral:

$$\displaystyle \int_{-3}^54~dx$$

We can apply the Fundamental Theorem of Calculus to achieve this:

$$\displaystyle \int_{-3}^54~dx = F(5)-F(-3)$$

$$\displaystyle F(x) = \int 4 ~dx =4x$$

So:

$$\displaystyle \int_{-3}^54~dx = F(5)-F(-3) = 4\times5 - 4 \times -3 = 20 + 12 = 32$$

##### Definite Integral of a Piecewise Function
Given the piecewise function:
$$\displaystyle f(x) = \begin{cases} x + 1 & \text{ for } x < 0 \\\ \cos(\pi x) & \text{ for } x \ge 0 \end{cases}$$

Find the integral:
$$\displaystyle \int_{-1}^1 f(x)~dx$$

When given a piecewise function, you can split this integral into different parts:

$$\displaystyle \int_{-1}^1 f(x)~dx = \int_{-1}^0f(x)~dx + \int_0^1 f(x)~dx = \int_{-1}^0 x+1 ~dx + \int_0^1 \cos(\pi x)~dx$$

Now, we can apply the Fundamental Theorem of Calculus to both integrals to solve them, starting with the first:

$$\displaystyle \int_{-1}^0x+1~dx =F(0) -F(-1)$$

$$\displaystyle F(x) = \int x+1~dx = \frac{x^2}{2} + x$$=

$$\displaystyle \int_{-1}^0x+1~dx =F(0) - F(-1) = (\frac{0^2}{2} + 0) - (\frac{-1^2}{2} - 1) = 0- -\frac{1}{2} = \frac{1}{2}$$

And now the second:

$$\displaystyle \int_0^1 \cos(\pi x)~dx = \frac{1}{\pi} \int_0^1 \pi \cos(\pi x)~dx$$

We added this $\pi$ here so as to solve this expression easier, it is equal because we are basically only multiplying by $1$.

$$\displaystyle \frac{1}{\pi} \int_0^1 \pi \cos(\pi x)~dx = \frac{1}{\pi} (F(1) - F(0))$$

$$\displaystyle F(x) = \int \pi \cos(\pi x)~dx = \sin(\pi x)$$

$$\displaystyle \frac{1}{\pi} \int_0^1 \pi \cos(\pi x)~dx = \frac{1}{\pi} (F(1) - F(0)) = \frac{1}{\pi}(\sin(\pi) -\sin(0)) = \frac{1}{\pi} (0-0) = 0$$

So we can now put this together:

$$\displaystyle \int_{-1}^1 f(x)~dx = \int_{-1}^0f(x)~dx + \int_0^1 f(x)~dx = \int_{-1}^0 x+1 ~dx + \int_0^1 \cos(\pi x)~dx = \frac{1}{2}+\frac{1}{2}$$

###### Absolute Value Functions
If given an absolute value function, split it into a piecewise function, for instance:
$$\displaystyle f(x) = |x+2| = \begin{cases} -(x+2) & \text{ for } x<-2 \\\ x+2 & \text{ for } x \ge -2 \end{cases}$$

Then you solve like any other piecewise.

#### *u*-substitution

##### Introduction

We are asked to solve the indefinite integral:

$$\displaystyle \int (3x^2+2x)e^{x^3+x^2}~dx$$

How would we go about doing this? Well notice that we are multiplying $e$ by the derivative of $e$'s exponent:

$$\displaystyle \int (\textcolor{cyan}{3x^2+2x})e^{\textcolor{cyan}{x^3+x^2}}~dx$$

This is where we can apply what is known as $u$-substitution, where we set $u$ to equal:

$$u = x^3+x^2$$

Where:

$$\frac{du}{dx} = 3x^2+2x$$

Although $\frac{du}{dx}$ does not represent a fraction, for the sake of explanation and reasoning, we can sort of think like it is, where we are solving for $du$:

$$dx\times\frac{du}{dx}=(3x^2 + 2x) \times dx$$

$$du=\textcolor{magenta}{(3x^2+2x)dx}$$

Now, we see a pattern emerge here. We can rewrite our integral to look like:

$$\displaystyle \int \textcolor{magenta}{(3x^2+2x)dx} ~e^\textcolor{cyan}{x^3+x^2}$$

Notice that the magenta section is equal to $du$, and the cyan section is equal to $u$. Thus:

$$\displaystyle \int \textcolor{magenta}{du}~e^\textcolor{cyan}{u} = \int e^\textcolor{cyan}{u}~\textcolor{magenta}{du}$$

So we now have expressed this in terms of $u$, but how do we integrate the original integral? Well we unsubstitute $u$:

$$\displaystyle \int e^\textcolor{cyan}{u}~\textcolor{magenta}{du} = \int e^\textcolor{cyan}{x^3+x^2}~\textcolor{magenta}{du}=e^{x^3+x^2}+C$$

Finally:
$$\displaystyle \int (3x^2+2x)e^{x^3+x^2}~dx = e^{x^3+x^2} + C$$

When we analyze what we have figured out, we realize that the $u$-definition is "undoing" the chain rule.

###### *u*-substitution form

For $u$-substitution to apply, we must be able to write an integrand as:
$$w(u(x))\times u'(x)$$

##### Multiplying by a Constant

Given the indefinite integral:

$$\displaystyle \int \sqrt{7x+9}~dx$$

We are asked to solve the integral using $u$-substitution. It is easy to see that our $u$ will be:

$$u = 7x + 9$$

The issue is that the derivative of $u$:

$$\frac{du}{dx}=7$$

And we know from the previous example that the most crucial feature to solve an integral using $u$-substitution is that an expression and its derivative are clearly seen for $f(x)$, and in this case no $7$ can be found outside of the square root. To remedy this, we can use the Constant Multiply Property of integrals to write our integral as:

$$\displaystyle \frac{1}{7} \int 7\sqrt{7x+9}~dx$$

Now, we can apply $u$-substitution:

$$\displaystyle \frac{1}{7} \int 7\sqrt{7x+9}~dx$$

$$\displaystyle \frac{1}{7} \int \sqrt{u}~du = \frac{1}{7}\int u^{\frac{1}{2}}~du = \frac{1}{7}(\frac{2}{3}u^{\frac{3}{2}} + C) = \frac{2}{21}u^{\frac{3}{2}}+C$$

Now, we unsubstitute $u$ and find our answer:

$$\frac{2}{21}(7x+9)^\frac{3}{2} + C$$

##### *u*-substitution with Definite Integrals

Performing $u$-substitution for definite integrals is basically the same as indefinite, with an addition of an extra step called **accounting for the limits of the integration.** For instance, it may be easy to do the following:

$$\displaystyle \int_1^2 2x(x^2+1)^3~dx = \int_1^2 u^3~du$$

But, when we are thinking about what an integral actually represents, if we were to graph the functions of these two integrals, you will find that they are different and thus will yield different areas underneath them. To fix this we are to change the interval. For our original integral, the lower bound was 1 and the upper bound 2, for our new integral we must account for the limits of the integration. To do this, we must find what values of our $u$ correspond for each boundary.

$u = x^2 +1$

$\text{Lower bound: } (1)^2+1=2$

$\text{Upper bound: } (2)^2+1=5$

These are new lower and upper bound for the $u$-substituted integral:

$$\displaystyle \int_1^2 2x(x^2+1)^3~dx = \int_2^5 u^3~du$$

So then to solve this, we don't unsubstitute $u$ like in the previous examples, instead solve the integral as it is:

$$\displaystyle \int_2^5 u^3~du = F(5) - F(2)$$

$$F(u) = \frac{u^4}{4}$$

$$\displaystyle \int_2^5 u^3~du = F(5) - F(2) = \frac{5^4}{4} - \frac{2^4}{4} = 152.25$$

Though this is a way of doing it, you can also keep the current boundaries and unsubstitute $u$:

$$\displaystyle \int_1^2 2x(x^2+1)^3~dx = \left[\frac{(x^2 +1)^4}{4}\right]^2_1$$

I'm not going to simplify this, just something to keep in mind when approaching this. You can either solve without unsubstituting $u$ or with, just remember your boundaries.

#### Integration by Parts

Recall the Derivative Product Rule, it states:

$$\displaystyle \frac{d}{dx}[f(x)g(x)] = g(x)\frac{d}{dx}[f(x)] + f(x)\frac{d}{dx}[g(x)]$$

When we think about what an anti-derivative is, this must mean that:
$$\displaystyle [f(x)g(x) = \int f'(x)g(x)~dx + \int f(x)g'(x)~dx$$

Reordering this we get:
$$\displaystyle \int f(x)g'(x) ~dx = f(x)g(x) - \int f'(x) g(x)~dx$$

##### Example for $\int x \cos x~dx$

We are asked to solve the following integral:

$$\displaystyle \int x \cos x ~dx$$

We can apply Integration by Parts to do this. First, find which part of the integral is the easiest to solve for in the last part $\int f'(x) g(x)~dx$, in this case the derivative of $x$ is just $1$ so that is the least complex option, so that will be $f(x)$. $g'(x)$ must then be $\cos x$ and the antiderivative of $\cos x$ is $\sin x$ so $g(x) = \sin x$. With this we can fill in the blanks:
$$\displaystyle \int x \cos x ~dx = x \sin x - \int 1 \sin x~dx$$

$$\displaystyle \int x \cos x ~dx = x \sin x - - \cos x + C$$

$$\displaystyle \int x \cos x ~dx = x \sin x + \cos x + C$$

##### Example for $\int \ln x~dx$

We are asked to solve the following integral:

$$\displaystyle \int \ln x ~dx$$

Not as obvious, right? Well, lets rewrite:

$$\displaystyle \int 1 \ln x ~dx$$

In this case, lets set $f(x) = \ln x$ and $g'(x) = 1$. Thus:

$$f'(x) = \frac{1}{x}$$

$$g(x) = x$$

Thus:

$$\displaystyle \int 1 \ln x ~dx = x\ln x - \int\frac{1}{x}x~dx$$

$$\displaystyle \int 1 \ln x ~dx = x\ln x - \int1~dx$$

$$\displaystyle \int 1 \ln x ~dx = x\ln x - x + c$$

##### *uv* notation
Most text books and tests will use $uv$ notation for integrating by parts. Here it is as follows:
$$\displaystyle \int u(x)v'(x) ~dx = u(x)v(x) - \int u'(x)v(x)~dx$$

Or more commonly:
$$\displaystyle \int u ~dv = uv - \int v~du$$

#### Integration with Partial Fractions
We are asked to integrate the following antiderivative:
$$\displaystyle \int \frac{x-5}{(2x-3)(x-1)}~dx$$

Our first inclination may be to use $u$-substitution somehow, but we can see that would be impossible as the derivative isn't anywhere in sight. So, to solve this we must use [**partial fractions:**](https://www.khanacademy.org/math/algebra-home/alg-rational-expr-eq-func/alg-partial-fraction/e/partial_fraction_expansion_1)

$$\frac{x-5}{(2x-3)(x-1)} = \frac{A}{2x-3} + \frac{B}{x-1}$$

The goal is to solve for A and B such that we can have two separate fractions that we can integrate:

$$\frac{A}{2x-3} + \frac{B}{x-1} = \frac{A(x-1)}{(2x-3)(x-1)} + \frac{B(2x-3)}{(2x-3)(x-1)}$$

We now have the same denominator, which means we can add these together:

$$\frac{A(x-1)}{(2x-3)(x-1)} + \frac{B(2x-3)}{(2x-3)(x-1)} = \frac{A(x-1)+B(2x-3)}{(2x-3)(x-1)} = \frac{Ax -A +2Bx-3B}{(2x-3)(x-1)}$$

Now collect the constants and $x$ terms:
$$\frac{Ax -A +2Bx-3B}{(2x-3)(x-1)} = \frac{(A+2B)x-(A+3B)}{(2x+3)(x-1)}$$

If we notice now, this is very similar to our original numerator, $x-5$, where $A+2B$ should add up to 1, and $A+3B$ should add up to 5. This calls for a system of equations:

$A+2B = 1$

$A +3B=5$

Then:

$-(A+2B)=-1$

$-A-2B=-1$

$-A-2B=-1$

$A+3B=5$

$B=4$

If you're confused about what happened up above [review this](https://www.khanacademy.org/test-prep/sat/x0a8c2e5f:untitled-652/x0a8c2e5f:heart-of-algebra-lessons-by-skill/a/gtp--sat-math--article--solving-system-of-linear-equations--lesson) as it goes over elimination of system of equations. With this we can solve for A:

$$A+3(4)=5$$

$$A+12=5$$

$$A=-7$$

So now, we can build our partial fraction:

$$\frac{x-5}{(2x-3)(x-1)} = \frac{-7}{2x-3} + \frac{4}{x-1}$$

So this is cool and it took forever, but we aren't even done sadly, we have to now integrate each fraction:

$$\displaystyle \int \frac{x-5}{(2x-3)(x-1)} ~dx= \int\frac{-7}{2x-3}~dx + \int \frac{4}{x-1}~dx$$

Integrating each section:

$$\displaystyle \int\frac{-7}{2x-3}~dx = -\frac{7}{2} \int \frac{2}{2x-3} = -\frac{7}{2} \ln|2x-3| + C$$

$$\displaystyle \int \frac{4}{x-1}~dx = 4 \int\frac{1}{x-1}~dx =4 \ln |x-1| + C$$

Finally, putting it all together:

$$\displaystyle \int \frac{x-5}{(2x-3)(x-1)} ~dx= \int\frac{-7}{2x-3}~dx + \int \frac{4}{x-1}~dx = -\frac{7}{2} \ln|2x-3|+ 4 \ln |x-1| + C$$

#### Integration with Synthetic Division

##### Example for $\int \frac{x-5}{-2x+2} ~dx$

We are asked to solve the following indefinite integral:
$$\displaystyle \int \frac{x-5}{-2x+2}~dx$$ 

How would we go about doing this? One way is to use Polynomial Division with Synthetic Division. Personally this is how I approach these problems, but another way is through Long Division. In our denominator, search for our $0$. In this case the zero for $-2x + 2$ is $x=1$. So we can setup our Synthetic Division:

$$\displaystyle \begin{array}[t]{c|}1\\\ \,\end{array}\enspace \begin{array}[t]{rr}1& {-5}& \\\ & 1& \\ \hline 1& -4& \end{array}$$

We have a remainder of $-4$, but as we can see we have a $1$ as a coefficient. Thing is, we are dividing by a coefficient of $-2$, so we have to include this with all of our coefficients (not remainder) so this comes out to be:

$$\displaystyle \frac{x-5}{-2x+2} = -\frac{1}{2}-\frac{4}{-2x+2}= \frac{2}{x-1}-\frac{1}{2}$$

This leads us to the following:
$$\displaystyle \int \frac{x-5}{-2x+2}~dx = \int \left(\frac{2}{x-1}-\frac{1}{2}\right) ~dx$$

Thus we can just solve our new easier to understand integral:
$$\displaystyle \int \left(\frac{2}{x-1}-\frac{1}{2}\right) ~dx = \int \frac{2}{x-1}~dx - \int \frac{1}{2}~dx$$

$$2\displaystyle \int \frac{1}{x-1}~dx - \frac{1}{2}x + C$$

$$\displaystyle 2 \int \frac{1}{u}~du - \frac{1}{2}x + C$$

$$\displaystyle 2 \ln |u| - \frac{1}{2}x + C$$

$$\displaystyle 2 \ln |x-1| - \frac{1}{2}x + C$$

##### Example for $\int \frac{2x^3+1}{x-3}~dx$

Given:
$$\displaystyle \int \frac{2x^3+1}{x-3}~dx$$

Synthetic Division:
Zero for $x-3$ is $3$

$$\displaystyle \begin{array}[t]{c|}3\\\ \,\end{array}\enspace \begin{array}[t]{rrrr}2& 0& 0& {1}& \\\ & 6& 18& 54& \\ \hline 2& 6& 18& 55& \end{array}$$

Thus:

$$\displaystyle \frac{2x^3+1}{x-3} = 2x^2 + 6x + 18 + \frac{55}{x-3}$$

$$\displaystyle \int \frac{2x^3+1}{x-3}~dx = \int \left(2x^2 + 6x + 18 + \frac{55}{x-3}\right)dx$$

$$\displaystyle \int \left(2x^2 + 6x + 18 + \frac{55}{x-3} \right)dx = \int(2x^2)~dx+\int(6x)~dx+\int(18)~dx+\int(\frac{55}{x-3})~dx$$

$$\displaystyle \frac{2x^3}{3}+3x^2+18x+ C+ 55\int(\frac{1}{u})~du$$

$$\displaystyle \frac{2x^3}{3}+3x^2+18x+55 \ln{|u|}+C$$

$$\displaystyle \frac{2x^3}{3}+3x^2+18x+55 \ln{|x-3|}+C$$

#### Integration by Completing the Square

##### Example for $\int \frac{16}{\sqrt{12-x^2+4x}}~dx$

We are asked to solve the following integral:

$$\displaystyle \int \frac{16}{\sqrt{12-x^2+4x}}~dx$$

A rather complicated integral to say the least. Harder still when you realize that it is encapsulated by $\frac{1}{\sqrt{x}}$. How would we go about solving this? Well one way is by completing the square, first we are going to focus on the denominator:

$$\displaystyle \sqrt{12-x^2+4x}=\sqrt{-x^2+4x+12}$$

Now, group the terms to setup completing the square:

$\displaystyle \sqrt{(-x^2+4x+\_) +12-\_}$$

Where we are solving for the placeholder $\_$. Next, we eliminate the negative on $x^2$:
$$\displaystyle \sqrt{-(x^2-4x+\_) +12-\_}$$

Then, we can figure out our placeholder by using the following equation:
$\displaystyle \_ = \frac{b}{2}^2$

Where $b$ is the coefficient of $x$:
$$\displaystyle \frac{-4}{2}^2 = 4$$

$$\displaystyle \sqrt{-(x^2-4x+4) +12-(-4)}$$

$$\displaystyle \sqrt{-(x^2-4x+4) +16}$$

You may be wondering why we added by positive $4$ in the parenthesis and subtracted $12$ by $-4$. This is because we are multiplying the inside of the parenthesis by negative $1$ so it is important we account for this outside of the parenthesis. Now we just factor:

$$\displaystyle \sqrt{-((x-2)^2) +16}$$

$$\displaystyle \sqrt{16 - (x-2)^2}$$

Neat, so now we have:

$$\displaystyle \int \frac{16}{\sqrt{16 - (x-2)^2}}~dx$$

Focusing on the numerator now, let's simplify that to 1:

$$\displaystyle 16 \int \frac{1}{\sqrt{16 - (x-2)^2}}~dx$$

We are now left with a form that looks very similar to the derivative of $\sin^{-1}x$, and I will demonstrate the power of completing the square here to show this:

$$\displaystyle 16 \int \frac{1}{\sqrt{4^2 - (x-2)^2}}~dx$$

$$\displaystyle 16 \times 4 \int \left[\frac{1}{4\sqrt{\frac{4^2}{4^2} - \frac{(x-2)^2}{4^2}}}\right]~dx$$

$$\displaystyle 16 \int \frac{1}{\sqrt{1 - (\frac{(x-2)}{4})^2}}~dx$$

We have now just gotten into the form for the derivative of $\sin^{-1}x$ where $x=(\frac{x-2}{4})$, thus:

$$\displaystyle \int \frac{16}{\sqrt{12-x^2+4x}}~dx = 16 \int \frac{1}{\sqrt{1 - (\frac{(x-2)}{4})^2}}~dx = 16\sin^{-1}(\frac{x-2}{4})+C$$

### Improper Integrals

An Improper Integral are definite integrals that cover an area that is unbounded. There are two types of improper integrals, one where at least one of the endpoints is extended to infinity, such as $\int_1^\infin \frac{1}{x^2}~dx$. The other type of improper integral are integrals whose endpoints are finite but the integrated function is not bound at one or both endpoints, such as $\int_0^1 \frac{1}{\sqrt{x}}~dx$. In both cases, these integrals can be expressed with limits, which we will explore in the following two sections. When a limit exists we say that the integral is **convergent,** otherwise it is **divergent.**

#### Infinite Endpoints

##### Example for $\int_1^\infin \frac{1}{x^2}~dx$

In our previous example, we expressed the following improper integral:
$$\displaystyle \int_1^\infin \frac{1}{x^2}~dx$$

We can view this integral as:
$$\displaystyle \int_1^\infin \frac{1}{x^2}~dx = \lim_{b \rightarrow \infin} \int_1^b x^{-2}~dx$$

From here, we can utilize the fundamental theorem of calculus and express this integral with indefinite integrals:
$$\displaystyle \int_1^b x^{-2}~dx = \left[\frac{x^{-1}}{-1}\right]_1^b = \left[-\frac{1}{x}\right]_1^b$$

Solving this:
$$\displaystyle \left[-\frac{1}{x}\right]_1^b = -\frac{1}{b}-(-\frac{1}{1})= 1-\frac{1}{b}$$

So, we have determined the form of this integral so now we can find the limit:
$$\displaystyle \lim_{b \rightarrow \infin} \int_1^b x^{-2}~dx = \lim_{b \rightarrow \infin} 1-\frac{1}{b} = 1-0 =1$$

$\displaystyle \int_1^\infin \frac{1}{x^2}~dx$ is convergent.

##### Example for $\int_1^\infin \frac{1}{x} ~dx$

$\displaystyle \int_1^\infin \frac{1}{x} ~dx$

$\displaystyle \int_1^\infin \frac{1}{x} ~dx = \lim_{b \rightarrow \infin} \int_1^b \frac{1}{x}~dx$

$\displaystyle \lim_{b \rightarrow \infin} \int_1^b \frac{1}{x}~dx = \lim_{b \rightarrow \infin} \left[\ln x\right]_1^b$

$\displaystyle \lim_{b \rightarrow \infin} \left[\ln x\right]\_1^b = \lim_{b \rightarrow \infin} (\ln b - \ln 1) = \lim_{b \rightarrow \infin} \ln b = \infin$

$\displaystyle \lim_{b \rightarrow \infin} \int_1^b \frac{1}{x}~dx = \infin$

$\displaystyle \int_1^\infin \frac{1}{x} ~dx$ is divergent.

#### Finite Endpoints

##### Example for $\int_0^1 \frac{1}{\sqrt{x}}~dx$

In our previous example, we expressed the following improper integral:
$$\displaystyle \int_0^1 \frac{1}{\sqrt{x}}~dx$$

We can view this integral as:
$$\displaystyle \lim_{a \rightarrow 0} \int_a^1  \frac{1}{\sqrt{x}}~dx = \displaystyle \int_0^1 \frac{1}{\sqrt{x}}~dx$$

From here, we can utilize the fundamental theorem of calculus and express this integral with indefinite integrals:
$$\displaystyle \int_a^1  \frac{1}{\sqrt{x}}~dx = \left[ \frac{x^\frac{1}{2}}{\frac{1}{2}}\right]^1_a = \left[2 \sqrt x\right]^1_a$$

Solving this:
$$\displaystyle \left[2 \sqrt x\right]^1_a = 2\sqrt{1} - 2\sqrt a = 2 - 2 \sqrt a$$

So, we have determined the form of this integral so now we can find the limit:
$$\displaystyle \lim_{a \rightarrow 0} \int_a^1  \frac{1}{\sqrt{x}}~dx = \lim_{a \rightarrow 0}(2-2\sqrt a) = 2-2 \times 0 = 2$$

$\displaystyle \int_0^1 \frac{1}{\sqrt{x}}~dx$ is convergent.
