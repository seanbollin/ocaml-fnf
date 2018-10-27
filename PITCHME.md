![OCaml](http://connachtspringshow.com/wp-content/uploads/2018/04/camel-945x627.jpg
 "OCaml")

---

# Functions

let sum a b = a +. b;;

val sum : float -> float -> float = <fun>

let sum a b = a + b;;

val sum : int -> int -> int = <fun>

---

# Higher-Order Functions & Currying

let plus_two = sum 2;;

val plus_two : int -> int = <fun>

plus_two 3;;

int = 5

