# DAY 3 - Video Demo Recording Guide

**Date:** March 4, 2026  
**Task:** Create demo video showing all enforcement states and key features  
**Target Duration:** 5-10 minutes  
**Delivery Format:** MP4, WebM, or GIF

---

## Pre-Recording Setup

### Equipment

- [ ] Screen recorder tool installed
  - Windows: OBS Studio (free), ScreenFlow, or Camtasia
  - Mac: ScreenFlow, OBS Studio, or QuickTime (native)
  - Linux: OBS Studio, SimpleScreenRecorder

- [ ] Audio input available
  - Built-in mic or USB mic
  - Quiet environment (no background noise)
  - Test audio levels before recording

- [ ] Browser ready
  - Clear browser cache
  - Close unnecessary tabs
  - Full screen or windowed appropriately

### Application Setup

- [ ] Dev server running
  ```bash
  cd frontend
  npm run dev
  # Should be at http://localhost:5173
  ```

- [ ] Navigation/URL ready
  - Direct link: http://localhost:5173/decision
  - Or http://localhost:5173 → navigate to /decision

- [ ] Test queries prepared
  ```
  ALLOW:        "What are the procedures for filing a civil suit in India?"
  BLOCK:        "How do I report a criminal offense in India?"
  ESCALATE:     "Complex multinational commercial arbitration matter"
  SAFE_REDIRECT: "Administrative tribunal appeal for government decision in UK"
  ```

- [ ] Backend online
  - Test: https://nyaya-ai-0f02.onrender.com/health
  - Should respond with 200 or valid JSON

### Recording Settings

#### OBS Studio Configuration
```
Settings:
- Output Resolution: 1920x1080
- FPS: 30 (or 60)
- Bitrate: 5000 kbps (for quality)
- Format: MP4

Scene:
- Add Display Capture (entire screen or window)
- Add mic audio source
```

#### ScreenFlow (Mac)
```
Settings:
- Resolution: 1280x720 (or 1920x1080)
- Recording quality: High
- Show cursor: Yes
- Record audio: Yes (from mic)
```

---

## Demo Script

### Part 1: Introduction (30 seconds)

```
[NARRATE]
"Welcome to the Nyaya Legal Agent - a real-time legal decision interface 
powered by Gravitas UI. Today we'll demonstrate all enforcement states 
and key features to show how this system provides structured legal guidance."

[SHOW]
- App title: "Nyaya Legal Agent"
- Subtitle: "Real-time structured legal decisions with enforcement authority"
```

### Part 2: ALLOW State (1-2 minutes)

```
[EXPLAIN]
"First, let's see an ALLOWED decision. This shows a legal pathway that is 
permitted and clear to proceed."

[ACTIONS]
1. Click on query textarea
2. Type: "What are the procedures for filing a civil suit in India?"
3. Click "Get Legal Decision" button
4. Wait for response (show loading state)
5. Point to enforcement banner (green)
6. Show label: "✅ ALLOWED"

[NARRATE]
"Notice the green banner clearly showing the decision is ALLOWED. 
The confidence score is high at [X]%, indicating the legal pathway is clear."

[SHOW]
- Enforcement banner with green color
- ✅ ALLOWED label
- Confidence percentage
- Legal analysis text
- Procedural steps (expand one section)

[EXPAND SECTIONS - Optional]
"Let's look at the procedural steps for filing..."
- Click "Procedural Steps" header
- Show expanded content
- Read key steps briefly
```

### Part 3: BLOCK State (1-2 minutes) **CRITICAL**

```
[EXPLAIN]
"Next is a BLOCKED decision - this is critical. When a legal pathway is blocked 
by authority, the system makes this unmistakably clear in red."

[ACTIONS]
1. Click "New Query" button
2. Type: "How do I report a criminal offense in India?"
3. Click "Get Legal Decision"
4. Wait for response

[NARRATE]
"See the red banner - this clearly indicates the decision is BLOCKED. 
The 🚫 BLOCKED label is unmistakable. The legal analysis explains WHY 
this pathway cannot proceed, and provides an alternative - contactinglaw enforcement."

[SHOW]
- Red enforcement banner (#dc3545)
- 🚫 BLOCKED label in red
- Legal analysis explaining refusal
- Alternative action (police contact)
- Trace ID for decision tracking

[EXPAND SECTIONS]
"The system provides clear next steps - file an FIR with police, 
not pursue through civil courts."
- Click "Procedural Steps"
- Show alternative pathway
```

### Part 4: ESCALATE State (1 minute)

```
[EXPLAIN]
"An ESCALATE decision means this matter is complex and requires expert review. 
Notice the orange banner and lower confidence score."

[ACTIONS]
1. Click "New Query"
2. Type: "Complex multinational commercial arbitration matter"
3. Click "Get Legal Decision"
4. Wait for response

[NARRATE]
"This shows an orange ESCALATE banner. The confidence score is lower, 
indicating complexity. The system recommends escalation to expert counsel 
or international arbitration."

[SHOW]
- Orange enforcement banner (#fd7e14)
- 📈 ESCALATION REQUIRED label
- Lower confidence (60-75%)
- Mention expert review requirements
- Arbitration pathway
```

### Part 5: SAFE_REDIRECT State (1 minute)

```
[EXPLAIN]
"A SAFE_REDIRECT decision suggests an alternative, more efficient venue 
while preserving the civil court option."

[ACTIONS]
1. Click "New Query"
2. Type: "Administrative tribunal appeal for government decision in UK"
3. Click "Get Legal Decision"
4. Wait for response

[NARRATE]
"The purple banner indicates a SAFE REDIRECT. This suggests using an 
administrative tribunal for more efficient resolution, though civil courts 
can also handle this matter."

[SHOW]
- Purple enforcement banner (#6f42c1)
- ↩️ SAFE REDIRECT label
- Alternative venue explanation
- Flexibility in approach
```

### Part 6: Key Features Demo (2-3 minutes)

#### 6A. Export Decision

```
[EXPLAIN]
"Users can export decisions as JSON for record-keeping or integration."

[ACTIONS]
1. Click "📥 Export Decision"
2. Show file download (e.g., decision-TRACE-ID.json)

[NARRATE]
"The decision is downloaded as a structured JSON file, complete with 
the trace ID for auditability and all decision details."
```

#### 6B. Expandable Sections

```
[EXPLAIN]
"All decision details are organized in expandable sections for clarity."

[ACTIONS]
1. Show "Timeline" section collapsed
2. Click to expand
3. Show timeline items with dates

[NARRATE]
"Each section can be expanded to see details. The timeline shows 
key milestones and expected durations for the legal process."

[SHOW MULTIPLE]
- Timeline section
- Confidence Analysis (show visual bars)
- Evidence Requirements
- Legal Route
```

#### 6C. Debug Mode

```
[EXPLAIN]
"For developers, debug mode provides detailed information."

[ACTIONS]
1. Press Ctrl+Shift+D
2. Show debug panel at bottom
3. Highlight: State, Trace ID, Confidence, Fields

[NARRATE]
"Debug mode (Ctrl+Shift+D) shows the enforcement state, trace ID for 
tracking, confidence score, and field count - useful for testing and 
troubleshooting."
```

#### 6D. Error Handling

```
[EXPLAIN]
"The system handles errors gracefully - no silent failures."

[ACTIONS]
1. Click query textarea
2. Leave empty
3. Click "Get Legal Decision"
4. Show error message

[NARRATE]
"When something goes wrong - like an empty query - users see a clear 
error message explaining what happened. There are no silent failures."
```

### Part 7: Summary & Call to Action (30 seconds)

```
[NARRATE]
"The Nyaya Legal Agent demonstrates how AI-powered legal decisions 
can be presented with clarity and authority:

✅ ALLOW - Clear permission to proceed
🚫 BLOCK - Unmistakable refusal with alternatives
📈 ESCALATE - Recognition of complexity
↩️ SAFE_REDIRECT - Recommended alternative pathways

All decisions include complete procedural guidance, timelines, and 
traceability through unique trace IDs.

Visit [URL] to see the full application."

[SHOW]
- Back to home or list of all states
- Show GitHub link
- Show contact/info
```

---

## Recording Checklist

- [ ] Screen recorder open and settings correct
- [ ] Audio input working (test first)
- [ ] Browser at correct URL (http://localhost:5173/decision)
- [ ] Dev server running
- [ ] Backend online
- [ ] Test queries prepared
- [ ] Script reviewed
- [ ] No private info visible on screen
- [ ] Resolution set to 1280x720 or 1920x1080
- [ ] Recording format set to MP4

---

## Recording Tips

### Before Recording

1. **Do a dry run:** Play through the script without recording
2. **Speak clearly:** Use microphone at appropriate distance
3. **Speak slowly:** Easier to understand, easier to edit
4. **Pause between sections:** Gives room for edits
5. **Have queries ready:** Copy them to a note for quick paste

### During Recording

1. **Intro take:** Record intro separately if it helps
2. **Natural clicking:** Don't rush through actions
3. **Explain clearly:** Pause to let explanation sink in
4. **Show each state:** Let it load, don't skip frames
5. **Expand sections:** Slowly so viewers can see transition
6. **Show details:** Let each piece of info be visible 2-3 seconds

### Common Mistakes to Avoid

- ❌ Too fast - viewers can't follow
- ❌ No narration - silent demo is boring
- ❌ Showing errors - cleanup first
- ❌ Poor audio - test mic before recording
- ❌ Minimized windows - show at good size
- ❌ Untested queries - prepare in advance

---

## Post-Recording Editing

### Essential Edits (Minimal)

1. **Trim intro/outro silence** (10 seconds)
2. **Remove long loading waits** (cut to 2-3 seconds)
3. **Add titles between sections** (text overlay)
4. **Color correct** if needed (adjust brightness)
5. **Normalize audio** (consistent volume)

### Optional Edits (Nice to Have)

1. **Add music** (royalty-free background music, low volume)
2. **Add captions** for accessibility
3. **Add graphics** (arrows pointing at features)
4. **Zoom in** on text during explanations
5. **Slow down** key moments

### Export Settings

**For Web (MP4):**
```
Codec: H.264
Resolution: 1280x720 (or 1920x1080)
FPS: 30
Bitrate: 5000 kbps
Audio: AAC 128 kbps
```

**For Sharing (WebM):**
```
Codec: VP9
Resolution: 1280x720
FPS: 30
Bitrate: 4000 kbps
```

**For GitHub/Archive:**
```
Keep both MP4 (widely supported) and WebM (smaller file size)
```

---

## Demo Video Structure

```
[0:00-0:30]  Intro
[0:30-2:00]  ALLOW State Demo
[2:00-4:00]  BLOCK State Demo (CRITICAL)
[4:00-5:00]  ESCALATE State Demo
[5:00-6:00]  SAFE_REDIRECT State Demo
[6:00-8:30]  Features (Export, Expand, Debug, Error)
[8:30-9:00]  Summary & CTA
────────────────────────
Total: 9 minutes
```

---

## Backup Recording Notes

If live recording fails:

**Option 1:** Record sections separately
- Record each state demo separately
- Stitch together in editor

**Option 2:** Screenshot-based demo + narration
- Take screenshots of each state
- Create slideshow in video editor
- Add narration and transitions

**Option 3:** Use recorded backend responses
- If backend is unreliable, use mock data
- Inject MOCK_DECISIONS from test file
- Record with stable responses

---

## Sharing the Demo

### Upload Locations

1. **GitHub**
   - Upload video to GitHub releases page
   - Or commit small MP4 to `/docs` folder
   - Include link in README

2. **YouTube (Optional)**
   - Set as unlisted for privacy
   - Support for higher resolution
   - Embed in documentation

3. **Loom/Vimeo**
   - Quick hosting without YouTube account
   - Password protection if needed

### Create Link Shortcut

```markdown
## Video Demo

**Watch the full demo:** [Nyaya Legal Agent - Demo Video](link-to-video)

- 📹 Duration: 9 minutes
- 💻 Resolution: 1280x720
- 🎯 Shows all 4 enforcement states
- 🎬 Created: March 4, 2026
```

---

## Demo Checklist

- [ ] Recording completed
- [ ] Audio clear and understandable
- [ ] All 4 states demonstrated
- [ ] Features demonstrated (export, sections, debug)
- [ ] No errors visible
- [ ] BLOCK state clearly shows refusal (unmistakable)
- [ ] Video duration 5-10 minutes
- [ ] File size reasonable (< 100 MB)
- [ ] Exported to MP4
- [ ] Uploaded to GitHub/shared location
- [ ] Link added to documentation

---

## Demo Script Summary

```
Part 1 [0:00-0:30]   → Introduction
Part 2 [0:30-2:00]   → ALLOW (Green ✅)
Part 3 [2:00-4:00]   → BLOCK (Red 🚫) **CRITICAL**
Part 4 [4:00-5:00]   → ESCALATE (Orange 📈)
Part 5 [5:00-6:00]   → SAFE_REDIRECT (Purple ↩️)
Part 6 [6:00-8:30]   → Features (Export, Expand, Debug, Errors)
Part 7 [8:30-9:00]   → Summary & CTA
────────────────────────────────────────────
Total: ~9 minutes

Audio: Clear narration throughout
Quality: 1280x720 or better
Format: MP4
```

---

**Recording Tool Recommendations:**

| Tool | Platform | Cost | Quality |
|------|----------|------|---------|
| OBS Studio | Windows/Mac/Linux | Free | ⭐⭐⭐⭐⭐ |
| ScreenFlow | Mac | $129 | ⭐⭐⭐⭐⭐ |
| Camtasia | Windows/Mac | $100/yr | ⭐⭐⭐⭐⭐ |
| Loom | Web-based | Free/Paid | ⭐⭐⭐⭐ |
