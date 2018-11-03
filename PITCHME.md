![OCaml](http://connachtspringshow.com/wp-content/uploads/2018/04/camel-945x627.jpg
 "OCaml")

# Programming language ML and the Hindley-Milner type system

ML influenced Clojure, Coq, Cyclone, C++, Elm, F#, F*, Haskell, Idris, Miranda, Nemerle, OCaml, Opa, Erlang, Rust, Scala.

From Wikipedia:

"Among HM's more notable properties are its completeness and its ability to infer the most general type of a given program without programmer-supplied type annotations or other hints. Algorithm W is an efficient type inference method that performs in almost linear time with respect to the size of the source, making it practically useful to type large programs."

---

# Functions

let sum a b = a +. b;;

val sum : float -> float -> float = <fun>

let sum a b = a + b;;

val sum : int -> int -> int = <fun>

OCaml is a strongly statically typed language that uses type inference to work out types so you don't have to.

OCaml does not do any implicit casting.

---

# Higher-Order Functions & Currying

let plus_two = sum 2;;

val plus_two : int -> int = <fun>

plus_two 3;;

int = 5

# Lists and Pattern-matching

let numbers = [1; 2; 3; 4; 5; 6; 7; 8; 9; 10];;

val numbers : int list = [1; 2; 3; 4; 5; 6; 7; 8; 9; 10]

let is_odd n = 
  let result = n mod 2 in
  result = 1;;

val is_odd : int -> bool = <fun>

let rec odds l =
  match l with
  | [] -> []
  | h :: t -> 
      if is_odd h then
        h :: odds t
      else
        odds t;;

# Records

type connection =
  { protocol         : string;
    source_ip        : string;
    source_port      : int;
    destination_ip   : string;
    destination_port : int;
  };;

let my_connection = 
  { protocol = "tcp"; 
    source_ip = "1.2.3.4"; 
    source_port = 4832; 
    destination_ip = "4.3.2.1"; 
    destination_port = 80 
  };;