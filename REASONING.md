# Reasoning for the Predictions Table

Write one entry under every heading below, then commit this file together with
`predictions.tsv`, before you run a case or open `tests/expected.tsv`.

Each entry names the rule that produces the four predicted fields for that
case. One to three sentences is enough. The grader checks structure only. It
does not judge quality, and it sets no word minimum.

After you run the cases, add a short correction under each case you predicted
wrongly. Say what you predicted, what CLISP printed, and which rule you
misread. Those entries belong in the correction commits.

## P01
`(+ 1 (* 2 3))` heads with the function `+`, which evaluates all its arguments first. The inner `(* 2 3)` becomes `6`, then `+` gives `7`. That is an `integer`, and the length is `none` and the operator is `function`.

## P02
`'(+ 1 2)` heads with `quote`, a special operator that returns its argument unevaluated, so `+` is never called and the result is the list `(+ 1 2)`. A non-empty list is a cons, so the kind is `cons` and its length is `3`, with operator `special-operator`.  

## P03
The form `nil` evaluates to itself, so the value is `nil`. It is an empty list, so the kind is `null`, rather than cons or symbol. It has a length of `0` and the operator is `none`, since the form is an atom with no head. 

## P04
The form `t` is a symbol whose binding is itself, so the value is `t`. It is an atom and not `nil`, so the kind is `symbol` rather than `null` or `cons`. It is not a list or a string, so the length is `none` and the operator is `none` since the form is an atom with no head. 

## P05
The form `(symbolp nil)` checks if `nil` is a symbol, so the value is `t` because it answers true. The value `t` is a symbol, so the kind is `symbol` and the length is `none`. The operator is `function` because the head is `symbolp` which is an ordinary function that evaluates its argument first before it runs.

## P06
`(car '())` heads with the function `car`. The quote hands `car` the empty list unevaluated, and it returns the value `nil`. Since the value is `nil`, the kind is `null`, and the length is 0, and the operator is `function` because `car` is a function.

## P07
`(cons 1 '(2 3))` heads with the function `cons`, which evaluates both arguments and builds one new cell with `1` and `(2 3)`. The result is a chain of cells, so the kind is `cons` and the length is `3`. The operator is `function` because `cons` is a function, not a special operator or macro.

## P08
`(if (null '()) 'empty 'full)` heads with `if`, a special operator that evaluates the test first and then only evaluates the chosen branch. The test `(null '())` answers `t`, so the first branch `'empty` is evaluated, and the quote makes the value the symbol `empty`. So the kind is `symbol` and the length is `none`, and the operator is `special-operator` because of `if`.

## P09
`and` is the main operator, which is a special operator, evaluating three arguments: 1, nil and 3. According to the LISP documentation, `and` automatically returns nil upon reading any element that evaluates to nil. The second argument is nil, thus it evaluates to nil.

## P10
`progn` is a special operator that evaluates the argument statements in sequence. The first line defines *ps3-rate\* as 2, the second line defines ps3-scale as a function that multiplies an argument n by the value of *ps3-rate\*. The final line sets *ps3-rate\* to 10, overriding the previous value of 2, and then runs ps3-scale with n=3, giving us 3 times 10: the integer 30. `progn` always returns the output of the final statement.

## P11
`defun` is the main operation, which is a macro that returns a defined function object. We define ps3-twice as having a parameter n and returning n times 2, but those aren't reflected in the actual output, since the output only prints the function name preceded by a #.

## P12
According to the docs, `labels` is a special operator that acts similarly to `flet`, in that it defines functions that are local to the block and executes the following form sequentially similar to `progn`. However, `labels` also allows the functions to call themselves, which is shown here. `down(n)` is defined as a recursive function that creates a cons out of the current n + `down(n-1)`, with a base case of `down(0)` returning an empty cons. The following form calls `down(3)` which expands into a cons with elements 3, 2 and 1, and thus a length of 3.

## P13
`mapcar` applies a function to each element of a cons, and returns the resulting outputs as another cons. the syntax `#'` indicates to use the existing length function to evaluate the second argument. (1 2) is length 2, () is length 0, and (3) is length 1; therefore, the result is a cons of all the lengths: (2,0,3) which is obviously of length 3.

## P14
This time, the `mapcar` uses an anonymous lambda that accepts an argument n and returns its square. Applying this to (1 2 3), we call the lambda for each element and set n to the current element. The resulting output is (1 4 9), which is a cons of length 3.

## P15
`lambda` is a macro that defines an anonymous function. But since we never call this lambda, the output of this when printed simply returns an anonymous function object, which has no length.

## P16
As per the docs, `let` executes a series of forms using specified bindings. In this case, the outermost let sets `factor` to 2 and then executes the middle let. The middle let sets `f` to a lambda that multiplies an argument n with the factor value, then executes the innermost let as its form. The innermost let changes the binding of factor to 10 (the more local bindings override less local bindings), and then calls the lambda with n=3. This results in integer 30, which obviously has no length.