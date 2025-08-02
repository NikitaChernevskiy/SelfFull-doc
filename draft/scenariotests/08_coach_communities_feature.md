**Date:** 2025‑08‑02  
**File:** 08_coach_communities_feature.md  
**Purpose:** Ensure coaches can create, manage, and moderate **Communities**, and that clients can view, post, react, and reply within those communities.

---

# Test Scenario – Community Creation & Engagement

## 0  Pre‑conditions
- Coach is signed‑in and on **My Courses → Community** tab  
- At least one client exists in the coach’s *Users* list  
- Stable internet connection  

---

## A  Enable Community Tab for Clients

1. **Toggle “Enable Community Tab for Clients”**  
   - Default state **OFF** (grey)  
   - Tap toggle → turns **ON** (colour)  
   - Success toast *“Community tab enabled for clients”*  
   - Switching **OFF** again hides Community tab for clients (verify with test client login)  

---

## B  Create New Community

1. **Tap “+ Create New Community”**  
   - *Create New Community* form opens  

2. **Banner Image** *(optional)*  
   - Tap “➕” icon → image picker  
   - Accepts .jpg / .png, Max 10 MB, Min 600 × 200 px  
   - Preview thumbnail appears after upload  

3. **Name***  
   - Required text field  
   - Validation: 3 – 60 characters; letters, numbers, spaces, punctuation `. , ? ! -`  
   - Error “Name is required (3‑60 chars)” if invalid  

4. **Description***  
   - Required multi‑line field  
   - Validation: 10 – 300 characters; plain text only (HTML stripped)  
   - Live counter bottom‑right (`0/300`)  

5. **Invite Members**  
   - Search bar shows existing users after typing ≥ 2 chars  
   - Tap user → chip appears in list  
   - Repeat to add multiple members  
   - **Invite** button sends in‑app notification  
   - Success toast *“Invitations sent”*  

6. **Save Community**  
   - **Save / Create** button enabled when Name & Description valid  
   - Tap → form closes, Community list refreshes  
   - New card shows:  
     - **Name:** <community name>  
     - **Description:** first 100 chars  
     - **Members:** *n* members (initially count of invited users)  

---

## C  Open & Post in Community

1. **Tap community card**  
   - Community page opens; title and description at top  
   - **Members** icon top‑right navigates to member list  

2. **Create a post**

| Field | Validation Rules | Expected |
|-------|------------------|----------|
| **Post textarea** | Required; 1 – 2 000 characters | “Post To Community” disabled until content present |
| **Add Image** *(optional)* | .jpg / .png, Max 10 MB | Thumbnail preview under textarea |
| **Post To Community** button | Enabled when textarea valid | New post appears under **Posts** section |

3. **Post display**  
   - Avatar, author name, timestamp  
   - Body text wraps correctly; image thumbnail if attached  
   - **Heart icon** (outline) with count (default 0)  
   - Comment bubble icon with count (default 0)  
   - **Delete** link visible to coach and post author  

---

## D  Post Reactions & Replies

1. **Like a post**  
   - Tap heart → icon fills colour, count +1  
   - Tap again → icon outline, count ‑1  

2. **Reply to a post**

| Action | Steps | Expected |
|--------|-------|----------|
| **Reply field** | Tap “Say your thing…” | Field expands; placeholder clears |
| Type reply | 1 – 1 000 chars | “Reply” button enabled |
| Send reply | Tap **Reply** | Comment appears indented under post, with own heart & delete |

3. **Delete post or comment**  
   - Tap **Delete** link → confirm dialog *“Delete this post?”* / *“Delete this comment?”*  
   - **Delete** removes item; counts update  

---

## E  Members Panel

1. **Tap “Members”** icon  
   - Modal shows list of avatars, names, joined date  
   - **Remove** button next to each (coach only) → confirm removal  
   - Removed user cannot access community (verify with client account)  

---

## F  Edit & Delete Community

1. **Return to Community list**  
   - Tap card menu (⋯) → **Edit / Delete** options  

2. **Edit**  
   - Opens same form pre‑filled; update fields; **Save** persists changes  

3. **Delete**  
   - Dialog *“Delete community and all posts?”*  
   - Checkbox *“I understand”* enables **Delete**  
   - Card disappears; clients lose access  

---

## 1  Expected Outcome
- Communities can be enabled/disabled globally by coaches  
- Creation validates all required fields and image specs  
- Members receive invitations and gain access  
- Posts support text, optional image, like/unlike, replies, and deletion  
- Member list reflects real‑time additions/removals  
- Editing or deleting a community updates visibility appropriately without residual data  

---

**End of file**