# Portable Text for Svelte

Provides a way to render [Portable Text](http://www.portabletext.org) in Svelte applications.

## Install

```
npm add --save-dev @arzidava/svelte-portable-text
```

## Usage

```html
<script>
  import BlockContent from "@movingbrands/svelte-portable-text";

  import Image from "./Image";
  import Link from "./Link";

  export let content;
  export const customSerializers = {
    types: {
      image: props => {
        return {
          component: Image,
          props: {
            url: props.node.url,
          },
        };
      },
    },
    marks: {
      link: props => {
        return {
          component: Link,
          props: props.mark,
        };
      },
    },
  };
</script>

<BlockContent blocks="{content}" serializers="{customSerializers}" />
```

## Work in Progress

This package is under development but should cover the most basic usages.
A demo setup of this package using [Sanity](http://www.sanity.io) can be found [here](https://github.com/stephane-vanraes/demo-sveltekit-sanity).

If you find bugs, just open an issue (or even better a Pull Request) 😀
