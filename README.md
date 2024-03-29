# Awesome Sustainable Software Development

# About

In this list, we want to collect links, resources, and tips towards sustainable software development.

We especially want to highlight practical real-world tips which are directly applicable in practice.

## Supported with ❤️ by [sandstorm](https://sandstorm.de)

We are currently on our journey towards establishing sustainability goals and principles in our day-to-day work - and we want to
collaborate with others and form a community around this.

# Content

- [Awesome Sustainable Software Development](#awesome-sustainable-software-development)
- [About](#about)
  - [Supported with ❤️ by sandstorm](#supported-with-️-by-sandstorm)
- [Content](#content)
  - [Practices](#practices)
    - [Docker and Containerization](#docker-and-containerization)
    - [Web Server Configuration](#web-server-configuration)
    - [Rendering](#rendering)
    - [Application Configuration](#application-configuration)
    - [Tracking](#tracking)
    - [Development and Staging](#development-and-staging)
    - [Avoid waste](#avoid-waste)
    - [Hosting](#hosting)
    - [Accessibility](#accessibility)
  - [Knowledge Base](#knowledge-base)
- [Thank You ❤️](#thank-you-%EF%B8%8F)

## Practices

### Docker and Containerization

**Reducing Docker Image Size**

![](https://badgen.net/badge/Type/Storage/purple)

Often, docker images are quite big in terms of image size - more than 1 GB is pretty common in "classical applications".

- Use the tool [dive](https://github.com/wagoodman/dive) to analyze docker image size.
- Try to reduce the number of image layers and installed packages.

**Avoid running apps as root**

![](https://badgen.net/badge/Type/Security/orange)

**Consider Best practices**

![](https://badgen.net/badge/Type/Quality/green)

- Follow [Best practices for writing Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- Follow [Awesome Docker](https://github.com/veggiemonk/awesome-docker#readme)
### Web Server Configuration

**Activate GZIP Compression**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

Gzip compression needs to be explicitly activated in the server config (nginx/apache). With this, you can easily reach big improvements for transferred data, especially for text-like content.

**Configure HTTP Caching**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

By leveraging and properly configuring HTTP caching, you can also reduce data sizes quite a lot.

Common practices include:

- static assets (like JS/CSS) should be cached for a very long time and include a cache-bust mechanism
- f.e. in [Neos CMS](https://neos.io), Images are stored content-addressed (i.e. the URL changes if the image contents changes) - in this case, these assets can be also cached for a very long time.
- HTML pages should _not_ have caching enabled, as this makes changing cached pages impossible during the cache lifetime.

**Minify JS/CSS**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

JS/CSS/SCSS should be minified during the build. During this process, comments, white spaces etc are removed - and multiple scripts are concatenated to one big file (which is positive for compression ratios etc).

### Rendering

**Use WebP format**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

Images are often responsible for most of the traffic. By using the [WebP](https://developers.google.com/speed/webp) format, you can compress graphics lossy or lossless, such that they are 30% smaller than PNGs or JPGs.  
By using the `<picture>` tag, you can support fallbacks for older browsers.

**Optimize your images**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

- use (lossy) compression 
- consider dithering for your images

**Lazyly load offscreen images**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

By loading offscreen images only, when they enter the viewport for the first time, you can drastically reduce the weight of your webpage and save a lot of transferred megabytes. See for example the new [`loading` attribute on image](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img#loading) and iframe tags.
For support of older browsers see javascript solutions (e.g. https://github.com/aFarkas/lazysizes).

**Reduce colors in images**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

For quite some PNG or GIF images, you can drastically reduce the number of colors until you notice a visual difference. Sometimes, 6 or 4 colors are enough, sometimes 32 or 16. With this trick, you can reduce up to 90% of the file size.

**Only use pictures, where relevant**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

Pictures are a major source of traffic. Consider using less pictures, where they are not necessary, or transporting the information through different means (text, colors, …)

**Use videos as little as possible**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

- avoid background videos
- avoid auto-playing videos
- compress your video

**self host your fonts**

![](https://badgen.net/badge/Type/Privacy/cyan)

When embeddings fonts from external font services, user data is passed to external parties. This is bad privacy practice. Opposed to this, self-hosted fonts add to the transmitted data.

**Consider System Fonts**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

System fonts are already installed on your users device and don't need to be downloaded.

**Optimize your font usage**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

- load only the font-weights you need
- use variable fonts as all styles can be embedded into one small file
- use the `woff2` file format, as it is the smallest to date
- create a subset of only the characters you use

### Application Configuration

**Caching for reducing CPU load**

![](https://badgen.net/badge/Type/CPU/green)

**Prefer event pushing over event polling**

![](https://badgen.net/badge/Type/Efficiency/green)

"And now?", "And now?", "And now?", "And now?", "And now?"

**minimize number of requests**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

**minimize number of transmitted bytes**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

- minimize intermediate results
- … apply filter on server (instead of client)
- … or on database
- design APIs based on the user perspective

**cache large results**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

**render only what has changed**

![](https://badgen.net/badge/Type/Efficiency/green)

### Tracking

**use existing metrics**

![](https://badgen.net/badge/Type/Efficiency/green)

Eg use web server logs to count number of visits per page.

**track a sample set only**

![](https://badgen.net/badge/Type/Efficiency/green)

Do you need to track every visitor or one out of 100?

**avoid dark patterns**

![](https://badgen.net/badge/Type/User%20Happiness/green)

For example in cookie banners, make the _accept all_ and _reject all_ button visually/hirarchically equally important. Clearly mark ads. Don't put pressure on your users ("only 3 left", "SALE: 7 hours left", …)

**Think twice before using a pop-up**

![](https://badgen.net/badge/Type/User%20Happiness/green)

Can you inline consent modals for external content? Does your site really need external cookies?

### Development and Staging

**plan for local development**

![](https://badgen.net/badge/Type/Developer%20Happiness/green)

Make your project starts with one or two commands.
Consider using our [Dev Script Runner](https://github.com/sandstorm/dev-script-runner)

**plan for staging environments**

![](https://badgen.net/badge/Type/Developer%20Happiness/green)

**limit execution of CI/CD pipelines**

![](https://badgen.net/badge/Type/Efficiency/green)

- do I need to redeploy on readme changes
- and run E2E tests after typo fixes

**testing**

![](https://badgen.net/badge/Type/Developer%20Happiness/green)
![](https://badgen.net/badge/Type/Efficiency/green)

Make writing tests part of your projects.
Use efficient test scopes (E2E tests versus unit test).

**consider alternatives for tools and libraries when starting a project**

![](https://badgen.net/badge/Type/Developer%20Happiness/green)
![](https://badgen.net/badge/Type/Efficiency/green)

- [spring boot](https://spring.io/projects/spring-boot) or [micronaut](https://micronaut.io/)
- [react](https://reactjs.org/) or [preact](https://preactjs.com/) or [vue](https://vuejs.org/) or [next](https://nextjs.org/)
- [maven](https://maven.apache.org/) or [gradle](https://gradle.org/)
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
- [webpack](https://webpack.js.org/) or [esbuild](https://esbuild.github.io/)
- [node](https://nodejs.org/) or [deno](https://deno.land/)
- [react-native](https://reactnative.dev/) or [flutter](https://flutter.dev/)
- [electron](https://www.electronjs.org/) or [tauri](https://tauri.app/)

**don't use AI for trivial tasks**

![](https://badgen.net/badge/Type/Efficiency/green)

Prefer adequate algorithms.

**readable code**

![](https://badgen.net/badge/Type/Developer%20Happiness/green)

Follow best practices to structure your code, eg

- [Book Review: A Philosophy of Software Design](https://sandstorm.de/de/blog/post/book-review-a-philosophy-of-software-design.html)
- [How to become a better Software Developer](https://sandstorm.de/de/blog/post/how-to-become-a-better-software-developer.html)

**enable others to maintain you project**

![](https://badgen.net/badge/Type/Developer%20Happiness/green)

- aim for open source projects
- do not re-implement things
- pick a license, which allows others to improve/continue the project
- use contracts, which allow your customers to migrate to another agency

**measure and improve quality**

![](https://badgen.net/badge/Type/Developer%20Happiness/green)

> What you can't measure, you can't manage. _(Peter Drucker)_

- use [google lighthouse](https://developer.chrome.com/docs/lighthouse/)
- … or [Pa11y](https://github.com/pa11y/pa11y)
- linting
- [sonarlint](https://www.sonarsource.com/products/sonarlint/)
- TODO: what else

### Avoid waste

**abandon dead projects**

![](https://badgen.net/badge/Type/Sufficiency/blue)

only develop what will be used

**shutdown idle servers**

![](https://badgen.net/badge/Type/Sufficiency/blue)

**shutdown unused services**

![](https://badgen.net/badge/Type/Sufficiency/blue)

scale to zero or terminate

**think of your data retention policy**

![](https://badgen.net/badge/Type/Sufficiency/blue)

delete no longer needed data, ie

- logs and statistics
- old application version
- CI/CD results and artifacts

### Hosting

**co-locate small services**

![](https://badgen.net/badge/Type/Efficiency/green)

eg by using VMs, Kubernetes or serverless computing

**choose green hosters**

![](https://badgen.net/badge/Type/Efficiency/green)

We use [Hetzner](https://www.hetzner.com/unternehmen/umweltschutz/?country=de).

**Use a data centre close to your users**

![](https://badgen.net/badge/Type/Efficiency/green)

**deploy a secure SSH configuration**

![](https://badgen.net/badge/Type/Security/orange)

ie no root and password logins

**plan for regular updates**

![](https://badgen.net/badge/Type/Security/orange)

**throttle metric collection**

![](https://badgen.net/badge/Type/Efficiency/green)

You do not need to check the remaining disk space every minute 😉.

### Accessibility

![](https://badgen.net/badge/Type/Usability/green)

Follow [Awesome Accessibility](https://github.com/brunopulis/awesome-a11y#readme)

## Knowledge Base

Base Research and Knowledge

- [Set of criteria for sustainable software (PDF)](https://www.umwelt-campus.de/fileadmin/Umwelt-Campus/Greensoft/Set-of-Criteria_Sustainable-SW_v01_2017-05-31.pdf)

  This document is the outcome of the first of five work packages in the German Federal Environment Agency's UFOPLAN project “Sustainable software design— 
  Development and application of criteria for resource-efficient software products with consideration of existing methods.
  
- [Article: Sustainable software products—Towards assessment criteria for resource and energy efficiency (PDF)](https://www.umwelt-campus.de/fileadmin/Umwelt-Campus/Greensoft/1-s2.0-S0167739X17314188-main.pdf)
  
  Demonstration of the application of set of criteria, including the definition of standard usage scenarios for chosen categories of software products. Discussion 
  of the practicability of this type of assessment, its acceptability for several stakeholders and potential consequences for the eco-labeling of 
  software products and sustainable software design.
  
- [Blue Angel: Resources and Energy-Efficient Software Products (DE-UZ 215)](https://www.blauer-engel.de/en/productworld/resources-and-energy-efficient-software-products)

  The aim of the environmental label for resource and energy-efficient software products is to reduce the total energy consumed by information and communication 
  technology and improve resource efficiency.

- [Karlskrona Manifesto](https://www.sustainabilitydesign.org/karlskrona-manifesto/)

  This paper states the different responsibilities of software designers regarding sustainability. It is helpful as a general framework to understand the different
  dimensions of sustainability.
  
- [Article: Software and sustainability - how do they fit together? (German)](https://www.informatik-aktuell.de/management-und-recht/digitalisierung/software-und-nachhaltigkeit-wie-passt-das-zusammen.html)

  How is software designed efficiently in the sense of the global sustainability goals and what does that actually mean? What models are there and who supports 
  developers and administrators in implementing them? 

- [Podcast: Das Sandpapier by Sandstorm Media: #42 Sustainable Software (German)](https://sandstorm.de/de/blog/podcast-episodes/folge-42-nachhaltige-software.html)

  Sandstorm developers take a subjective look at sustainable software and evaluate the general and their own state of development. What role does sustainability 
  actually play in software architecture? What are we already doing, what are our as yet unachieved goals, what are our plans and what obstacles still lie in the 
  way?
  
- [Introduction in the Principles of Sustainable Software Engineering, Microsoft](https://docs.microsoft.com/en-us/learn/modules/sustainable-software-engineering-overview/1-introduction)

  Modular overview online course on the eight principles of sustainable software engineering.
  
- [Greenpeace Guide to Greener Electronics, 2017 (PDF)](https://www.greenpeace.de/sites/www.greenpeace.de/files/publications/20171016-greenpeace-guide-greener-electronics-englisch.pdf)

  In 2017, Greenpeace examined the 17 largest manufacturers of consumer electronics with regard to ecological production: How much and what kind of energy is used? 
  Which resources are used in the process and how much? And what chemicals are in the products?
  
- [Article: OpenSource Year Book 2008, OpenSource and Sustainablility, Torsten Busch (p.111-122)(German)](http://www.opensourcejahrbuch.de/download/jb2008/osjb08.pdf)

  The article deals with the role of open source software in terms of economic sustainability and ethics.

- [nachhaltiges-webdesign.jetzt (German)](https://nachhaltiges-webdesign.jetzt/) 

  A collection of methods to create sustainable websites, that looks beyond technical measures at content, SEO, and business approaches.
  
# Thank You ❤️

Thank You [Ole Langbehn @neurolabs](https://github.com/neurolabs) for pointing us towards [nachhaltiges-webdesign.jetzt](https://nachhaltiges-webdesign.jetzt/).