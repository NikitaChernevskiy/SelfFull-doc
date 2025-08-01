SelfFull universal Mobile App Standards: New Coach Onboarding & Public Bio Requirements  
v1.0 – 31 July 2025  

---

## Why We Need This Document  
A seamless first‑time experience is critical for converting qualified professionals into active SelfFull coaches. This standard defines the **end‑to‑end onboarding contract**—from account creation to a publish‑ready coach profile—so that Product, Design, Engineering, and QA share a single, measurable target. By codifying sign‑in/up flows, role selection, first‑login guidance, and public‑bio creation, we minimize drop‑off, ensure accessibility and compliance, and guarantee that every coach enters the marketplace with a complete, trustworthy presence.

---

## Sign‑Up / Sign‑In Requirements (1 – 15)

1. **Multi‑method entry** – Email + password, Apple ID, Google are available; each path lands on the same post‑auth flow.  
2. **Password policy** – Minimum 12 characters, at least one upper, lower, digit, and symbol; zxcvbn score ≥ 3; real‑time strength meter.  
3. **Social scope** – OAuth scopes limited to verified email and profile photo; no unnecessary data requested.  
4. **Email verification** – Verification link expires in 24 h; unverified users can explore but cannot publish a coach profile.  
5. **Magic link fallback** – If a coach forgets the password, “Send me a sign‑in link” option delivers a single‑use token valid 15 min.  
6. **2FA prompt** – After first successful login, display a non‑blocking banner encouraging 2FA enablement (TOTP/SMS).  
7. **Locale detection** – UI strings load from the device locale; fallback to en‑US.  
8. **Error copy** – Authentication errors ≤ 100 chars, never reveal whether email exists.  
9. **Inline progress** – Sign‑in button shows a spinner and disables while authenticating; latency target < 3 s (P95).  
10. **WCAG compliance** – All auth screens meet WCAG 2.2 AA contrast and focus‑order guidelines.  
11. **Analytics** – Emit `signup_start`, `signup_complete`, `signin_complete` with provider and timestamp.  
12. **Rate limiting** – Lock out IP after 10 failed attempts in 5 min; captchas appear after 6.  
13. **Device trust** – Remembered devices valid for 30 days; revoke on password change.  
14. **Deferred TOS/PP** – User must accept latest Terms of Service & Privacy Policy during sign‑up; links open in‑app webview.  
15. **Accessibility labels** – Text fields and buttons expose descriptive labels for VoiceOver/TalkBack.

---

## Role Selection Requirements (16 – 25)

16. **Single choice gate** – During auth, app presents a modal with “Coach” / Client” slider user cannot skip.  
17. **Mutually exclusive state** – Selecting one role disables the other; change requires Settings → Account Type switch and re‑onboarding.  
18. **Context copy** – Each option includes a ≤ 140‑char description of benefits to aid informed choice.  
19. **Illustrations** – Role cards include vector iconography; images size ≤ 200 KB; color‑blind friendly palette.  
20. **Persistence** – Chosen role stored locally and server‑side; user returns to correct dashboard on next launch.  
21. **Back‑navigation** – Hardware/software back button returns to login screen, not to a blank app shell.  
22. **A/B test flag** – Role‑selection screen is flag‑guarded for copy/UI experimentation; experiments logged to analytics.  
23. **Latency budget** – Role choice submission ≤ 1 s round‑trip.  
24. **Accessibility focus** – Focus starts on the modal title, arrow key navigation cycles buttons logically.  

---

## First‑Login Instruction Modal (26 – 35)

26. **Auto‑display** – Immediately after role selection, show an instructional overlay explaining dashboard, earnings, and profile steps.  
27. **Single‑use** – Modal auto‑dismiss never reappears post first completion; user can re‑open via **Settings → Tutorial PAge**.  
28. **Dismiss options** – “Skip” and “Next/Got it” buttons; “Skip” exits overlay.  
29. **Copy limits** – Each card ≤ 120 chars primary text, ≤ 80 chars secondary; supports dynamic‑type.  
30. **Illustrations & animation** – Lottie or static SVG ≤ 500 KB total; animation loops no more than twice.  
31. **Progress dots** – Indicator shows position 1/6, 2/6, 3/6, ...; tappable for direct navigation.  
32. **Offline cache** – Content served from local bundle to avoid blank state when offline.  
33. **Voice support** – “Listen” button reads card aloud; transcripts provided for captions.  
35. **Latency** – Overlay appears in < 500 ms after dashboard load; prevents interaction until dismissed.

---

## Public Coach Profile Setup Requirements (36 – 50)

36. **Mandatory fields** – Avatar, Display Name, Title (max 60 chars), Short Bio, Social Profiles.  
37. **Avatar upload** – Accept HEIC/JPEG/PNG; min resolution 400 × 400; in‑app crop to square; file size ≤ 2 MB.  
38. **Headline rules** – Sentence case, no emojis, profanity filter (DirtyAI v5) score must be 0.  
39. **Bio length** – 150–1 000 chars with live counter; Markdown italics and bullet lists allowed; no inline HTML.   
44. **Preview mode** – Real‑time preview panel mirrors changes before saving; responsive for phone/tablet breakpoints.  
45. **Save & publish CTA** – Disabled until all mandatory fields valid; tooltip explains missing items; save latency < 2 s.  
46. **Accessibility** – All fields have labels; avatar uploader supports camera capture.  
47. **Error handling** – If save fails, toast ≤ 100 chars appears at top with retry option.  
48. **Draft persistence** – Unsaved changes auto‑save to local storage every 10 s; restore prompt on next launch.  
49. **Profile visibility** – Toggle “Publish my profile” off by default until all required fields entered; cannot be forced on.  

---