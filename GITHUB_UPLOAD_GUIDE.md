# How to Upload Citizen AI Project to GitHub

## Step 1: Prepare Your Project

### Create .gitignore file in your project root:
```gitignore
# Dependencies
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Environment variables (IMPORTANT: Never commit these!)
.env
.env.local
.env.development.local
.env.test.local
.env.production.local

# Build outputs
dist/
build/
.next/
out/

# IDE files
.vscode/
.idea/
*.swp
*.swo
*~

# OS files
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db

# Logs
logs
*.log

# Runtime data
pids
*.pid
*.seed
*.pid.lock

# Coverage directory used by tools like istanbul
coverage/
.lcov

# ESLint cache
.eslintcache

# Temporary folders
tmp/
temp/

# Database files (if using SQLite)
*.sqlite
*.sqlite3
*.db

# Package manager lock files (optional - you can include these)
# package-lock.json
# yarn.lock
```

## Step 2: Initialize Git Repository

Open terminal in your project folder and run:

```bash
# Navigate to your project folder
cd citizen-ai

# Initialize git repository
git init

# Add all files to staging
git add .

# Make your first commit
git commit -m "Initial commit: Citizen AI civic engagement platform"
```

## Step 3: Create GitHub Repository

### Option A: Using GitHub Website
1. Go to https://github.com
2. Click the "+" icon in top right corner
3. Select "New repository"
4. Fill in repository details:
   - **Repository name**: `citizen-ai` (or any name you prefer)
   - **Description**: `AI-powered civic engagement platform for citizens`
   - **Visibility**: Public (or Private if you prefer)
   - **DON'T** initialize with README, .gitignore, or license (you already have these)
5. Click "Create repository"

### Option B: Using GitHub CLI (if installed)
```bash
# Create repository directly from terminal
gh repo create citizen-ai --public --description "AI-powered civic engagement platform"
```

## Step 4: Connect Local Repository to GitHub

After creating the GitHub repository, you'll see commands like this. Run them in your project folder:

```bash
# Add GitHub repository as remote origin
git remote add origin https://github.com/YOUR_USERNAME/citizen-ai.git

# Verify the remote was added
git remote -v

# Push your code to GitHub
git branch -M main
git push -u origin main
```

**Replace `YOUR_USERNAME` with your actual GitHub username!**

## Step 5: Verify Upload

1. Go to your GitHub repository page
2. You should see all your project files
3. Check that `.env` is NOT visible (it should be hidden by .gitignore)

## Step 6: Create a README.md

Create an attractive README for your project:

```markdown
# Citizen AI - Civic Engagement Platform

🏛️ **AI-powered platform for transparent government interaction**

## Features

✅ **AI Chat Assistant** - Real-time civic questions and answers  
✅ **Question Submission** - Citizens can submit detailed inquiries  
✅ **Policy Center** - Browse government policies by category  
✅ **FAQ Section** - Common civic questions answered  
✅ **Contact Forms** - Multiple ways to reach government officials  
✅ **Responsive Design** - Works on all devices  

## Tech Stack

- **Frontend**: React + TypeScript + Tailwind CSS
- **Backend**: Node.js + Express
- **AI**: OpenAI GPT-4o integration
- **UI Components**: Radix UI + shadcn/ui
- **State Management**: TanStack Query

## Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/YOUR_USERNAME/citizen-ai.git
   cd citizen-ai
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   ```bash
   cp .env.example .env
   # Add your OpenAI API key to .env
   ```

4. **Start development server**
   ```bash
   npm run dev
   ```

5. **Open in browser**
   ```
   http://localhost:5000
   ```

## Environment Variables

Create a `.env` file with:

```env
OPENAI_API_KEY=your_openai_api_key_here
NODE_ENV=development
```

## Project Structure

```
citizen-ai/
├── client/src/          # React frontend
│   ├── components/      # UI components
│   ├── pages/          # Application pages
│   └── lib/            # Utilities
├── server/             # Express backend
│   ├── services/       # Business logic
│   └── routes.ts       # API endpoints
├── shared/             # Shared types and schemas
└── docs/              # Documentation
```

## Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open Pull Request

## License

This project is licensed under the MIT License.

## Screenshots

[Add screenshots of your application here]

---

**Built with ❤️ for transparent governance and civic engagement**
```

## Step 7: Add Additional Documentation

### Create .env.example (template for other developers):
```env
# OpenAI Configuration
OPENAI_API_KEY=your_openai_api_key_here

# Application Settings
NODE_ENV=development
PORT=5000

# Optional: Database (for future expansion)
DATABASE_URL=postgresql://username:password@localhost:5432/citizen_ai
```

### Update your project with README:
```bash
# Add the new files
git add README.md .env.example

# Commit the changes
git commit -m "Add README and environment template"

# Push to GitHub
git push origin main
```

## Step 8: Set Up Repository Settings (Optional)

1. Go to your repository on GitHub
2. Click "Settings" tab
3. Scroll down to "Features" section
4. Enable:
   - ✅ Issues (for bug reports)
   - ✅ Projects (for project management)
   - ✅ Wiki (for documentation)

## Step 9: Add Topics/Tags

1. Go to your repository main page
2. Click the gear icon next to "About"
3. Add topics like: `civic-tech`, `ai`, `government`, `react`, `typescript`, `openai`

## Common Commands for Future Updates

```bash
# Check status
git status

# Add specific files
git add filename.txt

# Add all changes
git add .

# Commit with message
git commit -m "Your commit message"

# Push to GitHub
git push origin main

# Pull latest changes
git pull origin main
```

## Important Security Notes

🔒 **NEVER commit your .env file** - it contains sensitive API keys  
🔒 **Always check .gitignore** before committing  
🔒 **Use .env.example** for sharing environment variable templates  

## Troubleshooting

**Problem**: "Permission denied" error  
**Solution**: Set up SSH keys or use personal access token

**Problem**: Large files rejected  
**Solution**: Check if node_modules is in .gitignore

**Problem**: Can't push to repository  
**Solution**: Make sure you have write access to the repository

Your Citizen AI project will now be safely stored on GitHub and available for others to see, contribute to, or deploy!