![OCaml](http://connachtspringshow.com/wp-content/uploads/2018/04/camel-945x627.jpg
 "OCaml")

---

### Programming language ML and the Hindley-Milner type system

<p>ML influenced Clojure, Coq, Cyclone, C++, Elm, F#, F*, Haskell, Idris, Miranda, Nemerle, OCaml, Opa, Erlang, Rust, Scala.</p>

<p>From Wikipedia:</p>

<p>"Among HM's more notable properties are its completeness and its ability to infer the most general type of a given program without programmer-supplied type annotations or other hints. Algorithm W is an efficient type inference method that performs in almost linear time with respect to the size of the source, making it practically useful to type large programs."</p>

<p>Compiles to native code or byte code that can be interpreted.</p>

---

### Functions

```ocaml
let sum a b = a +. b;;

val sum : float -> float -> float = <fun>

let sum a b = a + b;;

val sum : int -> int -> int = <fun>
```

OCaml is a strongly statically typed language that uses type inference to work out types so you don't have to.

OCaml does not do any implicit casting.

---

### Higher-Order Functions & Currying

```ocaml
let plus_two = sum 2;;

val plus_two : int -> int = <fun>

plus_two 3;;

int = 5
```

---

### Lists and Pattern-matching

```ocaml
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

let rec fib x = if x <= 1 then 1 else fib (x - 1) + fib (x - 2);;

```

Exhaustivity checker - try removing the empty case.

---

### Records

```ocaml
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
```

---

### Modules

```ocaml
module Hello : sig
 val hello : unit -> unit
end = 
struct
  let message = "Hello"
  let hello () = print_endline message
end
  
(* At this point, Hello.message is not accessible anymore. *)
let goodbye () = print_endline "Goodbye"
let hello_goodbye () =
  Hello.hello ();
  goodbye ()

Common example in the stand library of a module is the List module:

List.fold_left
List.fold_right
```

https://caml.inria.fr/pub/docs/manual-ocaml/libref/List.html

---

### Functors

Modules that are parameterized by other modules.

```ocaml
module Int_set = Set.Make (struct
                              type t = int
                              let compare = compare
                            end);;
```

---

### Binary Trees

```ocaml
(* Binary tree with leaves car­rying an integer. *)
(* Algebraic types are a kind of composite type *)

type tree = Leaf of int | Node of tree * tree

let rec exists_leaf test tree =
  match tree with
  | Leaf v -> test v
  | Node (left, right) ->
      exists_leaf test left
      || exists_leaf test right

let has_even_leaf tree =
  exists_leaf (fun n -> n mod 2 = 0) tree
```

---

### ReasonML

https://reasonml.github.io/

```ocaml

type schoolPerson = Teacher | Director | Student(string);

let greeting = person =>
  switch (person) {
  | Teacher => "Hey Professor!"
  | Director => "Hello Director."
  | Student("Richard") => "Still here Ricky?"
  | Student(anyOtherName) => "Hey, " ++ anyOtherName ++ "."
  };
```

---

### ReasonReact

https://reasonml.github.io/reason-react/

```ocaml
let component = ReasonReact.statelessComponent("Greeting");

let make = (~name, _children) => {
  ...component,
  render: _self =>
    <button>
      {ReasonReact.string("Hello!")}
    </button>
};
```