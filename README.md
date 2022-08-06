# miragejs-uuidManager
miragejs custom uuid identityManager

## Custom Identity Manager into UUID v4 format
```typescript
import {v4} from 'uuid'

export default class UuidManager{
    ids = new Set()

    constructor(){
        this.ids = new Set()
    }
    fetch(){
        let id = v4()
        while(this.ids.has(id))
        {
            id = v4()
        }
        this.ids.add(id)

        return id
    }
    set(id: string)
    {
        if(this.ids.has(id))
        {
            throw new Error(`ID ${id} has already been used.`)
        }
        this.ids.add(id)
    }
    reset()
    {
        this.ids.clear()
    }
}
```

## Usage
```typescript
import {createServer,Factory,Model,Serializer} from 'miragejs'

import UuidManager from 'miragejs-uuidmanager'

export function MockServer({environment = 'development'}){
    return createServer({
        environment,
        identityManagers: {
            todo: UuidManager,
        } as any,
        ...
    })
}
```