[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=12596842&assignment_repo_type=AssignmentRepo)
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

Letting n = \log_3(n), the solution becomes:

$\Rightarrow T(n) = 3^4T\left(\frac{n}{3^4}\right) + \left(\frac{n^5}{3^{12}}\right) + \left(\frac{n^5}{3^8}\right) + \left(\frac{n^5}{3^4}\right) + n^5$

Can be written in the form of a geometric series:

- $\sum_{i=0}^n (\left(a)^i\right) = \frac{a^{n+1} - 1}{a-1}$

$\Rightarrow T(n) =  3^iT\left(\frac{n}{3^i}\right) + \sum_{i=0}^{\log_3(n)} \frac{n^5}{3^{4i}}$

## Asymtotic Complexity 

$O(n^5)$
