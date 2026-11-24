# Environments and the Toy Evaluator

We traced this form through our eval-expr: 

(let ((x 2)) (let ((f (lambda (y) (+ x y)))) (let ((x 100)) (f 1))))

The lambda branch of eval-expr, (make-closure (second expr) (third expr) env), captures the defining environment, the one the lambda was written in. When the lambda is evaluated, env is ((x . 2)), because only the outer let has run. make-closure stores that as the fourth item of (:closure (y) (+ x y) ((x . 2))). The other branches use env only to evaluate, but this line stores env inside the closure for later use.

Our apply-closure builds its environment with (extend-env c_params args c_env), where c_env is the saved fourth item. At the call (f 1), the caller's env is ((x . 100) (f . closure) (x . 2)), where closure is the (:closure ...) list for f. We use it only to find f and evaluate the argument 1. apply-closure never uses the (x . 100). The body sees ((y . 1) (x . 2)) and returns 3. If we extended the caller's env instead, the body would see x as 100 and return 101. That would make the language dynamically scoped, because a free variable would be resolved where the function is called, not where it was written. Ours is lexically scoped because make-closure saves the environment and apply-closure uses that saved one.

CLISP is a Lisp-2, so variables and functions live in separate namespaces. Writing (f 1) makes CLISP look for a function named f, not the closure in the variable f, so we must write (funcall f 1). Passing a function by name also needs #', as in our (mapcar #'cons params args). The toy language is a Lisp-1. In the last branch of eval-expr, (eval-expr (first expr) env) evaluates the operator position like any other expression, so f goes through lookup in the same environment as variables and returns the closure. apply-closure then runs it. No funcall is needed because there is no second namespace to cross.

Together these show that one saved environment in the closure, plus one shared namespace, is all our evaluator need for functions with lexical scope.