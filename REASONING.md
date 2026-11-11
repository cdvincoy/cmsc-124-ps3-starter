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
`(and 1 nil 3)` heads with `and`, which evaluates its arguments left to right and stops at the first `nil` and returns `nil`. The kind then becomes `null` and the length is `0`. The operator is `special-operator` because of `and` even though it is also a macro, because special operator is asked first.

## P10
This case heads with `progn`, a special operator that evaluates in order and returns the last one, so the operator is `special-operator`. The `defvar` makes `*ps3-rate*` special, so the `let` rebinding it to `10` is seen by `ps3-scale` when it runs, giving `3*10`, which is `30`. That is an `integer`, so the kind is `integer` and the length is `none`. 

## P11
This case heads with `defun`, which is a macro, so the operator is `macro`. A definition hands back the symbol it defines, so the value is `ps3-twice`. The kind is `symbol` and the length is `none`.

## P12
This case heads with `labels`, which is a special operator that defines a local function and can call itself, so the operator is `special-operator`. `(down 3)` calls `down` with 3, 2, 1 and 0, building `(cons 3 (cons 2 (cons 1 '())))`, so the value is the list `(3 2 1)`. A non-empty list is a chain of cons cells, so the kind is `cons` and the length is `3`.  

## P13
`(mapcar #'length '((1 2) () (3)))` heads with `mapcar` which is a function, so the operator is `function`. `mapcar` applies a function to every element, which is `#'length` in this case, giving it a resulting value of 2, 0, and 1 `(2 0 1)`. A non-empty list is a cons, so the kind is `cons` and the length is `3`.

## P14
This case heads with `mapcar`, which is a function, so the operator is `function`. `mapcar` calls the lambda with each element as `n`, squaring 1, 2, and 3 which results to `(1 4 9)`. A non-empty list is a cons, so the kind is `cons` and the length is `3`.

## P15
`(lambda (n) (* n 2))` heads with `lambda`, which is a macro, so the operator is `macro`.  Since it is a lambda, it returns the function itself, so the value is `#<function>`. The kind is `function` and the length is `none`.

## P16
This case heads with `let`, which is a special operator that runs the initializers first, binds the variable, and only evaluates the body. There is no defvar for factor, so it uses the `factor 2` and `f` does not see the `factor 10`, which gives `3*2`, and the value is `6`. The kind is `integer`, the length is `none`, and the operator is `special-operator`.
