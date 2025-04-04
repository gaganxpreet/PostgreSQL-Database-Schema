# DBMS Project: Content Management Platform

## Overview

This project implements a database schema for a content management platform designed to handle articles, user interactions (comments, reactions), and views efficiently. The schema ensures data consistency, integrity, and optimized retrieval using PostgreSQL.

### Author:
- **Gaganpreet Singh**

---

## Problem Statement

In today's digital age, organizations and individuals require robust platforms to create, publish, and engage with content. This project addresses the following challenges:
1. **Content Publishing and Management**: Users can create articles with unique identifiers and timestamps.
2. **User Engagement**: Support for comments, reactions (likes/dislikes), and view tracking.
3. **Data Consistency and Integrity**: Structured database with constraints like foreign keys and unique identifiers.
4. **Efficient Retrieval**: Indexes for optimized access to users, articles, comments, reactions, and views.

---

## Features

### 1. User Management
- Each user has a unique account with attributes like `id`, `email`, `name`, and `cloud_user_id`.
- Timestamps (`created_at`, `last_modified_at`) track account creation and updates.

### 2. Content Creation
- Users can create articles with titles and content linked to their accounts (`author_id`).
- Articles have unique identifiers and timestamps for chronological ordering.

### 3. Comment System
- Users can comment on articles.
- Comments are validated to contain between 1–1000 characters using `CHECK` constraints.
- Timestamps enable sorting by creation or modification date.

### 4. Reaction System
- Users can react to articles with "like" or "dislike".
- Unique constraint ensures each user can react only once per article.
- Supports updating reactions using `ON CONFLICT` handling.

### 5. Article View Tracking
- Tracks views for articles linked to user accounts (`user_id`) or anonymously.
- Indexing optimizes view-related queries.

---

## Database Schema

### Tables:
1. **user_accounts**
   - Attributes: `id`, `email`, `name`, `cloud_user_id`, `created_at`, `last_modified_at`
   - Constraints: Primary Key (`id`), Unique (`cloud_user_id`)

2. **articles**
   - Attributes: `id`, `title`, `content`, `author_id`, `created_at`, `last_modified_at`
   - Constraints: Primary Key (`id`), Foreign Key (`author_id` → user_accounts)

3. **comments**
   - Attributes: `id`, `content`, `author_id`, `article_id`, `created_at`, `last_modified_at`
   - Constraints: Primary Key (`id`), Foreign Keys (`author_id` → user_accounts, `article_id` → articles), CHECK constraints for content length.

4. **reaction**
   - Attributes: `id`, `reaction_type`, `author_id`, `article_id`, `created_at`, `last_modified_at`
   - Constraints: Primary Key (`id`), Foreign Keys (`author_id` → user_accounts, `article_id` → articles), CHECK constraint for reaction type ("like" or "dislike"), UNIQUE constraint on (`author_id`, `article_id`).

5. **views**
   - Attributes: `id`, `article_id`, `user_id`, `created_at`
   - Constraints: Primary Key (`id`), Foreign Keys (`user_id` → user_accounts, `article_id` → articles).

---

## Setup Instructions

### Prerequisites:
1. PostgreSQL installed on your system.
2. Basic knowledge of SQL commands.

### Steps:
1. Clone the repository or download the SQL scripts.
2. Open PostgreSQL terminal or any database client (e.g., pgAdmin).
3. Execute the following SQL commands in order:

