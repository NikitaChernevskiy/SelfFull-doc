**Date:** 2025‑08‑18  
**File:** `2025‑08‑18_1.0.3+9_10_notifications_push_inapp.md`  
**Purpose:** Validate end‑to‑end delivery and UX of **push** and **in‑app** notifications for Course/Module completion, Coach↔Client Chat, and Community events (invite/remove, reactions, new posts). Ensure correct recipients, channels, timing, deep links, unread counts, and read‑state consistency across desktop and mobile.

---

# Test Scenario 10 – Notifications (Push & In‑App)

## 0  Pre‑conditions
1) **Test accounts**  
   - **Coach A** (coach role)  
   - **Client B** (client role, enrolled in a course)  
   - **Member C** (community member)  
   - **Member D** (community member; use for “all members” broadcast verification)

2) **Devices / platforms**  
   - iOS phone (push enabled) signed in as **Client B**  
   - Android phone (push enabled) signed in as **Coach A**  
   - Web/Desktop session (for in‑app inbox/bell) signed in as **Member C**  
   - Optional extra web/mobile session signed in as **Member D**

3) **System readiness**  
   - Push permissions **Allowed** on both mobile devices  
   - Valid device tokens registered after login (check system/QA logs)  
   - Stable internet connection  
   - App versions/builds match test environment  
   - In‑app notification center (“bell” or inbox) visible; unread badge enabled

4) **States to test (each scenario runs in all three)**  
   - **Foreground:** recipient has app open  
   - **Background:** app in background  
   - **Terminated:** app killed

5) **KPI / timing**  
   - **In‑app** appears in ≤ 2 s (from event)  
   - **Push** delivered in ≤ 15 s (from event)  
   - Tapping a notification deep‑links and renders target screen in ≤ 1 s

> **Note:** On some OSes, push banners may not show while the app is foreground; still verify that the push was sent (server logs) and that the **in‑app** notification appears.

---

## A  Notification Types & Expected Recipients

| Area | Trigger | Channel(s) | Recipient(s) | Deep Link Target (expected) |
|---|---|---|---|---|
| **Course & Module** | User completes a **course** | Push + In‑app | The **completing user** | Course detail / completion screen |
|  | User completes a **module** | Push + In‑app | The **completing user** | Module summary / next step |
| **Chat** | **Coach → Client** message | Push + In‑app | The **client** (recipient) | The 1:1 chat thread |
|  | **Client → Coach** message | Push + In‑app | The **coach** (recipient) | The 1:1 chat thread |
| **Community** | Coach **invites** a member | Push | The **invited member** | Community page / invites tab |
|  | Coach **removes** a member | Push | The **removed member** | App home (community access removed) |
|  | **Like** on a post | Push | **Post author** | The specific post |
|  | **Comment** on a post | Push | **Post author** | The specific post (scroll to comment) |
|  | **New post** by coach/member | Push + In‑app | **All community members** + coach | Community feed / new post anchor |

**Common acceptance:**  
- Title/body are accurate and actionable.  
- Deep link opens the correct screen.  
- Unread badge increments; reading the item decrements.  
- No duplicate notifications for the same event/user.

---

## B  Validation Rules (All Notifications)

1) **Payload** contains: event type, actor, recipient(s), entity (course/module/chat/post), title, body, deep link, dedup key, timestamp.  
2) **Deduplication**: repeated events within 10 s do **not** create multiple entries.  
3) **Read state**: opening via push **or** in‑app marks the corresponding item as **read** in both channels.  
4) **Badge counts**:  
   - In‑app bell shows cumulative unread count.  
   - App icon badge (mobile) increases for push‑eligible unread items.  
5) **Permissions & fallback**: if push permission is **Denied**, only in‑app appears; no errors.  
6) **Localization** (if enabled): strings render in the device/user language.  
7) **Accessibility**: screen reader reads title, sender, and action; focus lands on content after deep link.  
8) **Error handling**: if deep link target no longer exists, route to a safe fallback (e.g., dashboard) with a toast “Content not available”.

---

## C  Step‑by‑Step Tests

> Run each test in **Foreground**, **Background**, and **Terminated** app states for the **recipient**. Where “tap push” is not possible in Foreground (OS‑suppressed), skip the banner tap step and only verify send & in‑app.

### 1) Course Completion → Push + In‑App (Recipient = Completer)

**Setup:** Client B is enrolled; last module ready to complete.  
**Steps (repeat for module completion as 1b):**  
1. As **Client B**, complete the **course**.  
2. Observe **in‑app**: notification appears within 2 s in the inbox/banner.  
3. On recipient device, observe **push** delivery (Background/Terminated).  
4. **Tap** the notification (push or in‑app).  
5. Verify deep link → **Course completion** screen, badge decremented, item marked read.  
6. Confirm **no duplicate** entries for the same completion event.

**Pass criteria:** In‑app + push sent; correct recipient; deep link valid; read/badge consistent; no duplicates.

---

### 1b) Module Completion → Push + In‑App (Recipient = Completer)

**Steps:** Same as 1), but complete a **module**.  
**Pass criteria:** As above; deep link targets the **module summary**.

---

### 2) Chat: Coach → Client (Push + In‑App to Client)

**Setup:** Existing 1:1 thread Coach A ↔ Client B.  
**Steps:**  
1. As **Coach A**, send “Test message #C2” to **Client B**.  
2. On **Client B**’s device: verify **in‑app** arrival (foreground) and **push** banner (background/terminated).  
3. **Tap** notification → opens the **same chat thread** and scrolls to the new message.  
4. Verify chat message is marked **read**; in‑app/push item no longer unread.

**Pass criteria:** Timely delivery to client; correct thread deep link; accurate sender/title.

---

### 3) Chat: Client → Coach (Push + In‑App to Coach)

**Steps:**  
1. As **Client B**, send “Test message #C3” to **Coach A**.  
2. On **Coach A**’s device: verify in‑app/push as in Test 2.  
3. **Tap** notification → correct chat thread; read state synced.

**Pass criteria:** As in Test 2, roles reversed.

---

### 4) Community: Coach **Invites** Member (Push to Member)

**Setup:** Community exists; **Member C** not yet joined.  
**Steps:**  
1. As **Coach A**, send invite to **Member C**.  
2. On **Member C**’s device: verify **push** arrival (title references community).  
3. **Tap** push → deep link to Community **invites** (or community landing with invite prompt).  
4. Accept invite; ensure no stale unread items remain.

**Pass criteria:** Push only (no in‑app requirement); correct recipient; correct deep link.

---

### 5) Community: Coach **Removes** Member (Push to Member)

**Setup:** **Member C** is currently in the community.  
**Steps:**  
1. As **Coach A**, remove **Member C**.  
2. On **Member C**’s device: receive **push** describing removal.  
3. **Tap** push → opens safe fallback (e.g., Dashboard) with toast “Access removed”.  
4. Confirm community access is gone.

**Pass criteria:** Push delivered; link safe; permissions updated.

---

### 6) Community: **Like** on a Post (Push to Author)

**Setup:** **Member C** authored a post visible to Coach A and Member D.  
**Steps:**  
1. As **Coach A**, **like** Member C’s post.  
2. On **Member C**’s device: receive **push** “Coach A liked your post”.  
3. **Tap** push → opens the **post**; like visible.  
4. **Negative check (if product suppresses self‑notify):** Author liking own post should **not** send a push.

**Pass criteria:** Push to author only; correct post deep link; self‑action behavior matches product rule.

---

### 7) Community: **Comment** on a Post (Push to Author)

**Steps:**  
1. As **Member D**, comment “Great work!” on **Member C**’s post.  
2. On **Member C**’s device: receive **push** “Member D commented on your post”.  
3. **Tap** push → opens post scrolled to the **new comment**.  
4. **Burst check:** Two comments within 5 s should **not** generate duplicate pushes; either a single push or batched per product rule.

**Pass criteria:** Push to author; correct anchor; dedup/batching respected (per product rule).

---

### 8) Community: **New Post** → Broadcast (Push + In‑App to All)

**Setup:** Members: Coach A, Member C, Member D.  
**Steps:**  
1. As **Member C**, create a **new post**.  
2. On **Coach A** and **Member D** devices/sessions:  
   - **In‑app** notification appears (foreground/web).  
   - **Push** banner arrives (background/terminated).  
3. **Tap** notification → community feed **anchored at the new post**.  
4. **Badge** counts increment per recipient and clear after viewing.

**Pass criteria:** Broadcast to **all members + coach** via both channels; deep link correct; counts consistent.

---

### 9) Read‑State & Badge Consistency (Cross‑Channel)

**Steps:**  
1. Trigger any one notification (e.g., chat).  
2. Open the **push**; verify the **in‑app** item becomes **read** and badge decrements.  
3. Trigger another; open from **in‑app** instead; verify home‑screen/app icon badge decrements accordingly.  
4. Refresh/relaunch app; ensure state persists.

**Pass criteria:** Single source of truth for read/unread across channels.

---

### 10) Fallbacks, Permissions, and Edge Cases

**Steps:**  
1. **Permissions denied** on recipient device → trigger any event; verify **in‑app** only, no errors.  
2. **Connectivity loss** at recipient → trigger event; after reconnect, verify **in‑app** backfills and **push** arrives if still eligible.  
3. **Terminated app** → tap push; verify cold start to correct deep link in ≤ 1 s.  
4. **Outdated deep link** (delete post before opening) → safe fallback + toast.  
5. **Duplicate prevention**: trigger two identical likes in < 3 s (unlike+like); confirm one push or product‑approved batching.

**Pass criteria:** Graceful behavior; no crashes; user always lands somewhere safe and informed.

---

## D  Expected Outcome
- Correct **recipients** receive the intended **channel(s)** for each event.  
- **Timing** meets KPIs; no excessive delays.  
- **Deep links** open the relevant screens; errors fall back safely with messaging.  
- **Unread badges** and **read states** sync across push and in‑app.  
- No **duplicates**; no **self‑notifications** where not intended (per product rule).  
- Behavior consistent across **Foreground/Background/Terminated** states and across **iOS/Android/Web**.

---

## Test Checklist

| Test | Pass |
|---|---|
| Push permissions allowed on test devices | ☐ |
| Device tokens registered (Coach A, Client B) | ☐ |
| In‑app inbox/bell visible with unread badge | ☐ |
| **Course completion** → push + in‑app to completer | ☐ |
| **Module completion** → push + in‑app to completer | ☐ |
| **Coach → Client chat** → push + in‑app to client | ☐ |
| **Client → Coach chat** → push + in‑app to coach | ☐ |
| **Coach invites member** → push to invited member | ☐ |
| **Coach removes member** → push to removed member | ☐ |
| **Like on post** → push to author (self‑notify rule verified) | ☐ |
| **Comment on post** → push to author | ☐ |
| **New post** → push + in‑app to all members + coach | ☐ |
| Foreground behavior correct (in‑app visible; push may be OS‑suppressed) | ☐ |
| Background/terminated behavior correct (push visible; in‑app queued) | ☐ |
| Tapping notification deep‑links to correct screen in ≤ 1 s | ☐ |
| Read state sync between push and in‑app | ☐ |
| Badge increment/decrement accurate | ☐ |
| Dedup/batching prevents duplicate pushes (per product rule) | ☐ |
| Fallback route + toast for missing content | ☐ |
| Localization strings correct (if applicable) | ☐ |
| Accessibility: screen reader reads title/sender/action | ☐ |

---

## E  Logging & Evidence (for each test)
- **Screenshots / screen recordings**: show the push banner, in‑app entry, and deep‑linked screen.  
- **Timestamps**: record event time and arrival times (for KPI).  
- **Server / QA logs**: capture payloads (event type, recipient(s), dedup key, deep link).  
- **Notes**: state (Foreground/Background/Terminated), device/OS, app build, and any anomalies.

---

## F  Post‑Test Cleanup
- Clear notifications and reset unread counts.  
- Revoke/restore community membership as needed.  
- Re‑enable push permissions if changed.  
- Log defects with: **Area → Scenario → Steps → Actual vs Expected → Evidence → Build/Device**.

---

### Quick Run Order (Step‑by‑Step)
1) Complete **module** (Client B) → verify push+in‑app.  
2) Complete **course** (Client B) → verify push+in‑app.  
3) **Coach A → Client B** chat message → verify.  
4) **Client B → Coach A** chat message → verify.  
5) Coach **invites** **Member C** → verify push; then **removes** → verify push & fallback.  
6) **Like** then **comment** on **Member C**’s post (by Coach A / Member D) → verify pushes to author and dedup.  
7) **Member C** creates **new post** → verify broadcast push+in‑app to Coach A & Member D.  
8) Verify **read state + badge** sync across channels.  
9) Run **edge cases** (permissions denied, offline, terminated app, stale deep link).
