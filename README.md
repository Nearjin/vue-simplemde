# Vue-SimpleMDE
> Markdown Editor component for Vue.js. Support only vue2.x.

[![npm package](https://img.shields.io/npm/v/vue-simplemde.svg)](https://npmjs.org/package/vue-simplemde)
[![npm downloads](http://img.shields.io/npm/dm/vue-simplemde.svg)](https://npmjs.org/package/vue-simplemde)

# Demo
[Demo Page](https://F-loat.github.io/vue-simplemde/)

# Use Setup

## Requirements
- vue@^2.0
- webpack@^2.0

## Install

``` bash
npm install vue-simplemde --save
```

## Use

``` javascript
// Global reference
import Vue from 'vue'
import VueSimplemde from 'vue-simplemde'

Vue.use(VueSimplemde)
```

``` javascript
// Internal reference in a single component
import markdownEditor from 'vue-simplemde/src/markdown-editor'

export default {
  components: {
    markdownEditor
  }
}
```

## Props
| property | type | default | describe |
| ----| ----- | ----- | ---- |
| value | String | None | Initial value, v-model binding can be used |
| preview-class | String | None | Custom preview style class |
| autoinit | Boolean | true | Automatic initialization |
| highlight | Boolean | false | Is it open to highlight |
| sanitize | Boolean | false | HTML that does not render input after opening |
| configs | Object | {} | [SimpleMDE's config](#configuration) |

## Examples

> No longer support Vue1.x, you can modify to use

``` vue
<template>
  <!-- use v-model control value -->
  <markdown-editor v-model="content" ref="markdownEditor"></markdown-editor>

  <!-- use event control value -->
  <markdown-editor :value="content" @input="handleInput"></markdown-editor>

  <!-- add config -->
  <markdown-editor :configs="configs"></markdown-editor>

  <!-- disable auto init -->
  <markdown-editor :autoinit="false"></markdown-editor>
</template>

<style>
  @import '~simplemde/dist/simplemde.min.css';
</style>

<script>
  import markdownEditor from 'vue-simplemde/src/markdown-editor'

  // Base example
  export default {
    components: {
      markdownEditor
    },
    data () {
      return {
        content: '',
        configs: {
          spellChecker: false // disable spell check
        }
      }
    }
  }

  // Complete example
  export default {
    components: {
      markdownEditor
    },
    data () {
      return {
        content: '',
        configs: {
          status: false, // disable the status bar at the bottom
          spellChecker: false // disable spell check
        }
      }
    },
    computed: {
      simplemde () {
        return this.$refs.markdownEditor.simplemde
      }
    },
    mounted: {
      console.log(this.simplemde)
      this.simplemde.togglePreview()

      // 'change' envent has bound, via @input attache an event listener
      // You can attache events in this [list](https://codemirror.net/doc/manual.html#events) yourself if necessary
      this.simplemde.codemirror.on('beforeChange', (instance, changeObj) => {
        // do some things
      })

      // remove SimpleMDE, when component destroy will invoke
      this.simplemde = null

      // some useful methods
      this.$refs.markdownEditor.initialize() // init
      this.simplemde.toTextArea()
      this.simplemde.isPreviewActive() // returns boolean
      this.simplemde.isSideBySideActive() // returns boolean
      this.simplemde.isFullscreenActive() // returns boolean
      this.simplemde.clearAutosavedValue() // no returned value
      this.simplemde.markdown(this.content) // returns parsed html
      this.simplemde.codemirror.refresh() // refresh codemirror
    },
    methods: {
      handleInput () {
        // do some things
      }
    }
  }
</script>
```

## Markdown style
> e.g. use Github's markdown style

[github-markdown-css](https://github.com/sindresorhus/github-markdown-css)

### install
``` bash
$ npm install --save github-markdown-css
```

### use
``` vue
<template>
  <markdown-editor preview-class="markdown-body"></markdown-editor>
</template>

<style>
  @import '~simplemde/dist/simplemde.min.css';
  @import '~github-markdown-css';
</style>
```

## Highlight

### install
```
$ npm install --save highlight.js
```

### use
``` vue
<template>
  <markdown-editor :highlight="true"></markdown-editor>
</template>

<script>
  import hljs from 'highlight.js';

  window.hljs = hljs;
</script>

<style>
  @import '~simplemde/dist/simplemde.min.css';
  @import '~highlight.js/styles/atom-one-dark.css';
  /* Highlight theme list: https://github.com/isagalaev/highlight.js/tree/master/src/styles */
</style>
```

## Editor Theme ([simplemde-theme-base](https://github.com/xcatliu/simplemde-theme-base/wiki/List-of-themes))
> e.g. use simplemde-theme-base theme

### install
```
$ npm install --save simplemde-theme-base
```

### use
``` vue
<style>
  @import '~simplemde-theme-base/dist/simplemde-theme-base.min.css';
  /* no need import imposimplemde.min.css */
</style>
```

## Configuration
> SimpleMD's config

* [中文](doc/configuration_zh.md)
* [English](doc/configuration_en.md)

## Dependencies

* [SimpleMDE](https://github.com/sparksuite/simplemde-markdown-editor)

## Licence

vue-simplemde is open source and released under the MIT Licence.

Copyright (c) 2017 F-loat
