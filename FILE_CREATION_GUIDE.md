# Complete File Creation Guide - Citizen AI Project

## Step-by-Step File Creation

### Phase 1: Setup and Configuration
1. Create project folder and initialize
2. Install dependencies (see CONFIG_FILES.md)
3. Create all configuration files (see CONFIG_FILES.md)

### Phase 2: Backend Files (Create in this order)

#### 1. shared/schema.ts (Database Schema)
```typescript
import { pgTable, text, serial, timestamp, boolean, integer } from "drizzle-orm/pg-core";
import { createInsertSchema } from "drizzle-zod";
import { z } from "zod";

export const users = pgTable("users", {
  id: serial("id").primaryKey(),
  username: text("username").notNull().unique(),
  password: text("password").notNull(),
});

export const citizenQuestions = pgTable("citizen_questions", {
  id: serial("id").primaryKey(),
  category: text("category").notNull(),
  subject: text("subject").notNull(),
  message: text("message").notNull(),
  name: text("name"),
  email: text("email"),
  anonymous: boolean("anonymous").default(false),
  urgent: boolean("urgent").default(false),
  status: text("status").default("pending"),
  createdAt: timestamp("created_at").defaultNow(),
});

export const aiResponses = pgTable("ai_responses", {
  id: serial("id").primaryKey(),
  questionId: integer("question_id").references(() => citizenQuestions.id),
  response: text("response").notNull(),
  helpful: boolean("helpful"),
  createdAt: timestamp("created_at").defaultNow(),
});

export const chatMessages = pgTable("chat_messages", {
  id: serial("id").primaryKey(),
  message: text("message").notNull(),
  response: text("response").notNull(),
  sessionId: text("session_id"),
  createdAt: timestamp("created_at").defaultNow(),
});

export const policyTopics = pgTable("policy_topics", {
  id: serial("id").primaryKey(),
  title: text("title").notNull(),
  description: text("description").notNull(),
  category: text("category").notNull(),
  icon: text("icon").notNull(),
  viewCount: integer("view_count").default(0),
  helpfulCount: integer("helpful_count").default(0),
  createdAt: timestamp("created_at").defaultNow(),
});

export const contactMessages = pgTable("contact_messages", {
  id: serial("id").primaryKey(),
  name: text("name").notNull(),
  email: text("email").notNull(),
  subject: text("subject").notNull(),
  message: text("message").notNull(),
  createdAt: timestamp("created_at").defaultNow(),
});

// Insert schemas
export const insertCitizenQuestionSchema = createInsertSchema(citizenQuestions).omit({
  id: true,
  createdAt: true,
  status: true,
});

export const insertAiResponseSchema = createInsertSchema(aiResponses).omit({
  id: true,
  createdAt: true,
});

export const insertChatMessageSchema = createInsertSchema(chatMessages).omit({
  id: true,
  createdAt: true,
});

export const insertContactMessageSchema = createInsertSchema(contactMessages).omit({
  id: true,
  createdAt: true,
});

export const insertPolicyTopicSchema = createInsertSchema(policyTopics).omit({
  id: true,
  createdAt: true,
  viewCount: true,
  helpfulCount: true,
});

export const insertUserSchema = createInsertSchema(users).pick({
  username: true,
  password: true,
});

// Types
export type CitizenQuestion = typeof citizenQuestions.$inferSelect;
export type InsertCitizenQuestion = z.infer<typeof insertCitizenQuestionSchema>;
export type AiResponse = typeof aiResponses.$inferSelect;
export type InsertAiResponse = z.infer<typeof insertAiResponseSchema>;
export type ChatMessage = typeof chatMessages.$inferSelect;
export type InsertChatMessage = z.infer<typeof insertChatMessageSchema>;
export type PolicyTopic = typeof policyTopics.$inferSelect;
export type InsertPolicyTopic = z.infer<typeof insertPolicyTopicSchema>;
export type ContactMessage = typeof contactMessages.$inferSelect;
export type InsertContactMessage = z.infer<typeof insertContactMessageSchema>;
export type User = typeof users.$inferSelect;
export type InsertUser = z.infer<typeof insertUserSchema>;
```

#### 2. server/services/openai.ts (AI Service)
```typescript
import OpenAI from "openai";

// the newest OpenAI model is "gpt-4o" which was released May 13, 2024. do not change this unless explicitly requested by the user
const openai = new OpenAI({ 
  apiKey: process.env.OPENAI_API_KEY || process.env.OPENAI_API_KEY_ENV_VAR || "default_key"
});

export interface ChatResponse {
  response: string;
  category?: string;
}

export interface PolicyAnalysis {
  summary: string;
  keyPoints: string[];
  impact: string;
  nextSteps: string[];
}

export async function generateCivicResponse(question: string): Promise<ChatResponse> {
  try {
    const response = await openai.chat.completions.create({
      model: "gpt-4o",
      messages: [
        {
          role: "system",
          content: `You are a helpful civic AI assistant for a citizen engagement platform. You provide accurate, helpful information about government services, policies, procedures, and civic processes. Always be professional, clear, and encouraging of civic participation. If you don't know something specific to a locality, explain general processes and suggest they contact local officials for specific details.`
        },
        {
          role: "user",
          content: question
        }
      ],
      max_tokens: 500,
      temperature: 0.7
    });

    return {
      response: response.choices[0].message.content || "I apologize, but I couldn't generate a response. Please try rephrasing your question."
    };
  } catch (error) {
    console.error("OpenAI API error:", error);
    throw new Error("Failed to generate AI response. Please try again later.");
  }
}

export async function categorizeCitizenQuestion(question: string, subject: string): Promise<string> {
  try {
    const response = await openai.chat.completions.create({
      model: "gpt-4o",
      messages: [
        {
          role: "system",
          content: `Categorize the following citizen question into one of these categories: "policy", "services", "budget", "permits", "infrastructure", "elections", "legal", "other". Respond with only the category name.`
        },
        {
          role: "user",
          content: `Subject: ${subject}\nQuestion: ${question}`
        }
      ],
      max_tokens: 10,
      temperature: 0.1
    });

    const category = response.choices[0].message.content?.toLowerCase().trim() || "other";
    const validCategories = ["policy", "services", "budget", "permits", "infrastructure", "elections", "legal", "other"];
    
    return validCategories.includes(category) ? category : "other";
  } catch (error) {
    console.error("OpenAI categorization error:", error);
    return "other";
  }
}

export async function generateCitizenQuestionResponse(question: string, category: string): Promise<string> {
  try {
    const response = await openai.chat.completions.create({
      model: "gpt-4o",
      messages: [
        {
          role: "system",
          content: `You are a civic AI assistant responding to a citizen's question in the ${category} category. Provide a helpful, detailed response that addresses their concern. Include relevant general information and suggest next steps or resources when appropriate. If the question requires specific local information, suggest they contact the appropriate department.`
        },
        {
          role: "user",
          content: question
        }
      ],
      max_tokens: 400,
      temperature: 0.7
    });

    return response.choices[0].message.content || "Thank you for your question. For specific information about this matter, please contact your local government office or the appropriate department.";
  } catch (error) {
    console.error("OpenAI question response error:", error);
    throw new Error("Failed to generate response to your question. Please try again later.");
  }
}

export async function generatePolicyAnalysis(policyText: string): Promise<PolicyAnalysis> {
  try {
    const response = await openai.chat.completions.create({
      model: "gpt-4o",
      messages: [
        {
          role: "system",
          content: `Analyze the following policy or government document. Provide a JSON response with this structure: {"summary": "brief summary", "keyPoints": ["point1", "point2"], "impact": "citizen impact description", "nextSteps": ["step1", "step2"]}`
        },
        {
          role: "user",
          content: policyText
        }
      ],
      response_format: { type: "json_object" },
      max_tokens: 600,
      temperature: 0.3
    });

    const result = JSON.parse(response.choices[0].message.content || "{}");
    
    return {
      summary: result.summary || "Policy analysis unavailable",
      keyPoints: result.keyPoints || [],
      impact: result.impact || "Impact assessment unavailable",
      nextSteps: result.nextSteps || []
    };
  } catch (error) {
    console.error("OpenAI policy analysis error:", error);
    throw new Error("Failed to analyze policy. Please try again later.");
  }
}
```

### Continue to next phase for storage and routes...

#### 3. server/storage.ts (In-Memory Storage)
Create this file with the storage implementation (too long to include here - refer to the existing file)

#### 4. server/routes.ts
Create this file with all API routes (refer to existing file)

#### 5. server/vite.ts
Create this file for Vite integration (refer to existing file)

#### 6. server/index.ts
Create this file as the main server entry point (refer to existing file)

### Phase 3: Frontend Files

#### 1. client/src/lib/utils.ts
```typescript
import { type ClassValue, clsx } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

#### 2. client/src/lib/queryClient.ts
Create the React Query client configuration (refer to existing file)

#### 3. client/src/hooks/use-toast.ts
Create the toast hook (refer to existing file)

#### 4. Create all UI components in client/src/components/ui/
- Start with basic components like Button, Input, Card
- Add all Radix UI components as needed

#### 5. Create main page components:
- client/src/components/header.tsx
- client/src/components/hero-section.tsx
- client/src/components/features-section.tsx
- client/src/components/ai-chat-section.tsx
- client/src/components/submission-form-section.tsx
- client/src/components/policy-center-section.tsx
- client/src/components/faq-section.tsx
- client/src/components/contact-section.tsx
- client/src/components/footer.tsx

#### 6. Create pages:
- client/src/pages/home.tsx
- client/src/pages/not-found.tsx

#### 7. Create main app files:
- client/src/types/index.ts
- client/src/index.css
- client/src/App.tsx
- client/src/main.tsx
- client/index.html

## Quick Start Commands

1. Create project and install dependencies
2. Set up your OpenAI API key in .env
3. Run development server:
```bash
npm run dev
```

The application will be available at http://localhost:5000

## Important Notes

- All files use TypeScript with strict type checking
- The project uses in-memory storage (no database required)
- Responsive design works on all screen sizes
- AI features require a valid OpenAI API key
- The project includes comprehensive error handling and loading states