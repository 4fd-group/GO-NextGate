NextGate

Unified Proxy & DNS Gateway for Tailscale Networks

NextGate is a lightweight, high-performance network gateway built from scratch in Go. It combines dual-layer reverse proxying, selective JWT verification, integrated DNS resolution, and centralized network management within a single process.

Designed specifically for personal infrastructure, home networks, and custom business environments, NextGate provides a unified way to securely access and manage internal services over a Tailscale network — without requiring a public IPv4 address or a commercial domain registrar.

💡 Origin & Purpose

NextGate originated from a practical infrastructure challenge: managing and exposing privately hosted services over a Tailscale network without relying on a public IPv4 address or external domain registration.

The goal was to build an independent, lightweight gateway capable of handling internal domain resolution, intelligent traffic routing, and secure reverse proxying through a single application.

NextGate is designed for people and organizations that operate their own infrastructure, including:

- Personal & Home Infrastructure: Accessing home Wi-Fi router administration panels, CCTV systems, IP cameras, NAS devices, and other local network services remotely through Tailscale.
- Custom Business Infrastructure: Connecting privately hosted business applications, internal dashboards, management panels, and backend services without requiring public IP addresses.
- Self-Hosted Applications: Providing private domain-based access to independently developed applications and services running within a Tailscale network.
- Private Network Management: Centralizing DNS resolution, reverse proxying, and service management in one place.

Originally developed for a private infrastructure environment, NextGate is now being developed as an independent, open-source project for the wider community.

✨ Key Features

1. Tailscale-Bound Architecture

NextGate is specifically designed to operate through a Tailscale network.

- Automatic Interface Discovery: Automatically detects the system's "tailscale0" network interface.
- Automatic IP Binding: Retrieves the Tailscale IPv4 address and binds its services directly to that address.
- No Manual Address Configuration: Does not accept manually configured bind addresses.
- Mandatory Tailscale Interface: Terminates startup with a fatal error if the Tailscale interface or its required IPv4 address cannot be found.
- Private Network Access: Enables access to internal services across connected Tailnet devices without requiring a public IPv4 address.

2. Dual-Layer Dynamic Reverse Proxy

NextGate uses a two-stage domain lookup mechanism to determine how incoming requests should be handled.

Layer 1 — Authenticated Proxy

- Performs domain-based lookup in the first routing map.
- Verifies JWT authentication before forwarding requests.
- Designed for custom applications and backend services that require centralized authentication at the proxy layer.

Layer 2 — Direct Proxy

- Performs a secondary domain lookup when no matching Layer 1 record exists.
- Forwards requests directly to the configured upstream without proxy-level JWT verification.
- Designed for services that handle their own authentication, including home routers, CCTV systems, IoT devices, and administrative panels.

Unregistered Domains

If neither routing map contains a matching domain, NextGate immediately returns an appropriate unregistered-domain error without attempting further upstream routing.

3. Integrated DNS Resolver

NextGate includes its own DNS resolution functionality within the same application process.

- Supports TCP and UDP DNS queries.
- Maintains an internal domain-to-IPv4 record mapping.
- Designed for private domain resolution across Tailscale-connected devices.
- Uses MessagePack for compact data serialization.
- Operates alongside both proxy layers without requiring a separate DNS application.

4. Centralized Management Console

NextGate includes a dedicated management server for controlling and managing its services.

- Centralized administration of proxy and DNS configurations.
- Dedicated management interface running on a separate port within the same process.
- Reserved internal management domain: "nextgate.internal".
- The "nextgate.internal" namespace is exclusively reserved for NextGate's internal management services and is separated from user and business domain registrations.

5. Lightweight & High-Concurrency Design

- Built using Go's standard networking capabilities.
- Uses "net/http" for HTTP reverse proxying.
- Designed for efficient concurrent request handling.
- Minimal external dependencies.
- Optimized for low resource consumption and high throughput.

🛠️ Tech Stack

- Language: Go (Golang)
- HTTP Engine: "net/http" (Standard Library)
- Network Environment: Tailscale Private Mesh
- DNS Transport: TCP / UDP
- Data Serialization: MessagePack
- Routing Architecture: Dual-Map Dynamic Routing
- Authentication: JWT Verification (Layer 1)
- Management: Integrated Admin Console

🎯 Designed For

NextGate is intended for infrastructure owners who want to manage their own private network services without depending on public-facing infrastructure.

Typical use cases include:

- Remotely accessing home routers and Wi-Fi administration panels.
- Accessing CCTV cameras and local surveillance systems.
- Managing NAS, IoT devices, and self-hosted services.
- Providing private access to custom business applications.
- Hosting internal dashboards and administrative panels.
- Exposing privately hosted services to authorized Tailnet devices.
- Managing private DNS and reverse proxy routing from a single gateway.

🌐 Network & Domain Architecture

NextGate uses Tailscale as its underlying network environment.

Its internal management namespace is reserved independently of any business or customer domain namespace.

Reserved Management Domain:

"nextgate.internal"

This namespace is intended exclusively for NextGate's own management services and must not be used for customer or business domain registrations.

📌 Project Status

NextGate is currently under active development.

Features, architecture, and management capabilities may evolve as the project progresses.

---

Built with Go for independent, self-hosted, and private network infrastructure.