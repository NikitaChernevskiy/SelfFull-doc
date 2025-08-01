SelfFull universal Mobile App Standards: Settings / Account Setup Requirements  
v1.0 – 31 July 2025  

---

## Why We Need This Document  
The **Settings** screen is the control center for identity, privacy, support, and advanced actions such as account deletion. A clear, consistent, and secure experience boosts user trust and reduces support tickets. This specification establishes a single, measurable contract for the design, functionality, accessibility, and telemetry of the SelfFull Settings module.

---

## Layout & Navigation Requirements (1 – 10)

1. **Single‑column list** – Settings are presented as a vertically scrollable list; no horizontal scrolling on reference viewports (≥ 320 × 568 px).  
2. **Sticky header** – The top bar contains a back arrow, page title **“Settings”**, and user avatar thumbnail; header height = 56 dp.  
3. **User chip** – Directly under the header, display the signed‑in name (bold) and primary email (sub‑text, 70 % opacity).  
4. **Section dividers** – Use a 1 dp #E6E6E6 separator and a muted header label (e.g., **Support**); at least 24 dp top padding.  
5. **Row height** – Each tappable row = 56 dp, with a right‑chevron icon; hit target ≥ 48 × 48 dp.  
6. **Typography** – Row title uses 16 sp Medium; subtitles (if any) 14 sp Regular.  
7. **Dark / Light parity** – Contrast ratio ≥ 4.5 : 1; divider color adapts to theme.  
8. **Scroll indicators** – Native scrollbar appears on scroll; iOS elastic overscroll allowed.  
9. **Back navigation** – OS back gesture and header arrow both pop to previous screen without data loss.  
9. **Row click** - the whole button row should be clickable.
10. **Latency budget** – Tapping a row must push or present the destination view in < 300 ms (P95).  

---

## Account Management Requirements (11 – 20)

11. **Update Social Bio/Profile** – Deep‑links to **Public Profile** editor; pre‑loads current values for instant editing.  
12. **Change Password** – Opens a 3‑field form (Current, New, Confirm); password rules and real‑time strength meter per AUTH‑02.  
13. **Edit Contact Info** – Allows editing phone and secondary email; fields validated on blur; changes require re‑auth within the same session (OAuth re‑fresh).  
14. **Avatar edit** – Tapping the avatar thumbnail from the header opens avatar cropper; same specs as BIO‑37.  
16. **Offline restrictions** – Editing actions are disabled offline; greyed‑out state with tooltip “Connect to the internet to edit”.  
17. **Autosave draft** – If the user edits contact info but navigates away, draft persists for 10 min.  
18. **Success toast** – Successful save shows a green toast ≤ 2 s, accessible via screen readers.  
19. **MFA prompt** – After password change, present “Enable Two‑Factor Authentication” banner if 2FA is off.  
20. **Rate limiting** – Password change endpoint limited to 5 attempts per hour per user.  

---

## Support & Feedback Requirements (21 – 30)

21. **Tutorial Page** – Opens in‑app markdown viewer; content cached locally; shows date of last update.  
22. **Submit a Bug** – Opens a modal with: title, repro steps, screenshot attach (≤ 3 files, 5 MB each), severity picker.  
23. **Submit a Feature Request** – Similar modal but with “Impact” radio buttons (Nice‑to‑have, Important, Critical).  
24. **Auto‑log** – Bug reports auto‑attach anonymised device logs from the last 60 s (opt‑in toggle).  
25. **Ticket ID** – On submit, display Zendesk/Jira ticket ID and send confirmation email.  
26. **Accessibility** – All support modals keyboard‑navigable; voice dictation enabled.  
27. **Analytics** – Emit `bug_submitted` / `feature_request_submitted` with payload size and category.  
28. **Spam throttle** – Max 3 submissions per device per hour; CAPTCHA after 3.  
29. **Error handling** – If submission fails, retain form data locally for 24 h.  

---

## Legal & Version Info Requirements (31 – 35)

31. **Review Data Privacy & Terms** – Opens the current EULA and Privacy Policy in an in‑app webview; versions displayed at top.  
32. **Explore Our Website** – Launches the default browser via HTTPS deep‑link; confirm exit with native sheet on iOS (Apple HIG).  
33. **Current Version label** – Fixed at the bottom of the list, above the **Log Out** button:  
    - Displays `App vX.Y.Z (YYYY‑MM‑DD build)`  
    - Beta builds append “BETA” badge.  
34. **Update indicator** – If a newer version is available, append “– Update available” in orange text and deep‑link to store listing.  

---

## Danger Zone Requirements (36 – 45)

36. **Delete Your Profile** – Row styled in #C62828 (error) text; opens a 3‑step confirmation flow:  
    1. Password re‑entry (or biometric)  
    2. Context copy of irreversible consequences (≤ 120 chars)  
    3. Final “Delete” button disabled for 5 s countdown  
37. **Data export option** – Prior to deletion, offer “Download my data” (JSON + media ZIP); link emailed when ready.  
38. **Cooldown period** – Account is soft‑deleted for 30 days; user can restore via login email link.  
39. **Push token purge** – On soft delete, backend immediately invalidates push tokens.  
41. **Rate limit** – One delete attempt per 24 h.  
42. **Error copy** – If delete fails, show toast ≤ 100 chars; logs sent to Sentry.  
43. **GDPR log** – Deletion process writes audit trail with user ID hash, timestamp, and scrub status.  
44. **MDM block** – Managed devices hide Delete option; row invisible if `mdm_managed=true`.  
45. **Accessibility** – Countdown button announces remaining seconds via screen reader.  

---

## Session & Logout Requirements (46 – 50)

46. **Log Out button** – Centered, full‑width pill, located beneath the version label; color = primary brand 500.  
47. **Confirmation** – Logging out prompts “Are you sure?” modal; offers “Just log out” or “Log out & clear cached data”.  
48. **Token revocation** – Access and refresh tokens revoked server‑side; push token set to null.  
49. **Return route** – Post logout, app returns to the sign‑in screen, not the welcome carousel.  