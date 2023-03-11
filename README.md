# React TypeScript 

## What is the difference between JSX.Element, ReactNode and ReactElement?

### ReactElement

A ReactElement is an object with a type and props.

```javascript
type Key = string | number

 interface ReactElement<P = any, T extends string | JSXElementConstructor<any> = string | JSXElementConstructor<any>> {
    type: T;
    props: P;
    key: Key | null;
}
```

### JSX.Element

JSX.Element is a ReactElement, with the generic type for props and type being any. It exists, as various libraries can implement JSX in their own way, therefore JSX is a global namespace that then gets set by the library, React sets it like this:

```javascript
declare global {
  namespace JSX {
    interface Element extends React.ReactElement<any, any> { }
  }
}
```

The ReactElement and JSX.Element are the result of invoking React.createElement directly or via JSX transpilation.

```javascript
const jsx = <div>hello</div>
const reactelement = React.createElement("div", null, "hello");

```

### ReactNode

A ReactNode is a ReactElement, a ReactFragment, a string, a number or an array of ReactNodes, or null, or undefined, or a boolean:

```javascript
type ReactText = string | number;
type ReactChild = ReactElement | ReactText;

interface ReactNodeArray extends Array<ReactNode> {}
type ReactFragment = {} | ReactNodeArray;

type ReactNode = ReactChild | ReactFragment | ReactPortal | boolean | null | undefined;
```

**Example:**

```javascript
<p> // <- ReactElement = JSX.Element
   <Custom> // <- ReactElement = JSX.Element
     {isLogin && "user is Logged"} // <- ReactNode
  </Custom>
 </p>
```

## as keyword

The compiler is sometimes incorrect and infers the wrong type. TypeScript offers a type assertion.

Type assertion is a technique that informs the compiler about the type of a variable.

When we want to change a variable from one type to another such as any to number etc, we use Type assertion.

We can either use <> angular brackets or as keywords to do type assertion.

**Example:**

```javascript
let num: any = 77;
let num1 = num as Number;
console.log(typeof num1); // number
```
