# p-all

> Run promise-returning & async functions concurrently with optional limited concurrency

Similar to `Promise.all()`, but accepts functions instead of promises directly so you can limit the concurrency.

If you're doing the same work in each function, use [`p-map`](https://github.com/sindresorhus/p-map) instead.

See [`p-series`](https://github.com/sindresorhus/p-series) for a serial counterpart.

## Install

```
$ npm install p-all
```

## Usage

```js
import pAll from 'p-all';
import got from 'got';

const actions = [
	() => got('https://sindresorhus.com'),
	() => got('https://avajs.dev'),
	() => checkSomething(),
	() => doSomethingElse()
];

console.log(await pAll(actions, {concurrency: 2}));
```

## API

### pAll(tasks, options?)

Returns a `Promise` that is fulfilled when all promises returned from calling the functions in `tasks` are fulfilled, or rejects if any of the promises reject. The fulfilled value is an `Array` of the fulfilled values in `tasks` order.

#### tasks

Type: `Iterable<Function>`

Iterable with promise-returning/async functions.

#### options

Type: `object`

##### concurrency

Type: `number`\
Default: `Infinity`\
Minimum: `1`

Number of concurrent pending promises.

##### stopOnError

Type: `boolean`\
Default: `true`

When set to `false`, instead of stopping when a promise rejects, it will wait for all the promises to settle and then reject with an [aggregated error](https://github.com/sindresorhus/aggregate-error) containing all the errors from the rejected promises.

## Related

- [p-map](https://github.com/sindresorhus/p-map) - Map over promises concurrently
- [p-series](https://github.com/sindresorhus/p-series) - Run promise-returning & async functions in series
- [p-props](https://github.com/sindresorhus/p-props) - Like `Promise.all()` but for `Map` and `Object`
- [p-queue](https://github.com/sindresorhus/p-queue) - Promise queue with concurrency control
- [p-limit](https://github.com/sindresorhus/p-limit) - Run multiple promise-returning & async functions with limited concurrency
- [More…](https://github.com/sindresorhus/promise-fun)
