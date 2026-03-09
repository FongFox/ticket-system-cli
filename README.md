# Ticket System CLI

A command-line Ticket Management System built with **Java 21** to practice core Java concepts hands-on.

---

## What is this?

A simplified ticket management system that mirrors real-world helpdesk workflows, designed as a personal learning project to solidify:

- **Java OOP** — class design, inheritance, interfaces, enums
- **Stream API & Lambda** — filtering, sorting, and aggregating data
- **Concurrency** — Thread, Lock, Volatile, Synchronized, ReentrantLock, Virtual Threads (JDK 21)
- **JDK evolution** — understanding what changed across JDK 8 → 11 → 17 → 21

The system runs entirely in the **CLI** with **in-memory storage** to keep things simple and focused on learning.

---

## Domain Overview

```
User (3 roles: USER / AGENT / ADMIN)
 └── creates → Ticket (priority: Normal/Low/High/Urgent | status: Open/Closed)
                 └── has many → TicketReply
                 └── belongs to → Department
                                    └── has many → Agents
```

**Core flow:**
`User creates ticket → Agent/Admin gets notified → Agent replies → User gets notified → Ticket closed`

---

## How do I try it?

### Prerequisites

- Java 21 (LTS) — recommended: [Eclipse Temurin 21](https://adoptium.net)
- Maven 3.8+

### Build & Run

```bash
git clone https://github.com/FongFox/ticket-system-cli.git
cd ticket-system-cli

# Build
mvn clean package

# Run
java -jar target/ticket-system-cli.jar
```

---

## Project Structure

```
ticket-system-cli/
├── src/
│   ├── main/
│   │   └── java/
│   │       └── com/ticketsystem/
│   │           ├── Main.java
│   │           ├── model/          # Entities: User, Ticket, Department, TicketReply...
│   │           ├── repository/     # In-memory storage (HashMap / List)
│   │           ├── service/        # Business logic
│   │           ├── notification/   # Async notification (Thread / BlockingQueue)
│   │           └── cli/            # CLI menu & interaction
├── pom.xml
└── README.md
```

---

## Concurrency Scenarios

One of the main learning goals of this project is applying concurrency in realistic situations:

| Scenario | Concept applied |
|---|---|
| Multiple users creating tickets simultaneously | `AtomicLong` for ID generation |
| Notification service running in background | `Thread` + `BlockingQueue` |
| Preventing two agents from claiming the same ticket | `ReentrantLock` |
| Concurrent read of ticket list | `ReadWriteLock` |
| Realtime ticket counters | `volatile` |
| Scalable notification workers | Virtual Threads (JDK 21) |

---

## JDK Features by Version

As the project evolves, code is intentionally written to highlight what each JDK version introduced:

| Version | Features used in this project |
|---|---|
| JDK 8 | Stream API, Lambda, Optional, Method references |
| JDK 11 | `var`, new String methods (`isBlank`, `strip`) |
| JDK 17 | Sealed classes, Records, Pattern matching |
| JDK 21 | Virtual Threads (`Thread.ofVirtual()`), Sequenced Collections |

---

## Learning Outcomes

Through this project, I am practicing:

- Designing a layered architecture (Model → Repository → Service → CLI)
- Applying OOP principles in a realistic domain
- Writing idiomatic Java with Stream API and Lambda expressions
- Understanding thread safety and when to use `synchronized` vs `ReentrantLock`
- Tracing the evolution of Java features across LTS versions

---

## Inspired by

- [Boot.dev](https://boot.dev) — for the structured, project-based learning approach
- Laravel Ticket Management System — as the domain reference

---

## License

MIT License

---

## Contact

- GitHub: [FongFox](https://github.com/FongFox)
- Email: phong.tgn.coder@gmail.com
