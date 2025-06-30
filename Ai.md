# Citizen AI - Civic Engagement Platform

## Overview

Citizen AI is a modern civic engagement platform built with React and Express, designed to help citizens interact with government services through AI-powered assistance. The platform provides intelligent responses to civic questions, policy information, and streamlined communication with government officials.

## System Architecture

### Frontend Architecture
- **Framework**: React with TypeScript
- **Build Tool**: Vite for fast development and optimized builds
- **Routing**: Wouter for lightweight client-side routing
- **State Management**: TanStack Query for server state management
- **UI Components**: Shadcn/ui component library with Tailwind CSS
- **Styling**: Tailwind CSS with custom civic color variables

### Backend Architecture
- **Runtime**: Node.js with Express.js framework
- **Language**: TypeScript with ESM modules
- **API Pattern**: RESTful API design
- **Error Handling**: Centralized error handling middleware
- **Development**: Hot reloading via Vite integration

### Database & ORM
- **Database**: PostgreSQL with Neon Database serverless
- **ORM**: Drizzle ORM for type-safe database operations
- **Schema Management**: Drizzle Kit for migrations
- **Connection**: Pool-based connections for optimal performance

## Key Components

### AI Integration
- **Provider**: OpenAI GPT-4o for natural language processing
- **Services**: 
  - Civic response generation for general inquiries
  - Citizen question categorization
  - Policy analysis and summarization
- **Features**: Context-aware responses, session management, response quality tracking

### Data Models
- **Users**: Basic user authentication and management
- **Citizen Questions**: Categorized citizen inquiries with status tracking
- **AI Responses**: Generated responses with helpfulness feedback
- **Chat Messages**: Session-based chat history
- **Policy Topics**: Structured policy information with engagement metrics
- **Contact Messages**: Direct communication with government officials

### User Interface Sections
- **Hero Section**: Landing page with call-to-action
- **AI Chat**: Real-time chat interface with the AI assistant
- **Submission Form**: Structured question submission with categorization
- **Policy Center**: Browse and search policy topics by category
- **FAQ Section**: Common questions and answers
- **Contact Section**: Multiple communication channels
- **Features Section**: Platform capabilities overview

## Data Flow

1. **User Interaction**: Citizens access the platform through a responsive web interface
2. **Question Processing**: User questions are categorized and processed by AI services
3. **Response Generation**: OpenAI generates contextually appropriate civic responses
4. **Data Persistence**: All interactions are stored in PostgreSQL for tracking and analysis
5. **Feedback Loop**: Users can rate responses to improve AI performance over time

## External Dependencies

### Core Dependencies
- **@neondatabase/serverless**: Serverless PostgreSQL connection
- **drizzle-orm**: Type-safe ORM for database operations
- **openai**: Official OpenAI API client
- **@tanstack/react-query**: Server state management
- **express**: Web application framework

### UI Dependencies
- **@radix-ui/***: Accessible UI primitives
- **tailwindcss**: Utility-first CSS framework
- **lucide-react**: Icon library
- **react-hook-form**: Form handling with validation

### Development Dependencies
- **vite**: Build tool and development server
- **typescript**: Type safety and development experience
- **tsx**: TypeScript execution for Node.js

## Deployment Strategy

### Build Process
- **Frontend**: Vite builds optimized static assets
- **Backend**: esbuild bundles server code with external dependencies
- **Database**: Drizzle migrations handle schema changes

### Environment Configuration
- **Development**: Local development with hot reloading
- **Production**: Compiled JavaScript with environment-specific configurations
- **Database**: Environment-based connection strings

### Hosting Requirements
- Node.js runtime environment
- PostgreSQL database (Neon Database recommended)
- Environment variables for API keys and database connections
- Static file serving for frontend assets

## Changelog

```
Changelog:
- June 30, 2025. Initial setup
```

## User Preferences

```
Preferred communication style: Simple, everyday language.
```