**Date:** 2025‑08‑02  
**File:** 07_ai_notes_auto_summary.md  
**Purpose:** Verify the full **AI Notes** workflow — create a note, add/edit content (transcript, session note, AI instruction), auto‑generate a recap, capture *Like* feedback, and manage the list (filter, delete).

---

# Test Scenario – AI Notes & Auto‑generated Recap

## 0  Pre‑conditions
- Coach is signed‑in  
- Stable internet connection  
- Browser / mobile app updated to latest version  

---

## A  AI Notes List

1. **Open “AI Notes”** from sidebar  
   - Page title “AI Notes” visible  
   - Banner hint “AI can make mistakes…” present  
   - **New** button at top‑left, **Filter (Date)** field at top‑right  
   - Existing notes show **Name** (e.g., 5222‑199) and date; each row has a red trash icon

2. **Filter notes**  
   - Tap **Filter (Date)** → date‑picker opens  
   - Select one date → list collapses to matching notes  
   - Clear (x) filter resets list  

3. **Delete note**  
   - Tap trash icon → confirm dialog *“Delete this note?”* → **Delete**  
   - Row disappears; count decrements  

---

## B  Create New Note

1. **Tap “New”**  
   - Modal “New AI Note Name” appears  
   - **Name** field  
     - Required  
     - 3 – 15 characters  
     - Digits or alphanumerics & hyphens allowed (`0‑9 A‑Z a‑z ‑`)  
     - Live counter bottom‑right (`0/15`)  
   - **Add** button disabled until input valid  
2. Enter valid name → **Add**  
   - Modal closes; new row appears in list (status draft)  
   - App navigates to **AI Note Details**

---

## C  Add Transcript

1. **Tap “Add Transcript”** bar  
   - Full‑page textarea appears  
   - **Show Sample** link populates sample text (optional)  
   - Validation  
     - Min 20 chars, Max 20 000 chars  
     - Plain text only (HTML tags stripped)  
   - **Save** button persists text and returns to details screen  

---

## D  Add Session Note

1. **Tap “Add Session Note”**  
   - Textarea & **Show Sample** link  
   - Validation  
     - Min 20 chars, Max 10 000 chars  
   - **Save** stores session note  

---

## E  Add AI Instruction (Optional)

1. **Tap “Add AI Instruction”**  
   - Textarea & **Show Sample** link  
   - Validation  
     - Min 10 chars, Max 2 000 chars  
   - **Save**   

2. **Apply AI Bot instructions** toggle  
   - Default **ON**; turn **OFF** to ignore instruction when generating recap  

---

## F  Generate Recap

1. **Suggestion input** (single‑line)  
   - Placeholder “Enhance this AI Note in…”  
   - Optional prompt, Max 200 chars  
2. **Generate** button  
   - Disabled if transcript missing  
   - On tap → spinner shows; recap area appears in ≤ 10 s  
3. **Recap output**  
   - Section title
   - Sub‑sections
   - Rich-text formatting
   - Speaker button (🔊) plays TTS of recap  

---

## G  User Feedback & Actions

| Action | Steps | Expected |
|--------|-------|----------|
| **Like** | Tap heart icon under recap | "Are you sure?" message; Heart turns solid |
| **Share** | Tap *Share* button | System share sheet |
| **Reniew** | Tap *Reniew* button | Regenerates the Recap |
| **Audio** | Tap speaker | TTS plays; tap again pauses |

*System logs*  
- Each Like event sends `POST` to App Insights
- 200 OK returned; no toast = error  

---

## H  Edit Existing Content

1. Bars now show **Edit Transcript / Edit Session Note / Edit AI Instruction**  
2. Tap any bar → textarea pre‑filled; edit and **Save**  
3. **Renew** → recap regenerates with latest inputs  

---

## I  Delete the Note (Details Screen)

1. Tap back arrow ← to return to list  
2. Trash icon for the new note → confirm **Delete**  
   - Note removed; user redirected to list view  

---

## 1  Expected Outcome
- Users can create, modify, and delete AI notes without errors  
- Generate produces a structured recap that reflects current inputs and optional AI instruction  
- Like events are captured and can be toggled; API returns success; No spamming to App Insights 
- Share open appropriate in‑app functionality  
- Filters and list maintenance (create, delete) update UI immediately  

---

**End of file**