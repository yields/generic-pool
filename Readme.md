
# apool

  generic object pool for node.

## Installation

```bash
$ npm install apool
```

## API

### pool(max)

  Initialize a new `Pool` with optional `max`.

#### #max(max)

  Set `max` objects that the pool can hold.

#### #constructor(fn)

  Set the `constructor` that the pool will use when it needs more objects.

#### #destructor(fn)

  Set the `destructor` that will be used to destroy objects.

#### #min(n)

  Set the `min` number of objects that will remain in the pool, defaulted to whatever
  is passed to `populate()`.

#### #length()

  Get the `length()` of objects (including used ones).

#### #populate(n[, fn])

  Populate `n` objects with optional `fn(err)`.

#### #acquire(fn[, timeout])

  Acquire an object with `fn(err, obj)` and optional `timeout` defaulting to `500ms`.

#### #return(obj)

  Return an object to the pool.

##### Events

  - `add`, emitted when an object is added.
  - `return`, emitted when an object is returned.
  - `acquired`, emitted when an object is acquired.
  - `populate`, emitted after `populate(n)`.

## Example

  See `./example`, there are two real-world examples using phantomjs with a pool of `page()` objects,
  benchmarking each with `wrk` yields:

`no-pool.js`
``` text
Running 30s test @ http://localhost:3000/
  12 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency   457.23ms    9.24ms 459.79ms   97.25%
    Req/Sec     0.67      3.22    18.00     95.50%
  336 requests in 30.01s, 62.02KB read
  Socket errors: connect 0, read 0, write 0, timeout 1344
Requests/sec:     11.20
Transfer/sec:      2.07KB
```

`pool.js`
```text
Running 30s test @ http://localhost:3000/
  12 threads and 100 connections
  Thread Stats   Avg      Stdev     Max   +/- Stdev
    Latency   310.84ms   35.91ms 385.16ms   89.66%
    Req/Sec    25.23      4.51    38.00     80.32%
  9218 requests in 30.01s, 1.66MB read
Requests/sec:    307.16
Transfer/sec:     56.69KB
```

## Tests

```bash
$ make test
```

## License

(MIT)
