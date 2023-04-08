---
title: 'Introducing Krate: A Rate Limiter Library for Kotlin'
layout: single
status: publish
published: true
author:
  display_name: Luiz Picanço
  login: lpicanco
  email: lpicanco@gmail.com
author_login: lpicanco
author_email: lpicanco@gmail.com
categories:
- Projetos
tags:
- krate
- rate-limiter
---

As a software developer, I'm always on the lookout for tools and libraries that can help streamline my projects and improve their overall efficiency. 

Today, I will share with you my latest creation, an open-source rate limit library for Kotlin called Krate! 

In this post, I'll introduce you to Krate, explain its features, and show you how it can be a valuable addition to your Kotlin-based applications.

### What is Krate?

Krate is a rate limiter library designed specifically for Kotlin applications. It provides a simple yet powerful solution for managing and enforcing rate limits in various types of applications, such as APIs, web services, or any other projects that require rate limiting to control request rates and protect your resources from abuse.

### Why Use Krate?

Rate limiting is a crucial aspect of any application that exposes resources over a network, as it helps prevent abuse, ensures fair usage, and maintains the stability and performance of your services. With Krate, you can effortlessly implement rate limiting in your Kotlin projects, thanks to its easy-to-use and highly configurable design.

### Key Features of Krate

1. Token Bucket Algorithm: Krate uses the token bucket algorithm, a widely-used technique for rate limiting, to ensure efficient and fair resource allocation.

2. Burst Support: Krate allows for bursty request patterns, letting clients make a certain number of requests in a short time before being rate-limited.

3. Redis Support: Krate offers support for Redis as a backend for storing rate limit information, enabling distributed rate limiting across multiple instances of your application.

4. Keys eviction support: Krate automatically evicts unused keys, optimizing memory usage and ensuring optimal performance.

5.  Easy Integration: Krate can be easily integrated into your existing Kotlin projects without any hassle.

6. Customizable Rate Limits: Krate allows you to define custom rate limits based on your specific requirements, ensuring that your application's resources are protected and fairly distributed.

### Getting Started with Krate

To get started with Krate, you can simply add it as a dependency to your Kotlin project. Here's an example of how you can add Krate to your project using Gradle:

```kotlin
implementation("io.github.lpicanco:krate-core:1.0.1")
```

Once you've added Krate to your project, you can start using it to enforce rate limits. 


Here's a simple example of how to use Krate to limit requests to an API endpoint:
```kotlin
import com.neutrine.krate.rateLimiter

// 60 requests per minute
val rateLimiter = rateLimiter(maxRate = 60) {
   maxRateTimeUnit = ChronoUnit.MINUTES
}

fun handleRequest(request: Request) {
    if (rateLimiter.tryTake()) {
        // Process the request
    } else {
        // Reject the request due to rate limit
    }
}
```

Here's another example, limiting requests by client ID:
```kotlin
import com.neutrine.krate.rateLimiter

// 5 requests per second
val rateLimiter = rateLimiter(maxRate = 5) 

fun handleRequest(request: Request, clientId: String) {
    if (rateLimiter.tryTake(clientId)) {
        // Process the request
    } else {
        // Reject the request due to rate limit
    }
}
```


### Learn More and Contribute
To learn more about Krate and explore its features, please visit the project repository on [GitHub](https://github.com/lpicanco/krate). 

If you'd like to contribute to the project, feel free to submit issues, pull requests, or help improve the documentation.

Additionally, you can visit the Krate [documentation site](https://lpicanco.github.io/krate) for more detailed information, usage examples, and API reference.

I hope this post has given you a good introduction to Krate and how it can help you implement rate limiting in your Kotlin applications. Feel free to share your thoughts, experiences, or questions in the comments section below. Happy coding!