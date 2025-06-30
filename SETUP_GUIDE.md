# Citizen AI - Setup Guide

## Prerequisites
- Node.js 18+ installed
- VS Code or any code editor
- OpenAI API key (get from https://platform.openai.com)

## Quick Setup Steps

### 1. Create Project Structure
```bash
mkdir citizen-ai
cd citizen-ai
npm init -y
```

### 2. Install Dependencies
```bash
# Core dependencies
npm install @hookform/resolvers @neondatabase/serverless @radix-ui/react-accordion @radix-ui/react-alert-dialog @radix-ui/react-aspect-ratio @radix-ui/react-avatar @radix-ui/react-checkbox @radix-ui/react-collapsible @radix-ui/react-context-menu @radix-ui/react-dialog @radix-ui/react-dropdown-menu @radix-ui/react-hover-card @radix-ui/react-label @radix-ui/react-menubar @radix-ui/react-navigation-menu @radix-ui/react-popover @radix-ui/react-progress @radix-ui/react-radio-group @radix-ui/react-scroll-area @radix-ui/react-select @radix-ui/react-separator @radix-ui/react-slider @radix-ui/react-slot @radix-ui/react-switch @radix-ui/react-tabs @radix-ui/react-toast @radix-ui/react-toggle @radix-ui/react-toggle-group @radix-ui/react-tooltip @tanstack/react-query class-variance-authority clsx cmdk connect-pg-simple date-fns drizzle-orm drizzle-zod embla-carousel-react express express-session framer-motion input-otp lucide-react memorystore next-themes openai passport passport-local react react-day-picker react-dom react-hook-form react-icons react-resizable-panels recharts tailwind-merge tailwindcss-animate tw-animate-css vaul wouter ws zod zod-validation-error nanoid

# Dev dependencies
npm install -D @types/connect-pg-simple @types/express @types/express-session @types/node @types/passport @types/passport-local @types/react @types/react-dom @types/ws @vitejs/plugin-react autoprefixer drizzle-kit esbuild postcss tailwindcss tsx typescript vite @tailwindcss/typography @tailwindcss/vite
```

### 3. Create Folder Structure
```bash
mkdir -p client/src/{components,hooks,lib,pages,types}
mkdir -p client/src/components/ui
mkdir -p server/services
mkdir -p shared
```

### 4. Configuration Files to Create
1. `package.json` - Update scripts section
2. `tsconfig.json` - TypeScript configuration
3. `vite.config.ts` - Vite configuration
4. `tailwind.config.ts` - Tailwind CSS configuration
5. `postcss.config.js` - PostCSS configuration
6. `components.json` - Shadcn/ui configuration
7. `drizzle.config.ts` - Database configuration

### 5. Environment Variables
Create a `.env` file:
```
OPENAI_API_KEY=your_api_key_here
NODE_ENV=development
```

### 6. Start Development Server
```bash
npm run dev
```

## File Creation Order

1. Configuration files (package.json, tsconfig.json, etc.)
2. Shared schema (`shared/schema.ts`)
3. Server storage (`server/storage.ts`)
4. Server OpenAI service (`server/services/openai.ts`)
5. Server routes (`server/routes.ts`)
6. Server main file (`server/index.ts`)
7. Client utilities (`client/src/lib/`)
8. Client components (`client/src/components/`)
9. Client pages (`client/src/pages/`)
10. Client main files (`client/src/App.tsx`, `client/src/main.tsx`)
11. HTML entry point (`client/index.html`)

## Important Notes

- Make sure to add `.env` to your `.gitignore` file
- The project uses in-memory storage, no database setup required
- All AI features require an OpenAI API key
- The project is fully responsive and mobile-friendly
- Uses TypeScript for type safety
- Includes comprehensive error handling

## Features Included

✅ AI-powered chat assistant
✅ Question submission with AI responses
✅ Policy center with categorized topics
✅ Contact forms and FAQ section
✅ Responsive design with modern UI
✅ Type-safe API with validation
✅ Real-time chat functionality
✅ Privacy-focused data handling

## Next Steps After Setup

1. Get your OpenAI API key and add it to `.env`
2. Run `npm run dev` to start the development server
3. Open `http://localhost:5000` in your browser
4. Test the AI chat functionality
5. Customize the content and styling as needed
6. Deploy to your preferred hosting platform