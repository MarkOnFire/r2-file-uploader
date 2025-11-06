[Skip to main content](https://docs.ghost.org/themes#content-area)
[Ghost Developer Docs home page![light logo](https://mintcdn.com/ghost/aGR3I5_lq1oxakuc/logo/light.png?fit=max&auto=format&n=aGR3I5_lq1oxakuc&q=85&s=21b0a8eb2cb31ff62e99362023cc2de7)![dark logo](https://mintcdn.com/ghost/aGR3I5_lq1oxakuc/logo/dark.png?fit=max&auto=format&n=aGR3I5_lq1oxakuc&q=85&s=bf70847c5fb515f7414edad80653b09d)](https://ghost.org/)
Search...
⌘K
  * [Sign in](https://account.ghost.org/signin/)
  * [Get Started](https://account.ghost.org/signup/)
  * [Get Started](https://account.ghost.org/signup/)


Search...
Navigation
Themes
Ghost Handlebars Themes
[Home](https://docs.ghost.org/)[Documentation](https://docs.ghost.org/introduction)[Migration Guides](https://docs.ghost.org/migration)
  * [](https://ghost.org/tutorials/)
  * [](https://forum.ghost.org/)


##### Getting Started
  * [Introduction](https://docs.ghost.org/introduction)
  * [Installation](https://docs.ghost.org/install)
  * [Hosting Guide](https://docs.ghost.org/hosting)
  * [Updates & Versions](https://docs.ghost.org/update)


##### Core Concepts
  * [Overview](https://docs.ghost.org/product)
  * [Architecture](https://docs.ghost.org/architecture)
  * [Configuration](https://docs.ghost.org/config)
  * [Staff Users](https://docs.ghost.org/staff)
  * [Publishing](https://docs.ghost.org/publishing)
  * [Memberships](https://docs.ghost.org/members)
  * [Recommendations](https://docs.ghost.org/recommendations)
  * [Newsletters](https://docs.ghost.org/newsletters)
  * [Security](https://docs.ghost.org/security)


##### Themes
  * [Overview](https://docs.ghost.org/themes)
  * [Structure](https://docs.ghost.org/themes/structure)
  * Contexts
  * [Assets](https://docs.ghost.org/themes/assets)
  * Helpers
  * [Content](https://docs.ghost.org/themes/content)
  * [Search](https://docs.ghost.org/themes/search)
  * [Members](https://docs.ghost.org/themes/members)
  * [Routing](https://docs.ghost.org/themes/routing)
  * [Custom Settings](https://docs.ghost.org/themes/custom-settings)
  * [GScan](https://docs.ghost.org/themes/gscan)


##### Advanced Tools
  * [Ghost CLI](https://docs.ghost.org/ghost-cli)
  * Content API
  * Admin API
  * JAMstack
  * [Webhooks](https://docs.ghost.org/webhooks)


##### Resources
  * [FAQ](https://docs.ghost.org/faq)
  * [Breaking Changes](https://docs.ghost.org/changes)
  * [Contributing](https://docs.ghost.org/contributing)
  * [LLM](https://docs.ghost.org/llm)
  * [License](https://docs.ghost.org/license)
  * [Logos](https://docs.ghost.org/logos)
  * [Trademark](https://ghost.org/trademark)


On this page
  * [Theme development](https://docs.ghost.org/themes#theme-development)
  * [Handlebars](https://docs.ghost.org/themes#handlebars)
  * [Custom settings](https://docs.ghost.org/themes#custom-settings)
  * [GScan](https://docs.ghost.org/themes#gscan)
  * [Command line](https://docs.ghost.org/themes#command-line)
  * [What’s next?](https://docs.ghost.org/themes#what%E2%80%99s-next%3F)


[Themes](https://docs.ghost.org/themes)
# Ghost Handlebars Themes
The Ghost theme layer has been engineered to give developers and designers the flexibility to build custom publications that are powered by the Ghost platform.
* * *
## 
[​](https://docs.ghost.org/themes#theme-development)
Theme development
Ghost themes use the Handlebars templating language which creates a strong separation between templates (the HTML) and any JavaScript logic with the use of helpers. This allows themes to be super fast, with a dynamic client side app, and server side publication content that is sent to the browser as static HTML. Ghost also makes use of an additional library called `express-hbs` which adds some additional features to Handlebars, such as layouts and partials. If you’ve previously built themes for other popular platforms, working with the Ghost theme layer is extremely accessible. This documentation gives you the tools required to create static HTML and CSS for a theme, using Handlebars expressions when you need to render dynamic data. Our tutorial on the [essential concepts to known when building a Ghost theme](https://ghost.org/tutorials/essential-concepts/), provides a fantastic introduction to everything you need to know to start building beautiful themes.
## 
[​](https://docs.ghost.org/themes#handlebars)
Handlebars
The Handlebars templating language provides the power to build semantic templates effectively.
  * [Handlebars documentation](https://handlebarsjs.com/guide/expressions.html)

Installation of Handlebars is already done for you in Ghost ✨
## 
[​](https://docs.ghost.org/themes#custom-settings)
Custom settings
Offering customization options to theme users can be done using custom settings. This allows theme developers to empower non-developers to make controlled changes. Head to the [Custom settings documentation](https://docs.ghost.org/themes/custom-settings) to learn more.
## 
[​](https://docs.ghost.org/themes#gscan)
GScan
Validating your Ghost theme is handled efficiently with the [GScan tool](https://gscan.ghost.org/). GScan will check your theme for errors, deprecations and compatibility issues.
  * The [GScan site](https://gscan.ghost.org/) is your first port of call to test any themes that you’re building to get a full validation report
  * When a theme is uploaded in Ghost admin, it will automatically be checked with `gscan` and any fatal errors will prevent the theme from being used
  * `gscan` is also used as a command line tool


### 
[​](https://docs.ghost.org/themes#command-line)
Command line
To use GScan as a command line tool, globally install the `gscan` npm package:
Copy
Ask AI
```
# Install the npm package
npm install -g gscan
# Use gscan <file path> anywhere to run gscan against a folder
gscan /path/to/ghost/content/themes/casper
# Run gscan on a zip file
gscan -z /path/to/download/theme.zip

```

## 
[​](https://docs.ghost.org/themes#what%E2%80%99s-next%3F)
What’s next?
That’s all of the background context required to get started. From here, take a look at the [structure](https://docs.ghost.org/themes/structure) of Ghost themes and templates, and learn everything you need to know about the `package.json` file. For community led support about theme development, visit [the forum](https://forum.ghost.org/c/themes/).
[Security](https://docs.ghost.org/security)[Structure](https://docs.ghost.org/themes/structure)
⌘I
[github](https://github.com/tryghost/ghost)[twitter](https://twitter.com/ghost)[bluesky](https://bsky.app/profile/ghost.org)[reddit](https://www.reddit.com/r/ghost)
[Powered by Mintlify](https://www.mintlify.com?utm_campaign=poweredBy&utm_medium=referral&utm_source=ghost)
