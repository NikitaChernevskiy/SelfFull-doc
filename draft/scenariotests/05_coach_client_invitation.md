**Date:** 2025‑08‑02  
**File:** 05_coach_client_invitation.md  
**Purpose:** Verify that a coach can invite a client by email, that the invitation is delivered with correct links, and that the client can create a standard (non‑coach) account and appear in the coach’s **Users** list.

---

# Test Scenario – Coach → Client Invitation Flow

## 0  Pre‑conditions
- Coach is signed‑in and on **Coach Dashboard**  
- At least one course exists (needed only if the coach plans to assign content)  
- Client’s email address is not yet registered in SelfFull  

---

## A  Coach Sends an Invitation

1. **Open “Invite”**  
   - Coach taps **Invite** button in the *Users* panel  
   - *Invite User* modal appears

2. **Fill in *Name***  
   - Required  
   - 2 – 50 characters  
   - Letters, spaces, hyphens only  

3. **Fill in *Email***  
   - Required  
   - Valid address format `local@domain.tld`  
   - 6 – 254 characters  

4. **Toggle “Want to assign any course”**  
   - Default **OFF**; when **ON**, dropdown shows all existing courses  
   - Coach may leave **OFF** to invite without course access  

5. **Tap “Invite”**  
   - Button disabled until Steps 2‑3 valid  
   - Success toast *“Invitation sent”*  
   - New user row appears in *Users* list with status **Pending**  

6. **Copy‑link panel**  
   - Modal displays auto‑generated email text with platform URLs (Web, Android, iOS)  
   - “Copy” icon copies full message to clipboard  

---

## B  Client Receives the Email

1. **Open email “Invitation from your coach”**  
   - Subject line correct  
   - Body contains the same text shown in copy‑link panel  
   - Three platform links open respective stores / web app without 404  

2. **Verify sender**  
   - “Notification from SelfFull” as the sender name  
   - Email address uses `@selffull.io` domain  

---

## C  Client Creates an Account

1. **Follow the Web link** (or install mobile app and open)  
   - Landing page shows **Sign In** / **Sign Up** choice  

2. **Tap “Sign Up”** – *Create Account* form appears  

3. **Complete the form**

| Field | Validation Rules | Expected After Input |
|-------|------------------|----------------------|
| **Name** | Required; 2 – 50 letters / spaces / hyphens | Green border (valid) |
| **Email** | Required; matches invited email; valid format; 6 – 254 chars | Green border |
| **Password** | Required; ≥ 8 chars, ≥ 1 uppercase, ≥ 1 number, ≥ 1 symbol | Strength bar ≥ “Medium” |
| **Confirm Password** | Required; must equal **Password** | No mismatch error message |
| **Create a Coach Account** toggle | Must remain **OFF** | Toggle colour stays grey |

4. **Tap “Create Account”**  
   - Button enabled only when all fields valid  
   - Account is created; client taken to *Data Privacy* page  

5. **Accept Data Privacy**  
   - “Accept” button enables checklist  
   - On acceptance, client sees welcome screen “Excited to Meet You!”  

6. **Tap “Next”**  
   - Onboarding message (if previously set up by coach)
   - Minimal profile prompt appears (photo optional, phone optional)  
   - Skip allowed; client lands on **Client Dashboard**  

---

## D  Post‑registration Checks

1. **Coach refreshes *Users* list**  
   - Client row status changes from **Pending** to **Active**  
   - If “assign any course” was toggled **ON**, *Courses* column shows “All”  
   - If a specific course was selected, course name is listed

2. **Client access**  
   - Client can open *My Courses* and sees any assigned course  
   - If no course assigned, page shows message “No courses yet – ask your coach”  

3. **Re‑invite safeguard**  
   - Coach attempts to invite same email again → error *“User already exists.”*  

---

**End of file**