# Next.js Blog Platform

A modern, full-stack blog application built with Next.js, Drizzle ORM, and PostgreSQL. Features user management with role-based access, blog posts with comments and likes.

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     Client Layer                             │
│  (Next.js Pages, React Components, Tailwind CSS)            │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────┐
│                     Next.js Server                           │
│  (API Routes, Server Components, Middleware)                │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────┐
│                  Drizzle ORM Layer                           │
│  (Database abstraction, query building)                     │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────┐
│              PostgreSQL Database (Neon)                      │
│                                                              │
│  Tables:                                                     │
│  ├── users (id, name, email, role, createdAt, updatedAt)   │
│  ├── posts (id, title, content, author, createdAt, ...)    │
│  ├── comments (id, postId, userId, content, ...)           │
│  └── post_likes (postId, userId)                           │
└─────────────────────────────────────────────────────────────┘
```

## Quick Start

### Prerequisites
- Node.js 18+ 
- pnpm (or npm/yarn)
- PostgreSQL database (Neon account recommended)

### Installation

1. **Clone and install dependencies:**
```bash
git clone <repository-url>
cd nextjs1516-blog
pnpm install
```

2. **Configure environment:**
Create a `.env.local` file with your database URL:
```
DATABASE_URL=postgresql://user:password@host/database
```

3. **Set up the database:**
```bash
# Generate initial migration
pnpm run db:generate

# Run migrations
pnpm run db:migrate

# Seed with sample data
pnpm run db:seed
```

4. **Start development server:**
```bash
pnpm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

## Available Scripts

- `pnpm run dev` - Start development server
- `pnpm run build` - Build for production
- `pnpm run start` - Start production server
- `pnpm run lint` - Run ESLint
- `pnpm run db:generate` - Generate new migrations
- `pnpm run db:migrate` - Apply pending migrations
- `pnpm run db:studio` - Open Drizzle Studio GUI
- `pnpm run db:seed` - Seed database with sample data

## Project Structure

```
src/
├── app/              # Next.js app directory
│   ├── page.tsx      # Homepage
│   ├── layout.tsx    # Root layout
│   └── globals.css   # Global styles
└── db/               # Database layer
    ├── schema.ts     # Database schema definitions
    ├── drizzle.ts    # Drizzle client configuration
    └── seed.ts       # Database seeding script
```

## Technology Stack

- **Framework**: Next.js 16
- **UI Library**: React 19
- **Styling**: Tailwind CSS 4
- **ORM**: Drizzle 0.44.7
- **Database**: PostgreSQL (Neon)
- **Language**: TypeScript 5
- **Linting**: ESLint 9

## Database Schema

### Users
- Roles: admin, editor, viewer
- Tracks creation and update timestamps
- Email is unique

### Posts
- Written by users (author relationship)
- Contains title and content
- Automatically cascades delete when author is removed

### Comments
- Associated with posts and users
- Can exist without a user (anonymous comments)
- Cascades delete when post is deleted

### Post Likes
- Many-to-many relationship between users and posts
- Composite primary key (postId, userId)

## Development Workflow

1. Create a new feature branch
2. Make changes and test locally
3. Generate migrations if schema changes: `pnpm run db:generate`
4. Run migrations: `pnpm run db:migrate`
5. Commit and push changes
6. Create a pull request

## Deployment

This project is ready to deploy to:
- **Vercel** - Recommended for Next.js (supports serverless functions)
- **Other platforms** - Configure Node.js environment with the same database connection

## Learn More

- [Next.js Documentation](https://nextjs.org/docs)
- [Drizzle ORM](https://orm.drizzle.team/)
- [Neon Database](https://neon.tech/)
- [Tailwind CSS](https://tailwindcss.com/)
