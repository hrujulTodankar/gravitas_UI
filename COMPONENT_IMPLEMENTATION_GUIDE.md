# Gravitas UI - Component Implementation Specification

**Version:** 1.0.0  
**Status:** Production Ready  
**Last Updated:** 2026-03-04

## Executive Summary

Gravitas UI is a production-ready legal decision display system that converts Nyaya AI backend responses into a visually impressive, user-friendly interface. This document provides complete engineering specifications for implementing, customizing, and deploying the Gravitas UI component suite.

---

## Architecture Overview

```
┌─────────────────────────────────┐
│   GravitasLegalDecisionScreen   │ ← Entry Point
│   (Integration & State Mgmt)    │
└──────────────┬──────────────────┘
               │
               ├─────────────────────────────────────────┐
               │                                         │
       ┌──────▼─────────┐                    ┌──────────▼──────────┐
       │GravitasDecision │                    │  Response          │
       │Panel            │                    │  Transformer       │
       │(Main Display)   │◄────────Transform──┤  (Validation &     │
       │                 │                    │   Formatting)      │
       └──────┬──────────┘                    └────────────────────┘
              │
              ├─────────────────────────────────────────────────┐
              │                                                 │
       ┌──────▼────────────────┐  ┌──────────────────────────┐ │
       │Existing Components    │  │New Layout &             │ │
       │(Reused/Integrated)    │  │Styling                  │ │
       │                       │  │                         │ │
       │- ConfidenceIndicator  │  │- GravitasDecisionPanel  │ │
       │- JurisdictionInfoBar  │  │  .jsx/.css              │ │
       │- EnforcementStatusCard│  │- Responsive Grid Layout │ │
       │- SkeletonLoader       │  │- Dark Mode Support      │ │
       └───────────────────────┘  │- Smooth Animations      │ │
                                   └──────────────────────────┘ │
                                                                  │
                         ┌────────────────────────────────────────┘
                         │
                    ┌────▼─────────┐
                    │ Nyaya API    │
                    │ Backend      │
                    │ /nyaya/query │
                    └──────────────┘
```

---

## Component Specifications

### 1. GravitasDecisionPanel

**File:** `frontend/src/components/GravitasDecisionPanel.jsx`

**Purpose:** Main visual component that renders the complete legal decision with all supporting information.

**Props:**

| Prop | Type | Required | Description |
|------|------|----------|-------------|
| `decision` | Object | Yes | NyayaResponse object with legal decision data |
| `loading` | Boolean | No | Loading state (default: false) |
| `onExplainClick` | Function | No | Callback when user clicks "Explain Reasoning" |
| `onFeedbackClick` | Function | No | Callback when user clicks "Provide Feedback" |

**Decision Object Schema:**

```javascript
{
  domain: String,              // "criminal", "civil", "constitutional"
  jurisdiction: String,        // "India", "UK", "UAE"
  confidence: Number,          // 0.0 to 1.0
  legal_route: String[],       // [agentId, agentId, ...]
  constitutional_articles: String[], // Referenced articles
  provenance_chain: Array,     // Decision audit trail
  reasoning_trace: Object,     // Detailed reasoning data
  trace_id: String,            // Unique identifier
  enforcement_status: Object   // Optional enforcement data
}
```

**Key Features:**

- Dynamic color scheme based on confidence (high/medium/low)
- Expandable sections for detailed information
- Provenance chain visualization
- Responsive grid layout (2-column on desktop, 1-column on mobile)
- Export decision as JSON
- Integrated action buttons for feedback/explanation

**Styling:** Production CSS with:
- Gradient backgrounds and smooth animations
- Glassmorphic UI elements
- Color-coded severity indicators
- Responsive breakpoints at 768px and 1024px
- Dark mode support via `@media (prefers-color-scheme: dark)`

**Example Usage:**

```jsx
import GravitasDecisionPanel from './components/GravitasDecisionPanel.jsx'

<GravitasDecisionPanel
  decision={{
    domain: "civil",
    jurisdiction: "India",
    confidence: 0.87,
    legal_route: ["jurisdiction_router_agent", "legal_agent"],
    constitutional_articles: ["Article 21", "Article 226"],
    provenance_chain: [],
    reasoning_trace: {},
    trace_id: "trace_123456",
    enforcement_status: null
  }}
  loading={false}
  onExplainClick={(traceId) => console.log("Explain:", traceId)}
  onFeedbackClick={(traceId) => console.log("Feedback:", traceId)}
/>
```

---

### 2. GravitasResponseTransformer

**File:** `frontend/src/lib/GravitasResponseTransformer.js`

**Purpose:** Utility library for validating, transforming, and formatting API responses.

**Core Methods:**

#### `transform(apiResponse) → Object`
Validates and transforms raw API response into component-ready format.

```javascript
const validatedDecision = GravitasResponseTransformer.transform(apiResponse)
```

#### `isValid(decision) → Boolean`
Checks if decision object meets minimum requirements for display.

```javascript
if (GravitasResponseTransformer.isValid(decision)) {
  // Safe to render
}
```

#### `getSummary(decision) → String`
Generates human-readable one-liner about the decision.

```javascript
// Returns: "87% confidence - civil case in India"
const summary = GravitasResponseTransformer.getSummary(decision)
```

#### `formatConfidence(confidence) → String`
Converts numeric confidence to descriptive text.

```javascript
// Returns: "Very High (87%)"
const confident = GravitasResponseTransformer.formatConfidence(0.87)
```

#### `getConfidenceColor(confidence) → String`
Returns hex color based on confidence level.

```javascript
// Returns: "#28a745" (green)
const color = GravitasResponseTransformer.getConfidenceColor(0.87)
```

#### `formatEnforcementStatus(status) → Object`
Normalizes enforcement status with display labels and severity.

```javascript
const formatted = GravitasResponseTransformer.formatEnforcementStatus(
  decision.enforcement_status
)
// Returns: { state, reason, displayLabel, severity, ... }
```

#### `getKeyPoints(decision) → String[]`
Extracts 5-7 key data points for sidebar display.

```javascript
const points = GravitasResponseTransformer.getKeyPoints(decision)
// Returns: ["Domain: Civil", "Jurisdiction: India", "Confidence: Very High...", ...]
```

#### `toDebugString(decision) → String`
Creates compact debug representation for logging.

```javascript
console.log(GravitasResponseTransformer.toDebugString(decision))
// Logs: "[trace_12345] civil @ India (87%)"
```

#### `mergeMultiple(decisions) → Object`
Combines multiple jurisdiction responses into single object.

```javascript
const merged = GravitasResponseTransformer.mergeMultiple([india, uk, uae])
// Returns: { merged: true, count, decisions, average_confidence, ... }
```

**Error Handling:**

All methods include defensive programming:
- Default values for missing fields
- Type checking and sanitization
- Graceful fallbacks
- No exceptions thrown on invalid input

---

### 3. GravitasLegalDecisionScreen

**File:** `frontend/src/components/GravitasLegalDecisionScreen.jsx`

**Purpose:** Complete integration wrapper showing how to use GravitasDecisionPanel with API calls.

**Features:**

1. **Query Input Form**
   - Textarea for legal question entry
   - Submit button with loading state
   - Input validation and error display

2. **API Integration**
   - Calls `nyayaApi.queryLegal()` with user query
   - Transforms response using GravitasResponseTransformer
   - Validates before rendering

3. **Decision Display**
   - Renders GravitasDecisionPanel
   - Sidebar with quick summary and confidence explanation
   - Key points extraction and display

4. **Explanation & Feedback**
   - Callback handlers for explanation requests
   - Feedback submission with success confirmation
   - Error handling and user feedback

5. **Responsive Layout**
   - Desktop: 2-column (decision + sidebar)
   - Tablet: Single column
   - Mobile: Optimized single column

**Usage:**

```jsx
import GravitasLegalDecisionScreen from './components/GravitasLegalDecisionScreen.jsx'

// Use as primary route/page
function App() {
  return <GravitasLegalDecisionScreen />
}
```

---

## Data Flow Specification

### Query Submission → Decision Display

```
1. User enters legal query
   │
2. Form validation
   │
3. API Call: POST /nyaya/query
   │  └─ Request: { query, jurisdiction_hint?, domain_hint?, user_context }
   │  └─ Response: NyayaResponse
   │
4. Response Transformation
   │  └─ GravitasResponseTransformer.transform(response)
   │  └─ Validation: GravitasResponseTransformer.isValid()
   │
5. Decision Rendered
   │
6. User Interactions
   ├─ Click "Explain Reasoning"
   │  └─ API: POST /nyaya/query/{trace_id}/explain
   │  └─ Display explanation panel
   │
   ├─ Click "Provide Feedback"
   │  └─ API: POST /nyaya/feedback
   │  └─ Show success message
   │
   └─ Click "Export Decision"
      └─ Download decision as JSON
```

---

## Nyaya API Integration

### Required Endpoints

#### 1. Query Legal Decision
```
POST /nyaya/query

Request:
{
  query: string,
  jurisdiction_hint?: "India" | "UK" | "UAE",
  domain_hint?: "criminal" | "civil" | "constitutional",
  user_context: {
    role: "citizen" | "lawyer" | "student",
    confidence_required: boolean
  }
}

Response:
{
  success: boolean,
  data: {
    domain: string,
    jurisdiction: string,
    confidence: number,
    legal_route: string[],
    constitutional_articles: string[],
    provenance_chain: object[],
    reasoning_trace: object,
    trace_id: string,
    enforcement_status?: object
  },
  error?: string
}
```

#### 2. Explain Reasoning
```
POST /nyaya/query/{trace_id}/explain

Request:
{
  explanation_level: "brief" | "detailed" | "constitutional"
}

Response:
{
  success: boolean,
  data: {
    trace_id: string,
    explanation: object,
    reasoning_tree: object,
    constitutional_articles: string[]
  }
}
```

#### 3. Submit Feedback
```
POST /nyaya/feedback

Request:
{
  trace_id: string,
  rating: 1-5,
  feedback_type: "clarity" | "correctness" | "usefulness",
  comment?: string
}

Response:
{
  success: boolean,
  message: string,
  trace_id: string
}
```

---

## Customization Guide

### Theming

Modify colors by editing CSS variables or updating gradient definitions in `GravitasDecisionPanel.css`:

```css
/* Primary Gradient */
background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);

/* Alternative Gradients */
/* Warm */
background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);

/* Cool */
background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);

/* Professional */
background: linear-gradient(135deg, #2c3e50 0%, #3d5a6c 100%);
```

### Layout Customization

Adjust grid layout in component:

```jsx
// Default: 2-column layout
const gridStyle = {
  display: 'grid',
  gridTemplateColumns: '1fr 1fr', // Modify ratio or remove secondary column
  gap: '30px'
}
```

### Adding Custom Sections

Extend GravitasDecisionPanel:

```jsx
function CustomGravitasPanel(props) {
  const { decision, ...rest } = props
  
  return (
    <div className="gravitas-panel">
      {/* Original content */}
      <GravitasDecisionPanel decision={decision} {...rest} />
      
      {/* Custom section */}
      <div className="custom-section">
        {/* Your custom component */}
      </div>
    </div>
  )
}
```

---

## Performance Optimization

### Code Splitting

```jsx
// Use React.lazy for route-level splitting
const GravitasScreen = React.lazy(() => 
  import('./components/GravitasLegalDecisionScreen.jsx')
)

<Suspense fallback={<SkeletonLoader />}>
  <GravitasScreen />
</Suspense>
```

### Memoization

```jsx
import { memo } from 'react'

const OptimizedPanel = memo(GravitasDecisionPanel)
```

### Request Optimization

- Cache responses by trace_id
- Debounce explanation requests
- Limit provenance chain display to 10 items

---

## Accessibility Requirements

- WCAG 2.1 Level AA compliant
- Semantic HTML with proper heading hierarchy
- ARIA labels for interactive elements
- Color not sole means of information
- Keyboard navigation support
- Sufficient color contrast ratios (4.5:1 minimum)

Example ARIA implementation:

```jsx
<button
  aria-label="Explain the reasoning behind this decision"
  onClick={handleExplain}
>
  Explain Reasoning
</button>
```

---

## Testing Specifications

### Unit Tests (Jest)

```javascript
// GravitasResponseTransformer.test.js
describe('GravitasResponseTransformer', () => {
  test('transform validates required fields', () => {
    const result = GravitasResponseTransformer.transform(testResponse)
    expect(result).toHaveProperty('trace_id')
    expect(result).toHaveProperty('jurisdiction')
  })

  test('formatConfidence returns descriptive text', () => {
    expect(GravitasResponseTransformer.formatConfidence(0.87))
      .toBe('Very High (87%)')
  })
})
```

### Component Tests (React Testing Library)

```javascript
// GravitasDecisionPanel.test.jsx
import { render, screen } from '@testing-library/react'
import GravitasDecisionPanel from './GravitasDecisionPanel.jsx'

test('renders decision title', () => {
  render(<GravitasDecisionPanel decision={mockDecision} />)
  expect(screen.getByText('Legal Decision')).toBeInTheDocument()
})
```

### E2E Tests (Cypress)

```javascript
// gravitas.cy.js
describe('Gravitas Legal Decision Screen', () => {
  before(() => cy.visit('/gravitas'))
  
  it('submits query and displays decision', () => {
    cy.get('[class*="query-input"]').type('Can I sue my landlord?')
    cy.get('[class*="query-button"]').click()
    cy.get('[class*="gravitas-panel"]').should('be.visible')
  })
})
```

---

## Browser Compatibility

| Browser | Version | Support |
|---------|---------|---------|
| Chrome | Latest 2 | Full |
| Firefox | Latest 2 | Full |
| Safari | Latest 2 | Full |
| Edge | Latest 2 | Full |
| Mobile Safari | iOS 15+ | Full |
| Chrome Mobile | Latest | Full |

---

## Deployment Checklist

- [ ] CSS is compiled and minified
- [ ] JavaScript bundles are optimized
- [ ] Images are compressed
- [ ] API endpoints are accessible
- [ ] CORS is properly configured
- [ ] Error tracking (Sentry) is configured
- [ ] Analytics events are firing
- [ ] Performance metrics are monitored
- [ ] Accessibility audit passed
- [ ] User acceptance testing complete

---

## Troubleshooting Guide

### Component Doesn't Render

**Symptom:** Empty or blank page

**Solutions:**
1. Verify decision object has required fields (trace_id, jurisdiction, domain)
2. Check browser console for errors
3. Validate API response using `GravitasResponseTransformer.isValid()`

### Styling Issues

**Symptom:** CSS not applied

**Solutions:**
1. Verify CSS file is imported in component
2. Check class names match CSS selectors
3. Clear browser cache and rebuild

### API Integration Issues

**Symptom:** "Query failed" error

**Solutions:**
1. Verify API endpoint is accessible
2. Check request/response format matches schema
3. Review API error response in browser DevTools
4. Confirm CORS headers are set correctly

---

## Future Enhancements

- [ ] Multi-language support (i18n)
- [ ] PDF export functionality
- [ ] Collaborative features (annotations, sharing)
- [ ] Advanced filtering and search
- [ ] Real-time notifications
- [ ] Voice input support
- [ ] Integration with legal databases
- [ ] Machine learning confidence calibration

---

## Support & Documentation

- **Component API docs:** See JSDoc comments in source files
- **Demo:** GravitasLegalDecisionScreen.jsx shows complete usage
- **Issues:** Report to development team with trace_id and browser details
- **Feedback:** Use in-app feedback system (4x / 5 rating feature)

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0.0 | 2026-03-04 | Initial release - Production ready |

---

**Document Contact:** Gravitas UI Development Team
