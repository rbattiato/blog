---
title: "Tailwind CSS — all you need to know to get started"
date: "2021-02-05"
description: "Learn about Tailwind CSS, what it is and what it isn't, why and when to use it and how to get started quickly."
tags: [tailwindcss, framework, css]
categories: [themes, syntax]
---

Tailwind CSS is a relatively new CSS framework that can be easily seen as the next big revolution of the way we style our HTML elements. It encourages and facilitates an **utility-first** approach where you write as little custom styles as possible and use hundreds of small, low level [utility (or helper) classes](https://css-tricks.com/need-css-utility-library/) instead. For this reason Tailwind CSS isn't really a CSS framework such as Bootstrap or Bulma; it's really just a JavaScript based utility classes generator.  
My first impact with it wasn't good: being used to traditional styling I liked my HTML clean and my classes semantic, the latter having an important role in the frontend [separation of concerns](https://en.wikipedia.org/wiki/Separation_of_concerns#HTML,_CSS,_JavaScript). Using Tailwind and its so many classes was weird and reminded me of [inline styling](https://tailwindcss.com/docs/utility-first#why-not-just-use-inline-styles).

> Classes should be the glue that connects your HTML, CSS, and JavaScript together. In my experience
> they’re are the easiest and best way to connect the three technologies without intermingling them too
> much.
> — <cite>Philip Walton[^1]</cite>

[^1]: [Decoupling Your HTML, CSS, and JavaScript](https://philipwalton.com/articles/decoupling-html-css-and-javascript/)

However, times are changing and with them the way our HTML, CSS and JavaScript are connected. This opens up the possibility of changing the role that classes have in our projects, and the utility-first approach fits perfectly in our modern, JavaScript based era. Today I really appreciate Tailwind CSS and sometimes wonder how we managed without it for so long.

### Tailwind isn't the new Bootstrap

> Most CSS frameworks do too much.
> <cite>[^2]</cite>

[^2]: [Tailwind CSS v1.x Documentation](https://v1.tailwindcss.com/)

Traditional CSS frameworks such as Bootstrap provide the user with a number of prepackaged features like components and layout systems. This is not the case with Tailwind, since it doesn't ship with a single prepackaged component. Both aim to make the developer's life easier, but they differ in the way they do it: traditional frameworks try to make you *avoid* CSS and its complexities, whereas Tailwind CSS wants to *change* the way you write it. For this reason I don't see Tailwind CSS and Bootstrap, or Tailwind CSS and Semantic UI just to name a few, as competitors.  
If you're interested on prepackaged components created by the Tailwind CSS team, check out [Tailwind UI](https://tailwindui.com/).

## Getting started

I won't cover the setup process of Tailwind CSS since the team made a really great job writing the [official documentation](https://tailwindcss.com/docs/installation). Instead, I will focus on the two fundamental aspects of learning how to use Tailwind: its **core concepts** and the **customization**. You will find this subdivision in the official documentation too.

## Core concepts

Being a utility classes generator, the most important part of learning how to use Tailwind CSS is actually using its classes, getting used to the utility-first approach and letting go of the old habits.  
Let's say you want to style a simple button.

{{< highlight html >}}
<button class="btn"> Example </button>
{{< /highlight >}}

A traditional approach would look like this:

{{< highlight css >}}
.btn {
    display: inline-block;
    border: 1px solid #34D399;
    background-color: transparent;
    border-radius: 0.375rem;
    padding: 0.5rem 1.5rem;
    color: #34D399;
    line-height: 1;
    cursor: pointer;
    text-decoration: none;
    transition: background-color 300ms, color 300ms;
}

.btn:hover {
    background-color: #34D399;
    color: #FFF;
}
{{< /highlight >}}

With Tailwind CSS, this button can be recreated without writing a single line of CSS, using a bunch of low level utility classes instead:

{{< highlight html >}}
<button class="inline-block border border-green-400 bg-transparent rounded-md py-2 px-6 text-green-400 leading-none cursor-pointer hover:bg-green-400 hover:text-white transition-colors duration-300">
    Example
</button>
{{< /highlight >}}

If you think this is an *atrocity*, your reaction is quite normal and even described in the [official documentation](https://tailwindcss.com/docs/utility-first)! But after you get used to it, it gets better. The aesthetic side is probably the biggest flaw of the utility-first approach: from now on there will be only advantages.

As you can see in the example above, lots of classes are used to style the exact same button as before, but each class manages one or a few CSS properties if these get often used together.
These classes do exactly what they're named after describes: `inline-block` sets the CSS `display` property to `display: inline-block;`, `bg-transparent` sets the `background-color` property to `background-color: transparent;` and `cursor-pointer`, you guessed it, sets `cursor` to `cursor: pointer;`.

Some classes are less straightforward, like `py-2` that manages vertical padding and `px-6` that manages horizontal padding. Some other sets more than one property like `transition-colors`:

{{< highlight css >}}
.transition-colors {
	transition-property: background-color,border-color,color,fill,stroke;
	transition-timing-function: cubic-bezier(.4,0,.2,1);
	transition-duration: 150ms;
}
{{< /highlight >}}

Learning who does what is a matter of experience, going back and forth in the documentation until you learn most of the naming conventions, but the basic concept is always the same. Aside from the basics, customization and plugins, all the chapters of the documentation are devoted to explaining the names and the defaults of the classes Tailwind generates, covering pretty much every common — and even some less common — CSS property.

### Variants

You might have noticed some weird classes among all the others: `hover:bg-green-400` and `hover:text-white`. This colon notation is what Tailwind uses to activate a class only when a certain condition is met. In this case, we wanted the classes `bg-green-400` and `text-white` to be applied only on hover. The classes resulting are called [**variants**](https://tailwindcss.com/docs/configuring-variants) and the notation stays the same for every kind of state change: `condition:class`. There are variants for hover, focus, active and other element state changes, and even variants for the [dark mode](https://tailwindcss.com/docs/dark-mode), officially supported from Tailwind CSS 2.0 and beyond.

While all of them are useful, the most important variants are the **responsive** variants.

### Responsive Design

Tailwind CSS is responsive by default, and this means that every class it generates has variants to be applied only when certain media queries match. By default, Tailwind is **mobile first**: all of its media queries are of the `min-width` type.
Each class gets a variant for every breakpoint: for example, you have the `sm` breakpoint that corresponds to `640px`. So, if you'd want to apply the class `text-white` only from a screen width of `640px` and above, you'd write `sm:text-white`.  
You can combine responsive and state variants, for example having `sm:hover:text-white`.

### Functions and Directives

If you include Tailwind CSS in your build process, for example as a PostCSS plugin, you will be able to extend your custom CSS using special Tailwind [functions and directives](https://tailwindcss.com/docs/functions-and-directives).

#### Directives

Tailwind directives are special declarations to perform various activities, like generating variants for some classes using the `@variants` directive or using one of Tailwind media queries with the `@screen` directive. Special attention is required for the `@apply` directive. This directive allows you to use your Tailwind utility classes inside your custom styles:

{{< highlight css >}}
.btn {
    @apply inline-block border border-green-400 bg-transparent rounded-md; // And so on...
}
{{< /highlight >}}

But what it really does is to apply every rule your classes refer to, one by one, defeating the whole point of Tailwind. It was in fact mainly created to have some kind of bridge, a middle point between utility-first and traditional styling, but [its usage is not recommended by Tailwind's very creator](https://twitter.com/adamwathan/status/1226511611592085504).

The only recommended use case is when you have to [extract a component](https://tailwindcss.com/docs/extracting-components), meaning that you very often find yourself using the same, many utility classes always together and find convenient to just create a wrapper class. Think of a project full of buttons like the one in the example above: instead of always repeating the same fourteen classes, you can just declare a `.btn` class and `@apply` them.

#### Functions

At the time of writing, the only function Tailwind exposes to your CSS is the [theme](https://tailwindcss.com/docs/functions-and-directives#theme) function. You can use it to read a parameter from the Tailwind configuration file (we'll see it in the next section), be it a color or a font size. For example, you can use it like this:

{{< highlight css >}}
.btn {
    border-color: theme('colors.green.400');
}
{{< /highlight >}}

When you provide the parameter to read to the `theme()` function, remember that you are directly reading from your configuration file, and the configuration file is a JavaScript object; for this reason you should access your parameters using the dot notation when necessary.

Let's now discuss the Tailwind CSS configuration file.

## Customization

The default Tailwind CSS settings are great for very generic use cases, but if your projects demands it you'll have to tweak and customize the utility classes according to your needs. There are usually two [configuration files](https://tailwindcss.com/docs/configuration) in a Tailwind project: the one the framework uses internally and the `tailwind.config.js` file you can **optionally** create at the root of your project. Every time you build your project, before generating all the utility classes, Tailwind looks for a custom configuration file and when found it tries to merge it with the internal configuration that serves as a fallback for the parameters you didn't specify. For this reason, your custom configuration file can specify the settings to generate only a few classes, but all of Tailwind default classes will keep working if you didn't specify anything about them.

### File structure

Every Tailwind CSS configuration file has at least these parameters:

{{< highlight javascript >}}
module.exports = {
  purge: [],
  presets: [],
  darkMode: false, // or 'media' or 'class'
  theme: {
    screens: {},
    colors: {},
    spacing: {},
    /* etc. */
  },
  variantOrder: [
    'first',
    'last',
    'odd',
    /* etc. */
  ],
  variants: {
    accessibility: ['responsive', 'focus-within', 'focus'],
    alignContent: ['responsive'],
    alignItems: ['responsive'],
    /* etc. */
  },
  plugins: [],
}

{{< /highlight >}}

Some of the settings such as [presets](https://tailwindcss.com/docs/configuration#presets) aren't related to utility class customization. The [darkMode](https://tailwindcss.com/docs/dark-mode) parameter allows you to enable dark mode variant for your classes, [plugins](https://tailwindcss.com/docs/configuration#plugins) allow you to extend Tailwind with more features and utility classes such as [Tailwind Typography](https://github.com/tailwindlabs/tailwindcss-typography), useful for markdown generated content styling. There are more settings and the official documentation describes them in detail, but the most important are [theme](https://tailwindcss.com/docs/theme), [variants](https://tailwindcss.com/docs/configuring-variants) and [purge](https://tailwindcss.com/docs/optimizing-for-production#purge-css-options).

#### Theme

The `theme` parameter is where most of the customization happens. Here you will be able to customize your color palette, responsiveness and container settings, spacing utilities or even the [*placeholder opacity*](https://tailwindcss.com/docs/placeholder-opacity) utilities.  
The most common utilities to change are [breakpoints](https://tailwindcss.com/docs/breakpoints), [color palette](https://tailwindcss.com/docs/customizing-colors) and [spacing](https://tailwindcss.com/docs/customizing-spacing).

##### Customizing breakpoints

Project's **breakpoints** are managed in the `screens` object.

{{< highlight javascript >}}
module.exports = {
  theme: {
    screens: {
      sm: '640px',
      md: '768px',
      lg: '1024px',
      xl: '1280px',
      '2xl': '1536px',
    },
  },
}

{{< /highlight >}}

By default Tailwind doesn't generate only the normal version of a utility, for example `text-white`, but also a responsive variant for every breakpoint specified inside the `screens` object: `sm:text-white`, `md:text-white`, `xl:text-white`...  
You can include more or less breakpoints, and the `screens` object supports various degrees of customization as for example, using desktop-first *max-width* media queries, or range media queries using *both min and max-width*. You can find all the details on the official documentation.

##### Customizing color palette

The **color palette** is managed inside the `colors` object.

{{< highlight javascript >}}
module.exports = {
  theme: {
    colors: {
      transparent: 'transparent',
      current: 'currentColor',
      teal: {
        50: '#f0fdfa',
        100: '#ccfbf1',
        200: '#99f6e4',
      },
      emerald: {
        50: '#ecfdf5',
        100: '#d1fae5',
        200: '#a7f3d0',
      },
      /* ...and so on */
    },
  },
}

{{< /highlight >}}

When you provide a **string** parameter Tailwind will generate all the color-related utilities for that color, such as `bg-transparent`, `border-transparent` etc.  
When you provide an **object**, the utilities will be "nested" like in `bg-teal-50`, `text-emerald-200`. You can also provide a special `DEFAULT` value inside your object, and Tailwind will generate a "non-nested" version of that color:

{{< highlight javascript >}}
module.exports = {
  theme: {
    colors: {
      emerald: {
        DEFAULT: '#059669', // Generates bg-emerald, text-emerald, border-emerald...
        50: '#ecfdf5',
        100: '#d1fae5',
        200: '#a7f3d0',
      },
    },
  },
}

{{< /highlight >}}

The same nesting logic applies to almost all the utilities supported by Tailwind.

Note that everything is based on objects: this is why you have to use the dot notation when accessing nested utilities from your custom CSS using the `theme()` function.

##### Customizing spacing

The **spacing** object inside the Tailwind configuration doesn't generate any utility by itself; it is a setting object many real utilities inherit from by default, as you can see in the [default configuration](https://tailwindcss.com/docs/configuration#scaffolding-the-entire-default-configuration):

{{< highlight javascript >}}
module.exports = {
  theme: {
    margin: (theme, { negative }) => ({
      auto: 'auto',
      ...theme('spacing'),
      ...negative(theme('spacing')),
    }),
    padding: (theme) => theme('spacing'),
    width: (theme) => ({
      auto: 'auto',
      ...theme('spacing'),
      '1/2': '50%',
      /* ...and so on */
    }),
  },
}

{{< /highlight >}}

Its usage is very simple, just modify the key/value pairs according to your needs and all the spacing related utilities such as `margin` or `padding` will inherit these values by default.

{{< highlight javascript >}}
module.exports = {
  theme: {
    spacing: {
      px: '1px',
      0: '0px',
      0.5: '0.125rem',
      1: '0.25rem',
      1.5: '0.375rem',
      2: '0.5rem',
      2.5: '0.625rem',
      3: '0.75rem',
      /* ...and so on */
    },
  },
}

{{< /highlight >}}

##### Overwrite or extend

When customizing your theme you have the possibility to both **extend** or **overwrite** Tailwind's default values for every utility you customize.

By default, when you are setting an utility inside the `theme` object, you are overriding the defaults. Take for example [transition-duration](https://tailwindcss.com/docs/transition-duration). Inside the default configuration file, its values are:

{{< highlight javascript >}}
module.exports = {
  theme: {
    transitionDuration: {
      DEFAULT: '150ms',
      75: '75ms',
      100: '100ms',
      150: '150ms',
      200: '200ms',
      300: '300ms',
      500: '500ms',
      700: '700ms',
      1000: '1000ms',
    },
  },
}

{{< /highlight >}}

This will allow you to use classes such as `duration-300` to declare a `transition-duration` of `300ms` just as the setting defines. If inside your custom `tailwind.config.js` file you declare

{{< highlight javascript >}}
module.exports = {
  theme: {
    transitionDuration: {
      2000: '2000ms',
    },
  },
}

{{< /highlight >}}

Tailwind will generate the `duration-2000` class setting the `transition-duration` to `2000ms`, but you will also lose all the other classes such as `duration-300` or the default `duration` class for a `transition-duration` of `150ms`. I actually prefer this approach, because this way Tailwind CSS will only generate the classes I actually use, which can lead to performance improvements during development mode.

If, in the example above, the default values were fine, you could extend them. Every utility you want to extend has to be inside the special `extend` object. Let's add a `2000ms` `transition-duration` by extending the default utilities instead of replacing them:

{{< highlight javascript >}}
module.exports = {
  theme: {
    /* ... overwriting utilities */
    extend: {
      transitionDuration: {
        2000: '2000ms',
      },
    }
  },
}

{{< /highlight >}}

This way you could use the `duration-2000` class without losing `duration-300` and all the other default utilities.


#### Variants

Many [variants](https://tailwindcss.com/docs/configuring-variants) can be generated for every utility: `hover`, `visited`, `focus`, `checked`, `active`, `odd`, `even`... Generating all the possible variants for every utility would lead to thousands useless classes, a slow build process, huge CSS file in development mode and lots of useless styles to purge for production. For this reason the only always enabled variant by default is the `responsive` variant, while all the others are activated by default only where you would expect to find them (for example the `hover` variant for the `backgroundColor` utilities).

Every property in the `variants` object must have a utility name as key and an array of enabled variants as value:

{{< highlight javascript >}}
module.exports = {
  variants: {
    accessibility: ['responsive', 'focus-within', 'focus'],
    alignContent: ['responsive'],
    alignItems: ['responsive'],
  },
}

{{< /highlight >}}

As in for `theme`, when customizing your `variants` you have the possibility to both overwrite or extend the settings for your utilities:

{{< highlight javascript >}}
module.exports = {
  variants: {
    // The 'active' variant will be generated in addition to the defaults
    extend: {
      backgroundColor: ['active']
    }
  },
}

{{< /highlight >}}

One important thing to know about variants is that **the order in which you specify them matters**. Variants are defined by an array, and their order inside the array determines the position of the relative classes inside the final stylesheet. This is important because an element, for example, can be under both `active` and `focus` conditions at the same time: the classes that take precedence aren't determined by the order in which you type them in your HTML elements, but rather by the order the classes have inside the final CSS. You can read more about this topic [here](https://tailwindcss.com/docs/configuring-variants#ordering-variants).

When overwriting variants you have full control over the array for a given utility, but you don't when you are extending them. Variants you add by extension are automatically sorted by Tailwind respecting an internal order that you can customize using the [variantOrder](https://tailwindcss.com/docs/configuration#variant-order) parameter.

#### Purge

By default, Tailwind generates so many classes that the final uncompressed CSS weight reaches [3739.4 kB](https://tailwindcss.com/docs/optimizing-for-production) and that's *huge*. You could carefully pick [which utility to enable or disable](https://tailwindcss.com/docs/configuration#core-plugins), disable all the unused variants and less common breakpoints, but eventually you would still need to **purge** all the classes and variants you didn't use.  
Tailwind CSS uses [PurgeCSS](https://purgecss.com/) to tree-shake unused styles and get a much smaller final CSS. By default, PurgeCSS is run only in production mode.

The configuration file exposes the [purge parameter](https://tailwindcss.com/docs/optimizing-for-production#removing-unused-css) you can customize according to your needs. To get started, you can provide a simple array of paths of every file using Tailwind CSS utilities, so that PurgeCSS can detect which classes to keep and what to remove:

{{< highlight javascript >}}
module.exports = {
  purge: [
    './src/**/*.html',
    './src/**/*.vue',
    './src/**/*.jsx',
  ],
  theme: {},
  variants: {},
  plugins: [],
}

{{< /highlight >}}

It's important to include *every possibile file* referencing one of Tailwind's utilities by name, for example a JavaScript file dynamically toggling some classes; if you don't, PurgeCSS won't see those classes are being used somewhere and will delete them if not used anywhere else.

#### Other settings

There are some other settings you can use to tweak your utilities. You can [mark all the utilities as important](https://tailwindcss.com/docs/configuration#important), [change the colon notation](https://tailwindcss.com/docs/configuration#separator) to separate the condition from the class for variants and [disable entire subsets of utilities](https://tailwindcss.com/docs/configuration#core-plugins) if you know you'll never use them.


## Useful practices

When starting a new Tailwind CSS project the first thing to do after framework installation is usually tweaking the configuration file, adapting the utilities to the new project's needs. In an ideal case, you know all the spacings, typography settings and color palette *before* creating your components. In reality, this rarely happens and you will find yourself constantly tweaking the configuration file — and therefore regenerating all the utilities — until most of the project is complete. There are some practices I find useful that can make your colors, spacing and typography setting, your development build speed and ultimately your life easier.

### Sorting colors

Tailwind's default palette is beautiful, but most projects will require to replace it with a custom one. When customizing colors I find useful to keep using Tailwind's default numbered notation grouping colors by shade. To sort the colors from light to dark just as in the default palette I use [this great tool](https://elektrobild.org/tools/sort-colors) by [elektrobild.org](https://elektrobild.org/tools).

### Setting spacings

In an ideal design system, all spacings are consistent with each other and a few dozen parameters are enough. But even in the most coherent systems, knowing *all* the spacings before writing your components is almost impossible and would require meticulous analysis. This is why I almost never try to recreate Tailwind's default spacing classification using arbitrary numbers in a pretty scale covering all my spacing needs.

What I do instead is to define every spacing with its exact value as spacing name while I encounter it in the design, to come back only when most of the project is over and then evaluate if it's the case to adapt and simplify my spacing classes.

{{< highlight javascript >}}

/* This is ideal... */
module.exports = {
  theme: {
    spacing: {
      28: '7rem',
      32: '8rem',
      36: '9rem',
      40: '10rem',
    },
  },
}

/* This is reality! Many more classes, but often you can optimize them in the end. */
module.exports = {
  theme: {
    spacing: {
      16: '16px',
      24: '24px',
      32: '32px',
      64: '64px',
    },
  },
}

{{< /highlight >}}

### Setting typography

From the Tailwind CSS 2.0 version most of typography customization is managed inside the `fontSize` parameter where you can define categories of typography sizing acting on the `font-size` and the `line-height` at the same time:

{{< highlight javascript >}}
module.exports = {
  theme: {
    fontSize: {
      xs: ['0.75rem', { lineHeight: '1rem' }],
      sm: ['0.875rem', { lineHeight: '1.25rem' }],
      base: ['1rem', { lineHeight: '1.5rem' }],
      lg: ['1.125rem', { lineHeight: '1.75rem' }],
      xl: ['1.25rem', { lineHeight: '1.75rem' }],
    },
  },
}

{{< /highlight >}}

But if your project makes it harder to define a typography scale just like this, you can follow the same approach described above for spacing.

### Disabling unused utilities in development mode

When using TailwindCSS, the only real optimization comes in production mode when the generated stylesheets get processed by PurgeCSS to get a way lighter final CSS. When in development mode PurgeCSS doesn't activate (and it's not recommended to change this behaviour, your build process would get much slower) so you'll have a big CSS file containing every customized and default utility. But there's more! Every time you modify a parameter in your custom configuration file, Tailwind will generate *all* the classes again.

Since you'll easily find yourself going back and forth through the configuration file changing one parameter at a time, especially at the beginning of a project, it's useful to disable almost *every* utility functionality and then enable them back again as you need in the project.  
You can disable utility functionalities in the [corePlugins](https://tailwindcss.com/docs/configuration#core-plugins) section of the configuration file.

{{< highlight javascript >}}
module.exports = {
  corePlugins: {
    float: false,
    objectFit: false,
    objectPosition: false,
    /* and so on */
  }
}

{{< /highlight >}}

This way every time you save Tailwind will generate many more classes, and there will be less final code to purge when building.

## Final considerations

That's it! This should be enough to get started and get your own opinion of this framework, the utility-first approach and better practices to suit your needs. There's much more to learn, but [Tailwind's official documentation](https://tailwindcss.com/docs) is one of the best curated.

If you like Tailwind CSS check out the team's other projects like [Tailwind UI](https://tailwindui.com/) and [Tailwind Typography](https://github.com/tailwindlabs/tailwindcss-typography).