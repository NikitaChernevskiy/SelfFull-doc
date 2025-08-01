 SelfFull universal Mobile App Standards: Coach → Client Course Invitation & Onboarding Requirements  
v1.0 – 31 July 2025  

---

## Why We Need This Document  
The invitation flow is the **first touch‑point** many clients have with SelfFull. A broken or confusing experience here translates directly into lost revenue and support tickets. This standard provides a single, measurable contract—covering everything from the coach’s “Invite Client” button to the client’s first visit to the course dashboard—so that Product, Design, Engineering, and QA can ship improvements confidently and auditors can trace the full enrollment lifecycle.

---

## Coach‑Side Invitation Requirements (1 – 15)

1. **Invite CTA**  
   “Invite Client” button appears on the **Users** card and inside the **Course Builder** Access‑Control panel.  

2. **Course picker**  
   Invitation modal requires a Course dropdown (searchable, max 20 visible items); default = last edited course.  

3. **Email field**  
   Accepts a single valid RFC 5322 address; real‑time validation; duplicate‑email check against existing users and pending invites.  

4. **Bulk mode**  
   “Add Another Email” link allows up to 20 addresses; each row independently validated.  

5. **Role confirmation**  
   Modal displays role badge **Client**; role is immutable for this invite.  

6. **Send button state**  
   Disabled until at least one valid email + course selected; shows inline spinner on submit.  

7. **Server response**  
   Endpoint `/api/invitations` returns 201 with `inviteId`, `courseRef`, and `expiresAt`; latency < 700 ms (P95).  

8. **UI feedback**  
   On success, green toast “Invitation sent” (≤ 2 s) plus line‑item appears in **Pending Invites** list with status “Sent”.  

9. **Analytics**  
   Emit `invite_sent` with courseRef, emailCount, coachId.  

10. **Resend**  
    Coach can resend after 5 min cooldown; status updates to “Resent (Timestamp)”.  

11. **Cancel invite**  
    Coach may cancel before acceptance; confirmation modal ≤ 120 chars.  

12. **Rate limit**  
    100 invites per coach per 24 h; additional attempts return 429.  

13. **Expiration**  
    Invites expire after 7 days; cron job marks status “Expired” and emails coach.  

14. **Error copy**  
    If email fails to enqueue, red toast ≤ 100 chars; list row shows “Error – Retry”.  

15. **Accessibility**  
    Modal fully keyboard navigable; focus trap within modal; labels exposed for screen readers.  

---

## Email Delivery Requirements (16 – 25)

16. **Template**  
    Subject: “Your coach invited you to SelfFull 🏆”; body ≤ 120 words, includes course name, coach name, and **Accept Invite** button.  

17. **Deep link**  
    `https://app.selffull.io/accept?token=<JWT>` opens the mobile app if installed (Universal/Applinks); else web sign‑up.  

18. **SPF/DKIM/DMARC**  
    Pass alignment; no “via sendgrid.net” warning in Gmail.  

19. **Delivery window**  
    95 % of messages reach recipient mailbox within 60 s.  

20. **Plain‑text part**  
    Multi‑part email includes plain‑text fallback with clickable URL.  

21. **Brand assets**  
    Logo ≤ 40 KB, alt text “SelfFull logo”.  

22. **Unsubscribe footer**  
    Because this is transactional, only “Contact Support” link is required—no unsubscribe.  

23. **Accessibility**  
    Button color contrast ≥ 4.5 : 1; link text not solely color‑coded.  

24. **Analytics**  
    Web beacon records `email_opened` and `email_click` events (if not disabled by client).  

25. **Security**  
    Token is JWT signed with RS256, payload = inviteId, email, courseRef, exp; expiresAt ≤ 7 days.  

---

## Client Sign‑Up & Onboarding Requirements (26 – 45)

26. **Token validation**  
    Hitting `/accept` with valid token auto‑prefills email field and locks it read‑only.  

27. **Account check**  
    If email already in SelfFull:  
    * **Logged‑out** – show “Login to accept invite” with password field.  
    * **Logged‑in** – skip to step 31.  

28. **New user path**  
    Displays sign‑up form (name, password, locale) with role fixed to **Client**; password rules per AUTH‑02.  

29. **Duplicate prevention**  
    Attempting normal sign‑up at `/signup` with invited email shows banner “We found an invitation—tap to accept”.  

30. **Post‑sign‑up redirect**  
    Successful account creation redirects to `/onboarding/welcome?courseRef=<id>`.  

31. **Onboarding overlay**  
    Shows coach avatar, course name, and benefits list (≤ 3 bullets); primary CTA **Get Started**.  

32. **Progress tracker**  
    3‑step progress bar: *Welcome → Profile → Finish*.  

33. **Profile step**  
    Mandatory fields: Avatar (400 × 400, ≤ 2 MB), Display Name (≤ 40 chars), Phone (E.164). “Skip” disabled until complete.  

34. **Data save**  
    Profile POST `/api/user/profile` latency < 700 ms; optimistic UI shows spinner in Save button.  

35. **Finish step**  
    Confirmation screen “You’re all set – jump into your course!” with **Go to Dashboard** button.  

36. **Role lock**  
    Client role cannot be changed during onboard; settings page hides coach‑only controls.  

37. **Re‑entry**  
    If onboarding interrupted, app resumes at last incomplete step.  

38. **Accessibility**  
    All onboarding dialogs support TalkBack/VoiceOver; progress bar announces step name on focus.  

39. **Analytics**  
    Emit `invite_accepted`, `onboarding_step_completed` (welcome|profile|finish), `onboarding_complete`.  

40. **Timeouts**  
    If invite token expired during sign‑up (> 7 days), app shows “Invitation expired—contact your coach”.  

41. **Error copy**  
    Network failures show toast ≤ 100 chars + retry button.  

42. **Rate limit**  
    Account creation limited to 3 attempts per IP per minute.  

43. **GDPR consent**  
    Checkbox “I agree to Privacy Policy” required; links to latest doc in webview.  

44. **Localization**  
    Email and onboarding strings loaded from locale bundles; default en‑US.  

45. **Security audit**  
    All endpoints require HTTPS; invite token verified server‑side before exposing coach/course data.  

---

## Post‑Acceptance & Dashboard Requirements (46 – 55)

46. **Enrollment record**  
    Backend creates Enrollment row (`userId`, `courseRef`, `status=active`, `joinedAt`).  

47. **Client Dashboard**  
    After onboarding, client lands on **My Courses** tab; invited course appears with status “New”.  

48. **Push token**  
    Device push token uploaded; server subscribes user to course notifications.  

49. **Coach notification**  
    Coach receives dashboard toast “<ClientName> joined AI Course” and email summary nightly.  

50. **Audit log**  
    `inviteId` marked `accepted`, timestamp recorded, invite row archived after 30 days.  

51. **Resilience**  
    If dashboard fails to load, app retries up to 3 times then shows offline fallback.  

52. **Logout safety**  
    Client can log out; invite token cannot be reused after acceptance.  

53. **Delete invite**  
    If coach cancels invite before acceptance, token returns 410 Gone with explanatory copy.  

54. **Accessibility**  
    Course card focusable; “New” badge announced by screen reader.  

55. **Analytics**  
    Emit `dashboard_loaded` with courseCount; client’s first session duration tracked.  