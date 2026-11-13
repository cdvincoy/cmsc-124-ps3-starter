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
Replace this line with the rule behind this case's four fields.

## P10
Replace this line with the rule behind this case's four fields.

## P11
Replace this line with the rule behind this case's four fields.

## P12
Replace this line with the rule behind this case's four fields.  

## P13
Replace this line with the rule behind this case's four fields.

## P14
Replace this line with the rule behind this case's four fields.

## P15
Replace this line with the rule behind this case's four fields.

## P16
Replace this line with the rule behind this case's four fields.