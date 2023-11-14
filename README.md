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

## Recursive Procedure Analysis

The recursive procedure can be analyzed as follows:

- $3\left(3T\left(\frac{n}{9}\right) + \left(\frac{n}{3}\right)^5\right) = 9T\left(\frac{n}{9}\right) + \left(\frac{n^5}{3^4}\right) + n^5$
- $9\left(3T\left(\frac{n}{27}\right) + \left(\frac{n}{9}\right)^5\right) = 27T\left(\frac{n}{27}\right) + \left(\frac{n^5}{9^4}\right) + \left(\frac{n^5}{3^4}\right) + n^5$
- $27\left(3T\left(\frac{n}{81}\right) + \left(\frac{n}{27}\right)^5\right) = 81T\left(\frac{n}{81}\right) + \left(\frac{n^5}{27^4}\right) + \left(\frac{n^5}{9^4}\right) + \left(\frac{n^5}{3^4}\right) + n^5$


$\Rightarrow 3^4T\left(\frac{n}{3^4}\right) + \left(\frac{n^5}{3^{12}}\right) + \left(\frac{n^5}{3^8}\right) + \left(\frac{n^5}{3^4}\right) + n^5$

Letting \$n = \log_3(n)$, the solution becomes:

$\Rightarrow T(n) = 3^4T\left(\frac{n}{3^4}\right) + \left(\frac{n^5}{3^{12}}\right) + \left(\frac{n^5}{3^8}\right) + \left(\frac{n^5}{3^4}\right) + n^5$

Can be written in the form of a geometric series:

- $\sum_{i=0}^n (a)^i = \frac{a^{n+1} - 1}{a-1}$

$\Rightarrow T(n) =  3^iT\left(\frac{n}{3^i}\right) + \sum_{i=0}^{\log_3(n)} \left(\frac{n^5}{3^{4i}}\right)$

- $3^{lon_3(n)}T(1) + \sum_{i=0}^{\log_3(n)} \left(\frac{n^5}{3^{4i}}\right)$

- $\ T(n) = n + n^{5}\sum_{i=0}^{\log_3(n)}\left(\frac{1}{3^{4i}}\right)$

- $\ T(n) = n + n^{5}\sum_{i=0}^{\log_3(n)}\left(\frac{1}{3^{4}}\right)^{i}$

- $\ a = \left(\frac{1}{3^{4}}\right)$

- $\ n = log_3\left(9n\right)$

This give us:

- $\sum_{i=0}^{\log_3(n)}\left(\frac{1}{3^4}\right)^i = \frac{\left(\frac{1}{3^4}\right)^{\log_3(n+1)} - 1}{\frac{1}{3^4} - 1} $

- $\frac{\left(\left(\frac{1}{3^4}\right)^{\log_3(n)} \cdot \frac{1}{3^4}\right) - 1}{\frac{1}{3^4} - 1}$

- $\frac{\left(\left(3^{-4}\right)^{\log_3(n)} * 3^{-4}\right) - 1}{\frac{1}{3^4} - 1} $

- $\frac{\left(n^{-4} * 3^{-4}\right) - 1}{\frac{1}{3^4} - 1} $

- $\frac{(n^{-4}\left(\frac{1}{81}\right) - 1}{\frac{1}{81} - 1} $

Now we can multiple this fraction by the $\left(n\right)^{5} coefficient from: $T(n) = n + n^{5}\sum_{i=0}^{\log_3(n)}\left(\frac{1}{3^{4}}\right)^{i}$:

- $\frac{\frac{1}{81}n - n^{5}}{\frac{1}{81}-1}$

- $\frac{\frac{1}{81}n - n^{5}}{\frac{-80}{81}-1}$

  Now we take the sigma part of the equation and plug it back into the T(n) equation:

- $\ T(n) = n + \frac{\frac{1}{81}n - n^{5}}{\frac{-80}{81}-1}$

- $\ T(n) = n + \left(\frac{-n}{80}\right) - \frac{81}{80}n^{5}$


## Asymtotic Complexity 

$O(n^5)$
