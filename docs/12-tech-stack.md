# PokéOS Tech Stack

> **Version:** 0.1.0
> **Status:** Draft
> **Last Updated:** 1 July 2026

---

# Purpose

This document defines the planned technology stack for PokéOS.

Its purpose is to explain which technologies will be used, why they are being considered and what role each technology plays in the overall application.

This document should be updated whenever a major technology decision changes.

---

# Tech Stack Philosophy

PokéOS should use technologies that support:

- Long-term maintainability
- Strong developer experience
- Type safety
- Scalability
- Fast iteration
- Modern UI development
- Clear project structure
- Reliable deployment

The goal is not to use every popular tool.

The goal is to choose tools that work well together and support the product vision.

---

# Stack Summary

| Area               | Recommended Tool  |
| ------------------ | ----------------- |
| Framework          | Next.js           |
| Language           | TypeScript        |
| Styling            | Tailwind CSS      |
| UI Components      | Custom components |
| Database           | PostgreSQL        |
| ORM                | Prisma            |
| Authentication     | Clerk             |
| Hosting            | Vercel            |
| Database Hosting   | Neon PostgreSQL   |
| Server State       | TanStack Query    |
| Client State       | Zustand           |
| Forms              | React Hook Form   |
| Validation         | Zod               |
| Testing            | Vitest            |
| End-to-End Testing | Playwright        |
| Error Monitoring   | Sentry            |
| Analytics          | Vercel Analytics  |
| Package Manager    | pnpm              |
| Version Control    | GitHub            |
| Project Management | GitHub Projects   |

---

# Frontend

---

## Next.js

**Status:** Recommended
**Priority:** High
**MVP Required:** Yes

## Purpose

Next.js will be the main application framework for PokéOS.

It will handle:

- Routing
- Pages
- Layouts
- Server rendering
- Client rendering
- API routes or route handlers
- Deployment compatibility
- Full-stack application structure

## Why Next.js

Next.js is a strong fit for PokéOS because the project requires both frontend and backend functionality.

PokéOS needs:

- Public pages
- Protected user dashboards
- Server-side data loading
- API endpoints
- Authentication
- Database integration
- Responsive UI
- Good deployment support

Next.js supports all of these in one framework.

## Recommended Approach

Use:

- App Router
- Server Components where appropriate
- Client Components for interactive UI
- Route Handlers for internal API endpoints
- Server Actions only where they simplify forms or mutations

## Alternatives Considered

- Astro
- Vite + React
- Remix
- SvelteKit
- Nuxt

## Decision

Use Next.js for the MVP.

---

## TypeScript

**Status:** Recommended
**Priority:** High
**MVP Required:** Yes

## Purpose

TypeScript will be used across the PokéOS codebase.

## Why TypeScript

PokéOS will have many data models, API responses and user-generated records.

TypeScript helps prevent common errors by making data structures explicit.

It is useful for:

- API responses
- Database models
- Component props
- Form data
- Team data
- TCG collection data
- User profile data

## Decision

Use TypeScript throughout the project.

---

# Styling

---

## Tailwind CSS

**Status:** Recommended
**Priority:** High
**MVP Required:** Yes

## Purpose

Tailwind CSS will be used for styling the PokéOS interface.

## Why Tailwind CSS

PokéOS needs a polished, responsive and highly custom user interface.

Tailwind is useful because it allows fast UI development without creating large custom CSS files.

It supports:

- Responsive design
- Design tokens
- Consistent spacing
- Dark mode
- Utility-first styling
- Rapid prototyping

## Recommended Approach

Use Tailwind for:

- Layouts
- Spacing
- Typography
- Colours
- Responsive behaviour
- Component styling

Avoid overusing custom CSS unless Tailwind cannot handle the requirement cleanly.

## Alternatives Considered

- CSS Modules
- Sass
- Styled Components
- Vanilla CSS
- Chakra UI
- Material UI

## Decision

Use Tailwind CSS for the MVP.

---

# UI Components

---

## Custom Component Library

**Status:** Recommended
**Priority:** High
**MVP Required:** Yes

## Purpose

PokéOS should use its own reusable component system.

## Components To Build

- Button
- Card
- Input
- Modal
- Sheet
- Navigation Item
- Sidebar
- App Icon
- Dashboard Widget
- Progress Bar
- Badge
- Avatar
- Tabs
- Search Bar
- Loading State
- Empty State
- Error State

## Why Custom Components

PokéOS has a very specific design direction.

A custom component library allows the app to feel unique while still remaining consistent.

## Possible Supporting Libraries

- Radix UI
- shadcn/ui
- Lucide React

## Recommendation

Use custom components, supported by Radix UI or shadcn/ui where useful.

Do not rely too heavily on a generic component library because PokéOS should have its own identity.

---

# Backend

---

## Next.js Route Handlers

**Status:** Recommended
**Priority:** High
**MVP Required:** Yes

## Purpose

Route Handlers will provide internal API endpoints for PokéOS.

## Example API Areas

- Profile
- Dashboard
- Teams
- TCG Collection
- Pokédex cache
- Settings
- Activity log

## Why Route Handlers

They keep the backend close to the frontend and reduce the need for a separate backend service during the MVP.

## Decision

Use Next.js Route Handlers for the MVP.

---

# Database

---

## PostgreSQL

**Status:** Recommended
**Priority:** High
**MVP Required:** Yes

## Purpose

PostgreSQL will store PokéOS application data.

## Data Stored

- Users
- Trainer profiles
- Settings
- Teams
- Team members
- Card collections
- Wishlists
- Activity logs
- Cached Pokémon data
- Cached TCG data

## Why PostgreSQL

PokéOS has relational data.

Examples:

- One user has many teams.
- One team has many Pokémon.
- One user owns many cards.
- One card belongs to one set.
- One user has many activities.

PostgreSQL is a strong fit for this type of structured data.

## Alternatives Considered

- MongoDB
- Firebase
- SQLite
- Supabase-only client model

## Decision

Use PostgreSQL as the main database.

---

## Prisma

**Status:** Recommended
**Priority:** High
**MVP Required:** Yes

## Purpose

Prisma will be used as the ORM for database access.

## Why Prisma

Prisma provides:

- Type-safe database queries
- Schema management
- Database migrations
- Clear data modelling
- Good TypeScript support

## Use Cases

Prisma will be used for:

- User profile queries
- Team queries
- Collection queries
- Activity log queries
- Cached API data
- Admin data management

## Alternatives Considered

- Drizzle
- Raw SQL
- TypeORM
- Supabase client

## Decision

Use Prisma for the MVP unless a better option is identified during setup.

---

## Neon PostgreSQL

**Status:** Recommended
**Priority:** High
**MVP Required:** Yes

## Purpose

Neon is the recommended managed PostgreSQL provider.

## Why Neon

Neon is a strong fit for modern serverless web applications.

It provides:

- Managed PostgreSQL
- Good developer experience
- Database branching
- Serverless-friendly usage
- Easy integration with modern JavaScript apps

## Alternatives Considered

- Supabase
- Railway
- Render
- Prisma Postgres

## Decision

Use a managed PostgreSQL provider.

Neon is the preferred first option, but the final provider can be confirmed during project setup.

---

# Authentication

---

## Clerk

**Status:** Recommended
**Priority:** High
**MVP Required:** Yes

## Purpose

Clerk will manage authentication and user sessions.

## Features

- Sign up
- Login
- Logout
- Session management
- Google authentication
- GitHub authentication
- Protected routes
- User management

## Why Clerk

Clerk reduces the amount of custom authentication code needed.

This lets development focus on PokéOS features instead of building authentication from scratch.

## Alternatives Considered

- Auth.js
- Supabase Auth
- Better Auth
- Custom authentication

## Risks

- External vendor dependency
- Pricing should be reviewed before public launch
- Migration may require work later

## Decision

Use Clerk for MVP authentication unless the project later decides to avoid external auth vendors.

---

# State Management

---

## TanStack Query

**Status:** Recommended
**Priority:** Medium
**MVP Required:** Yes

## Purpose

TanStack Query will manage server state.

## Server State Examples

- Pokémon data
- TCG card data
- Teams
- User profile
- Collection data
- Dashboard data

## Why TanStack Query

TanStack Query helps manage:

- Data fetching
- Loading states
- Error states
- Caching
- Refetching
- Mutations

## Decision

Use TanStack Query for client-side server-state handling where required.

---

## Zustand

**Status:** Recommended
**Priority:** Medium
**MVP Required:** Maybe

## Purpose

Zustand will manage lightweight client state.

## Client State Examples

- Sidebar open or closed
- Active app window
- Theme toggle
- Temporary Team Builder state
- Local UI preferences

## Why Zustand

Zustand is small, simple and does not require lots of boilerplate.

## Decision

Use Zustand only when React state becomes too messy.

Do not add global state unnecessarily.

---

# Forms and Validation

---

## React Hook Form

**Status:** Recommended
**Priority:** Medium
**MVP Required:** Yes

## Purpose

React Hook Form will manage user forms.

## Example Forms

- Profile setup
- Team creation
- Team editing
- Card collection updates
- Settings
- Search filters

## Decision

Use React Hook Form for important forms.

---

## Zod

**Status:** Recommended
**Priority:** High
**MVP Required:** Yes

## Purpose

Zod will handle schema validation.

## Use Cases

- Form validation
- API request validation
- Environment variable validation
- Data parsing
- Type-safe schemas

## Why Zod

Zod works well with TypeScript and helps ensure data is valid before it reaches the database.

## Decision

Use Zod for validation.

---

# External APIs

---

## PokéAPI

**Status:** Confirmed
**Priority:** High
**MVP Required:** Yes

## Purpose

Primary Pokémon reference data.

## Used For

- Pokémon search
- Pokémon details
- Types
- Abilities
- Moves
- Evolutions
- Forms

## Decision

Use PokéAPI REST for the MVP.

---

## Pokémon TCG API

**Status:** Confirmed
**Priority:** High
**MVP Required:** Yes

## Purpose

Primary TCG card and set data.

## Used For

- Card search
- Set search
- Card details
- Collection tracking
- Wishlist
- Set completion

## Decision

Use Pokémon TCG API with an API key.

---

# Testing

---

## Vitest

**Status:** Recommended
**Priority:** Medium
**MVP Required:** Yes

## Purpose

Vitest will be used for unit and integration testing.

## Test Examples

- Utility functions
- Type coverage logic
- Team analysis logic
- Validation schemas
- Data transformation functions

## Decision

Use Vitest for unit and integration tests.

---

## Playwright

**Status:** Recommended
**Priority:** Medium
**MVP Required:** Later MVP

## Purpose

Playwright will be used for end-to-end testing.

## Test Examples

- User can log in
- User can create a team
- User can search Pokémon
- User can add a card to collection
- User can update profile

## Decision

Use Playwright before public preview.

It does not need to be configured on day one.

---

# Monitoring and Analytics

---

## Sentry

**Status:** Future
**Priority:** Medium
**MVP Required:** No

## Purpose

Sentry may be used for error monitoring.

## Use Cases

- Frontend errors
- Backend errors
- API failures
- Production crashes

## Decision

Add Sentry before public launch or when the app has real users.

---

## Vercel Analytics

**Status:** Future
**Priority:** Low
**MVP Required:** No

## Purpose

Vercel Analytics may be used to track basic usage and performance.

## Decision

Add analytics after the MVP has meaningful user activity.

---

# Deployment

---

## Vercel

**Status:** Recommended
**Priority:** High
**MVP Required:** Yes

## Purpose

Vercel will host the PokéOS web application.

## Why Vercel

Vercel works extremely well with Next.js and provides:

- Simple deployments
- GitHub integration
- Preview deployments
- Environment variables
- Serverless support
- Strong developer experience

## Decision

Use Vercel for deployment.

---

# Package Manager

---

## pnpm

**Status:** Recommended
**Priority:** Medium
**MVP Required:** Yes

## Purpose

pnpm will manage project dependencies.

## Why pnpm

pnpm is fast, efficient and commonly used in modern JavaScript projects.

## Alternatives Considered

- npm
- yarn
- bun

## Decision

Use pnpm unless tooling conflicts appear.

---

# Code Quality

---

## ESLint

**Status:** Recommended
**Priority:** High
**MVP Required:** Yes

## Purpose

ESLint will help catch code issues.

## Decision

Use ESLint from the start.

---

## Prettier

**Status:** Recommended
**Priority:** High
**MVP Required:** Yes

## Purpose

Prettier will format code consistently.

## Decision

Use Prettier from the start.

---

# Version Control and Project Management

---

## GitHub

**Status:** Confirmed
**Priority:** High
**MVP Required:** Yes

## Purpose

GitHub will be used for:

- Version control
- Issues
- Pull requests
- Project board
- Documentation
- Releases

## Decision

Use GitHub for all project management and code tracking.

---

## GitHub Projects

**Status:** Confirmed
**Priority:** High
**MVP Required:** Yes

## Purpose

GitHub Projects will track:

- Epics
- Features
- Tasks
- Bugs
- Roadmap progress
- Release planning

## Decision

Use GitHub Projects as the main project management tool.

---

# Recommended Initial Install Stack

The initial setup should include:

```text
Next.js
TypeScript
Tailwind CSS
ESLint
Prettier
Prisma
Clerk
Zod
React Hook Form
TanStack Query
```

Testing and monitoring tools can be added after the first working app shell exists.

---

# MVP Stack

The MVP should use:

| Area             | Tool            |
| ---------------- | --------------- |
| Framework        | Next.js         |
| Language         | TypeScript      |
| Styling          | Tailwind CSS    |
| Auth             | Clerk           |
| Database         | PostgreSQL      |
| ORM              | Prisma          |
| Hosting          | Vercel          |
| Database Hosting | Neon            |
| Forms            | React Hook Form |
| Validation       | Zod             |
| Server State     | TanStack Query  |
| Client State     | Zustand         |
| Unit Testing     | Vitest          |
| E2E Testing      | Playwright      |

---

# Future Stack Considerations

These tools may be considered later:

## Mobile

- React Native
- Expo

## Notifications

- Firebase Cloud Messaging
- OneSignal
- Resend

## AI

- OpenAI API
- Anthropic API

## Search

- Meilisearch
- Algolia
- PostgreSQL full-text search

## Background Jobs

- Inngest
- Trigger.dev
- Vercel Cron Jobs

## File Storage

- Vercel Blob
- UploadThing
- Supabase Storage

---

# Stack Risks

## Vendor Lock-In

Tools like Clerk, Vercel and Neon are external providers.

Risk:

The project may become dependent on third-party pricing or platform changes.

Mitigation:

Keep the application architecture modular and avoid spreading provider-specific code everywhere.

---

## Over-Engineering

PokéOS could become too complex if too many tools are added too early.

Risk:

Development slows down before the MVP is usable.

Mitigation:

Add tools only when they solve a real problem.

---

## Scope Creep

The project has many possible features.

Risk:

The stack becomes bloated before core functionality is complete.

Mitigation:

Focus on the MVP stack first.

---

# Stack Principles

PokéOS should follow these technical principles:

- Prefer simple solutions first.
- Use TypeScript everywhere.
- Keep user data secure.
- Cache external data where practical.
- Avoid unnecessary dependencies.
- Keep modules separated by feature.
- Add complexity only when the product needs it.
- Keep documentation updated when stack decisions change.

---

# Final Recommendation

The recommended PokéOS stack is:

```text
Next.js
TypeScript
Tailwind CSS
Clerk
PostgreSQL
Prisma
Neon
Vercel
TanStack Query
Zustand
React Hook Form
Zod
Vitest
Playwright
GitHub Projects
```

This stack provides a strong balance between modern development, professional structure and realistic solo-developer maintainability.

It is powerful enough for a large-scale project while still being manageable for the MVP.
