# preload-it-extended

This lib is a fork of the project [preload-it](https://github.com/andreupifarre/preload-it).

A tiny 1kb JavaScript library for preloading assets on the browser via XHR2.
It provides the ability to preload assets of different file types and composite progress events.

## Installing

If you use npm, `npm i preload-it-extended`. Otherwise, download the [latest release](https://github.com/brunopiaui/preload-it-extended/releases/latest). The released bundle supports anonymous AMD, CommonJS, and vanilla environments. You can load directly from [unpkg](https://unpkg.com/preload-it-extended/). For example:

```html
<script src="https://unpkg.com/preload-it-extended@latest/dist/preload-it-extended.js"></script>
```

For the minified version:

```html
<script src="https://unpkg.com/preload-it-extended"></script>
```

preload-it-extended is written using [ES2015 modules](http://www.2ality.com/2014/09/es6-modules-final.html). To import preload-it-extended into an ES2015 application, import into a namespace:

```html
<script type="module">
  import preload from "https://unpkg.com/preload-it-extended@latest/dist/preload-it-extended.esm.min.js";
</script>
```

or

```js
import Preload from "preload-it-extended";
const preload = Preload();
```

## Getting started

```js
const preload = Preload();

preload
  .fetch([
    "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerEscapes.mp4",
    "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4",
    "https://images.pexels.com/photos/248797/pexels-photo-248797.jpeg"
  ])
  .then(items => {
    // use either a promise or 'oncomplete'
    console.log(items);
  });

preload.oncomplete = items => {
  console.log(items);
};

preload.onprogress = event => {
  console.log(event.progress + "%");
};

preload.onfetched = item => {
  console.log(item);
};

preload.onerror = item => {
  console.log(item);
};
```

## Canceling preload of assets

Preloading of assets can be canceled at any time during fetching, when calling `preload.cancel()` all assets already preloaded will be available to use, however the download of pending assets will be abandoned, and `status` will be set to `0` for those remaining items.

```js
preload.cancel();

preload.oncancel = items => {
  console.log(items);
};
```

## License

Released for free under the MIT license, which means you can use it for almost any purpose (including commercial projects). We appreciate credit where possible, but it is not a requirement.

[MIT](LICENSE).
