---
description: "Creating and rendering Metal components."
icon: "module"
layout: "docs"
title: "Metal Components"
weight: 6
---

<article id="creating">

## Creating Components

One of the major benefits of `electric` is the ability to create metal.js
components and invoke them in your `soy` layouts and pages.

Components can exist anywhere in the `src` directory, for this example we will
place them inside `src/components`.

```bash
|--src/
   |--layouts/
	  |--base.soy
	  |--docs.soy
   |--pages/
	  |--index.soy
   |--components/
	  |--MyComponent.soy
	  |--MyComponent.js
```

`MyComponent.soy`.

```soy
{lb}namespace MyComponent{rb}

/**
 *
 */
{lb}template .render{rb}
	<div>Hello, World!</div>
{lb}/template{rb}
```

`MyComponent.js`.

```js
'use strict';

import Component from 'metal-component';
import Soy from 'metal-soy';

import templates from './MyComponent.soy';

class MyComponent extends Component {
	attached() {
		console.log('MyComponent attached!');
	}
};

Soy.register(MyComponent, templates);

export default MyComponent;
```

Now that you have the base component files, the `MyComponent` template simply
needs to be rendered in a page/layout.

</article>

<article id="rendering">

## Rendering Components

To render a metal component in a page/layout, simply use the `call` command to
render the `.render` template of the component.

```soy
---
description: "Page description."
title: "Page"
---

{lb}namespace page{rb}

/**
 *
 */
{lb}template .render{rb}
	<div>
		{lb}call MyComponent.render /{rb}
	</div>
{lb}/template{rb}
```

Now you should see 'MyComponent attached!' in the browser console.

</article>

<article id="metal_sgg_components">

## Electric Components

The [electric-components](https://github.com/liferay/electric-components) package
contains a number of components that are compatible with the site meta data,
such as navigation and search components.

See [configuration](/docs/tasks.html#configuration) for information on
adding `plugins` to your project.

These components are invoked the same way as your own components.

```soy
---
description: "Page description."
title: "Page"
---

{lb}namespace page{rb}

/**
 * @param site
 */
{lb}template .render{rb}
	<div>
		{lb}call ElectricNavigation.render{rb}
			{lb}param depth: 1 /{rb}
			{lb}param section: $site.index /{rb}
		{lb}/call{rb}
	</div>
{lb}/template{rb}
```

This will render a list with all direct descendants of the index page.

</article>
