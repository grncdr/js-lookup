# lookup

[![browser support](https://ci.testling.com/grncdr/js-lookup.png)](https://ci.testling.com/grncdr/js-lookup)

## module.exports = function makeReducer (hash=pluck("id"), onCollision="last")

`lookupReducer` creates a reducing function (suitable for passing to 
`Array.prototype.reduce` or [reducible](https://npm.im/reducible)) that builds a
lookup table of objects based on the provided hash function:

```javascript
function reducer (mapping, object) {
  mapping[hash(object)] = object
  return mapping
}
```

The `hash` parameter provided to `makeReducer` may also be a string, in which
case it will be passed to [pluck](https://npm.im/pluck) to create a hash function.

Different reducer implementations can be selected by the `onCollision` parameter
provided to `lookupReducer`. The default shown above ("last") keeps the last value
seen for any given hash. The other options are "first", which retains the first
value seen for a given key, and "concat" which handles collisions by creating an
array containing every value seen for a given key.

## makeReducer.reduce(arr, hash=pluck("id"), onCollision="last")

A short-hand way of writing `arr.reduce(makeReducer(hash, onCollision), {})`.

## makeReducer.writableStream(hash=pluck("id"), onCollision="last", callback)

Returns a writable stream that will use the reducer function to aggregate
objects written to it into a single mapping. While the first two arguments are
optional a callback must be provided. The callback will be called with the
complete lookup table on the streams "end" event.

# License

BSD (2 clause)
