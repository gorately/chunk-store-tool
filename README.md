# chunk-store-tool

#### A test suite and interface you can use to implement a chunk based storage backend

## Install

```
npm install chunk-store-tool
```

## Some modules that use this

Recommended chunk stores:

- [memory-chunk-store](https://npmjs.com/package/memory-chunk-store)
- [fs-chunk-store](https://npmjs.com/package/fs-chunk-store)
- [idb-chunk-store](https://www.npmjs.com/package/idb-chunk-store)
- [fs-access-chunk-store](https://www.npmjs.com/package/fs-access-chunk-store)

Recommended chunk store utilities:

- [immediate-chunk-store](https://npmjs.com/package/immediate-chunk-store)
- [cache-chunk-store](https://npmjs.com/package/cache-chunk-store)
- [chunk-store-stream](https://npmjs.com/package/chunk-store-stream)

Other modules that follow the chunk store spec:

- [chunk-store-multi-get](https://npmjs.com/package/chunk-store-multi-get)
- [abstract-chunk-transport](https://npmjs.com/package/abstract-chunk-transport)
- [fd-chunk-store](https://www.npmjs.com/package/fd-chunk-store)
- [sparse-chunk-store](https://www.npmjs.com/package/sparse-chunk-store)
- [ls-chunk-store](https://www.npmjs.com/package/ls-chunk-store)
- [deferred-chunk-store](https://www.npmjs.com/package/deferred-chunk-store)
- [indexeddb-chunk-store](https://www.npmjs.com/package/indexeddb-chunk-store)
- [idbkv-chunk-store](https://www.npmjs.com/package/idbkv-chunk-store)
- [cache-storage-chunk-store](https://www.npmjs.com/package/cache-storage-chunk-store)

Send a PR adding yours if you write a new one.

## API

#### `chunkStore = new ChunkStore(chunkLength)`

Create a new chunk store. Chunks must have a length of `chunkLength`.

#### `chunkStore.put(index, chunkBuffer, [cb])`

Add a new chunk to the storage. Index should be an integer.

#### `chunkStore.get(index, [options], cb)`

Retrieve a chunk stored. Index should be an integer.
Options include:

``` js
{
  offset: chunkByteOffset,
  length: byteLength
}
```

If the index doesn't exist in the storage an error should be returned.

#### `chunkStore.close([cb])`

Close the underlying resource, e.g. if the store is backed by a file, this would close the
file descriptor.

#### `chunkStore.destroy([cb])`

Destroy the file data, e.g. if the store is backed by a file, this would delete the file
from the filesystem.

#### `chunkStore.chunkLength`

Expose the chunk length from the constructor so that code that receives a chunk
store can know what size of chunks to write.

## Test Suite

Publishing a test suite as a module lets multiple modules all ensure compatibility since
they use the same test suite.

To use the test suite from this module you can `require('abstract-chunk-store/tests')`.

An example of this can be found in the
[memory-chunk-store](https://github.com/mafintosh/memory-chunk-store/blob/master/test.js)
test suite.

To run the tests simply pass your test module (`tap` or `tape` or any other compatible
modules are supported) and your store's constructor (or a setup function) in:

```js
var tests = require('abstract-chunk-store/tests')
tests(require('tape'), require('your-custom-chunk-store'))
```

## Background

An abstract chunk store is a binary data store that allows you to interact with individual chunks of a larger blob (a.k.a. binary file).  A chunk can be thought of as a small partial blob that fits in memory.

Related:

- [Abstract Blob Store](https://github.com/maxogden/abstract-blob-store)

## License

MIT
