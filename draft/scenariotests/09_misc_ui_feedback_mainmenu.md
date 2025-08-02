**Date:** 2025‑08‑02  
**File:** 09_misc_ui_feedback_mainmenu.md  
**Purpose:** Validate global navigation and utility controls: sidebar menu consistency, header actions (settings ⚙, refresh ⟳), in‑app *Feedback* panel, and Help Center access. Ensures all users experience uniform, bug‑free navigation across desktop and mobile breakpoints.

---

# Test Scenario – Main Menu, Feedback & Help Center

## 0  Pre‑conditions
- User (coach **or** client) is signed‑in  
- Stable internet connection  
- Tests executed on:  
  - **Desktop** viewport ≥ 1024 px  
  - **Mobile** viewport ≤ 768 px  

---

## A  Sidebar / Main Menu

| Pos | Menu Item | Icon | Validation Rules | Expected Behaviour |
|-----|-----------|------|------------------|--------------------|
| 1 | **Dashboard** | Hourglass ⏳ | Label text *exactly* “Dashboard”; icon 24 × 24 px | Click loads dashboard in ≤ 1 s; item highlights (bg‑colour change) |
| 2 | **Chat With AIAI** | Sparkles ✨ | No truncation; tooltip on hover | Opens chat; sidebar remains visible |
| 3 | **My Courses** | Stack 🗂 | Icon stroke width 2 px | Opens last‑visited sub‑tab (*My Quest*, *Direct Chat*, or *Community*) |
| 4 | **AI Notes** | Document 📄 | Label identical on coach & client | Opens notes list screen |

**Desktop:** Sidebar fixed at 72 px width; icons + labels visible.  
**Mobile:** Sidebar fixed at the bottom; icons + labels visible.  

### Keyboard Navigation

- Tab order follows list order (Dashboard → … AI Notes)  
- Focus outline 2 px solid #6200EE (WCAG compliant)

---

## B  Header Utilities

| Control | Desktop Location | Mobile Location | Behaviour |
|---------|------------------|-----------------|-----------|
| **Settings ⚙** | Top‑right | Inside header | Opens *My Settings*; ESC or ← closes |
| **User Avatar** | Top‑right | Hidden (use *My Settings* for profile) | Hover shows email tooltip (desktop) |

Latency KPI: each action opens its destination in ≤ 1 s on reference connection.

---

## C  In‑App Feedback / Report Issue

1. **Locate “Feedback” vertical tab** (right edge, purple)  
   - Visible on every screen, fixed to 40 % viewport height  

2. **Open Feedback panel**  
   - Slide‑in drawer width 420 px (desktop) / full‑width (mobile)  
   - Title “Send Feedback”  

3. **Form fields & rules**

| Field | Type | Validation |
|-------|------|------------|
| **Bug Name** | Single line | 5–100 chars |
| **Description** | Multiline | 10–2 000 chars |
| **Attach Screenshot** | .png / .jpg | Optional |
| **Attach Video** | .mp4 | Optional |

4. **Submit**  
   - **Submit Ticket** button disabled until required fields valid  
   - On success → toast “Thank you for your feedback!” and drawer closes  

5. **Cancel**  
   - Tap <- or press ESC → drawer closes, no API call  

---

## E  Global Navigation Consistency Checks

| Scenario | Steps | Expected |
|----------|-------|----------|
| **Deep link reload** | Refresh while on AI Notes | Remains on the same page; sidebar item still highlighted |
| **Unauthorized access** | Attempt to open a coach‑only page as client | Redirect to home screen with toast “Access denied” |
| **Unknown URL** | Enter an invalid address | Custom 404 page with Back to Dashboard button |
| **Theme persistence** | Toggle dark mode in Settings | Sidebar & header adopt dark palette; persists after logout/login |

---

## 1  Expected Outcome
- Sidebar items load correct screens, highlight state, and obey keyboard navigation  
- Feedback drawer validates inputs, submits tickets, and closes gracefully  
- Help Center link always reachable and opens externally  
- Header utilities work on both breakpoints without layout shift  
- Unauthorized or invalid URLs handled with friendly messages and safe redirects  

---

**End of file**