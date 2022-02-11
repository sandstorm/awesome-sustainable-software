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

- [Karlskrona Manifesto](https://www.sustainabilitydesign.org/karlskrona-manifesto/)

  This paper states the different responsibilities of software designers regarding
  sustainability. It is helpful as a general framework to understand the different
  dimensions of sustainability.



## Practices

### Docker and Containerization

**Reducing Docker Image Size**

Often, docker images are quite big in terms of image size - more than 1 GB is pretty common in "classical applications".

- Use the tool [dive](https://github.com/wagoodman/dive) to analyze docker image size.
- Try to reduce the number of image layers and installed packages.
