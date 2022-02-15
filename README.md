# Awesome Sustainable Software Development

# About

In this list, we want to collect links, resources, and tips towards sustainable software developent.

We especially want to highlight practical real-world tips which are directly applicable in practice.

## Supported with ❤️ by [sandstorm](https://sandstorm.de)

We are currently on our journey towards estabilishing sustainability goals and principles in our day-to-day work - and we want to
collaborate with others and form a community around this.

# Content

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

## Practices

### Docker and Containerization

**Reducing Docker Image Size**

Often, docker images are quite big in terms of image size - more than 1 GB is pretty common in "classical applications".

- Use the tool [dive](https://github.com/wagoodman/dive) to analyze docker image size.
- Try to reduce the number of image layers and installed packages.

### Web Server Configuration

**Activate GZIP Compression**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

Gzip compression needs to be explicitly activated in the server config (nginx/apache). With this, you can easily reach big improvements for transferred data, especially for text-like content.

**Configure HTTP Caching**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

By leveraging and properly configuring HTTP caching, you can also reduce data sizes quite a lot.

Common practices include:

- static assets (like JS/CSS) should be cached for a very long time, and include a cache-bust mechanism
- f.e. in Neos CMS, Images are stored content-addressed (i.e. the URL changes if the image contents change) - in this case, these assets can be also cached for a very long time.
- HTML pages should NOT have caching enabled, as this makes changing cached pages impossible during the cache lifetime.

**Minify JS/CSS**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

JS/CSS/SCSS should be minified during the build. During this process, comments, white spaces etc are removed - and multiple scripts are concatenated to one big file (which is positive for compression ratios etc).


### Image/Picture Rendering

**Use WebP format**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

Images are often responsible for most of the traffic. By using the [WebP](https://developers.google.com/speed/webp) format, you can compress graphics lossy or lossless, such that they are 30% smaller than PNGs or JPGs.

By using the `<picture>` tag, you can support fallbacks for older browsers.

**Reduce colors in images**

![](https://badgen.net/badge/Type/NetworkTransmission/purple)

For quite some PNG or GIF images, you can drastically reduce the number of colors until you notice a visual difference. Sometimes, 6 or 4 colors are enough, sometimes 32 or 16. With this trick, you can reduce up to 90% of the file size.


### Application Configuration

**Caching for reducing CPU load**

![](https://badgen.net/badge/Type/CPU/green)
