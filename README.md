# Firefly Framework - Notifications

[![CI](https://github.com/fireflyframework/fireflyframework-notifications/actions/workflows/ci.yml/badge.svg)](https://github.com/fireflyframework/fireflyframework-notifications/actions/workflows/ci.yml)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)
[![Java](https://img.shields.io/badge/Java-21%2B-orange.svg)](https://openjdk.org)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-green.svg)](https://spring.io/projects/spring-boot)

> Notifications core library with email, SMS, and push notification service contracts and provider abstraction.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [Configuration](#configuration)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)

## Overview

Firefly Framework Notifications provides the core service layer and provider contracts for sending email, SMS, and push notifications. It defines provider interfaces (`EmailProvider`, `SMSProvider`, `PushProvider`) that concrete notification providers implement, along with application services that orchestrate notification delivery.

The module is structured as a multi-module project with a core sub-module containing the service implementations, DTOs, and provider interfaces. The notification services delegate to the appropriate provider implementation, which is supplied by separate provider modules (SendGrid, Resend, Twilio, Firebase).

This architecture allows applications to switch notification providers without changing business logic, as all providers implement the same standardized interfaces.

## Features

- `EmailService` with template-based email sending and attachments
- `SMSService` for SMS message delivery
- `PushService` for push notification delivery
- `EmailProvider` interface for pluggable email providers
- `SMSProvider` interface for pluggable SMS providers
- `PushProvider` interface for pluggable push notification providers
- DTOs for email requests/responses with attachment support
- DTOs for SMS requests/responses
- DTOs for push notification requests/responses
- Email status tracking enum

## Requirements

- Java 21+
- Spring Boot 3.x
- Maven 3.9+

## Installation

```xml
<dependency>
    <groupId>org.fireflyframework</groupId>
    <artifactId>fireflyframework-notifications</artifactId>
    <version>26.02.04</version>
</dependency>
```

## Quick Start

```java
import org.fireflyframework.notifications.core.services.email.v1.EmailService;
import org.fireflyframework.notifications.interfaces.dtos.email.v1.EmailRequestDTO;

@Service
public class OrderNotificationService {

    private final EmailService emailService;

    public Mono<EmailResponseDTO> sendOrderConfirmation(Order order) {
        EmailRequestDTO request = EmailRequestDTO.builder()
            .to(order.getCustomerEmail())
            .subject("Order Confirmation - " + order.getId())
            .body("Your order has been confirmed.")
            .build();
        return emailService.send(request);
    }
}
```

## Configuration

Configuration is provided by the specific notification provider module (SendGrid, Resend, Twilio, Firebase).

## Documentation

No additional documentation available for this project.

## Contributing

Contributions are welcome. Please read the [CONTRIBUTING.md](CONTRIBUTING.md) guide for details on our code of conduct, development process, and how to submit pull requests.

## License

Copyright 2024-2026 Firefly Software Solutions Inc.

Licensed under the Apache License, Version 2.0. See [LICENSE](LICENSE) for details.
