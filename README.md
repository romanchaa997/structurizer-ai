# structurizer-ai
AI-powered text structuring tool with Gemini API, caching, chunking, and streaming support


## Features

✅ **AI-Powered Structuring**: 6 preset modes (Summary, Tasks, Table, JSON, Cleanup, Custom)
✅ **Smart Caching**: SHA-256 hash-based localStorage caching to avoid redundant API calls
✅ **Text Chunking**: Auto-split large texts (>3000 chars) and batch-process them
✅ **Streaming Support**: Real-time response streaming from Gemini API
✅ **Dark/Light Theme**: Toggle theme with Ctrl+B
✅ **History Management**: Save up to 50 recent operations
✅ **Request Queue**: Max 2 concurrent requests with AbortController support
✅ **Telemetry**: Console logging for latency, cache hits, and error tracking
✅ **Hotkeys**: Ctrl+Enter to process, Ctrl+B to toggle theme
✅ **TypeScript**: Full type safety
✅ **CI/CD**: GitHub Actions pipeline with lint, typecheck, and build

## Quick Start

### Prerequisites
- Node.js 20+
- Gemini API Key from [Google AI Studio](https://aistudio.google.com)

### Local Setup

```bash
# Clone the repository
git clone https://github.com/romanchaa997/structurizer-ai.git
cd structurizer-ai

# Install dependencies
npm install

# Create .env.local
echo "GEMINI_API_KEY=your_api_key_here" > .env.local

# Development server
npm run dev

# Build for production
npm run build

# Type checking
npm run typecheck

# Lint
npm run lint
```

## Project Structure

```
src/
├── config/
│   └── llm.ts          # LLM models, prompts, configs
├── api/
│   └── gemini.ts       # Gemini API client with streaming
├── hooks/
│   └── useLlmClient.ts # React hook for LLM requests
├── lib/
│   ├── cache.ts        # SHA-256 hashing and localStorage
│   └── chunkText.ts    # Text chunking utilities
└── index.tsx           # Main UI component

.github/
└── workflows/
    └── ci.yml          # GitHub Actions CI pipeline
```

## Deployment

### Vercel

```bash
npm i -g vercel
vercel login
vercel --prod
```

### Netlify

1. Push to GitHub
2. Connect repository at [netlify.com](https://netlify.com)
3. Set build command: `npm run build`
4. Set publish directory: `dist`

## Environment Variables

Create `.env.local` in the project root:

```
GEMINI_API_KEY=your_gemini_api_key
```

## How It Works

1. **Input**: User enters text and selects a processing mode
2. **Cache Check**: System checks localStorage for previous identical requests
3. **Chunking**: If text > 3000 chars, it's split into smaller chunks
4. **API Call**: Request sent to Gemini with selected model and temperature
5. **Streaming**: Response streamed to UI in real-time
6. **Caching**: Result saved to localStorage with content hash as key
7. **History**: Operation saved to history (max 50 items)

## Optimization Strategies

- **Request Queue**: Never more than 2 concurrent API requests
- **Debouncing**: 300-400ms debounce on text input
- **Caching**: Skip API call if exact same request was processed before
- **Chunking**: Handle texts up to ~10k characters efficiently
- **Model Selection**: Light model (flash) for quick tasks, heavy model (pro) for complex ones
- **Lazy Loading**: React components split via code splitting

## Metrics & Telemetry

Open DevTools console to see:
- Request latency (ms)
- Input text length
- Cache hit/miss status
- Selected model and mode

```javascript
// Example telemetry output
{
  task: "heavy",
  cached: false,
  ms: 1234,
  length: 5000
}
```

## CI/CD Pipeline

Every push triggers:
1. ✅ `npm ci` - Install exact dependencies
2. ✅ `npm run typecheck` - TypeScript type checking
3. ✅ `npm run lint` - ESLint checking
4. ✅ `npm run build` - Vite production build

Failed checks prevent merge to main.

## License

MIT © 2025 Roman Chaa

## Support

For issues or feature requests, open a GitHub issue.
