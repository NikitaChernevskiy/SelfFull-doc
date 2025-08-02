**Date:** 2025‑08‑02  
**File:** 02_new_coach_onboarding_bio.md  
**Purpose:** Verify the *New Coach* onboarding flow – from first launch through profile setup – and confirm that the user lands on the dedicated **Coach Dashboard**.

---

# Test Scenario – Coach Sign‑up & Onboarding

## 0  Pre‑conditions
- **App:** Latest SelfFull version is installed  
- **Device:** Connected to the internet and running iOS 15 + / Android 11 +  
- **Account:** User is signed out; no existing SelfFull profile on the device  

---

## A  Sign‑up Screen (Screenshot 1)

1. **Launch SelfFull**  
   - Splash loads in ≤ 3 s  
   - **Sign In** screen is displayed

2. **Tap “Sign Up”**  
   - Navigation to *Create Account* form

3. **Fill in the form**  
   - **Name** field  
     - Required; alphabetic & space characters only  
     - Max 50 characters  
   - **Email** field  
     - Required; valid email format (`local@domain.ext`)  
     - Max 254 characters  
   - **Password** field  
     - Required; min 8 characters, inc. 1 uppercase, 1 number, 1 symbol  
     - Eye icon toggles show/hide  
   - **Confirm Password** field  
     - Must exactly match *Password*  
   - **“Create a Coach Account”** toggle  
     - Default OFF → toggle ON; switch moves and label changes colour  
   - **Create Account** button  
     - Disabled until all required fields valid  
     - Shows loading spinner after tap  

4. **Submit**  
   - Account created without validation errors  
   - Redirected to *Data Privacy* screen  

---

## B  Data Privacy & Welcome

5. **Accept Data Privacy**  
   - “Accept” button enabled  
   - On tap, confirmation toast appears and screen advances  

6. **Welcome message**  
   - Heading “Excited to Meet You!” visible  
   - **Next** button present and functions  

---

## C  Coach Profile Setup (Screenshot 2)

7. **Profile photo**  
   - Tap **Add Photo** → device photo picker opens  
   - Select or take picture → circular preview updates  

8. **Display name**  
   - Input *“What Shall We Call You?”*  
     - Required; max 30 characters; accepts letters, spaces, hyphens  
   - Field outline turns green when valid  

9. **Custom terminology**  
   - *Rename “Quests” To:* field  
     - Optional; max 20 characters  
     - Accepts letters & spaces  

10. **Proceed**  
    - **Next / Continue** button enabled when required fields met  
    - Advances to *Coach Welcome Guide* slides  

---

## D  Coach Welcome Guide

11. **Read guide**  
    - Horizontal swipe or “Next” button moves through pages  
    - Progress indicator updates (e.g., 1 / 3, 2 / 3…)  

12. **Finish onboarding**  
    - Tap **Get Started** (final slide)  
    - Navigated to **Coach Dashboard**  

---

## 1  Expected Outcome
- New user is registered with **coach role**  
- Profile picture and display name appear on dashboard header  
- Coach‑specific navigation items are visible  

---

**End of file**