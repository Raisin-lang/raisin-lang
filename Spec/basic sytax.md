# WARNING: NONE OF THIS IS SET IN STONE, EVERYTHING CAN AND WILL CHANGE. MANY TIMES.

# Variables

## Declaration
```C
x:int // varName:T
```

## Assignment
```C
x = 5 // varName = (value), varName must be declared prior
```

## Declaration with assignment
```C
x:int = 5 // varName:T = (value)
```

# Functions

## Function with parameters and return type
```C
addTwo:int = x:int, y:int => (
    x + y
)

/*
    fnName:T = arg1:T, arg2T => (
        <fn body>
    )
*/
```

## Function with no parameters and return type
```C
addTwo:int => (
    5 + 2
)

/*
    fnName:T => (
        <fn body>
    )
*/
```

## Function with parameters and no return type
```C
addTwo = x:int, y:int => (
    PrintLn $"x=<x>, y=<y>"
)

/*
    fnName = arg1:T, arg2:T => (
        <fn body>
    )
*/
```
## Function with no parameters and no return type
```C
helloWorld => (
    PrintLn "Hello, World!"
)

/*
    fnName => (
        <fn body>
    )
*/
```

# Types

## Defining a simple type
```C
type Point (
    // Prefixing a property name with an underscore renders it private
    // Alternatively, the [private] attr can be added to a non _ prefixed property
    _x:float
    _y:float

    // Simple "getters"
    // Technically, x and  y are fns, but in Raisin fn calls do not take ()s
    // therefore, since this is a parametersless fn we can easily do :
    // myX:float = pointObj.x
    x:float => _x
    y:float => _y 

    Point = x:int, y:int => (
        _x = x
        _y = y
    )

    // Default parameterless constructor, _ is pretty much a noop
    Point => _
)
```

## Instantiating a type with constructor
```C
myPoint:Point = Point 2, 5 // Point < x: 2, y: 5>
```

## Instantiating a type without constructor
```
myPoint2:Point = Point
myPoint2.x = 5
myPoint2.y = 2
```

## Defining a Generic Type with an equality operator overload

```C
// 1. The immut (builtin) attribute makes it so the resulting objects are immutable
// 2. The & operator allows combining attributes
// 3. The constraint attribute (builtin) takes 2+ args, which define type constraints
//    The first argument is the Type keyword used (T is common but could be TKey
//    and TVal if we were defining a generic dictionary class, for instance)
//    In this case, it means that type T must inherit from the number class
[immut &
 constraint T, number]
type Box<T> (
    // Private member without underscore prefix example
    [private]
    val:T = zero T

    getType:type => T
    
    getValue:T => val

    Box<T> => _
    Box<T> = val:T => (
        @val = val // @ is basically the equivalent to 'this.' in many langs
    )

    // Define an operator overload
    // The op attribute (builtin) indicates that a specific fn is to be used for a specific operator
    // The fn name does not matter, but some consistency should be maintained (TBD)
    [op ==]
    eq = this:T, other:T => this.getValue == other.getValue
)
```

## Instantiating a generic Type
```C
myInt:int = 7
myIntBox:Box<int> = Box<int> myInt
myIntFromBox:int = myIntBox.getValue // myIntFromBox == 7
myIntBox2:Box<int> = Box<int> myIntFromBox

PrintLn (myIntBox == myIntBox2) // => 'true'
```