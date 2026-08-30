
> Name

TypeScript-demo
> Author

inventor quantification
> Strategy Description

The platform has added native TypeScript support, you only need to add it at the beginning of the source code (the strategic language type is still JavaScript)
```
// @ts-check
```

It can be automatically recognized as TypeScript



> Source (javascript)

``` javascript
// @ts-check

class Greeter {
    greeting: string;

    constructor(message: string) {
        this.greeting = message;
    }

    greet() {
        return "Hello, " + this.greeting;
    }
}


function peopleName(firstName: string, ...restOfname: string[]) {
    return firstName + " " + restOfname.join(" ");
}


function main() {
    let greeter = new Greeter("world");
    Log(greeter.greet());

    
    Log(peopleName('xiaochuan', 'xiaoming', 'xiaohong'))
}


```

> Detail

https://www.fmz.com/strategy/405326

> Last Modified

2023-04-30 20:17:23
