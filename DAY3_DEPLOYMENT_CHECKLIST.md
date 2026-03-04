# DAY 3 - Production Deployment Checklist

**Date:** March 4, 2026  
**Phase:** DAY 3 - Final Production Hardening  
**Deploy To:** Production Environment  

---

## Pre-Deployment Verification

### Code Quality

- [ ] No console errors (run DAY3_TEST_RUNNER.js)
- [ ] No console warnings about missing fields
- [ ] No undefined variables in page
- [ ] No TypeErrors or ReferenceErrors
- [ ] Performance acceptable (page loads < 3s)
- [ ] No memory leaks in DevTools

**Check Script:**
```javascript
// In browser console
console.log('Errors in page:');
let errorCount = 0;
const oldError = console.error;
console.error = (...args) => {
  errorCount++;
  oldError(...args);
};
// Do something, then check errorCount
```

### Component Testing

- [ ] All components render without errors
  - [ ] DecisionPage.jsx
  - [ ] GravitasDecisionPanel.jsx (if integrated)
  - [ ] GravitasLegalDecisionScreen.jsx (if integrated)

- [ ] All CSS loads and applies correctly
  - [ ] DecisionPage.css colors render
  - [ ] Responsive breakpoints work
  - [ ] Animations smooth (60 FPS)

- [ ] All services functional
  - [ ] nyayaBackendApi.js connects
  - [ ] queryNyayaDecision() works
  - [ ] Error handling works

### Backend Integration

- [ ] Backend endpoint online: https://nyaya-ai-0f02.onrender.com
  ```bash
  curl https://nyaya-ai-0f02.onrender.com/health
  ```
  Expected: 200 status or response

- [ ] Query endpoint working
  ```bash
  curl -X POST https://nyaya-ai-0f02.onrender.com/query \
    -H "Content-Type: application/json" \
    -d '{"query":"test","jurisdiction":"IN"}'
  ```
  Expected: Valid decision with enforcement_decision field

- [ ] All response fields present (12 required)
- [ ] enforcement_decision field non-empty
- [ ] trace_id field unique per query
- [ ] confidence scores valid (0-1 range)
- [ ] Timeout properly set (30s)

### Security & Privacy

- [ ] No API keys exposed in code
  ```bash
  grep -r "REACT_APP_API" src/
  # Should return nothing sensitive
  ```

- [ ] No hardcoded credentials
- [ ] HTTPS used for backend
- [ ] CORS properly configured
- [ ] No sensitive data in localStorage
- [ ] Environment variables used correctly

### Browser Compatibility

- [ ] Chrome/Edge (latest 2 versions): ✅
- [ ] Firefox (latest 2 versions): ✅
- [ ] Safari (latest 2 versions): ✅
- [ ] Mobile browsers tested: ✅

### Accessibility

- [ ] WCAG AA contrast compliance
  - [ ] Text readable on all backgrounds
  - [ ] Enforcement banner colors distinguishable

- [ ] Keyboard navigation works
  - [ ] Tab through form
  - [ ] Enter submits form
  - [ ] Escape closes modals (if any)

- [ ] Touch targets 44px+ (mobile)
- [ ] Screen reader friendly (test with NVDA/JAWS)
- [ ] No auto-play sounds
- [ ] Alt text on images (if any)

### Performance

- [ ] Page load time < 3 seconds (4G)
- [ ] Largest Contentful Paint (LCP) < 2.5s
- [ ] First Input Delay (FID) < 100ms
- [ ] Cumulative Layout Shift (CLS) < 0.1
- [ ] JavaScript bundle size reasonable
- [ ] CSS minified
- [ ] No render-blocking resources

**Check in DevTools:**
```
1. Ctrl+Shift+I (DevTools)
2. Go to Lighthouse tab
3. Run audit
4. Check scores (target: 90+)
```

---

## Testing Checklist

### Functional Testing

- [ ] Form submission works
  - [ ] Can type in textarea
  - [ ] Button clickable
  - [ ] Enter/Ctrl+Enter submits

- [ ] Decision rendering works
  - [ ] All 4 enforcement states display
  - [ ] Correct colors appear
  - [ ] Correct labels/emojis show

- [ ] Sections expand/collapse
  - [ ] Click expands section
  - [ ] Click collapses section
  - [ ] Content fully visible
  - [ ] No text overflow

- [ ] Export button works
  - [ ] Downloads JSON file
  - [ ] JSON valid format
  - [ ] Contains all fields

- [ ] Reset button works
  - [ ] Clears query
  - [ ] Clears decision
  - [ ] Clears errors
  - [ ] Ready for new query

### Error Cases

- [ ] Empty query error shows
- [ ] Backend timeout handled gracefully
- [ ] Network connection failure message
- [ ] Invalid response handled
- [ ] Malformed JSON handled
- [ ] 500 server error handled

### State Validation

#### ALLOW State
- [ ] Green banner (#28a745)
- [ ] ✅ ALLOWED label
- [ ] Reasonable confidence (80-95%)
- [ ] Legal route shown
- [ ] Procedural steps listed
- [ ] No error indication

#### BLOCK State (CRITICAL)
- [ ] Red banner (#dc3545)
- [ ] 🚫 BLOCKED label
- [ ] Legal analysis explains refusal
- [ ] Alternative pathway shown
- [ ] Trace ID present and valid
- [ ] NOT confusion with error state
- [ ] Reasonable confidence (60-90%)

#### ESCALATE State
- [ ] Orange banner (#fd7e14)
- [ ] 📈 ESCALATION REQUIRED label
- [ ] Mentions expert review
- [ ] Lower confidence (60-75%)
- [ ] Arbitration pathway
- [ ] Longer timeline

#### SAFE_REDIRECT State
- [ ] Purple banner (#6f42c1)
- [ ] ↩️ SAFE REDIRECT label
- [ ] Alternative venue clear
- [ ] Civil court option preserved
- [ ] Reasoning provided

### Mobile Testing

- [ ] iPhone X (375x812): ✅
- [ ] iPad (768x1024): ✅
- [ ] Galaxy S10 (360x800): ✅
- [ ] Pixel 4 (412x869): ✅
- [ ] No horizontal scroll
- [ ] Buttons touchable (44px+)
- [ ] Text readable (14px+)
- [ ] Orientation change works

### Cross-Browser Testing

- [ ] Chrome on Windows
- [ ] Firefox on Windows
- [ ] Safari on Mac
- [ ] Chrome on Android
- [ ] Safari on iOS
- [ ] Firefox on Android

---

## Production Deployment Steps

### Step 1: Pre-Deployment Build

```bash
cd frontend
npm install        # Install dependencies
npm run build      # Production build
```

Verify:
- [ ] Build succeeds with no errors
- [ ] No console warnings
- [ ] Build size reasonable (< 500KB gzip)
- [ ] dist/ folder created

### Step 2: Build Verification

```bash
# Serve production build locally
npm run preview  # or python -m http.server
```

Test:
- [ ] App loads at http://localhost:5000 (or assigned port)
- [ ] Submit query and verify response
- [ ] All states test successfully
- [ ] Enforcement colors correct
- [ ] Export button works

### Step 3: Deploy to Hosting

**If using Vercel (recommended for Vite):**

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel --prod
```

**If using other hosting:**
- [ ] Upload dist/ folder to server
- [ ] Configure routing (SPA setup)
- [ ] Enable HTTPS/SSL
- [ ] Set up CORS if needed
- [ ] Configure environment variables

### Step 4: Post-Deployment Verification

**Smoke Tests on Production:**

```bash
# Test 1: Page loads
curl -I https://your-domain.com   # Should return 200

# Test 2: All endpoints accessible
curl https://your-domain.com/decision

# Test 3: Backend connection
curl https://nyaya-ai-0f02.onrender.com/health
```

**Browser Testing on Production:**

- [ ] Open https://your-domain.com in browser
- [ ] Submit query → Receive decision
- [ ] Check all enforcement states work
- [ ] Export & reset buttons functional
- [ ] No console errors
- [ ] Performance acceptable

### Step 5: Monitoring Setup

**Enable Monitoring:**
- [ ] Sentry for error tracking
- [ ] Google Analytics for usage
- [ ] Uptime monitoring
- [ ] Performance tracking (Lighthouse CI)

**Monitor:**
```
Every 4 hours for first day:
- Error logs
- User sessions
- Performance metrics
- Backend response time
```

---

## Deployment Environment Variables

### Required for Production

```bash
# .env.production
VITE_API_BASE_URL=https://nyaya-ai-0f02.onrender.com
VITE_ENVIRONMENT=production
VITE_LOG_LEVEL=error
VITE_ENABLE_ANALYTICS=true
```

### Optional

```bash
VITE_SENTRY_DSN=https://your-sentry-dsn
VITE_GA_ID=UA-your-analytics-id
VITE_HEAP_ID=xxxx
```

**Verify in built app:**
```javascript
// In browser console
console.log(import.meta.env.VITE_API_BASE_URL)
// Should show production URL
```

---

## Rollback Plan

### If Deployment Fails

1. **Immediate Action:**
   - [ ] Roll back to previous version
   - [ ] Verify previous version working
   - [ ] Check error logs

2. **Investigation:**
   - [ ] Review deployment logs
   - [ ] Check backend status
   - [ ] Review recent changes
   - [ ] Check browser console for errors

3. **Communication:**
   - [ ] Notify team about rollback
   - [ ] Provide ETA for fix
   - [ ] Document issue

### Version Control

```bash
# Tag production releases
git tag -a v1.0.0 -m "Production release"
git push origin v1.0.0

# Rollback if needed
git revert <commit-hash>
git push origin main
```

---

## Post-Deployment Validation

### Day 1 (Launch Day)

- [ ] Monitor errors in first hour
- [ ] Test critical paths
- [ ] Check performance metrics
- [ ] Verify backend connectivity
- [ ] Monitor user sessions (if applicable)

**Checklist:**
```
08:00 - Deploy to production
08:15 - Smoke tests pass
09:00 - Monitor for 1 hour, check for errors
12:00 - Check performance metrics
16:00 - End of day review
```

### Day 2-7 (First Week)

- [ ] Daily error log review
- [ ] Weekly performance analysis
- [ ] User feedback collection
- [ ] Monitor backend uptime

---

## Communication Checklist

### Before Deployment

- [ ] Notify stakeholders of deployment time
- [ ] Schedule maintenance window (if needed)
- [ ] Prepare rollback plan
- [ ] Brief QA team on testing

### During Deployment

- [ ] Provide status updates
- [ ] Show live demo of working states
- [ ] Confirm all enforcements working

### After Deployment

- [ ] Confirmation email to team
- [ ] Link to production URL
- [ ] Document deployment notes
- [ ] Log deployment metrics

---

## Sign-Off Checklist

**QA (Vinayak):**
- [ ] All test cases passed
- [ ] No critical bugs found
- [ ] Mobile responsiveness verified
- [ ] Enforcement states validated
- [ ] Ready for production: YES / NO

**Final Approval:**
- [ ] Backend team confirms API ready
- [ ] DevOps confirms infrastructure ready
- [ ] Product owner approves deployment
- [ ] Security review passed

---

## Deployment Log

```
Date: ___________
Time: ___________
Deployed by: ___________

Pre-deployment checks: [ ] PASS [ ] FAIL
Tests executed: ___/13 passed
Deployment method: [ ] Vercel [ ] Manual [ ] Other: _____
Production URL: _____________________
Backend: https://nyaya-ai-0f02.onrender.com
Status: [ ] SUCCESS [ ] ROLLED BACK

Post-deployment issues: 
1. ____________
2. ____________

Sign-off:
QA: __________ Date: __________
Backend: __________ Date: __________
DevOps: __________ Date: __________
```

---

## Quick Troubleshooting

### Issue: White blank page

**Troubleshoot:**
```javascript
// In console
document.body.innerHTML   // Should show something
window.location.href      // Should be correct URL
```

**Fix:** Check build output, rebuild and redeploy

### Issue: Backend connection fails

**Troubleshoot:**
```bash
curl https://nyaya-ai-0f02.onrender.com/health
```

**Fix:** Check backend URL, CORS settings, network

### Issue: Styles not loading

**Troubleshoot:**
- Check CSS files in DevTools Network tab
- Verify CSS file sizes

**Fix:** Clear cache, rebuild, redeploy

### Issue: API calls timeout

**Troubleshoot:**
- Check backend response time
- Monitor network in DevTools

**Fix:** Increase timeout, optimize backend

---

## Final Deployment Sign-Off

| Item | Status | Signed By | Date |
|------|--------|-----------|------|
| Code Review | ✅ | | |
| QA Approval | ✅ | | |
| Security Review | ✅ | | |
| Performance Check | ✅ | | |
| Backend Ready | ✅ | | |
| Deployment Complete | [ ] | | |
| Post-Deploy Verified | [ ] | | |

---

**Ready for Production Deployment** ✅
