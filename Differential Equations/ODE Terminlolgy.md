# ODE Terminology
## Variables
- The **independant** variable is the value that is changed in the function
- The **dependant** is the variable whose value depends on that of the independant variables
- $$\begin{align}\dv {\color{lightblue} y} {\color{orange} x} = x^2 + y \\ \color{orange} {x \text{ is the independant variable}} \\ \color{lightblue} {y \text{ is the dependant variable}}\end{align}$$
## Order
- The **order** of a DE is the highest nth derivative in the equation
## Linear vs Non Linear
- A **Linear** DE is one where the dependant variable or a derivative of the dependant variable, is only ever to the power 1 or 0, so each term is allowed to be in the form $a f \left( x \right) y^{(n)}$ or $a f \left( x \right)$
- A **Non Linear** DE has at least 1 term where $y$ or a derivative of $y$ is raised to some power that is not $0$ or $1$, or a function is applied to $y$
## Homogenous
- A DE in which every term involves the dependant variable
- Every non homogenous DE has a homogenous DE associated with it
- It can be formed by removing all terms that dont contain the independant variable
## Solving
- To solve a DE, you must find $y$ in terms of $x$
- Since solving a DE is in effect integration (anti derivative), the solution will have arbitrary constants
- The soltion containing all arbitrary constants is the general solution
- To find a **particular solution**, **initial conditions** (values of $y, \dv{y}{x}, \cdots$, at some value of $x$) can be used
- Or **boundary conditions** (values of $y, \dv{y}{x}, \cdots$, at several values of $x$)
- The value of each constant can be determined using simultaneous equations
- Any solution to a DE is called a **particular integral**
- the solution to the associated homogenous DE is the **complimentary function**, which can be used to resolve the arbitrary constants