[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/OlW38W4k)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

## Answer
The recurrence relation that I derived is: 

$$\begin{equation}T(n)=\begin{cases}1, & \text{if $n<=1$} \\
3T(\frac{n}{3})+n^5+C, & \text{if $n>1$}.\end{cases}\end{equation}$$

Solving this relation using substitution:

$T(n)=3T(\frac{n}{3})+n^5+C$

$=3[3T(\frac{n}{9})+(\frac{n}{3})^5+C]+n^5+C$

$=9T(\frac{n}{9})+3(\frac{n}{3})^5+3C+n^5+C$

$=9T(\frac{n}{9})+3(\frac{n}{3})^5+n^5+3C+C$

$=3^kT(\frac{n}{3^k})+\sum\limits_{i=0}^{k-1} 3^i(\frac{n}{3^i}) +\sum\limits_{i=0}^{k-1} 3^iC$

$=3^kT(\frac{n}{3^k})+\sum\limits_{i=0}^{k-1} \frac{n^5}{3^{4i}} +C\sum\limits_{i=0}^{k-1} 3^i$

$=3^kT(\frac{n}{3^k})+n^5\cdot \frac{1-3^{-4k}}{1-3^{-4}} + C\cdot \frac{1-3^k}{3-1}$

The base case is encountered when $\frac{n}{3^k} \le 1 \Rightarrow 3^k \ge n \Rightarrow k \ge \log_3 n$

For $k=\log_3 n$ :

$3^{\log_3 n}T(\frac{n}{3^{\log_3 n}})+n^5 \cdot (1-\frac{1}{n^4})+ C \cdot \frac{1-3^{log_3 n}}{2}$

$=nT(1)+n^5+C(\frac{1-n}{2})$

Highest order term:

$=n^5\in O(n^5)$

Sources: Google was used to find the relevant formula for the geometric series.







