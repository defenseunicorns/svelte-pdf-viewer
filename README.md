# svelte-pdf-viewer-viewer

Simple svelte PDF Viewer component with controls like

- Page navigation
- Zoom
- Rotation
- Print
- AutoFlip Page

## How to install

```
npm install @defenseunicorns/svelte-pdf-viewer-viewer
```

## How to use

#### Using local path

```js
<script>
 import PdfViewer from '@defenseunicorns/svelte-pdf-viewer-viewer';
</script>

<PdfViewer url='./sample.pdf' />

```

#### Using url

```js
<script>
 import PdfViewer from '@defenseunicorns/svelte-pdf-viewer-viewer';
</script>

<PdfViewer url='https://raw.githubusercontent.com/vinodnimbalkar/svelte-pdf-viewer/369db2f9edbf5ab8c87184193e1404340729bb3a/public/sample.pdf' />

```

#### Using `base64` encoded string

```js
<script>
 import PdfViewer from 'svelte-pdf-viewer';
  const base64 =
    "JVBERi0xLjcKCjEgMCBvYmogICUgZW50cnkgcG9pbnQKPDwKICAvVHlwZSAvQ2F0YWxvZwogIC9QYWdlcyAyIDAgUgo+PgplbmRvYmoKCjIgMCBvYmoKPDwKICAvVHlwZSAvUGFnZXMKICAvTWVkaWFCb3ggWyAwIDAgMjAwIDIwMCBdCiAgL0NvdW50IDEKICAvS2lkcyBbIDMgMCBSIF0KPj4KZW5kb2JqCgozIDAgb2JqCjw8CiAgL1R5cGUgL1BhZ2UKICAvUGFyZW50IDIgMCBSCiAgL1Jlc291cmNlcyA8PAogICAgL0ZvbnQgPDwKICAgICAgL0YxIDQgMCBSIAogICAgPj4KICA+PgogIC9Db250ZW50cyA1IDAgUgo+PgplbmRvYmoKCjQgMCBvYmoKPDwKICAvVHlwZSAvRm9udAogIC9TdWJ0eXBlIC9UeXBlMQogIC9CYXNlRm9udCAvVGltZXMtUm9tYW4KPj4KZW5kb2JqCgo1IDAgb2JqICAlIHBhZ2UgY29udGVudAo8PAogIC9MZW5ndGggNDQKPj4Kc3RyZWFtCkJUCjcwIDUwIFRECi9GMSAxMiBUZgooSGVsbG8sIHdvcmxkISkgVGoKRVQKZW5kc3RyZWFtCmVuZG9iagoKeHJlZgowIDYKMDAwMDAwMDAwMCA2NTUzNSBmIAowMDAwMDAwMDEwIDAwMDAwIG4gCjAwMDAwMDAwNzkgMDAwMDAgbiAKMDAwMDAwMDE3MyAwMDAwMCBuIAowMDAwMDAwMzAxIDAwMDAwIG4gCjAwMDAwMDAzODAgMDAwMDAgbiAKdHJhaWxlcgo8PAogIC9TaXplIDYKICAvUm9vdCAxIDAgUgo+PgpzdGFydHhyZWYKNDkyCiUlRU9G";
</script>

<PdfViewer data={atob(base64)} />

```

## Props

| Prop               |   Type    | Default                                                                                       |  Req  |
| ------------------ | :-------: | --------------------------------------------------------------------------------------------- | :---: |
| `url`              | `string`  | `N/A`                                                                                         | `Yes` |
| `data`             | `string`  | `N/A`                                                                                         | `No`  |
| `mode`             | `string`  | `"dark"`                                                                                      | `No`  |
| `scale`            |  `float`  | `1.5`                                                                                         | `No`  |
| `pageNum`          | `number`  | `1`                                                                                           | `No`  |
| `flipTime`         | `number`  | `120`                                                                                         | `No`  |
| `showButtons`      |  `array`  | `"['navigation', 'zoom', 'print', 'rotate', 'download', 'autoflip', 'timeInfo', 'pageInfo']"` | `No`  |
| `showBorder`       | `boolean` | `true`                                                                                        | `No`  |
| `downloadFileName` | `string`  | `N/A`                                                                                         | `No`  |

## Examples

To view the examples, clone the **@defenseunicorns/svelte-pdf-viewer-viewer** repo and install the dependencies:

```bash
git clone git@github.com:defenseunicorns/svelte-pdf-viewer-viewer.git
cd example
npm install
npm run dev
```

Then run the **http://localhost:5000**:

## How to use it in Sapper with SSR enabled

### 1. Install it as part of `devDependencies`

> When using Svelte components installed from npm, it needs the original component source (rather than any precompiled
> JavaScript that ships with the component). This allows the component to be rendered server-side, and also keeps your
> client-side app smaller...

      -- [Rich Harris](https://github.com/Rich-Harris/svelte-workshop#using-external-components)

We have to install `@defenseunicorns/svelte-pdf-viewer-viewer` as part of `devDependencies`

```bash
npm install -D @defenseunicorns/svelte-pdf-viewer-viewer
```

...this will cause it to get bundled (and therefore compiled) with your app.

### 2. Make our `PdfViewer` component SSR compatible

Since out `PdfViewer` component has a dependency on `window` object, we have to use dynamic import, from within the
`onMount` function (which is only called on the client), so that our import code is never called on the server.
[Refer to the official doc here...](https://sapper.svelte.dev/docs#Making_a_component_SSR_compatible)

```bash

<script>
  import { onMount } from "svelte";
  let PdfViewer;

  onMount(async () => {
    const module = await import("@defenseunicorns/svelte-pdf-viewer-viewer");
    PdfViewer = module.default;
  });
</script>

<svelte:component this={PdfViewer} url="YOUR-PDF-URL"/>
```

## Contributing

Feel free to open an issue (or even better, send a Pull Request). Contributions are very welcome!! 😄

## License

**[MIT](https://github.com/vinodnimbalkar/svelte-pdf-viewer/blob/master/LICENSE)**
