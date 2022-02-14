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

### Web Server Configuration

**Activate GZIP Compression**

Gzip kompression muss oft explizit in der Config vom Server (z.B. nginx, apache) aktiviert werden. Dadurch können sehr einfach große Einsparungen in der Größe der übertragenden Daten erzielt werden.

### Image/Picture Rendering

**Use WebP format**

Images are often responsible for most of the traffic. By using the [WebP](https://developers.google.com/speed/webp) format, you can compress graphics lossy or lossless, such that they are 30% smaller than PNGs or JPGs.

By using the `<picture>` tag, you can support fallbacks for older browsers.

**Reduce colors in images**

For quite some PNG or GIF images, you can drastically reduce the number of colors until you notice a visual difference. Sometimes, 6 or 4 colors are enough, sometimes 32 or 16. With this trick, you can reduce up to 90% of the file size.

