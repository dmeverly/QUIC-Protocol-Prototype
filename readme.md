# QUIC Protocol Prototype (Stateful Protocol Study)

**Author**: David Everly  
**Language**: Python  
**Transport**: QUIC (MsQuic)  
**Status**: Proof of Concept

---

## Description

This project is a proof-of-concept application-layer protocol built on top of QUIC to explore **stateful client–server interaction, message framing, and deterministic protocol behavior** over a long-lived connection.

The implementation uses a simple turn-based game as a concrete vehicle for exercising protocol state transitions, message validation, and session lifecycle management. The focus of the project is **protocol structure and correctness**, not gameplay or production security.

---

## Why This Exists

Many protocol examples focus on stateless request/response patterns or hide complexity behind frameworks.

This project intentionally explores:

- explicit protocol states
- message-driven transitions
- validation at the application layer
- long-lived session semantics over QUIC

The goal is to better understand how application protocols behave when **state, ordering, and correctness matter**, independent of performance tuning or cryptographic guarantees.

---

## Protocol Design

### Application-Layer State Machine

The protocol is defined as a deterministic finite-state machine (FSM), with explicit states such as:

- connection initialization
- session setup
- active gameplay
- termination

All client and server behavior is governed by valid state transitions. Messages received outside of an expected state are rejected.

---

### Message Framing

Communication occurs through explicitly defined Protocol Data Units (PDUs), each encoding:

- message type
- payload structure
- expected handling behavior

This design avoids implicit assumptions about message order or meaning.

---

### Client–Server Separation

- The **client** is responsible for sending user-driven commands.
- The **server** enforces protocol rules, validates transitions, and maintains authoritative state.

This separation mirrors real-world protocol design where the server is the source of truth.

---

## Implementation Notes

- Built using **MsQuic** to leverage QUIC’s stream multiplexing and connection semantics.
- Uses a single long-lived QUIC connection per session.
- Application-layer logic is deliberately explicit rather than abstracted.

---

## Scope and Non-Goals

This project intentionally does **not** include:

- authentication or authorization
- cryptographic key management
- resistance to denial-of-service attacks
- production-grade error handling
- performance optimization

TLS configuration and certificate validation are simplified for development purposes.

These exclusions are explicit and intentional, as the project’s goal is **protocol reasoning**, not secure deployment.

---

## What This Project Demonstrates

- Application-layer protocol design over QUIC  
- Explicit state machines governing client–server interaction  
- Message framing and validation independent of transport  
- Clear separation between protocol logic and application logic  
- Disciplined scoping of non-production systems  

---

## Limitations

- Not secure against adversarial clients
- Hardcoded configuration and parameters
- Single-use proof-of-concept implementation

---

## Relationship to Other Projects

This project informed later work focused on **explicit boundaries, validation, and failure handling**, including:

- guard-based validation pipelines
- deterministic system behavior under invalid input
- separation of transport, protocol, and application concerns

---

## Disclaimer

This project was developed independently on personal time and is not affiliated with or endorsed by any employer.  
All code is provided for educational and exploratory purposes only.
