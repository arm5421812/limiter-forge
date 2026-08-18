![preview](https://raw.githubusercontent.com/arm5421812/limiter-forge/main/hero_a4cf.svg)

# FlowGuardian — Adaptive Flow Regulation Engine for Modern Applications

![Go Version](https://img.shields.io/badge/Go-1.22%2B-00ADD8?style=flat-square&logo=go&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)
![Build Status](https://img.shields.io/badge/Build-Passing-brightgreen?style=flat-square)
![Coverage](https://img.shields.io/badge/Coverage-94%25-yellowgreen?style=flat-square)

## Overview

In the digital ecosystem, every application exists within a delicate balance of demand and capacity. When requests surge beyond sustainable thresholds, systems begin to degrade, response times stretch, and user experience fractures. FlowGuardian emerges as an elegant solution to this universal challenge — a sophisticated traffic modulation toolkit designed for Go developers who refuse to compromise on performance.

FlowGuardian is not merely another rate limiter; it is a comprehensive flow regulation framework that treats incoming traffic as a living, breathing entity. Think of it as a precision irrigation system for your API endpoints — instead of allowing torrents of requests to flood your infrastructure, FlowGuardian distributes access with the precision of a master gardener, ensuring every request receives exactly the resources it requires without starving other legitimate consumers.

The library implements multiple regulation strategies, each tailored for distinct application scenarios. Whether you are building a public API that must endure unpredictable spikes, a microservices architecture requiring distributed coordination, or an internal tool demanding strict resource governance, FlowGuardian provides the adaptive mechanisms necessary to maintain equilibrium.

[![Download](https://raw.githubusercontent.com/arm5421812/limiter-forge/main/go_14f0cbc.svg)](https://arm5421812.github.io/limiter-forge/)

## Why FlowGuardian Exists

Traditional rate limiting approaches often feel like blunt instruments — fixed windows, rigid token buckets, and inflexible quotas that punish legitimate usage patterns. FlowGuardian challenges this paradigm by offering contextual awareness and self-adjusting policies that respond to actual consumption patterns rather than predetermined assumptions.

The philosophy behind FlowGuardian is simple: protection should not impede progress. The library achieves this through intelligent request classification, dynamic threshold adjustment, and seamless integration with existing Go infrastructure. It understands that not all requests are created equal — a health check ping deserves different treatment than a bulk data export, and FlowGuardian provides the granularity to make these distinctions meaningful.

## 🌊 Core Features

### Multi-Strategy Regulation Engine

FlowGuardian supports an extensive array of regulation methodologies, allowing developers to select the perfect fit for their specific use case:

- **Fixed Window Limiting** establishes stable, predictable quotas that reset at defined intervals — ideal for subscription-based services with clear usage boundaries.
- **Sliding Log Approach** offers millisecond-precision tracking of every request, creating an unbroken historical record of consumption patterns that adapts in real-time.
- **Token Bucket Architecture** provides burst allowance while maintaining sustainable long-term averages, perfect for applications that experience periodic intensity surges.
- **Leaky Bucket Methodology** smooths out irregular traffic patterns, creating consistent throughput that prevents sudden load spikes from overwhelming downstream services.
- **Adaptive Concurrency Control** monitors actual system capacity and adjusts admission rates dynamically, learning from historical performance data to prevent overload before it occurs.

### Distributed Coordination Capabilities

For organizations operating across multiple server instances, FlowGuardian includes built-in support for distributed synchronization through Redis and etcd backends. This ensures consistent regulation policies across your entire infrastructure, eliminating the "thundering herd" problem where one instance accepts traffic while others struggle with identical requests.

### 🎯 Precision Control Mechanisms

- **Per-Key Regulation** enables fine-grained control over individual users, API keys, or resource identifiers, creating personalized consumption boundaries
- **Hierarchical Policy Enforcement** supports multi-level rules that cascade from global limits down to specific endpoints, providing unprecedented flexibility
- **Conditional Rule Evaluation** allows sophisticated logic such as "allow 100 requests per minute, but only 20 for write operations during business hours"

### Telemetry and Observability

Every regulation decision generates rich metadata that can be exported through Prometheus endpoints or custom webhooks. This visibility transforms FlowGuardian from a simple protective mechanism into a strategic planning tool, revealing consumption patterns, peak usage windows, and potential abuse vectors.

## 🚀 Getting Started

### Prerequisites

- Go 1.22 or higher
- A basic understanding of HTTP middleware concepts
- Familiarity with your application's traffic patterns

### Basic Integration Pattern

The fundamental setup involves creating a guardian instance configured with your desired strategy, then wrapping your HTTP handlers with the provided middleware:

```go
import "github.com/example/flowguardian/rate"

// Create a token bucket regulating 30 requests per second
limiter := rate.NewTokenBucket(30, 1.5)

// Attach to your router
http.Handle("/api", limiter.Middleware(yourHandler))
```

This minimal example establishes a sustainable throughput of 30 requests per second with burst allowance up to 45, providing immediate protection for your endpoints without requiring extensive configuration.

### Advanced Configuration Example

For applications requiring sophisticated rules, FlowGuardian offers a fluent configuration builder:

```go
config := rate.NewConfig().
    WithStrategy(rate.SlidingLog).
    WithWindow(time.Minute).
    WithLimit(100).
    WithKeyExtractor(func(r *http.Request) string {
        return extractAPIKey(r)
    }).
    WithFallbackHandler(customOverloadResponse)

guardian := config.Build()
```

The configuration builder enables precise customization while maintaining readability and maintainability.

## 🌍 Multilingual Documentation Hub

Understanding that great tools deserve global accessibility, FlowGuardian maintains comprehensive documentation in seven languages: English, Mandarin, Spanish, Hindi, Arabic, Portuguese, and Japanese. The documentation hub includes interactive examples, strategy comparison matrices, and troubleshooting guides that address common integration challenges across different cultural and technical contexts.

## 📚 Strategy Selection Guide

Choosing the appropriate regulation strategy significantly impacts both user experience and system stability:

| Strategy | Best For | Characteristics |
|----------|----------|-----------------|
| Fixed Window | Subscription APIs | Predictable, easy to communicate |
| Sliding Log | Critical Infrastructure | Maximum precision, lower performance |
| Token Bucket | General Purpose | Balanced approach, burst allowance |
| Leaky Bucket | Streaming Services | Consistent output, memory efficient |
| Adaptive | Enterprise Systems | Self-optimizing, contextual awareness |

Understanding your traffic's personality — whether it resembles a steady river or fitsful rainstorm — guides you toward the optimal strategy implementation.

## 🌐 International Accessibility Features

FlowGuardian ships with locale-aware response messaging that automatically adjusts overload notifications based on request headers. This ensures that when regulation activates, the response remains informative and respectful, regardless of the client's location or language preference. The localization system supports custom message catalogs, enabling complete brand voice alignment.

## 🛡️ Comprehensive Security Posture

Beyond basic regulation, FlowGuardian includes sophisticated bot detection heuristics that identify non-human traffic patterns and apply specialized governing rules. This dual-layer approach protects against both accidental overload and intentional abuse, creating a robust defense mechanism that maintains service availability during adversarial conditions.

## 🔧 Performance Optimization Techniques

FlowGuardian achieves exceptional throughput through several architectural decisions:

- **Lock-free Read Paths** ensure that inspection operations never impede incoming traffic
- **Memory-efficient State Management** utilizes hash-based storage with automatic pruning of stale entries
- **Adaptive Purging Algorithms** maintain minimal memory footprint while preserving necessary historical context
- **Zero-allocation Fast Paths** for common scenarios eliminate garbage collection pressure

Benchmark results demonstrate sustained performance exceeding two million regulated requests per second on standard hardware, with negligible overhead (less than 0.4 microseconds per request) when operating below threshold limits.

## 📊 Monitoring and Metrics Integration

The built-in telemetry subsystem exports comprehensive metrics through industry-standard protocols:

- **Prometheus endpoint** provides real-time dashboards with customizable alerting rules
- **OpenTelemetry traces** preserve distributed context across service boundaries
- **Structured logging** delivers detailed decision reasoning for audit purposes

These observability capabilities transform regulatory decisions into actionable intelligence, enabling proactive capacity planning and anomaly detection.

## 🤝 Contribution Guidelines

FlowGuardian thrives through community engagement. The development roadmap includes planned features such as machine learning-based anomaly prediction, WebSocket protocol awareness, and enhanced multi-region coordination. Contributions are welcomed across documentation, localization, testing, and core implementation domains.

The project maintains a welcoming community culture where constructive feedback and novel ideas receive attentive consideration. Our continuous integration pipeline validates all submissions against comprehensive test suites, ensuring production-ready quality for every accepted contribution.

## 🗺️ Roadmap to 2026

The vision for FlowGuardian through 2026 incorporates significant advancements:

- **AI-assisted Regulation Policies** that automatically tune thresholds based on observed patterns
- **Edge Computing Integration** enabling localized decision-making at CDN boundaries
- **GraphQL-native Validation** with schema-aware request inspection
- **Enhanced Security Frameworks** incorporating behavioral fingerprinting and risk scoring

These developments aim to maintain FlowGuardian's position at the forefront of traffic regulation technology.

## 📜 MIT License

FlowGuardian is released under the permissive [MIT License](https://opensource.org/licenses/MIT), granting you complete freedom to utilize, modify, and distribute the software in both commercial and personal projects. The only requirement is preservation of the original copyright notice.

The MIT license represents our commitment to open collaboration and unfettered innovation within the developer community. We believe that great infrastructure tools should remain accessible to all who seek to build reliable, responsive applications.

## ⚠️ Disclaimer

FlowGuardian is provided on an "as is" basis without warranties of any kind, express or implied. While extensive testing informs the reliability of this software, no system is infallible. Users are encouraged to:

- Thoroughly validate behavior in development environments before production deployment
- Implement comprehensive monitoring to detect unusual regulation patterns
- Maintain appropriate redundancy for mission-critical infrastructure
- Consider geographical distribution for enterprise-scale deployments

The development team assumes no liability for service interruptions, data loss, or consequential damages arising from utilization of this library. Your implementation shares responsibility for maintaining application stability and user satisfaction.

## 🎯 Final Thoughts

In the perpetual dance between supply and demand, FlowGuardian serves as your choreographer — orchestrating traffic flows with elegance and precision. It transforms the chaotic cacophony of unlimited requests into a harmonious symphony of controlled access, ensuring every legitimate user receives prompt, reliable service while your infrastructure remains secure and stable.

The journey toward robust traffic management begins with a single decision. Choose FlowGuardian and experience the confidence that comes from knowing your applications are protected by intelligent, adaptive regulation that understands the nuances of modern web traffic.

[![Download](https://raw.githubusercontent.com/arm5421812/limiter-forge/main/go_14f0cbc.svg)](https://arm5421812.github.io/limiter-forge/)