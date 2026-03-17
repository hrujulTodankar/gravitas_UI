# DAY 3 - Screenshot Documentation Template

**Date:** March 4, 2026  
**Task:** Document all enforcement states and key features with screenshots  
**Delivery:** Screenshots + explanatory text  

---

## Screenshot Capture Guide

### Tools

**Windows:**
- Snagit (paid, excellent)
- ShareX (free, powerful)
- Built-in: Win+Shift+S (Snip & Sketch)
- Greenshot (free, lightweight)

**Mac:**
- Built-in: Cmd+Shift+4 (selection) or Cmd+Shift+5
- Screenshot (system app)
- Skitch (free, annotatable)

**Linux:**
- GNOME Screenshot
- Flameshot (powerful, free)
- Shutter (free)

### Capture Settings

```
Resolution: 1280x720 or higher
Format: PNG (lossless)
Compression: PNG (good for archival)
Background: Clean (no desktop icons visible)
Browser Window: Maximized or well-framed
```

---

## Screenshot Checklist

### Homepage / Form

- [ ] Query textarea visible and labeled
- [ ] "Get Legal Decision" button prominent
- [ ] Placeholder text visible
- [ ] No errors showing
- [ ] Clean, professional appearance

**Caption Example:**
```
Gravitas Decision Query Interface
Users enter a legal question to receive a structured decision
from the Nyaya Legal Agent backend.
```

---

### ALLOW State - Full Page

**Screenshot Requirements:**
- [ ] Green enforcement banner visible (#28a745)
- [ ] ✅ ALLOWED label clear
- [ ] Decision summary info section shown
- [ ] At least one expandable section visible
- [ ] Good vertical scroll coverage

**Content to Show:**
```
1. Enforcement Banner (Top)
   - Green color unmistakable
   - ✅ ALLOWED label
   - Trace ID visible

2. Decision Summary
   - Domain: civil_litigation
   - Jurisdiction: India
   - Confidence: [95%]

3. Legal Analysis Section
   - Text visible and readable
   
4. Expandable Sections (collapsed states)
   - "Procedural Steps" ▼
   - "Timeline" ▼
   - "Evidence Requirements" ▼
   - "Confidence Analysis" ▼
```

**Caption:**
```
ALLOW State - Legal Decision Permitted ✅

The green banner clearly indicates this legal pathway is permitted.
Confidence score of 95% shows high certainty. Users can view:
- Legal analysis of why this pathway is allowed
- Detailed procedural steps required
- Timeline for each phase
- Evidence needed
```

---

### ALLOW State - Expanded Sections

**Screenshot Requirements:**
- [ ] At least 2 sections expanded
- [ ] Timeline items visible with dates/durations
- [ ] Confidence bars showing percentages
- [ ] All content readable

**Content to Show:**
```
1. Timeline Section (expanded)
   - Filing Stage: 1-2 weeks
   - Court Assignment: 2-4 weeks
   - Pre-trial: 1-3 months
   - Trial: 6-12 months
   - Visual markers on timeline

2. Confidence Analysis (expanded)
   - Overall: [bar] 95%
   - Legal: [bar] 92%
   - Procedural: [bar] 97%
   - Evidential: [bar] 90%

3. Procedural Steps (if expanded)
   - 1. File claim at district court
   - 2. Pay court fees
   - 3. Serve notice to defendant
   - 4. Wait for response
   - 5. Proceed to trial
```

**Caption:**
```
ALLOW State - Detailed Procedural Information

With sections expanded, users see:
- Timeline: Clear phases from filing to resolution (6-12 months)
- Confidence Breakdown: Each component analyzed with bars
- Procedural Steps: Ordered list of required actions
```

---

### BLOCK State - Full Page (CRITICAL)

**Screenshot Requirements - CRITICAL:**
- [ ] Red enforcement banner prominent (#dc3545)
- [ ] 🚫 BLOCKED label absolutely clear
- [ ] Legal analysis visible (explains refusal)
- [ ] Alternative pathway shown
- [ ] **No confusion with error state**

**Content to Show:**
```
1. Enforcement Banner (CRITICAL)
   - RED COLOR (#dc3545) unmistakable
   - 🚫 BLOCKED label bold
   - State: "BLOCK"

2. Legal Analysis (CRITICAL)
   - Shows WHY blocked
   - Example: "Criminal matters cannot be pursued through civil courts"
   - Example: "Referral to law enforcement required"

3. Alternative Action
   - Shows what user should do instead
   - Example: "Contact local police"
   - Example: "File FIR (First Information Report)"

4. Trace ID (CRITICAL)
   - Non-empty, valid format
   - Shows this is a DECISION, not an error
```

**Caption:**
```
BLOCK State - Legal Authority Refuses Pathway 🚫 (CRITICAL)

The RED banner clearly indicates a BLOCKED decision. This is NOT an error.
The system is explicitly denying this legal pathway because:
- Criminal matters must go to law enforcement, not civil courts
- The legal analysis explains why this pathway is not allowed
- An alternative pathway (police contact) is provided
- Trace ID confirms this is a valid decision with audit trail

User understands: Cannot proceed on this path. Know what to do instead.
```

---

### BLOCK State - Alternative Action

**Screenshot Requirements:**
- [ ] Legal route showing police/authority contact
- [ ] Procedural steps showing alternative process
- [ ] No suggestion of error
- [ ] Clear "next steps" guidance

**Content to Show:**
```
1. Legal Route
   Approach Police Station → File FIR → Investigation → Prosecution

2. Procedural Steps (expanded)
   - Contact local police
   - File FIR (First Information Report)
   - Provide evidence to investigating officer
   - Cooperate with investigation

3. Timeline
   - Police Registration: 1-3 days
   - Investigation Phase: 1-3 months
   - Chargesheet Filing: 90 days to 6 months
```

**Caption:**
```
BLOCK State - Alternative Legal Route

The system doesn't just refuse the pathway - it provides clear
alternative action. Users see:
- Correct venue: Police station (not civil court)
- Process: File FIR, provide evidence, cooperate
- Timeline: What to expect and when
```

---

### ESCALATE State - Full Page

**Screenshot Requirements:**
- [ ] Orange enforcement banner (#fd7e14)
- [ ] 📈 ESCALATION REQUIRED label
- [ ] Lower confidence score (60-80%)
- [ ] Mentions of expert review/escalation

**Content to Show:**
```
1. Enforcement Banner
   - ORANGE COLOR (#fd7e14)
   - 📈 ESCALATION REQUIRED label
   - State: "ESCALATE"

2. Confidence (Lower for ESCALATE)
   - Overall: 72%
   - Shows complexity
   
3. Legal Analysis
   - Mentions: "complex multinational"
   - Mentions: "expert legal review"
   - Mentions: "senior legal counsel recommended"
   
4. Legal Route
   - Includes: Arbitration
   - Includes: Expert consultation
```

**Caption:**
```
ESCALATE State - Expert Review Required 📈

For complex matters, the system displays an orange banner indicating
escalation is needed. The confidence score (72%) reflects the complexity.
Actions required:
- Consult international trade lawyer
- Consider arbitration pathways
- Expert review of international precedents
- Longer timeline due to complexity (2-6 months initial review)
```

---

### SAFE_REDIRECT State - Full Page

**Screenshot Requirements:**
- [ ] Purple enforcement banner (#6f42c1)
- [ ] ↩️ SAFE REDIRECT label
- [ ] Explanation of alternative venue
- [ ] Confirmation civil court still possible

**Content to Show:**
```
1. Enforcement Banner
   - PURPLE COLOR (#6f42c1)
   - ↩️ SAFE REDIRECT label
   - State: "SAFE_REDIRECT"

2. Legal Analysis
   - "redirect to administrative tribunal"
   - "more efficient resolution"
   - "civil courts can also handle it"
   
3. Legal Route
   - Administrative Tribunal (recommended)
   - With note: Civil courts also available

4. Timeline
   - Shows tribunal timeline
   - Shorter than civil court
```

**Caption:**
```
SAFE_REDIRECT State - Recommended Alternative Venue ↩️

The purple banner suggests a more efficient alternative pathway
while keeping civil court as an option. For administrative appeals:
- Recommended: Administrative tribunal (faster)
- Alternative: Civil judicial review (also possible)
- Processing time: 3-6 months vs. 12-24 months in courts
- Both are valid legal routes
```

---

### Features - Export Decision

**Screenshot Requirements:**
- [ ] "📥 Export Decision" button visible
- [ ] File dialog showing JSON export
- [ ] Filename with decision trace ID

**Content to Show:**
```
1. After clicking Export
   - Download dialog showing
   - Filename: decision-TRACE-ID.json
   - File size: reasonable (< 100 KB)
   - Format: JSON

2. File icon showing JSON
```

**Caption:**
```
Export Functionality

Users can export any decision as a structured JSON file for:
- Record-keeping and documentation
- Integration with other systems
- Audit trail (includes trace ID and all decision details)
- Backup and archival
```

---

### Features - Expandable Sections

**Screenshot 1: Collapsed State**

**Content:**
```
- Section header with ▼ icon
- Title: "Procedural Steps"
- No section content visible
- Clean, minimal appearance
```

**Caption:**
```
Collapsed Section View

Information is organized in expandable sections to reduce clutter.
Users click to expand relevant sections.
```

---

**Screenshot 2: Expanded State**

**Content:**
```
- Same section expanded
- ▲ icon (toggle open)
- Full content visible
- Smooth transition
```

**Caption:**
```
Expanded Section View

When clicked, sections smoothly expand to show full content:
- Procedural steps in ordered list
- All details readable and scannable
- Users can collapse to find other sections
```

---

### Features - Confidence Breakdown

**Screenshot Requirements:**
- [ ] Confidence Analysis section expanded
- [ ] Visual bars for each component
- [ ] Percentages clearly visible

**Content to Show:**
```
Confidence Analysis
├─ Overall ----------- [████████████░░░░] 92%
├─ Legal ------------- [█████████████░░░] 90%
├─ Procedural ------- [███████████████░░] 95%
└─ Evidential ------- [████████████░░░░░] 88%
```

**Caption:**
```
Confidence Breakdown Analysis

Each decision includes a confidence breakdown showing:
- Overall: Combined confidence (0-100%)
- Legal: Certainty in legal basis (0-100%)
- Procedural: Certainty in procedural pathway (0-100%)
- Evidential: Certainty in evidence requirements (0-100%)

Visual bars make it easy to understand decision certainty at a glance.
Lower scores indicate complexity or uncertainty requiring expert review.
```

---

### Features - Debug Mode

**Screenshot Requirements:**
- [ ] Debug panel visible at bottom of page
- [ ] Shows: Enforcement State, Trace ID, Confidence, Fields
- [ ] Can show Ctrl+Shift+D instruction

**Content to Show:**
```
DEBUG INFO:
Enforcement State: ALLOW
Trace ID: ALLOW-001-2026-03-04
Confidence: 95%
Fields: 12/12
Timestamp: 2026-03-04T10:00:00Z
```

**Caption:**
```
Debug Mode (Ctrl+Shift+D)

For development and troubleshooting, debug mode displays:
- Enforcement State: Current decision type (ALLOW/BLOCK/ESCALATE/SAFE_REDIRECT)
- Trace ID: Unique identifier for this decision
- Confidence: Overall confidence percentage
- Fields: Count of response fields from backend
- Timestamp: When the decision was generated

Helpful for developers testing and verifying backend responses.
```

---

### Features - Error Handling

**Screenshot Requirements:**
- [ ] Error message visible with warning icon
- [ ] Human-readable error text
- [ ] Clear "close" button
- [ ] Clean error styling (not jarring)

**Example Scenarios:**
1. Empty query error
2. Backend connection error
3. Timeout error

**Caption:**
```
Error Handling - No Silent Failures

The system displays clear error messages for:
- Empty query: "⚠️ Please enter a legal query"
- Backend unreachable: "⚠️ Cannot connect to backend..."
- Timeout (30s): "⚠️ Request timeout. Backend server may be experiencing issues."

Users always know what went wrong and can retry.
No errors are silently ignored or hidden from users.
```

---

### Mobile View - iPhone

**Screenshot Requirements:**
- [ ] Portrait orientation 375x812
- [ ] Full content visible
- [ ] No horizontal scroll
- [ ] Touch-friendly button sizes

**Content to Show:**
```
1. Query form full-width
2. Button prominent and tappable
3. Enforcement banner visible
4. Sections stack vertically
5. Text readable at small size
```

**Caption:**
```
Mobile Responsiveness - iPhone View

The interface adapts perfectly to small screens:
- Full-width form and buttons (44px+ for touch)
- Vertical stacking of sections
- Text remains readable (14px+ minimum)
- No horizontal scrolling needed
- All features fully functional on mobile
```

---

### Mobile View - Tablet

**Screenshot Requirements:**
- [ ] Landscape 1024x768 (iPad equivalent)
- [ ] Multi-column layout where appropriate
- [ ] Optimized spacing
- [ ] All content accessible

**Content to Show:**
```
1. Better use of horizontal space
2. 2-column layouts where helpful
3. Readable font sizes
4. Touch-friendly elements
```

**Caption:**
```
Mobile Responsiveness - Tablet View

Tablet screens get optimized layouts:
- Uses available horizontal space better
- 2-column grids where applicable
- Better spacing and padding
- Balances desktop and mobile needs
```

---

## Screenshot Naming Convention

```
Format: screenshot-[state]-[description]-[number].png

Examples:
- screenshot-allow-full-page-01.png
- screenshot-allow-expanded-sections-02.png
- screenshot-block-full-page-03.png
- screenshot-block-alternatives-04.png
- screenshot-escalate-full-page-05.png
- screenshot-safe_redirect-full-page-06.png
- screenshot-feature-export-07.png
- screenshot-feature-debug-mode-08.png
- screenshot-mobile-iphone-09.png
- screenshot-mobile-tablet-10.png
- screenshot-error-handling-11.png
```

---

## Screenshot Collection Checklist

### Before Screenshots

- [ ] Dev server running
- [ ] Browser at max quality (no zoom)
- [ ] Background clean
- [ ] Test queries prepared
- [ ] Backend online
- [ ] Theme loaded correctly
- [ ] No private data visible

### During Screenshots

- [ ] Capture at high resolution (1280x720+)
- [ ] Show each state
- [ ] Show expanded and collapsed
- [ ] Show error states
- [ ] Show mobile views
- [ ] Consistent naming

### After Screenshots

- [ ] Organize in `/docs/screenshots` folder
- [ ] Add descriptions
- [ ] Create `SCREENSHOTS.md` index
- [ ] Compress but maintain quality
- [ ] Add to GitHub repo

---

## Screenshot Documentation Index

Create `/docs/SCREENSHOTS.md`:

```markdown
# Gravitas UI - Feature Demonstrations

## Enforcement States

### ALLOW State ✅
- [Full Page](screenshots/allow-full-page.png)
- [Expanded Sections](screenshots/allow-expanded.png)
- [Legal Route](screenshots/allow-legal-route.png)

### BLOCK State 🚫 (CRITICAL)
- [Full Page](screenshots/block-full-page.png)
- [Alternative Route](screenshots/block-alternatives.png)
- [Clear Refusal Message](screenshots/block-refusal.png)

### ESCALATE State 📈
- [Full Page](screenshots/escalate-full-page.png)
- [Expert Consultation](screenshots/escalate-expert.png)

### SAFE_REDIRECT State ↩️
- [Full Page](screenshots/safe_redirect-full-page.png)
- [Alternative Venue](screenshots/redirect-alternative.png)

## Features

- [Export Decision](screenshots/feature-export.png)
- [Expandable Sections](screenshots/feature-sections.png)
- [Confidence Analysis](screenshots/feature-confidence.png)
- [Debug Mode](screenshots/feature-debug.png)

## Responsive Design

- [Mobile - iPhone](screenshots/mobile-iphone.png)
- [Tablet - iPad](screenshots/mobile-tablet.png)
- [Desktop](screenshots/desktop-full.png)

## Error Handling

- [Empty Query Error](screenshots/error-empty-query.png)
- [Backend Error](screenshots/error-backend.png)
```

---

## Screenshot Quality Standards

✅ **Good Screenshot:**
- Clear, sharp image (PNG)
- Resolution 1280x720+
- Relevant content centered
- No unnecessary margins
- All text readable
- Colors accurate
- No watermarks

❌ **Poor Screenshot:**
- Blurry or compressed
- Too many extra windows visible
- Desktop icons visible
- Wrong aspect ratio
- Outdated (shows errors)

---

## Recommended Tools for Annotation

If adding arrows/callouts to screenshots:

- **Mac:** Skitch (free), Preview (built-in)
- **Windows:** Snagit, Greenshot (has annotation)
- **Web:** Markup.io, Figma (import screenshot)

Keep annotations minimal and professional.

---

## Final Screenshot Delivery

### Folder Structure
```
/docs
├── screenshots/
│   ├── allow-full-page.png
│   ├── block-full-page.png
│   ├── escalate-full-page.png
│   ├── safe_redirect-full-page.png
│   ├── features/
│   │   ├── export.png
│   │   ├── debug.png
│   │   └── sections.png
│   └── mobile/
│       ├── iphone.png
│       └── tablet.png
└── SCREENSHOTS.md
```

### Delivery Checklist

- [ ] All necessary states captured
- [ ] All features demonstrated
- [ ] Mobile and desktop versions included
- [ ] High quality (no artifacts)
- [ ] Organized in folder structure
- [ ] Documented in SCREENSHOTS.md
- [ ] Uploaded to GitHub
- [ ] Accessible from README

---

**Total Screenshots Recommended: 12-15**

Estimated time: 30-45 minutes (capture + organization)
