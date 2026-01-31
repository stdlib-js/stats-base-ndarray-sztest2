<!--

@license Apache-2.0

Copyright (c) 2025 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# sztest2

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Compute a two-sample Z-test for two one-dimensional single-precision floating-point ndarrays.

<section class="intro">

A Z-test commonly refers to a two-sample location test which compares the means of two independent sets of measurements `X` and `Y` when the population standard deviations are known. A Z-test supports testing three different null hypotheses `H0`:

-   `H0: μX - μY ≥ Δ` versus the alternative hypothesis `H1: μX - μY < Δ`.
-   `H0: μX - μY ≤ Δ` versus the alternative hypothesis `H1: μX - μY > Δ`.
-   `H0: μX - μY = Δ` versus the alternative hypothesis `H1: μX - μY ≠ Δ`.

Here, `μX` and `μY` are the true population means of samples `X` and `Y`, respectively, and `Δ` is the hypothesized difference in means (typically `0` by default).

</section>

<!-- /.intro -->



<section class="usage">

## Usage

```javascript
import sztest2 from 'https://cdn.jsdelivr.net/gh/stdlib-js/stats-base-ndarray-sztest2@deno/mod.js';
```
The previous example will load the latest bundled code from the deno branch. Alternatively, you may load a specific version by loading the file from one of the [tagged bundles](https://github.com/stdlib-js/stats-base-ndarray-sztest2/tags). For example,

```javascript
import sztest2 from 'https://cdn.jsdelivr.net/gh/stdlib-js/stats-base-ndarray-sztest2@v0.1.0-deno/mod.js';
```

#### sztest2( arrays )

Computes a two-sample Z-test for two one-dimensional single-precision floating-point ndarrays.

```javascript
import Float32Results from 'https://cdn.jsdelivr.net/gh/stdlib-js/stats-base-ztest-two-sample-results-float32@deno/mod.js';
import resolveEnum from 'https://cdn.jsdelivr.net/gh/stdlib-js/stats-base-ztest-alternative-resolve-enum@deno/mod.js';
import structFactory from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-struct-factory@deno/mod.js';
import Float32Array from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-float32@deno/mod.js';
import scalar2ndarray from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-from-scalar@deno/mod.js';
import ndarray from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-ctor@deno/mod.js';

var opts = {
    'dtype': 'float32'
};

var xbuf = new Float32Array( [ 4.0, 4.0, 6.0, 6.0, 5.0 ] );
var x = new ndarray( opts.dtype, xbuf, [ 5 ], [ 1 ], 0, 'row-major' );

var ybuf = new Float32Array( [ 3.0, 3.0, 5.0, 7.0, 7.0 ] );
var y = new ndarray( opts.dtype, ybuf, [ 5 ], [ 1 ], 0, 'row-major' );

var alt = scalar2ndarray( resolveEnum( 'two-sided' ), {
    'dtype': 'int8'
});
var alpha = scalar2ndarray( 0.05, opts );
var diff = scalar2ndarray( 0.0, opts );
var sigmax = scalar2ndarray( 1.0, opts );
var sigmay = scalar2ndarray( 2.0, opts );

var ResultsArray = structFactory( Float32Results );
var out = new ndarray( Float32Results, new ResultsArray( 1 ), [], [ 0 ], 0, 'row-major' );

var v = sztest2( [ x, y, out, alt, alpha, diff, sigmax, sigmay ] );

var bool = ( v === out );
// returns true
```

The function has the following parameters:

-   **arrays**: array-like object containing the following ndarrays in order:

    1.  first one-dimensional input ndarray.
    2.  second one-dimensional input ndarray.
    3.  a zero-dimensional output ndarray containing a [results object][@stdlib/stats/base/ztest/two-sample/results/float32].
    4.  a zero-dimensional ndarray specifying the alternative hypothesis.
    5.  a zero-dimensional ndarray specifying the significance level.
    6.  a zero-dimensional ndarray specifying the difference in means under the null hypothesis.
    7.  a zero-dimensional ndarray specifying the known standard deviation of the first one-dimensional input ndarray.
    8.  a zero-dimensional ndarray specifying the known standard deviation of the second one-dimensional input ndarray.

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   As a general rule of thumb, a Z-test is most reliable for sample sizes greater than `50`. For smaller sample sizes or when the standard deviation is unknown, prefer a t-test.

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```javascript
import Float32Results from 'https://cdn.jsdelivr.net/gh/stdlib-js/stats-base-ztest-two-sample-results-float32@deno/mod.js';
import resolveEnum from 'https://cdn.jsdelivr.net/gh/stdlib-js/stats-base-ztest-alternative-resolve-enum@deno/mod.js';
import structFactory from 'https://cdn.jsdelivr.net/gh/stdlib-js/array-struct-factory@deno/mod.js';
import normal from 'https://cdn.jsdelivr.net/gh/stdlib-js/random-array-normal@deno/mod.js';
import ndarray from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-ctor@deno/mod.js';
import scalar2ndarray from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-from-scalar@deno/mod.js';
import ndarray2array from 'https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@deno/mod.js';
import sztest2 from 'https://cdn.jsdelivr.net/gh/stdlib-js/stats-base-ndarray-sztest2@deno/mod.js';

var opts = {
    'dtype': 'float32'
};

// Create one-dimensional ndarrays containing pseudorandom numbers drawn from a normal distribution:
var xbuf = normal( 100, 0.0, 1.0, opts );
var x = new ndarray( opts.dtype, xbuf, [ xbuf.length ], [ 1 ], 0, 'row-major' );
console.log( ndarray2array( x ) );

var ybuf = normal( 100, 0.0, 1.0, opts );
var y = new ndarray( opts.dtype, ybuf, [ ybuf.length ], [ 1 ], 0, 'row-major' );
console.log( ndarray2array( y ) );

// Specify the alternative hypothesis:
var alt = scalar2ndarray( resolveEnum( 'two-sided' ), {
    'dtype': 'int8'
});

// Specify the significance level:
var alpha = scalar2ndarray( 0.05, opts );

// Specify the difference in means under the null hypothesis:
var diff = scalar2ndarray( 0.0, opts );

// Specify the known standard deviations:
var sigmax = scalar2ndarray( 1.0, opts );
var sigmay = scalar2ndarray( 1.0, opts );

// Create a zero-dimensional results ndarray:
var ResultsArray = structFactory( Float32Results );
var out = new ndarray( Float32Results, new ResultsArray( 1 ), [], [ 0 ], 0, 'row-major' );

// Perform a Z-test:
var v = sztest2( [ x, y, out, alt, alpha, diff, sigmax, sigmay ] );
console.log( v.get().toString() );
```

</section>

<!-- /.examples -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/stats-base-ndarray-sztest2.svg
[npm-url]: https://npmjs.org/package/@stdlib/stats-base-ndarray-sztest2

[test-image]: https://github.com/stdlib-js/stats-base-ndarray-sztest2/actions/workflows/test.yml/badge.svg?branch=v0.1.0
[test-url]: https://github.com/stdlib-js/stats-base-ndarray-sztest2/actions/workflows/test.yml?query=branch:v0.1.0

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/stats-base-ndarray-sztest2/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/stats-base-ndarray-sztest2?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/stats-base-ndarray-sztest2.svg
[dependencies-url]: https://david-dm.org/stdlib-js/stats-base-ndarray-sztest2/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/stats-base-ndarray-sztest2/tree/deno
[deno-readme]: https://github.com/stdlib-js/stats-base-ndarray-sztest2/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/stats-base-ndarray-sztest2/tree/umd
[umd-readme]: https://github.com/stdlib-js/stats-base-ndarray-sztest2/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/stats-base-ndarray-sztest2/tree/esm
[esm-readme]: https://github.com/stdlib-js/stats-base-ndarray-sztest2/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/stats-base-ndarray-sztest2/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/stats-base-ndarray-sztest2/main/LICENSE

[@stdlib/stats/base/ztest/two-sample/results/float32]: https://github.com/stdlib-js/stats-base-ztest-two-sample-results-float32/tree/deno

</section>

<!-- /.links -->
