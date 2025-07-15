# Online Code Compiler/Editor

## Overview

This is a web-based code editor and compiler that allows users to write, execute, and test code in multiple programming languages. The application provides a VS Code-like editing experience with syntax highlighting, real-time code execution, and output display.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Build Tool**: Vite for fast development and optimized builds
- **Styling**: Tailwind CSS with shadcn/ui component library
- **State Management**: TanStack Query for server state management
- **Routing**: Wouter for lightweight client-side routing
- **Code Editor**: Monaco Editor (VS Code's editor) for syntax highlighting and code editing
- **Theme System**: Custom theme provider supporting light/dark modes

### Backend Architecture
- **Runtime**: Node.js with Express.js
- **Language**: TypeScript with ES modules
- **Database**: PostgreSQL with Drizzle ORM
- **Database Provider**: Neon Database serverless
- **Session Management**: PostgreSQL-backed sessions with connect-pg-simple
- **API Design**: RESTful API with structured error handling

### Key Components

#### Code Editor Features
- Multi-language support (Python, JavaScript, Java, C++, C, Go, Rust, TypeScript, PHP, Ruby, Swift, Kotlin)
- Monaco Editor with custom themes and configurations
- Auto-save functionality with localStorage persistence
- Input/output handling for code execution
- Execution metrics display (time, memory usage, status)

#### UI Components
- Comprehensive shadcn/ui component library
- Responsive design with mobile support
- Toast notifications for user feedback
- Theme switching capabilities
- Loading states and error handling

#### Language Support
- Predefined code templates for each language
- Language-specific Monaco configurations
- File extension mapping
- Default code examples (Fibonacci implementation)

## Data Flow

### Code Execution Flow
1. User selects programming language from dropdown
2. User writes code in Monaco Editor
3. Optional: User provides stdin input
4. User clicks "Run" button
5. Frontend sends POST request to `/api/execute` with code, language, and stdin
6. Backend validates request using Zod schema
7. Backend maps language to Piston API format
8. Backend makes API call to Piston execution service
9. Backend processes response and returns execution results
10. Frontend displays output, errors, and execution metrics

### Data Storage
- Code submissions stored in PostgreSQL database
- User sessions managed with PostgreSQL-backed store
- Client-side code persistence using localStorage
- Database schema includes users and code_submissions tables

## External Dependencies

### Code Execution Service
- **Piston API**: Free and open-source code execution service
- **API Endpoint**: https://emkc.org/api/v2/piston/execute
- **No API Key Required**: Completely free to use
- **Rate Limiting**: No rate limiting on free tier
- **Supported Languages**: 70+ programming languages

### Database Service
- **Neon Database**: Serverless PostgreSQL provider
- **Connection**: Uses DATABASE_URL environment variable
- **ORM**: Drizzle ORM for type-safe database operations

### UI Dependencies
- **Radix UI**: Headless UI components for accessibility
- **Tailwind CSS**: Utility-first CSS framework
- **Lucide React**: Icon library
- **Monaco Editor**: VS Code's editor component

## Deployment Strategy

### Development
- Vite dev server for frontend with HMR
- tsx for TypeScript execution in development
- Integrated development setup with single command (`npm run dev`)

### Production Build
- Vite builds frontend to `dist/public`
- esbuild bundles backend to `dist/index.js`
- Static file serving for production assets
- Environment variable configuration for API keys and database

### Database Management
- Drizzle migrations in `./migrations` directory
- Schema definition in `shared/schema.ts`
- Push-based database updates with `npm run db:push`

### Environment Configuration
- `NODE_ENV` for environment detection
- `DATABASE_URL` for database connection
- No API keys required for code execution (using free Piston API)
- Replit-specific configurations for development environment

The application follows a full-stack TypeScript approach with shared types and schemas, ensuring type safety across the entire application stack.