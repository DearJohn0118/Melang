### Function

Function is used to encapsulate a series of calculations and algorithms.

There are two mode:

- function definition
- function call



#### Definition

Syntax:

```
@funcname (parameters) {
  ...//statements
}
```

*funcname* is the name of function, it has to follow the rule:

> start with letter or underscore and the rest part can be number, letter or underscore.

*parameters* is a series of variables, like: *name*, *age* or anything you need.

e.g.

```
@plus(a, b)
{
  return a+b;
}
```

Here is a function named *plus*. It has two parameters named *a* and *b*. And its function is to calculate the sum of two parameters.



#### Call

Syntax:

```
@funcname(arguments);
```

*funcname* is the name of defined function.

*arguments* is a series of values.

e.g.

```
@plus(1, 2);
```

*plus* is the *funcname*, and 1, 2 correspond to parameter *a* and *b*.



#### Reference

Let's see an example at first.

```
@foo(data)
{
  return data + 100;
}

a = 0;
a = foo(a);
```

This program just modified *a* from 0 to 100, and that is what we wish it to be.

But the last statement is a little bit clumsy. How to make it better?

```
@foo(&data)
{
  data += 100;
}

a = 0;
foo(a);
```

We change function parameter *data* to be *&data*.

Operator *&* makes argument *a* to be a reference variable named *data* in function *foo*. Every modification on *data* will directly effect on *a*.

> Note. & only can be used on the parameters of function definition.



#### Lack of arguments

```
@foo(data)
{
  @mln_print(data);
}

@foo();
```

This program will not report error. Because interperter will set *nil* to *data* automatically.



#### Return function

Let's see an example:

```
@foo() {
  @bar() {
    @mln_print('bar');
  }
  return bar;
}

@foo()();
```

Guess what happened?

'bar' will be printed on terminal.

It is possible because function definition is a statement. So we can define a function in another function's definition.



#### Variable arguments

In most programming languages, they all support variable arguments, so does in Melang.

```
@log()
{
  s = 'argument list: ';
  for (i = 0; i < @mln_size(args); ++i) {
      s += args[i] + ' ';
  }
  @mln_print(s);
}

@log('this', 'is', 'a', 'variable', 'arguments', 'example');
```

The result of this program is:

```
argument list: this is a variable arguments example 
```

The key point is variable *args*. It's a internal variable in Melang function.

It is an array to record every arguments passed to this function.

> Function *mln_size* returns the number of array elements.