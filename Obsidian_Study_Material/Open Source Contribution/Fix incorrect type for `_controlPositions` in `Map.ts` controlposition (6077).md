
`
`controlPositions` is a private property of the Map class, defined in `src/ui/map.ts`. It is an object (or dictionary) that maps specific position names to their corresponding DOM container elements.

- **Type**: 
    
    ```
    Partial<Record<ControlPosition, HTMLElement>>
    ```
- **Keys**: 
	`'top-left'`, `'top-right'`, `'bottom-left'`, `'bottom-right'`

- **Values**: The `HTMLElement` (specifically a <div>) that serves as the container for controls in that corner.

This PR updates the type definition of the `_controlPositions` field in the `Map.ts` class from:

```ts
Record<string, HTMLElement>
```

to:

```ts
Partial<Record<ControlPosition, HTMLElement>>
```
which is already defined in `src/ui/control/control.ts` as 
```ts
export const ControlPosition = 'top-left' | 'top-right' | 'bottom-left' | 'bottom-right';
```

I used `Partial` so I can start `_controlPositions` as an empty object without TypeScript throwing an error. It still keeps the type safety for the known control positions and helps IntelliSense work properly while coding.


