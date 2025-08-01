SelfFull universal Mobile App Standards: **Communities (MVP)** Requirements  
v1.0 – 1 Aug 2025  

---

## Purpose  
The **Communities** module (Coach ↔ Coach / Client) lets users create a group, post thoughts, and invite others to collaborate.  
This MVP requirements list aligns with today’s UI (see screenshots) and will evolve as the feature matures.

---

## Community Creation Requirements (1 – 10)

1. **Create New Community CTA** — Purple **“+ Create New Community”** button visible on *Community* tab of **My Courses**.  
2. **Mandatory fields** — *Name* (≤ 40 chars) and *Description* (≤ 200 chars).  
3. **Optional field** — *Banner Image* (JPEG/PNG, ≥ 1280 × 360 px, ≤ 2 MB).  
4. **Inline validation** — Required fields show red asterisk; empty submission disables **Create** button.  
5. **Invite field** — Multi‑select dropdown pre‑filled with the coach’s own name; additional members can be added before save.  
7. **Success feedback** — Green toast “Community created”; auto‑redirect to Community list (see § 11).  
8. **Error copy** — Server errors show red toast ≤ 100 chars.  
10. **Accessibility** — All form inputs have visible labels; tab order follows Banner Image → Name → Description → Invite Members.

---

## Community List & Navigation Requirements (11 – 18)

11. **Tabs** — *My Quest*, *Direct Chat*, **Community**. Community tab stays highlighted when active.  
12. **Enable switch** — Toggle **“Enable Community Tab for Clients”** controls visibility in the client app; default **Off**.  
13. **Community card** — Displays *Name*, *Description* snippet (1 line), and member count.  
14. **Card action** — Tapping card opens Community page.  
15. **Empty state** — If 0 communities, show illustration + “Create your first community”.  
16. **Latencies** — List loads < 1 s on 4 G, 20 items per request.  
17. **Accessibility** — Card hit area ≥ 48 dp; screen reader reads name, description, member count.  

---

## Posting & Reactions Requirements (19 – 27)

19. **Post composer** — Multiline textarea placeholder “Share your thoughts with the community…”, 1–1 000 chars.  
20. **Add Image (optional)** — Button opens gallery/camera; JPEG/PNG ≤ 2 MB; thumbnail preview appears before post.  
21. **Post button state** — Disabled until text or image present; shows inline spinner on submit.  
22. **Post card** — Shows avatar, author name, timestamp (local), body text, optional image, **Delete** link for author.  
23. **Reactions** — ❤️ Like icon with counter; single‑tap toggles like; optimistic UI.  
24. **Comments** — Inline reply box “Say your thing…”; replies list under post; order = oldest‑first.  
25. **Delete** — Author may delete own post/reply; confirmation modal ≤ 120 chars.  
27. **Accessibility** — Like button toggles `aria-pressed`; comments live region polite.

---

## Member Management Requirements (28 – 33)

28. **Members icon** — Top‑right people icon opens Members sheet listing names and roles.  
29. **Inviting after creation** — Members sheet has **Invite** button; enters email(s) → sends invite email with deep link.  
30. **Member count** — Counter on Community card updates in real time.  
31. **Leave community** — Coaches/clients can leave; confirmation toast “Left community”.  
32. **Role** — Creator is **Admin**; other members are **Member**. For MVP, no mod tools beyond delete own posts.  

---

## Client Visibility Requirements (34 – 38)

34. **Toggle effect** — When **Enable Community Tab for Clients** is ON, client app shows *Community* tab inside **My Courses**.  
35. **Client capabilities** — Clients can: view list, open community, create text/image posts, like, comment, leave.  
36. **Permissions guard** — If toggle OFF, server denies community routes for client role (HTTP 403).  
37. **Latency parity** — Client list/post latencies match coach targets.  

---

## Performance & Compliance Requirements (39 – 45)

39. **Frame rate** — Scrolling posts ≥ 55 FPS on Pixel 5, iPhone SE 2nd gen.  
40. **Crash‑free** — < 0.3 % crash rate in Communities module (30‑day rolling).  
41. **Rate limits** — 30 posts/min/user; 100 likes/min/user; extra -> HTTP 429.  
42. **Storage** — Images stored on S3 with 30‑day lifecycle to glacier; URLs signed, 24 h expiry.               
44. **Moderation (basic)** — Posts run through text & image safety filter; blocked content shows “Removed for policy”.  
45. **GDPR** — On account deletion, posts & images purged ≤ 30 days; group remains with “Deleted User” label.