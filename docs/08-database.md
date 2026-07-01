# PokéOS Database Design

> **Version:** 0.1.0  
> **Status:** Draft  
> **Last Updated:** 1 July 2026

---

# Purpose

This document defines the planned database architecture for PokéOS.

Its purpose is to identify the core entities, relationships and data requirements before development begins. The design focuses on scalability, maintainability and flexibility, allowing new features to be added without major structural changes.

---

# Design Goals

The database should be:

- Scalable
- Secure
- Easy to maintain
- Easy to query
- Highly modular
- Built around user-owned data

---

# Technology

| Component | Technology      |
| --------- | --------------- |
| Database  | PostgreSQL      |
| ORM       | Prisma          |
| Hosting   | Neon PostgreSQL |

---

# High-Level Architecture

```text
User
│
├── Trainer Profile
├── User Settings
├── Teams
├── Card Collection
├── Living Dex
├── Shiny Hunts
├── Quest Progress
├── Achievement Progress
└── Activity Log
```

---

# Core Entities

## User

Represents an authenticated PokéOS account.

### Fields

- id
- email
- username
- createdAt
- updatedAt

### Relationships

- One Trainer Profile
- One User Settings
- Many Teams
- Many Collection Entries
- Many Activities

---

## Trainer Profile

Stores personalised trainer information.

### Fields

- id
- userId
- trainerName
- avatarUrl
- favouritePokemon
- favouriteRegion
- favouriteGeneration
- favouriteType
- trainerLevel
- xp

---

## User Settings

Stores user preferences.

### Fields

- id
- userId
- theme
- dashboardLayout
- notificationSettings
- privacySettings

---

# Pokédex

## Pokémon

Stores Pokémon reference data.

### Fields

- id
- pokedexNumber
- name
- generation
- primaryType
- secondaryType
- height
- weight
- baseStats
- imageUrl

Reference data should be synchronised from external APIs where possible.

---

## Pokémon Ability

Stores Pokémon abilities.

### Fields

- id
- name
- description

---

## Pokémon Move

Stores move information.

### Fields

- id
- name
- type
- category
- power
- accuracy
- pp

---

## Evolution

Stores evolution relationships.

### Fields

- id
- fromPokemon
- toPokemon
- method
- level
- item

---

# Team Builder

## Team

Stores a saved Pokémon team.

### Fields

- id
- userId
- name
- description
- format
- favourite
- createdAt

---

## Team Member

Stores individual Pokémon within a team.

### Fields

- id
- teamId
- pokemonId
- nickname
- level
- nature
- ability
- heldItem
- teraType
- moveOne
- moveTwo
- moveThree
- moveFour

---

# Trading Card Game

## Card Set

Stores Pokémon TCG expansion information.

### Fields

- id
- code
- name
- series
- releaseDate
- totalCards

---

## Card

Stores Pokémon TCG card information.

### Fields

- id
- setId
- cardNumber
- name
- rarity
- artist
- imageUrl
- marketPrice

---

## User Card

Represents a card owned by a user.

### Fields

- id
- userId
- cardId
- quantity
- condition
- favourite
- wishlist
- trade
- purchasePrice
- notes

---

# Living Dex

## Living Dex Entry

Tracks Pokémon owned by a user.

### Fields

- id
- userId
- pokemonId
- owned
- shiny
- lucky
- alpha
- favourite
- game

---

# Shiny Tracker

## Shiny Hunt

Stores active shiny hunts.

### Fields

- id
- userId
- pokemonId
- game
- method
- encounters
- status
- startedAt
- completedAt

---

# Quest System

## Quest

Stores available quests.

### Fields

- id
- title
- description
- frequency
- xpReward

---

## Quest Progress

Stores user quest progress.

### Fields

- id
- userId
- questId
- progress
- status
- completedAt

---

# Achievements

## Achievement

Stores available achievements.

### Fields

- id
- title
- description
- badge
- xpReward

---

## User Achievement

Tracks unlocked achievements.

### Fields

- id
- userId
- achievementId
- unlockedAt

---

# Pokémon GO

## GO Event

Stores Pokémon GO events.

### Fields

- id
- title
- eventType
- description
- startDate
- endDate
- sourceUrl

---

# Notifications

## Notification

Stores user notifications.

### Fields

- id
- userId
- title
- message
- type
- read
- createdAt

---

# Activity Log

Tracks recent user activity.

### Fields

- id
- userId
- activityType
- description
- metadata
- createdAt

Example activity types:

- Team Created
- Card Added
- Collection Updated
- Quest Completed
- Achievement Unlocked

---

# Entity Relationships

```text
User
├── Trainer Profile
├── User Settings
├── Team
│   └── Team Member
├── User Card
├── Living Dex Entry
├── Shiny Hunt
├── Quest Progress
├── Achievement Progress
├── Notification
└── Activity Log

Card Set
└── Card

Pokémon
├── Ability
├── Move
└── Evolution
```

---

# MVP Database

The first release of PokéOS will include the following entities:

- User
- Trainer Profile
- User Settings
- Pokémon
- Team
- Team Member
- Card Set
- Card
- User Card
- Activity Log

---

# Future Database Modules

Future versions will introduce:

- Living Dex
- Shiny Tracker
- Quest System
- Achievement System
- Pokémon GO Events
- Notifications
- Marketplace
- Friends
- Community
- Trading

---

# Database Design Principles

## User First

All personalised data belongs to a User.

---

## Reference Data

Pokémon and Trading Card data should be stored separately from user-owned data.

Example:

- Card = Card information
- User Card = User ownership

---

## Minimise Duplication

Store shared information once wherever possible.

---

## Modular Design

Each PokéOS application should have clearly defined entities that integrate through shared user data.

---

## Future Proof

The schema should support additional applications and integrations without requiring major redesigns.

---

# Notes

This document defines the logical database architecture for PokéOS.

The implementation will later be translated into a Prisma schema during the development phase and may evolve as requirements change.
