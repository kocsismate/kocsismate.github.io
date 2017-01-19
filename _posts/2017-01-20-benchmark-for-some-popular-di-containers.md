---
layout: post
title: "Benchmark for some popular DI Containers"
date: 2017-01-20 20:00:00
categories: php di benchmark
tags:
image: /assets/2017-10-20-benchmark-for-some-popular-di-containers/container.jpg
---

In 2014, a really interesting benchmark about DI Containers for PHP was [published on Sitepoint][sitepoint-article].
Unfortunately, the [implementation][old-benchmark] of the tests turned out to be quite controversial, so the benchmark
itself wasn't very insightful.

I have been interested in the topic since then so I wanted to finally conduct a better benchmark than the last one was:
I tried to fix its flaws while keeping its many good parts. So here is my take!

If you have any suggestion in mind about the benchmark or you want to add your container to the list, please create an
[Issue or a Pull Request][github-repo].

The containers examined are listed below along with some of their attributes:

I'll try to give a vague definition below for some of the aforementioned notions:

A DI Container is compiled if it can be generated into a new class for production usage from where container entries
then can be fetched. It means that your dependency graph is resolved during build time. This technique usually results
in a very fast DIC, because there is no need for any Reflection or configuration when consuming the container. Dynamic
containers however resolve your dependency graph Just-In-Time thus they are by design slower compared to the compiled
ones.

A DI Container supports autowiring if it can be configured to automatically inspect and resolve at least some
non-trivial subgraphs of the full dependency graph - no matter if the resolution takes place build time or run time.
Otherwise all dependencies have to be resolved manually which is probably done as configuration. In this case, a
DI Container does not support autowiring.

Essentially, dynamic containers usually need less attention during development than compiled ones, while containers
which support autowiring usually need much less configuration than the ones without autowiring capabilities.

## Method

Each container is given 6 tasks (Test Suites) where they have to create or fetch object graphs of different
sizes (10 or 100 objects). For this purpose, containers are configured either to always instantiate objects (this is
usually called as Prototype scope or not shared services) or to instantiate objects only at the first retrieval and
return the same instance on the subsequent calls (which is usually referred to as Singleton scope or shared services).

There are 3 main types of Test Suites: "Cold" ones (Test Suite 1-2) measure performance including autoloading and
startup time of containers as well as autoloading time of the retrieved objects. "Semi-Warm" ones (Test Suite 3-4)
measure performance excluding container autoloading time, but including startup time and autoloading time of the
retrieved objects, while "Warm" ones (Test Suite 5-6) exclude autoloading and startup time equally. Time of compilation
is always excluded from the results due to OPcache.

Each Test Suite contains three Test Cases which define the number of iterations the main task has to be repeated in
order to simulate real world usage patterns. This number ranges from 10 to 10 000. Furthermore, all Test Cases are
performed 20 times (this is referred to as "runs") in order to improve the accuracy of measurements.

The benchmark is run on a 15-inch MacBook Pro from 2015 using PHP 7.1 with OPcache enabled and autoloader
optimized (using authoritative mode). During the measurements, a PHP-FPM script served by nginx is executed each time.
This is needed because a production environment is simulated much better this way than in the CLI.

The examined DI Containers are configured for production usage as if it was probably done in case of a big project.
That's why I took advantage of autowiring capabilities when possible. Unfortunately, this discriminates some
participants giving them a big handicap, but I wanted to measure container performance with a configuration as
advertised or recommended by the documentation and most probable to be used in the real world.

## Results

### Test Suite 1: "Cold" Retrieval of a small object graph (10 objects)

In this Test Suite, containers have to fetch an object graph of 10 objects (defined as Singletons) 10, 100 and 1000
times. Autoloading and startup time of the containers are included in the measurements as well as autoloading time of
the retrieved objects. That's why this Test Suite simulates production usage very well.

### Test Suite 2: "Cold" Retrieval of a big object graph (100 objects)

In this Test Suite, containers have to fetch an object graph of 100 objects (defined as Singletons) 10, 100 and 1000
times. Autoloading and startup time of the containers are included in the measurements as well as autoloading time of
the retrieved objects. That's why this Test Suite simulates production usage very well.

### Test Suite 3: "Semi-Warm" Instantiation of a small object graph (10 objects)

In this Test Suite, containers have to create an object graph of 10 objects (defined as Prototypes) 10, 100 and 1000
times. Container autoloading time is excluded while startup time of the container and autoloading time of the retrieved
objects are included in the measurements.

### Test Suite 4: "Semi-Warm" Instantiation of a big object graph (100 objects)

In this Test Suite, containers have to create an object graph of 100 objects (defined as Prototypes) 10, 100 and 1000
times. Container autoloading time is excluded while startup time of the container and autoloading time of the retrieved
objects are included in the measurements.

### Test Suite 5: "Warm" Fetching of the same small object graph (10 objects)
  
In this Test Suite, containers have to fetch an object graph of 10 objects (defined as Singletons) 100, 1000 and 10 000
times. Neither autoloading time, nor startup time are included in the measurements.

### Test Suite 6: "Warm" Fetching of the same big object graph (100 objects)

In this Test Suite, containers have to fetch an object graph of 100 objects (defined as Singletons) 100, 1000 and 10 000
times. Neither autoloading time, nor startup time are included in the measurements.

## Conclusion

My hypothesis was that different types of containers have significantly different performance characteristics. It can
be concluded by looking at the results that the hypothesis can't be rejected as it seems that the more user-friendly a
container is (dynamic > compiled, dynamic with autowiring > dynamic without autowiring) the slower it is, especially in
tasks where object instantiation is measured (Test Suites 3-4).

However, keep in mind that in a well-architected application you won't call your DI Container hundreds or even thousands
of times because ideally there should be only one [composition root][composition-root]: when you invoke the
controller(s) which handle(s) the request (but there is a good chance of needing the container in other places of the
application layer - e.g. in your middleware or bootstrap files). That's why most results are exaggerated - you probably
won't see milliseconds of difference between the fastest and the slowest DIC in the real life.

To sum up, when choosing a container it only depends on your needs which one suits your project best: if you have a
performance-critical application then you probably want to choose a compiled container. If maximum performance is not
required, but you develop a big and complex system then I would recommend a dynamic container with autowiring
capabilities. Otherwise you can go with simpler containers.

[sitepoint-article]: https://www.sitepoint.com/php-dependency-injection-container-performance-benchmarks/
[old-benchmark]: https://github.com/TomBZombie/php-dependency-injection-benchmarks
[github-repo]: https://github.com/kocsismate/php-di-container-benchmarks
[jekyll-help]: https://github.com/jekyll/jekyll-help
[composition-root]: http://blog.ploeh.dk/2011/07/28/CompositionRoot/
