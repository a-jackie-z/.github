# a-jackie-z Organization

Welcome to the **a-jackie-z** organization! We are building a comprehensive suite of TypeScript microservice tools and utilities designed to streamline backend development with a focus on type safety, developer experience, and production readiness.

## 🎯 Mission

Our mission is to provide robust, well-documented, and easy-to-use TypeScript packages that solve common challenges in microservice architectures. We believe in:

- **Type Safety First**: Leveraging TypeScript and Zod for compile-time and runtime type safety
- **Developer Experience**: Clear APIs, comprehensive documentation, and minimal boilerplate
- **Production Ready**: Battle-tested patterns with reliability, observability, and scalability built-in
- **Microservice Architecture**: Tools designed for distributed systems and service-oriented architectures

## 📦 Our Packages

### Core Infrastructure

#### [@a-jackie-z/config](https://github.com/a-jackie-z/config)
**Type-safe configuration management for microservices**

A configuration factory that loads and validates environment variables using Zod schemas with automatic type coercion. Perfect for managing service configuration across different environments with full TypeScript support.

**Key Features:**
- 🔒 Type-safe configuration with Zod validation
- 🔄 Automatic type coercion (strings → numbers, booleans)
- 📝 Default values and optional fields
- ✅ Helpful validation error messages

**Quick Example:**
```typescript
import { z } from 'zod'
import { createConfig } from '@a_jackie_z/config'

const config = createConfig(
  z.object({
    port: z.number().int().positive(),
    apiKey: z.string().min(1),
  }),
  { port: 'APP_PORT', apiKey: 'API_KEY' }
)
```

#### [@a-jackie-z/logger](https://github.com/a-jackie-z/logger)
**Fast and lightweight logging for microservices**

A Pino-based logger wrapper optimized for microservice environments with environment-based configuration and production-ready JSON output.

**Key Features:**
- ⚡ Built on Pino (one of the fastest Node.js loggers)
- 🎨 Optional pretty-printing for development
- 🔧 Environment-based configuration
- 📊 Structured JSON logging for production

---

### Web Framework

#### [@a-jackie-z/fastify](https://github.com/a-jackie-z/fastify)
**Production-ready Fastify with batteries included**

A comprehensive Fastify setup with built-in JWT authentication, rate limiting, Swagger documentation, and Zod validation. Designed for building secure, scalable APIs with minimal configuration.

**Key Features:**
- 🔐 Dynamic multi-token JWT authentication with key rotation
- 🛡️ Built-in rate limiting and security
- 📚 Auto-generated Swagger documentation
- ✅ Zod schema validation for requests/responses
- 🎯 Standardized response formatting
- 🚀 Multiple token types with per-type configuration

**Quick Example:**
```typescript
import { createFastify, runFastify } from '@a_jackie_z/fastify'

const app = await createFastify({
  jwt: {
    secrets: { v1: 'secret-key' },
    defaultKeyId: 'v1',
    tokenTypes: {
      access: { headerName: 'authorization', expiresIn: '15m' }
    }
  },
  swagger: { title: 'My API', version: '1.0.0' }
})

await runFastify(app, '0.0.0.0', 3000)
```

---

### Data Layer

#### [@a-jackie-z/typeorm](https://github.com/a-jackie-z/typeorm)
**TypeORM wrapper with enhanced utilities**

Simplified TypeORM setup with environment-based configuration, automatic snake_case naming, and migration management. Get connected to your database in seconds.

**Key Features:**
- 🔧 Environment variable configuration
- 🐍 Automatic snake_case naming strategy
- 🔄 Automatic migration execution on startup
- 🗃️ Support for PostgreSQL, MySQL, MariaDB, SQLite
- 💾 Production-ready defaults

**Quick Example:**
```typescript
import { createOrm } from '@a_jackie_z/typeorm'

const dataSource = createOrm()
await dataSource.initialize()
// ✓ Connected!
```

---

### Messaging & Events

#### [@a-jackie-z/event-bus](https://github.com/a-jackie-z/event-bus)
**Robust event bus with RabbitMQ**

A TypeScript-first RabbitMQ wrapper supporting both point-to-point (queue-based) and broadcast (fanout exchange) messaging patterns with automatic reconnection and reliable delivery.

**Key Features:**
- 📨 Point-to-point and broadcast messaging
- 🔄 Automatic reconnection with state monitoring
- 💪 Durable queues and persistent messages
- ⚖️ Fair load distribution across consumers
- 🎯 Type-safe event handlers
- 📊 Connection state monitoring

**Quick Example:**
```typescript
import { EventBusProducer, EventBusConsumer } from '@a_jackie_z/event-bus'

// Producer
const producer = new EventBusProducer({ rabbitMqUrl: 'amqp://...' })
await producer.connect()
await producer.publish('orders', { orderId: 1, status: 'pending' })

// Consumer
const consumer = new EventBusConsumer({
  rabbitMqUrl: 'amqp://...',
  queueHandlers: new Map([['orders', [orderHandler]]])
})
await consumer.connect()
```

---

## 🛠️ Tech Stack

Our packages are built with modern technologies and best practices:

- **Language**: TypeScript for type safety and better developer experience
- **Runtime**: Node.js for server-side JavaScript execution
- **Validation**: Zod for runtime type validation and schema definition
- **Web Framework**: Fastify for high-performance HTTP servers
- **ORM**: TypeORM for database management with multiple database support
- **Message Queue**: RabbitMQ for reliable message delivery
- **Logging**: Pino for fast, structured logging
- **Testing**: Modern testing practices with TypeScript support

## 🏗️ Architecture Principles

Our packages are designed with microservice architecture in mind:

1. **Loose Coupling**: Each package solves a specific problem and can be used independently
2. **Configuration-driven**: Environment variables and type-safe config for different deployment environments
3. **Observability**: Built-in logging and monitoring support
4. **Resilience**: Automatic reconnection, graceful shutdown, and error handling
5. **Scalability**: Horizontal scaling support with load balancing and fair distribution
6. **Developer Experience**: Comprehensive documentation, examples, and TypeScript support

## 🚀 Getting Started

Each package is published to npm and can be installed independently:

```bash
npm install @a_jackie_z/config
npm install @a_jackie_z/logger
npm install @a_jackie_z/fastify
npm install @a_jackie_z/typeorm
npm install @a_jackie_z/event-bus
```

Visit individual repositories for detailed documentation, examples, and API references.

## 📚 Documentation

Each package includes:
- ✅ Comprehensive README with quick start guide
- ✅ API reference documentation
- ✅ Real-world usage examples
- ✅ Best practices and performance tips
- ✅ TypeScript type definitions

## 🤝 Contributing

We welcome contributions! Each repository follows standard open-source practices:
- Open issues for bugs or feature requests
- Submit pull requests with clear descriptions
- Follow TypeScript and code style conventions
- Add tests for new features

## 📄 License

All packages are released under the MIT License, making them free to use in both personal and commercial projects.

## 👨‍💻 Author

**Sang Lu**
- Email: connect.with.sang@gmail.com
- Organization: [a-jackie-z](https://github.com/a-jackie-z)

---

Built with ❤️ using TypeScript for the microservices ecosystem
