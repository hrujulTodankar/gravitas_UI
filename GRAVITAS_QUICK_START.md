# Gravitas UI - Quick Start & Implementation Guide

**For:** Frontend Engineers & Product Teams  
**Duration:** 15 minutes to integration, 1 hour to full deployment  
**Skill Level:** Intermediate (React/JavaScript knowledge required)

---

## What You're Getting

✅ **Production-ready React components** for displaying legal decisions  
✅ **Complete API integration** with Nyaya backend  
✅ **Responsive design** (desktop, tablet, mobile)  
✅ **Validation & error handling** built-in  
✅ **Professional UI** with animations and dark mode support  

---

## Files Included

### Components
- `frontend/src/components/GravitasDecisionPanel.jsx` - Main display component
- `frontend/src/components/GravitasDecisionPanel.css` - Complete styling
- `frontend/src/components/GravitasLegalDecisionScreen.jsx` - Full page integration

### Utilities
- `frontend/src/lib/GravitasResponseTransformer.js` - API response transformation

### Documentation
- `COMPONENT_IMPLEMENTATION_GUIDE.md` - Complete technical specification
- `GRAVITAS_QUICK_START.md` - This file

---

## Step 1: Verify Prerequisites ✓

Ensure your project has:

```bash
# Check Node.js version (need 16+)
node --version

# Check npm version (need 9+)
npm --version

# Check if React is installed
npm list react
```

---

## Step 2: Copy Files to Your Project

All files are in the workspace:

```
frontend/
├── src/
│   ├── components/
│   │   ├── GravitasDecisionPanel.jsx ✓ Copy this
│   │   ├── GravitasDecisionPanel.css ✓ Copy this
│   │   └── GravitasLegalDecisionScreen.jsx ✓ Copy this
│   │
│   └── lib/
│       └── GravitasResponseTransformer.js ✓ Copy this
```

If files don't exist in your specific project, manually create them with provided content.

---

## Step 3: Import in Your App (5 minutes)

### Option A: Full Page Integration (Recommended)

Replace your App.jsx with Gravitas screen:

```jsx
// App.jsx
import GravitasLegalDecisionScreen from './components/GravitasLegalDecisionScreen.jsx'

function App() {
  return <GravitasLegalDecisionScreen />
}

export default App
```

### Option B: Partial Integration

Use just the decision panel in your existing app:

```jsx
// YourPage.jsx
import { useState } from 'react'
import GravitasDecisionPanel from './components/GravitasDecisionPanel.jsx'
import GravitasResponseTransformer from './lib/GravitasResponseTransformer.js'

function YourPage() {
  const [decision, setDecision] = useState(null)

  // When you get API response:
  const handleResponse = (apiResponse) => {
    const validatedDecision = GravitasResponseTransformer.transform(apiResponse)
    setDecision(validatedDecision)
  }

  return (
    <div>
      {/* Your existing content */}
      
      {decision && (
        <GravitasDecisionPanel 
          decision={decision}
          onExplainClick={handleExplain}
          onFeedbackClick={handleFeedback}
        />
      )}
    </div>
  )
}

export default YourPage
```

---

## Step 4: Configure API Connection (5 minutes)

Ensure your API service has the required endpoints configured:

### Check `frontend/src/services/nyayaApi.js`

Add/verify these methods:

```javascript
export const nyayaApi = {
  // Main query endpoint
  async queryLegal(request) {
    const response = await apiClient.post('/nyaya/query', request)
    return response.data
  },

  // Explanation endpoint
  async explainReasoning(request) {
    const response = await apiClient.post('/nyaya/query/explain', request)
    return response.data
  },

  // Feedback endpoint
  async submitFeedback(request) {
    const response = await apiClient.post('/nyaya/feedback', request)
    return response.data
  }
}
```

### Verify API Base URL

Check `frontend/src/lib/apiConfig.js`:

```javascript
export const BASE_URL = process.env.REACT_APP_API_URL || 'http://localhost:8000'
```

Set environment variable if using different backend:

```bash
# .env.local
REACT_APP_API_URL=http://your-api-server:8000
```

---

## Step 5: Test Locally (5 minutes)

### Start Frontend Dev Server

```bash
cd frontend
npm install  # First time only
npm run dev  # Starts Vite dev server
```

Open http://localhost:5173 in your browser

### Backend Should Be Running

```bash
# In another terminal, ensure backend is running
cd /path/to/backend
python -m uvicorn api.main:app --reload
```

---

## Step 6: Test the Integration

### Manual Testing

1. **Load the Page**
   - Should see "Gravitas Legal AI" title
   - Query input textarea visible
   - Submit button enabled

2. **Submit a Query**
   - Enter: "Can I file a case for property damage against my neighbor?"
   - Click "Get Legal Guidance"
   - Wait for response (should show loading state)

3. **Verify Decision Panel**
   - Legal domain displays (Civil, Criminal, Constitutional)
   - Jurisdiction shows (India, UK, UAE)
   - Confidence score visible and color-coded
   - Legal route with step-by-step path
   - Expandable sections for details

4. **Test Interactions**
   - Click constitutional articles section → expands
   - Click provenance chain → shows decision audit trail
   - Click "Export Decision" → downloads JSON file
   - Click "Explain Reasoning" → loads detailed explanation
   - Click "Provide Feedback" → shows success message

### Automated Testing (Optional)

```bash
# Run component tests
npm run test

# Run E2E tests with Cypress
npm run test:e2e
```

---

## Step 7: Customize (Optional)

### Change Colors

Edit `GravitasDecisionPanel.css`:

```css
/* Change primary gradient */
.gravitas-header {
  background: linear-gradient(135deg, #YOUR_COLOR_1 0%, #YOUR_COLOR_2 100%);
}

.action-button.primary {
  background: linear-gradient(135deg, #YOUR_COLOR_1 0%, #YOUR_COLOR_2 100%);
}
```

### Adjust Layout

Change 2-column to 1-column in `GravitasDecisionPanel.jsx`:

```jsx
const gridStyle = {
  display: 'grid',
  gridTemplateColumns: '1fr', // Changed from "1fr 1fr"
  gap: '30px'
}
```

### Add Custom Sections

Extend the panel component:

```jsx
// CustomGravitasPanel.jsx
import GravitasDecisionPanel from './GravitasDecisionPanel.jsx'

export function CustomGravitasPanel(props) {
  return (
    <>
      <GravitasDecisionPanel {...props} />
      
      <div className="custom-section">
        {/* Your custom content */}
      </div>
    </>
  )
}
```

---

## Step 8: Deploy (Production)

### Build for Production

```bash
cd frontend
npm run build
```

This creates optimized build in `dist/` folder

### Deploy to Hosting

#### For Vercel (Recommended)

```bash
# Install Vercel CLI
npm install -g vercel

# Deploy from frontend directory
cd frontend
vercel --prod
```

#### For Docker

```dockerfile
# Dockerfile
FROM node:18-alpine

WORKDIR /app
COPY package*.json ./
RUN npm ci

COPY . .
RUN npm run build

FROM node:18-alpine
RUN npm install -g serve
COPY --from=0 /app/dist /app
CMD ["serve", "-s", "/app", "-l", "3000"]
```

```bash
# Build and run
docker build -t gravitas-ui .
docker run -p 3000:3000 gravitas-ui
```

#### For Traditional Hosting

1. Build: `npm run build`
2. Upload `dist/` folder to your web host
3. Configure SPA routing (all requests → index.html)
4. Test: Visit your domain

---

## API Response Examples

### Example 1: Successful Query

```json
{
  "success": true,
  "data": {
    "domain": "civil",
    "jurisdiction": "India",
    "confidence": 0.87,
    "legal_route": [
      "jurisdiction_router_agent",
      "india_legal_agent",
      "civil_law_specialist"
    ],
    "constitutional_articles": [
      "Article 21 - Right to Life and Liberty",
      "Article 226 - Power to Issue Writs",
      "Section 23 - Indian Contract Act, 1872"
    ],
    "provenance_chain": [
      {
        "source": "JurisdictionRouter",
        "description": "Identified India as target jurisdiction",
        "timestamp": "2026-03-04T10:30:00Z"
      },
      {
        "source": "LegalAgent",
        "description": "Analyzed contract and damage claim",
        "timestamp": "2026-03-04T10:30:05Z"
      }
    ],
    "reasoning_trace": {
      "query_classification": "civil_contract_dispute",
      "applicable_laws": ["Indian Contract Act", "Tort Law"],
      "recommended_action": "civil_suit"
    },
    "trace_id": "trace_1234567890_abc123def456",
    "enforcement_status": null
  }
}
```

### Example 2: Blocked Pathway

```json
{
  "success": true,
  "data": {
    "...other fields...",
    "enforcement_status": {
      "state": "block",
      "reason": "Case involves sensitive national security matters",
      "blocked_path": "direct_litigation",
      "escalation_required": true,
      "escalation_target": "Supreme Court of India",
      "safe_explanation": "This matter requires escalation to higher authorities"
    }
  }
}
```

---

## Common Issues & Solutions

### Issue: Component not rendering

**Solution:**
```jsx
// Verify decision object
console.log(GravitasResponseTransformer.isValid(decision))

// Transform if needed
const valid = GravitasResponseTransformer.transform(apiResponse)
```

### Issue: Styles not applied

**Solution:**
1. Ensure CSS file is imported: `import './GravitasDecisionPanel.css'`
2. Clear browser cache: `Ctrl+Shift+Delete` (Chrome)
3. Rebuild: `npm run dev`

### Issue: API errors

**Solution:**
```javascript
// Add error logging
try {
  const response = await nyayaApi.queryLegal(request)
  console.log('Response:', response)
} catch (error) {
  console.error('API Error:', error.response?.data || error.message)
}
```

### Issue: Styling looks wrong on mobile

**Solution:**
- Ensure viewport meta tag in HTML: `<meta name="viewport" content="width=device-width, initial-scale=1" />`
- Check CSS media queries are not overridden
- Test in Chrome DevTools mobile view

---

## Integration Checklist

Before going live:

- [ ] All 4 files copied to project
- [ ] GravitasLegalDecisionScreen integrated in App.jsx or routing
- [ ] API endpoints configured and tested
- [ ] Backend server running and accessible
- [ ] Test query works end-to-end
- [ ] Styling looks correct on mobile
- [ ] Error handling works (try invalid input)
- [ ] Export functionality works
- [ ] Feedback submission works
- [ ] Build completes without errors (`npm run build`)
- [ ] Built app works when served

---

## Performance Optimization Tips

### 1. Lazy Load Components

```jsx
import { lazy, Suspense } from 'react'
import SkeletonLoader from './SkeletonLoader.jsx'

const GravitasPanel = lazy(() => import('./GravitasDecisionPanel.jsx'))

export function App() {
  return (
    <Suspense fallback={<SkeletonLoader />}>
      <GravitasPanel />
    </Suspense>
  )
}
```

### 2. Memoize Components

```jsx
import { memo } from 'react'

const GravitasMemo = memo(GravitasDecisionPanel)
```

### 3. Cache API Responses

```javascript
const cache = new Map()

async function getCachedDecision(traceId) {
  if (cache.has(traceId)) {
    return cache.get(traceId)
  }
  const decision = await fetchDecision(traceId)
  cache.set(traceId, decision)
  return decision
}
```

---

## Monitoring & Analytics

### Track Key Events

```javascript
// Add to GravitasLegalDecisionScreen
const trackEvent = (eventName, data) => {
  // Send to your analytics service
  console.log(`Event: ${eventName}`, data)
  
  // Example with GA
  if (window.gtag) {
    window.gtag('event', eventName, data)
  }
}

// Usage
trackEvent('decision_generated', {
  domain: decision.domain,
  confidence: decision.confidence,
  jurisdiction: decision.jurisdiction
})
```

### Monitor Performance

```javascript
// Measure API response time
const start = performance.now()
const response = await nyayaApi.queryLegal(query)
const duration = performance.now() - start
console.log(`API took ${duration}ms`)
```

---

## Next Steps

1. ✅ **Copy files** to your project (5 min)
2. ✅ **Configure API** connection (5 min)
3. ✅ **Test locally** (5 min)
4. ✅ **Customize** if needed (optional)
5. ✅ **Deploy** to production (varies)

---

## Support Resources

### Documentation
- `COMPONENT_IMPLEMENTATION_GUIDE.md` - Full technical specs
- Component JSDoc comments in source files
- Inline code comments for complex logic

### Example Responses
- See "API Response Examples" section above
- Check `read files/API_CONTRACT.md` for schema definitions

### Debugging
- Browser DevTools → Console for errors
- Check API response format matches schema
- Use `GravitasResponseTransformer.isValid()` to verify data
- Review trace_id in error logs

### Getting Help
1. Check the troubleshooting section above
2. Review COMPONENT_IMPLEMENTATION_GUIDE.md
3. Check console errors and API response
4. Review nyayaApi.js for connection issues

---

## Demo Walkthrough (3 minutes)

### Quick Demo Flow

1. **Open App**
   - See Gravitas title and query input

2. **Enter Sample Query**
   ```
   I'm in India and my business partner
   won't honor our verbal agreement to
   split profits equally. What legal
   options do I have?
   ```

3. **Click Submit**
   - Watch loading animation
   - See decision appear

4. **Explore Decision**
   - Note confidence score color
   - Expand Constitutional Articles section
   - Expand Reasoning Details
   - Click Explain Reasoning button

5. **Test Export**
   - Click Export Decision
   - JSON file downloads with full data

6. **Provide Feedback**
   - Click Provide Feedback button
   - See success message

---

## Production Deployment Steps

### Pre-Deployment Checklist

```bash
# 1. Install dependencies
npm install

# 2. Run tests
npm run test

# 3. Build production bundle
npm run build

# 4. Check bundle size
npm run build -- --analyze

# 5. Test production build locally
npm run preview
```

### Environment Variables

Create `.env.production`:

```env
REACT_APP_API_URL=https://your-api-server.com
REACT_APP_ENV=production
REACT_APP_LOG_LEVEL=error
```

### Deployment Commands

```bash
# For Vercel
vercel --prod

# For Docker
docker build -t gravitas-ui:latest .
docker run -p 3000:3000 gravitas-ui:latest

# For traditional hosting
npm run build
# Upload dist/ folder to server
```

---

**Ready to deploy?** Follow the Deployment section above and your Gravitas UI will be live!

---

**Created:** 2026-03-04  
**Version:** 1.0.0  
**Status:** Production Ready
