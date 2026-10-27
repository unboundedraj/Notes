---
title: Redis
date: 2026-10-26
tags: [redis, cache]
---

**Redis is an in-memory data store that stores data in RAM, allowing applications to access it very quickly.**

Think of Redis as a super-fast storage space that your application can use to avoid repeatedly fetching the same data from a slower database.

## Simple example

Imagine you have a website with 10,000 users visiting the same page.

Without Redis:

1. Every request fetches data from a database.
2. The database does repeated work.
3. Responses may become slower.

With Redis:

1. The application fetches the data from the database once.
2. It stores the result in Redis.
3. Later requests read the result from Redis, which is usually much faster.

## What is Redis used for?

- **Caching:** Store frequently accessed data.
- **Session management:** Remember that a user is logged in.
- **Rate limiting:** Restrict how many requests a user can make.
- **Real-time leaderboards:** Maintain game scores and rankings.
- **Message queues:** Help applications exchange messages.

## How does Redis work?

Redis stores data as key-value pairs.

```
SET username "Rahul"
GET username
```

Here, `SET` stores the value and `GET` retrieves it.

Redis also supports data structures such as lists, sets, hashes, sorted sets, and streams.

## Redis vs. a traditional database


| Feature          | Redis                          | Traditional database (e.g., PostgreSQL)  |
| ---------------- | ------------------------------ | ---------------------------------------- |
| Main storage     | Primarily RAM                  | Usually disk-based                       |
| Speed            | Very fast                      | Depends on query and workload            |
| Best use         | Caching, real-time data        | Persistent application data              |
| Data persistence | Optional/configurable          | Typically built in                       |
| Data model       | Key-value and other structures | Tables and relational data in PostgreSQL |
