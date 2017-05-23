# Unit Test:  private functions
## Problem:
> We want test the __process__ fuction but we **can't** its is a **private** function

**widget-a/index.js**
``` typescript
import {DataItem} from "models"
export class WidgetA {
    data:DataItem[]
    constructor(data:DataItem[]){
        this.data=data;
    }
    private render(){
        let data:DataItem=process();
        // do you render logic here
    }
    private process(){
        // processing algorithm (complex or not) 
        return somedata_after_process;
    }
}
```

## Ideation
- **do not test it** -- we get a contract only to public interface
- **make it public** --  this way we can access ot them
- **externalize it to separate funcion** -- we can test it and use as a utility function in class

## Discussion
###  do not test it
it's easy and extrimly dangerous way we will pay for it later
###  make it public
This kill encapsulation, everything can be used outside your class which not be your real intent. this is can cause to unxepected result in latter 

### externalize it to separate funcion
in this way we have a ability to test function and we do not break the code design
it's sound safe way to do

## Realization

**widget-a/index.js**
``` typescript
import {DataItem} from "models"
import {processor} from "./processor"

export class WidgetA {
    data:DataItem[]
    constructor(data:DataItem[]){
        this.data=data;
    }
    private render(){
        let data:DataItem=process();
        // do you render logic here
    }
    private process(){
        return processor(this.data);
    }
}

```
**widget-a/processor.js**
``` typescript

import {DataItem} from "models";

export function processor (data:DataItem[]){
   // processing algorithm (complex or not) 
    return somedata_after_process;
}
```



