### This is a reddit post I made to simplify pointers for people who haven't used pointers before. It is a *compendium* clarifying a lot of pointer operations.

--

I think the & and \* are confusing because whenever people are talking about those *operators*, they use terminology without explaining the terminology and how the positions of the symbols matters. For instance, what does `var p *int` even mean to someone who doesn't know how memory is allocated in a program? It should really be explained step by step in the simplest way possible, so I'll try with some examples. Lets start with:

`var p *int`   : this means that variable p *is* a pointer *to* a value of the datatype int. 

`a := p`   : this would initialize a variable called "a" that is a pointer *of* the same value as p *to* a value of datatype int. So pointers are values in this way and they hold the *memory address* of whatever value they're referencing. "a" and "p" would be two variables in two *different* address spaces but would *hold* that same value. Every new variable you create has its own address space. If you want to refer to a variable using only one address space, don't declare any new variables!

`*p`   : this is very different from (var p \*int) because notice the position of the (\*) and *this is simply syntax*. In fact, it's confusing because this is *not* a pointer. It's called *dereferencing* (because pointers *reference*) and it gets that value of datatype int instead of returning the address which would just be plain "p". In this case, the output would be <nil> because we haven't pointed "p" to anything.

`&p`   : this tells you the memory address of the variable "p" that was instantiated in this program.

`*p = 1`   : this would *throw an error* because "p" is not pointing to anything so you can't set the value of a nonexistent variable to a value. So instead declare a variable of int value first and then point p to it. `z := 1` then, `p = &z`. Then you can change the value of "z" through "p" like `*p = 2` then "z" will equal 2.

`b := *p`   : this would be how you *get* (rather than *set*) the value of datatype int that p is pointing to. (\*p) is the value that is at the address value "p". Again, (\*p) is *not* a pointer and neither is "b". They are the values *of* the pointer "p" (which is an instantiated variable), in this case "z".

`c := &b` : this would initialize a variable "c" that *gets* the *memory address* of the value "b" (or the value in \*p but at a different memory address since "b" and \*p are distinct) and this *is* a pointer because the value that "c" holds is a *memory address*. &b is *not* a pointer, the variable "c" is the pointer. Remember to distinguish *operations* from *variables* and *values*, which are all different things.

***

`c := &b (==) c:= &(*p)` is **false**

it should be false because b is holding the same value as \*p but in different address

`c:= &(*p) (==) c:= p` is **true**

This should be true and correct because dereferencing and referencing gives you same pointer

`c := &b (==) c:= p` is **false**

it should be false because b's pointer is pointing to b's address which is different than z's address

****

`d := &c`   : d is a pointer *of* a pointer. It holds the memory location of the variable c which holds the memory location of "b" which is a value of datatype int. 

`e := &(&c)`   : this would *throw an error* because &c *isn't* a variable with a memory address so you can't get an address for it. Remember that "d" and "&c" are two *different* things. `e := &(d)` would work just fine because "d" has an address somewhere because it was initialized in the program.

`f := *(&c)`   : "f" would be the value of the address space of the pointer "b". Why is that? (&c) gets you the address for "c" and "c" is a pointer to "b" from `c := &b`, and *not* `c:= &(*p)` since (\*p) is an operation and not a variable. That means if we deference (&c) we get the value in the address space *of* "c" which is the address for "b" `c := &b`.
