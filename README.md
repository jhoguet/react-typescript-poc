# Proof of Concept demonstrating React, Typescript, and Webpack

This was built (mostly) following the instructions [here](https://www.typescriptlang.org/docs/handbook/react-&-webpack.html).
 
## Observations on Dec 2, 2016

Getting this stood up was pretty trivial. I installed everything locally instead of globally but that was my only deviation. 

Editor support in WebStorm is terrible - the benefits of typescript are significantly reduced without good editor support.
 
Verified that I still have type safety benefits, for example trying to access `this.props.msg` it failed, as it should since `compiler` is the property we are expecting. 

```tsx
import * as React from "react";

export interface HelloProps { compiler: string; framework: string; }

export class Hello extends React.Component<HelloProps, {}> {
    render() {
        return <h1>Hello from {this.props.msg} and {this.props.framework}!</h1>;
    }
}

```

The error message wasn't quite what I expected though (I expected just `HelloProps` not `HelloProps & { children?: ReactNode; }`)

> (7,43): error TS2339: Property 'msg' does not exist on type 'HelloProps & { children?: ReactNode; }'.
  
Verified that I also receive error messaging when sending attributes that are not expected
 
```tsx
<Hello compiler="TypeScript" framework="React" msg="some message" />,
```

resulted in 

> (7,52): error TS2339: Property 'msg' does not exist on type 'IntrinsicAttributes & IntrinsicClassAttributes<Hello> & HelloProps & { children?: ReactNode; }'.

or if I don't set the expected fields

```tsx
<Hello compiler="TypeScript" framework="React" msg="some message" />,
```

resulted in 

> (7,5): error TS2324: Property 'compiler' is missing in type 'IntrinsicAttributes & IntrinsicClassAttributes<Hello> & HelloProps & { children?: ReactNode; }'.
  
> (7,5): error TS2324: Property 'framework' is missing in type 'IntrinsicAttributes & IntrinsicClassAttributes<Hello> & HelloProps & { children?: ReactNode; }'.


Next Steps
- [ ] Try out Visual Studio Code to see if editor support is better (and doesn't require licensing that WebStorm does)
- [ ] Can we mix typescript and non typescript (what is the migration path without one huge refactor)?

 
 
