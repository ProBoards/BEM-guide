# BEM-guide

The purpose of this document is to provide guidelines for writing HTML class names. Code conventions are important for the long-term maintainability of code. Most of the time, developers are maintaining code, either their own or someone else’s. The goal is to have everyone’s code look the same, which allows any developer to easily work on another developer’s code.

Here are the articles which collectively inspired this guide:

* http://nicolasgallagher.com/about-html-semantics-front-end-architecture/
* http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/
* http://csswizardry.com/2015/03/more-transparent-ui-code-with-namespaces/
* http://csswizardry.com/2012/06/the-open-closed-principle-applied-to-css/
* http://www.stubbornella.org/content/2010/07/01/top-5-mistakes-of-massive-css/

### Class Names

```
.block {} // represents the higher level of an abstraction or component
.block__element {} // represents a descendent of .block that helps form .block as a whole
.block--modifier {} // represents a different state or version of .block
```

The reason for double rather than single hyphens and underscores is so that your block itself can be hyphen delimited, for example:

```
.site-search {} // Block
.site-search__field {} // Element
.site-search--full {} // Modifier
```

#### Analogy

In case you're having trouble figuring out whether something is an element or a modifier, here is a handy analogy using the same syntax (and also an example of how you can compose the two):

```
.person {}
.person__hand {}
.person--female {}
.person--female__hand {}
.person__hand--left {}
```

#### To BEM, or not to BEM?
<em>(Taken directly from http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)</em>

When you are using BEM, though, it is important to remember that you don't need to use it for everything. Take for example:

```
.caps { text-transform: uppercase; }
```

This CSS would never fall into any BEM category, it's merely a standalone rule.

Another example of code which isn't BEM:

```
.site-logo {}
```

Here we have our logo; it could be BEMmed up like so:

```
.header {}
.header__logo {}
```

But that is unecessary. The trick with BEM is knowing when something falls into a relevant category. Just because something happens to live inside a block it doesn't always mean is is actually a BEM element. In the case of our site logo it lives in the .header purely coincidentally; it could just as easily be in our sidebar or footer. An element's scope can start in any context, so you need to make sure you only apply BEM as far as you need to. Another example:

```
<div class="content">
    <h1 class="content__headline">Lorem ipsum dolor...</h1>
</div>
```

Here we might be able to just call the second class .headline; it depends on if it is styled that way because it's in .content, or whether it just happens to live in .content. If it is the latter then we do not need BEM.

Everything is potentially open to moving into BEM territory, though. Taking our .site-logo example again, imagine that we want to have a festive version of the logo for our Christmassy site design. We could have:

```
.site-logo {}
.site-logo--xmas {}
```

We can quickly build variations of things by using the -- modifier notation.

One of the hardest parts of BEM is deciding when to start and stop scope, and when (or not) to use it. It's a case of 'you'll just know when you know'.

### Namespacing

We're going to use namespacing to help overcome some of the issues introduced by using a primarily flat nesting structure for our CSS, as suggested by the OOCSS guide.  Not everything has to be namespaced, but anything that falls into one of these categories should be:

* <strong>o-</strong>: Signify that something is an Object, and that it may be used in any number of unrelated contexts to the one you can currently see it in. Making modifications to these types of class could potentially have knock-on effects in a lot of other unrelated places. Tread carefully.
* <strong>c-</strong>: Signify that something is a Component. This is a concrete, implementation-specific piece of UI. All of the changes you make to its styles should be detectable in the context you’re currently looking at. Modifying these styles should be safe and have no side effects.
* <strong>u-</strong>: Signify that this class is a Utility class. It has a very specific role (often providing only one declaration) and should not be bound onto or changed. It can be reused and is not tied to any specific piece of UI. You will probably recognise this namespace from libraries and methodologies like SUIT.
* <strong>t-</strong>: Signify that a class is responsible for adding a Theme to a view. It lets us know that UI Components’ current cosmetic appearance may be due to the presence of a theme.
* <strong>s-</strong>: Signify that a class creates a new styling context or Scope. Similar to a Theme, but not necessarily cosmetic, these should be used sparingly—they can be open to abuse and lead to poor CSS if not used wisely.
* <strong>is-, has-</strong>: Signify that the piece of UI in question is currently styled a certain way because of a state or condition. This stateful namespace is gorgeous, and comes from SMACSS. It tells us that the DOM currently has a temporary, optional, or short-lived style applied to it due to a certain state being invoked.
* <strong>_</strong>: Signify that this class is the worst of the worst—a hack! Sometimes, although incredibly rarely, we need to add a class in our markup in order to force something to work. If we do this, we need to let others know that this class is less than ideal, and hopefully temporary (i.e. do not bind onto this).
* <strong>js-</strong>: Signify that this piece of the DOM has some behaviour acting upon it, and that JavaScript binds onto it to provide that behaviour. If you’re not a developer working with JavaScript, leave these well alone.
* <strong>qa-</strong>: Signify that a QA or Test Engineering team is running an automated UI test which needs to find or bind onto these parts of the DOM. Like the JavaScript namespace, this basically just reserves hooks in the DOM for non-CSS purposes.

For example usage of these classes, check out this article: http://csswizardry.com/2015/03/more-transparent-ui-code-with-namespaces/






