SelfFull universal Mobile App Standards: Main Menu, In‑App Feedback & Global Navigation Requirements  
v1.0 – 1 Aug 2025  

---

## Purpose  
This document captures the **miscellaneous interface elements** that appear across every screen in SelfFull: the main‑menu (hamburger / tab bar) structure, in‑app feedback / “Report Issue” utilities, help‑center access, and rules that keep global navigation consistent. Consolidating these standards avoids “drift” as new features launch and ensures users can always find help, give feedback, or jump to common areas in ≤ 2 taps.

---

## Main‑Menu Structure Requirements (1 – 15)

1. **Placement** — Mobile: bottom 5‑tab bar (Clients) / 6‑tab bar (Coaches). Tablet & Web: left vertical rail.  
2. **Tab order (Client)** — *Courses*, *Notes*, *Chat*, *Community* (toggle), *Settings*.  
3. **Tab order (Coach)** — *Dashboard*, *Chat with AI*, *My Courses*, *AI Notes*, *Community* (toggle), *Settings*.  
4. **Iconography** — Feather icon set @24 × 24 dp; label under icon ≤ 10 chars; colour `brandPurple‑500` when active, `grey‑500` inactive.  
5. **Badge support** — Numeric badge top‑right of icon; max value “99+”; contrast ≥ 4.5 : 1.  
6. **Active state** — Filled‑icon variant + label bold; announce via screen reader “X tab, selected”.  
7. **Haptic feedback** — Light tap feedback on tab change; respect `reduce‑haptics` OS preference.  
8. **Back‑stack rule** — Switching tabs resets navigation stack of origin tab; returning later shows root.  
9. **Deep‑link mapping** — Every tab root has canonical route (e.g., `/notes`, `/dashboard`).  
10. **Latency** — Switching tab renders first meaningful paint < 400 ms (P95).  
11. **Role gating** — Tabs hidden when feature flag off or role lacks permission.  
12. **Adaptive layout** — On foldables (≥ 720 dp width) bottom bar converts to side rail.  
13. **Accessibility** — Tab bar labelled `role="tablist"`; each item `role="tab"` with `aria‑selected`.  
14. **Analytics** — Emit `main_tab_selected` with tabId, source=icon|deep‑link.  
15. **Theming** — Tab bar background `surface‑100` light / `surface‑900` dark; divider 1 dp `surface‑300`.

---

## In‑App Feedback & “Report Issue” Requirements (16 – 30)

16. **Floating FAB** — Violet ❊ icon bottom‑right on every screen except modal overlays.  
17. **Press action** — Opens bottom sheet with: *Send Feedback*, *Report a Bug*, *Request a Feature*.  
18. **Feedback form** — Single textarea 20–500 chars; required sentiment selector (😊 / 😐 / ☹️).  
19. **Bug form** — Fields: Title (≤ 60 chars), Description (required), Severity slider, screenshot attach (≤ 3 × 5 MB).  
20. **Feature form** — Title, Description, Severity dropdown.  
21. **File types** — PNG/JPEG; automatic redaction of EXIF location data.  
22. **Submit flow** — latency < 800 ms.  
23. **Success toast** — Green toast “Thanks! We got it.” shows 2 s; tap “View ticket” deep‑links if user is coach.  
24. **Offline mode** — Feedback queued in local store; retries on connectivity.  
25. **Rate limits** — Max 5 submissions / device / day; additional attempts grey out submit.  
26. **Spam guard** — Honeypot hidden field + backend reCAPTCHA Enterprise v3 score ≥ 0.5.  
27. **Analytics** — Emit `feedback_submitted` with type, length, attachments, latency.  
28. **Privacy notice** — Form footer: “Submitting logs shares device info per Privacy Policy”. Links to doc.  
29. **Accessibility** — Forms keyboard navigable; error text announced via `aria‑live`.  
30. **Data retention** — Raw attachments auto‑deleted after 180 days; ticket metadata kept 2 years.

---

## Help‑Center Access Requirements (31 – 40)

31. **Help entry** — Main Settings list contains **Tutorial Page** row; also accessible from hamburger menu on web.  
32. **Content host** — Markdown docs rendered in in‑app reader; fallback to external URL if offline.  
33. **Search bar** — Keyword search across titles & headings; debounce 100 ms; highlights hits.  
34. **Contextual deep link** — From error banners, **“Learn more”** opens specific article via slug.  
35. **Contact support** — Top‑right email icon composes message to `support@selffull.io` with prefilled app version & OS.  
37. **Article rating** — 👍/👎 at bottom; required optional comment if 👎 selected.  
38. **Localization** — Article versions stored per locale; default en‑US if missing.  
39. **Accessibility** — Reader supports dynamic text sizes & custom line‑height slider.  
40. **Caching** — Articles cached 7 days; purge on app update.

---

## Global Navigation Consistency Requirements (41 – 55)

41. **Header height** — 56 dp mobile, 64 dp tablet/web; title center‑aligned.  
42. **Back arrow** — Always left‑aligned; returns to previous route or dismisses modal.  
43. **Settings gear** — Top‑right on coach pages; single source of truth for account options.  
44. **Modal style** — Bottom sheet radius 16 dp; drag‑down dismiss; scrim `rgba(0,0,0,0.4)`.  
45. **Toast location** — Bottom‑center above tab bar; max width 90 % screen; z‑index > FAB.  
46. **Loading spinner** — 3‑dot pulse brand‑purple; center horizontally inside container.  
47. **Error banner** — Red 500 bg, white text, dismiss X right; announces polite for screen readers.  
48. **Link colour** — Brand purple 500; underlined on hover (web) or focus.  
49. **Focus ring** — 2 px brand purple 500 outline for interactive elements when keyboard used.  
50. **Motion** — All screen transitions 200 ms slide‑in‑up; obey OS *Reduce Motion*.  
51. **Keyboard safe area** — Input fields auto‑scroll into view; no element hidden behind keyboard.  
52. **Orientation** — All screens support portrait & landscape; bottom bar becomes side bar in landscape > 700 dp.  
53. **Deep‑link 404** — Unknown route shows branded “Page not found” with **Back Home** button.  
54. **Telemetry** — Emit `nav_route_change` with from, to, durationOnFrom.  
55. **Theming** — Brand gradient background allowed only on splash/home; other pages use solid surfaces.

---

## Performance, Security & Compliance Requirements (56 – 65)

56. **Bundle impact** — Global nav & feedback add ≤ 1.5 MB to APK/AAB/IPA.  
57. **Frame rate** — Tab switching ≥ 55 FPS; nav drawer ≥ 60 FPS on reference devices.  
58. **Memory** — Main menu+feedback idle adds < 40 MB RAM.  
59. **Crash‑free** — < 0.2 % crash rate tied to nav classes.  
62. **Pen‑test** — Annual pen‑test verifies feedback form XSS & SSRF protections.  
63. **Rate‑limit** — Global nav analytics capped 60 events/min/device.  
64. **GDPR** — Feedback payloads anonymise userId if setting “Send anonymous” toggled.  
65. **Observability** — Grafana board for nav p95 route change and feedback error rate.