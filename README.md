# Asynchronous File Server & Client System

## Project Information

**Project Title:** Asynchronous File Server & Client System

**Course:** Operating Systems and Systems Programming (OSSP)

**Programming Language:** C

**Platform:** Linux / Ubuntu

---

## Team Members

| Name | ID Number |
|---|---|
| Bammidi Yashwanth Sai | 2520030036 |
| Dhanvin Gupta | 2520030604 |
| Naga Pranadeep | 2520030390 |

---

## Supervisor

**Supervisor Name:** Harika

---

## Abstract

The Asynchronous File Server & Client System is a Linux-based C application designed to demonstrate asynchronous file processing, TCP networking, multithreading, inter-thread communication, request queuing, completion handling, and performance monitoring using Operating System and Linux system programming concepts.

The system consists of a TCP client and a multithreaded file server. The client can send READ and WRITE file requests to the server through a persistent TCP connection. It supports both single requests and multiple outstanding requests, allowing several file operations to be submitted without waiting for each individual response.

The server receives and separates multiple requests using a newline-delimited communication protocol and places them into a shared request queue. A pool of four worker threads processes requests concurrently. Each worker performs the required file operation and places the result into a completion queue.

A dedicated completion thread retrieves completed requests and sends framed responses containing the request ID and response payload back to the client. Request IDs allow the client to identify which response belongs to which request.

The system also includes performance measurement and logging mechanisms to monitor file operations and important server activities.

The project demonstrates important Operating Systems and Linux system programming concepts including TCP socket programming, process and thread management, POSIX threads, synchronization, producer-consumer queues, asynchronous processing, concurrent file operations, file handling, performance monitoring, logging, and inter-thread communication.

---

## Objectives

- Develop a Linux-based asynchronous file server and client system.
- Implement TCP-based communication between the client and server.
- Support file READ and WRITE operations.
- Allow a single client to maintain a persistent TCP connection.
- Allow the client to submit multiple file requests without waiting for each response.
- Implement a request queue for managing pending file operations.
- Implement multiple worker threads for concurrent request processing.
- Use four worker threads to process multiple file operations simultaneously.
- Implement a completion queue for completed requests.
- Use a dedicated completion thread to send responses to the client.
- Implement request IDs to associate responses with their corresponding requests.
- Implement TCP message framing for reliable request and response handling.
- Measure file operation performance.
- Maintain logs of important server and file-processing events.
- Demonstrate asynchronous and concurrent processing using Linux/POSIX system programming.

---

## Technologies Used

- C Programming
- Linux / Ubuntu
- GCC Compiler
- POSIX System Programming
- TCP Socket Programming
- POSIX Threads (`pthread`)
- Multithreading
- Request Queues
- Completion Queues
- Thread Synchronization
- File Handling
- `open()`
- `read()`
- `write()`
- `close()`
- Dynamic Memory / Buffers
- Performance Measurement
- Logging
- Makefile

---

## System Architecture

The system follows an asynchronous producer-consumer architecture.

```text
                    CLIENT
                       |
                       | TCP
                       |
                       v
              +----------------+
              |  TCP SERVER    |
              +----------------+
                       |
                       v
              +----------------+
              | Request Parser |
              +----------------+
                       |
                       v
              +----------------+
              | Request Queue  |
              +----------------+
                       |
          +------------+------------+
          |            |            |
          v            v            v
      Worker 1     Worker 2     Worker 3     Worker 4
          |            |            |            |
          +------------+------------+------------+
                       |
                       v
              +----------------+
              | File Operations|
              | READ / WRITE   |
              +----------------+
                       |
                       v
              +----------------+
              |Completion Queue|
              +----------------+
                       |
                       v
              +----------------+
              | Completion     |
              | Thread         |
              +----------------+
                       |
                       | TCP Response
                       v
                    CLIENT
