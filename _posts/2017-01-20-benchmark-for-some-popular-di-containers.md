---
layout: post
title: "Benchmark for some popular DI Containers"
date: 2017-01-20 20:00:00
categories: php di benchmark
tags:
image: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/cover.jpg
---

In 2014, a really interesting benchmark about DI Containers for PHP was [published on Sitepoint][sitepoint-article].
Unfortunately, the [implementation][old-benchmark] of the tests turned out to be quite controversial, so the benchmark
itself wasn't very insightful.

I have been interested in the topic since then - and my curiosity was just growing after I had started to develop my own DI container,
Zen - so I wanted to finally conduct a better benchmark than the last one was:
I tried to fix its flaws while keeping its many good parts. So here is my take! If you have any suggestion in mind about
the benchmark or you want to add your container to the list, please create an issue or a PR [in the repo][github-repo].

The examined containers are listed below along with some of their attributes:

| Name                | Compiled/Dynamic | Autowiring      | Project URL                                                                                            |
|---------------------|------------------|-----------------|--------------------------------------------------------------------------------------------------------|
| Aura                | dynamic          | supported       | [github.com/auraphp/Aura.Di](https://github.com/auraphp/Aura.Di)                                       |
| Auryn               | dynamic          | supported       | [github.com/rdlowrey/auryn](https://github.com/rdlowrey/auryn)                                         |
| Dice                | dynamic          | supported       | [github.com/Level-2/Dice](https://github.com/Level-2/Dice)                                             |
| Disco               | compiled         | not supported   | [github.com/bitExpert/disco](https://github.com/bitExpert/disco)                                       |
| Laravel             | dynamic          | supported       | [laravel.com/docs/5.3/container](https://laravel.com/docs/5.3/container)                               |
| Opulence IoC        | dynamic          | supported       | [opulencephp.com/docs/1.0/ioc-container](www.opulencephp.com/docs/1.0/ioc-container)                   |
| PhpDi               | dynamic          | supported       | [php-di.org/](http://php-di.org/)                                                                      |
| PHPixie DI          | dynamic          | not supported   | [github.com/phpixie/di](https://github.com/phpixie/di)                                                 |
| Pimple              | dynamic          | not supported   | [pimple.sensiolabs.org/](http://pimple.sensiolabs.org/ )                                               |
| Symfony             | compiled         | supported       | [symfony.com/doc/3.2/components/...](http://symfony.com/doc/3.2/components/dependency_injection.html)  |
| Yaco                | compiled         | not supported   | [github.com/thecodingmachine/yaco](https://github.com/thecodingmachine/yaco)                           |
| Zen                 | compiled         | supported       | [github.com/woohoolabs/zen](https://github.com/woohoolabs/zen)                                         |
| Zend ServiceManager | dynamic          | not supported   | [zendframework.github.io/...](https://zendframework.github.io/zend-servicemanager/)                    |

I'll try to give a vague definition below for some of the aforementioned notions:

A DI Container is _compiled_ if it can be generated into a new class for production usage from where container entries
then can be fetched. It means that your dependency graph is resolved during build time. This technique usually results
in a very fast DIC, because there is no need for any Reflection or configuration when consuming the container.
_Dynamic containers_ however resolve your dependency graph Just-In-Time thus they are by design slower compared to the compiled
ones.

A DI Container supports _autowiring_ if it can be configured to automatically inspect and resolve at least some
non-trivial subgraphs of the full dependency graph - no matter if the resolution takes place build time or run time.
Otherwise all dependencies have to be resolved manually which is probably done as configuration. In this case, a
DI Container does not support autowiring.

Essentially, dynamic containers usually need less attention during development than compiled ones, while containers
which support autowiring usually need much less configuration than the ones without autowiring capabilities.

## Method

Each container is given 6 tasks (Test Suites) where they have to create or fetch object graphs of different
sizes (10 or 100 objects). For this purpose, containers are configured either to always instantiate objects (this is
usually called as _Prototype scope_ or not shared services) or to instantiate objects only at the first retrieval and
return the same instance on the subsequent calls (which is usually referred to as _Singleton scope_ or shared services).

There are 3 main types of Test Suites: "Cold" ones (Test Suite 1-2) measure performance including autoloading and
startup time of containers as well as autoloading time of the retrieved objects. "Semi-Warm" ones (Test Suite 3-4)
measure performance excluding container autoloading time, but including startup time and autoloading time of the
retrieved objects, while "Warm" ones (Test Suite 5-6) exclude autoloading and startup time equally. Time of compilation
is always excluded from the results due to OPcache.

Each Test Suite contains three Test Cases which define the number of iterations the main task has to be repeated in
order to simulate real world usage patterns. This number ranges from 10 to 10 000. Furthermore, all Test Cases are
performed 20 times (this is referred to as "runs") in order to improve the accuracy of measurements.

The benchmark is run on a 15-inch MacBook Pro from 2015 using PHP 7.1 with OPcache enabled and autoloader
optimized (using authoritative mode). For each measurement, a PHP-FPM script served by nginx is executed. This is
needed because a production environment is simulated much better this way than in the CLI.

The examined DI Containers are configured for production usage as if it was probably done in case of a big project.
That's why I took advantage of autowiring capabilities when possible. Unfortunately, this discriminates some
participants giving them a big handicap, but I wanted to measure container performance with a configuration as
advertised or recommended by the documentation and most probable to be used in the real world.

## Results

### Suite 1: "Cold" Retrieval of a small object graph (10 objects)

In this Test Suite, containers have to fetch an object graph of 10 objects (defined as Singletons) 10, 100 and 1000
times. Autoloading and startup time of the containers are included in the measurements as well as autoloading time of
the retrieved objects. That's why this Test Suite simulates production usage very well.

![Results for test 1.1][result-11]

![Results for test 1.2][result-12]

![Results for test 1.3][result-13]

### Suite 2: "Cold" Retrieval of a big object graph (100 objects)

In this Test Suite, containers have to fetch an object graph of 100 objects (defined as Singletons) 10, 100 and 1000
times. Autoloading and startup time of the containers are included in the measurements as well as autoloading time of
the retrieved objects. That's why this Test Suite simulates production usage very well.

![Results for test 2.1][result-21]

![Results for test 2.2][result-22]

![Results for test 2.3][result-23]

### Suite 3: "Semi-Warm" Instantiation of a small object graph (10 objects)

In this Test Suite, containers have to create an object graph of 10 objects (defined as Prototypes) 10, 100 and 1000
times. Container autoloading time is excluded while startup time of the container and autoloading time of the retrieved
objects are included in the measurements.

![Results for test 3.1][result-31]

![Results for test 3.2][result-32]

![Results for test 3.3][result-33]

### Suite 4: "Semi-Warm" Instantiation of a big object graph (100 objects)

In this Test Suite, containers have to create an object graph of 100 objects (defined as Prototypes) 10, 100 and 1000
times. Container autoloading time is excluded while startup time of the container and autoloading time of the retrieved
objects are included in the measurements.

![Results for test 4.1][result-41]

![Results for test 4.2][result-42]

![Results for test 4.3][result-43]

### Suite 5: "Warm" Fetching of the same small object graph (10 objects)
  
In this Test Suite, containers have to fetch an object graph of 10 objects (defined as Singletons) 100, 1000 and 10 000
times. Neither autoloading time, nor startup time are included in the measurements.

![Results for test 5.1][result-51]

![Results for test 5.2][result-52]

![Results for test 5.3][result-53]

### Suite 6: "Warm" Fetching of the same big object graph (100 objects)

In this Test Suite, containers have to fetch an object graph of 100 objects (defined as Singletons) 100, 1000 and 10 000
times. Neither autoloading time, nor startup time are included in the measurements.

![Results for test 6.1][result-61]

![Results for test 6.2][result-62]

![Results for test 6.3][result-63]

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

[containers]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/containers.jpg
[result-11]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-11.jpg
[result-12]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-12.jpg
[result-13]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-13.jpg
[result-21]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-21.jpg
[result-22]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-22.jpg
[result-23]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-23.jpg
[result-31]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-31.jpg
[result-32]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-32.jpg
[result-33]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-33.jpg
[result-41]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-41.jpg
[result-42]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-42.jpg
[result-43]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-43.jpg
[result-51]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-51.jpg
[result-52]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-52.jpg
[result-53]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-53.jpg
[result-61]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-61.jpg
[result-62]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-62.jpg
[result-63]: /assets/image/2017-01-20-benchmark-for-some-popular-di-containers/result-63.jpg
