**Date:** 2025‑08‑02  
**File:** 03_app_setup_settings.md  
**Purpose:** Verify the **My Settings** area and all linked flows: profile editing, password reset, contact info, tutorial link, bug / feature submission, privacy page, external website, profile deletion, and logout.

---

# Test Scenario – Settings & Account Management

## 0  Pre‑conditions 
- Latest SelfFull build installed; device has internet access  

---

## A  Open *My Settings*
1. **Tap avatar** (top‑right)  
   - Navigates to *My Settings*  
   - Username & email shown under header  
2. Verify list contains:  
   - Update Social Bio/Profile  
   - Change Password  
   - Edit Contact Info  
   - Tutorial Page  
   - Submit a Bug  
   - Submit a Feature Request  
   - Review Data Privacy & Terms  
   - Explore Our Website  
   - Delete Your Profile  
   - *Log Out* button & current version text  

---

## B  Update Social Bio / Profile
1. **Tap “Update Social Bio/Profile”**  
   - Opens *Update Profile* form  
2. **Fields & limits**  
   - *Your Name* – required, max 50 chars, letters & spaces  
   - *Title* – optional, max 100 chars  
   - *Short Bio* – optional, max 300 chars  
   - Social URLs (LinkedIn, Instagram, Facebook, TikTok, Discord, Website) – optional, must start with `http(s)://`  
3. **Save Changes**  
   - “Save Changes” enabled when form valid  
   - Toast *“Profile updated”* and return to *My Settings*  

---

## C  Change Password
1. **Tap “Change Password”** → *Forgot/Change Password* screen  
2. **Enter email**  
   - Required, valid email format  
3. **Tap “Send Link”**  
   - Success message *“Password reset email sent”*  

---

## D  Edit Contact Info
1. **Tap “Edit Contact Info”**  
   - Opens *Contact Info Page* modal  
2. **Fields**  
   - Email – required, max 254 chars  
   - Phone – optional, numeric & `+` only, max 20 chars  
   - One‑line descriptions for each social icon – optional, max 100 chars  
3. **Save**  
   - “Save” button enabled when required fields valid  
   - Modal closes, values persist on re‑open  

---

## E  Tutorial Page
1. **Tap “Tutorial Page”**  
   - Navigates to the Coach onboarding/tutorial previously seen during sign‑up  
   - Back navigation returns to *My Settings*  

---

## F  Submit a Bug
1. **Tap “Submit a Bug”** → *Create Bug Report* form  
2. **Fields**  
   - *Bug Name* – required, max 100 chars  
   - *Short Description* – required, max 500 chars  
   - Urgency selector 1‑5 (default 1)  
   - Optional screenshot / video upload  
3. **Submit Ticket**  
   - Confirmation toast *“Ticket submitted”* and return to *My Settings*  

## F  Submit a Feature Request
1. **Tap “Submit a Feature** → *Create Feature Report* form  
2. **Fields**  
   - *Feature Name* – required, max 100 chars  
   - *Short Description* – required, max 500 chars  
   - Urgency selector 1‑5 (default 1)  
   - Optional screenshot / video upload  
3. **Submit Ticket**  
   - Confirmation toast *“Ticket submitted”* and return to *My Settings*  

---

## G  Review Data Privacy & Terms
1. **Tap “Review Data Privacy & Terms”**  
   - Opens in‑app document / web‑view  
   - Back arrow returns to *My Settings*  

---

## H  Explore Our Website
1. **Tap “Explore Our Website”**  
   - Device browser opens `https://selffull.io` in new tab  
   - Switching back to app returns to *My Settings*  

---

## I  Delete Your Profile
1. **Tap “Delete Your Profile”**  
   - Confirmation modal appears with irreversible warning  
2. **Check confirmation box**  
   - “Delete Profile” button becomes active  
3. **Tap “Delete Profile”**  
   - Account deleted; user redirected to *Sign In* screen  

---

## J  Log Out
1. **Tap “Log Out”** (bottom of *My Settings*)  
   - Session ends; app shows *Sign In* screen  

---

**End of file**