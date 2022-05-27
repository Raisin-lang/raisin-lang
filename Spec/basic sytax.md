# Variables

## Declaration
```
x:int // varName:T
```

## Assignment
```
x = 5 // varName = (value), varName must be declared prior
```

## Declaration with assignment
```
x:int = 5 // varName:T = (value)
```

# Functions

## Function with parameters and return type
```
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
```
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
```
addTwo = x:int, y:int => (
    PrintLn $"x={x}, y={y}
)

/*
    fnName = arg1:T, arg2:T => (
        <fn body>
    )
*/
```
## Function with no parameters and no return type
```
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
```
type Point (
    X:float
    Y:float

    Point = x:int, y:int => (
        X = x
        Y = y
    )

    // Default parameterless constructor
    Point => _
)
```

## Instantiating a type with constructor
```
myPoint:Point = Point 2, 5 // Point { x: 2, y: 5}
```

## Instantiating a type without constructor
```
myPoint2:Point = Point
myPoint2.X = 5
myPoint2.Y = 2
```