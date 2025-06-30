# Citizen AI - Civic Engagement Platform

## Overview

Citizen AI is a modern civic engagement platform that combines React frontend with Express backend to help citizens interact with government services through AI-powered assistance. The platform provides intelligent responses to civic questions, policy analysis, and streamlined communication with government officials.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript for type safety
- **Build Tool**: Vite for fast development and optimized production builds
- **Routing**: Wouter for lightweight client-side routing
- **State Management**: TanStack Query for server state management and caching
- **UI Framework**: Shadcn/ui component library built on Radix UI primitives
- **Styling**: Tailwind CSS with custom civic-themed color variables

### Backend Architecture
- **Runtime**: Node.js with Express.js framework
- **Language**: TypeScript with ES modules
- **API Design**: RESTful endpoints for chat, questions, policies, and contact
- **Error Handling**: Centralized middleware for consistent error responses
- **Development**: Hot reloading integration with Vite

### Database & ORM
- **Database**: PostgreSQL (designed for Neon Database serverless)
- **ORM**: Drizzle ORM with TypeScript for type-safe database operations
- **Schema Management**: Drizzle Kit for migrations and schema changes
- **Connection Strategy**: Pool-based connections optimized for serverless environments

## Key Components

### AI Integration
- **Provider**: OpenAI GPT-4o for natural language processing
- **Core Services**:
  - Civic response generation for general government inquiries
  - Automatic categorization of citizen questions
  - Policy analysis and plain-language summaries
- **Features**: Context-aware responses, session management, feedback collection

### Data Models
- **Users**: Basic authentication and user management system
- **Citizen Questions**: Categorized inquiries with status tracking (pending/answered/forwarded)
- **AI Responses**: Generated responses with helpfulness ratings
- **Chat Messages**: Session-based conversation history
- **Policy Topics**: Structured policy information with engagement metrics
- **Contact Messages**: Direct communication channels with government officials

### User Interface Sections
- **Hero Landing**: Clear call-to-action for civic engagement
- **AI Chat Interface**: Real-time conversation with civic AI assistant
- **Question Submission**: Structured form for detailed citizen inquiries
- **Policy Center**: Browse and search government policies by category
- **FAQ Section**: Common questions and answers about the platform
- **Contact Options**: Multiple channels for citizen-government communication

## Data Flow

1. **User Interaction**: Citizens access the platform through the React frontend
2. **AI Processing**: Questions are sent to OpenAI API for intelligent responses
3. **Data Storage**: All interactions are stored in PostgreSQL via Drizzle ORM
4. **Response Delivery**: AI-generated responses are returned to users in real-time
5. **Feedback Loop**: User feedback on response helpfulness improves future interactions

## External Dependencies

- **OpenAI API**: GPT-4o model for natural language processing
- **Neon Database**: Serverless PostgreSQL hosting
- **Radix UI**: Accessible component primitives
- **TanStack Query**: Server state management and caching
- **React Hook Form**: Form validation and management

## Deployment Strategy

- **Build Process**: Vite builds frontend assets, esbuild bundles server code
- **Environment**: Designed for serverless deployment (Replit, Vercel, etc.)
- **Database**: Serverless PostgreSQL with connection pooling
- **Static Assets**: Frontend builds to `dist/public` directory
- **Server**: Express server serves both API and static files

## Changelog

- June 30, 2025. Initial setup

## User Preferences

Preferred communication style: Simple, everyday language.