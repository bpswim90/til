# Promise.all() vs. Promise.allSettled()

1. `Promise.all` rejects if any of its elements reject, whereas `Promise.allSettled` will wait for all of its elements to complete regardless if they succeed or fail. 

```
const [result] = await Promise.all([Promise.reject('Nope'), Promise.resolve('Yeah!')]).catch((err) => {console.log(err)})

> 'Nope'

---

const result = await Promise.allSettled([Promise.reject('Nope'), Promise.resolve('Yeah!')])

console.log(result)
> [ 
    { status: 'rejected', reason: 'Nope'},
    { status: 'fulfilled', value: 'Yeah!}
]

```

2. `Promise.all` returns the values returned by its input promises, whereas `Promise.allSettled` returns objects containing the status and value.

```
const [blah] = await Promise.all([Promise.resolve('Hello')])

console.log(blah)
> 'Hello'

---

const [blah2] = await Promise.allSettled([Promise.resolve('Hello')])

console.log(blah2)
> { status: 'fulfilled', value: 'Hello' }

```