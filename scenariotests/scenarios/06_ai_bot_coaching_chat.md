SelfFull universal Mobile App Standards: AI‑Powered Coaching Chat Requirements  
v1.0 – 31 July 2025  

---

## Purpose  
This document defines the **functional, UX, accessibility, performance, and compliance standards** for the AI‑powered chat used by both coaches and clients. By codifying how conversations are started, routed, moderated, and stored, we guarantee a consistent, safe, and high‑value coaching experience—while giving Product, Design, Engineering, and QA a single measurable target.

---

## Interface & Interaction Requirements (1 – 15)

1. **Entry points** — “Chat with AI” icon in left rail (coach) and bottom nav (client); deep link `/chatAiScreen`.  
2. **Responsive layout** — One‑column chat thread, auto‑scroll to latest; no horizontal scroll on 320 × 568 px.  
3. **Input box** — Multi‑line, grows to 6 rows max, returns to single line after send.  
4. **Send button** — Disabled until text ≥ 1 visible character or voice recording ends.  
5. **Voice dictation** — Mic icon toggles speech‑to‑text; auto‑inserts text into input.  
6. **System message banner** — Grey italics for onboarding summary shown only once per thread.  
8. **Role colour** — AI bubbles purple 500, user bubbles surface 100; contrast ≥ 4.5 : 1.  
9. **Copy response** — “Copy” link bottom‑right of AI bubble; toast “Copied”.  
10. **Voice playback** — Play button on AI bubbles, text‑to‑speech with stop control; announces via screen reader.  
11. **Link previews** — URLs in AI responses render inline card with favicon, title, and domain.  
12. **Scrollback** — Infinite scroll up; fetches 20 older messages per page; spinner appears top.  
13. **Typing indicator** — Three‑dot animated ellipsis while AI is generating.  
14. **Error state** — If generation fails, red retry icon in bubble; tap to regenerate.  

---

## Prompt & Response Requirements (16 – 30)

16. **System prompt** — Inject “You are SelfFull AI Coach…” per role; versioned and stored with conversation.  
17. **Context window** — Last 20 messages + course metadata + user profile bio.  
18. **Token budget** — Max 4 000 tokens per request; truncate oldest messages first.  
19. **Latency target** — First token ≤ 3 s (P95), completion ≤ 12 s for 400‑token reply.  
20. **Streaming** — AI response streams 20 tokens / chunk; bubbles grow in real‑time.  
21. **Stop generation** — User may tap stop; partial response remains editable by AI.  
22. **Follow‑up actions** — Detect “/quiz”, “/summary”, “/resources” commands; render quick‑action chips.  
23. **Markdown support** — AI can return Markdown; renderer supports headings, lists, bold, italics, code.  
24. **Image links** — If AI returns `![alt](url)`, thumbnail shown; tap opens full screen viewer.  
25. **Hallucination guard** — Post‑generation filter scores response with credibility model; score < 0.4 triggers yellow banner “AI may be inaccurate”.  
26. **Safety filter** — Messages pass OpenAI moderation endpoint; flagged content blocked, user sees “Message violates policy”.  
27. **Language detection** — AI replies in user locale when locale confidence ≥ 0.8.  
28. **Custom instructions** — Coach can save “AI Bot Instructions” per course; appended to system prompt.  
29. **Retry policy** — On 5xx from LLM provider, retry up to 2× with exponential back‑off (max 8 s).  

---

## Session & Persistence Requirements (31 – 45)

31. **Thread ID** — UUIDv4; per user per course; stored in `threads` table.  
32. **Auto‑save** — Every sent/received message persists within 500 ms.  
33. **Local draft** — Unsent text cached locally; restored on re‑open.  
34. **Sync** — Offline messages queued.  
35. **History purge** — Messages older than 18 months auto‑archived; coach can export JSON.  
36. **Soft delete** — Deleting message hides in UI; server keeps for 30 days for moderation.  
37. **Attachment storage** — Voice notes stored in S3 with pre‑signed URLs expiring 24 h.  
38. **Data residency** — EU users’ chat data stored only in EU regions.  
39. **End‑to‑end encryption** — Message payload encrypted at REST (AES‑256) and TLS 1.3 in transit.  
40. **Recovery** — If last read ≠ last message, app shows unread badge with count.  
41. **Push** — New AI or coach reply triggers silent push; app decides whether to show notification.  
42. **Concurrency** — Client uses ETags to prevent overwrite; server returns 409 on stale write.  
43. **GDPR delete** — On account deletion, chat history purged within 30 days.  
44. **Audit log** — Each message insert/update logs userId, ipHash, moderationResult.  
45. **Rate limits** — Max 30 user messages / minute and 300 / day; UI blocks further sends.  

---

## Voice & Media Requirements (46 – 55)

46. **TTS voices** — Azure Neural Voice `en-US-JennyMultilingualNeural` default; fallback to OS TTS.  
47. **Playback latency** — Audio ready ≤ 1.5 s after tap (P95).  
48. **Controls** — Play/Pause, scrubbing disabled; Stop resets progress.  
49. **Captions** — Auto‑generated captions displayed above progress bar for accessibility.  
50. **Audio cache** — TTS MP3 cached in app sandbox for 1 h; size limit 20 MB.  
51. **Recording (coach only)** — Hold‑to‑record voice; max 120 s; uploaded as WebM/Opus ≤ 1 MB.  
52. **Noise suppression** — WebRTC `noiseSuppression=true` for recordings.  
53. **Transcription** — Server transcribes coach voice to text and stores alongside audio.  
54. **Moderation** — Voice transcriptions pass same content safety filter as text.   

---

## Content Safety & Compliance Requirements (56 – 65)

56. **PII scrubber** — AI responses run through PII‑redaction model; mask phone, email, address unless user shared explicitly.  
58. **Copyright check** — Large chunks (> 400 chars) scanned for similarity; score > 0.9 flags coach review.  
59. **Harassment filter** — Toxicity score > 0.8 triggers immediate block + user warning.  
60. **COE policy** — All moderation results logged for 2 years per Code of Ethics.  
61. **Child safety** — Mentions of self‑harm route to crisis‑response template and surface coach escalation UI.  
62. **Export / e‑Discovery** — Admins can export chat in PDF/JSON for legal holds; watermark “Confidential”.  
63. **Audit review queue** — Moderation flags create Jira tickets for Trust & Safety.  
64. **Transparency** — AI‑generated messages display “AI‑generated” badge with tooltip showing model name and last update date.  
65. **Accessibility compliance** — Chat meets WCAG 2.2 AA for color, focus, and captioning.  

---

## Performance & Reliability Requirements (66 – 75)

66. **App footprint** — Chat module adds < 3 MB to app bundle.  
67. **Memory usage** — Peak memory < 150 MB on iPhone SE 2nd gen during 100‑message scroll.  
68. **Frame rate** — Scrolling ≥ 55 FPS on reference devices with jank < 1 %.  
69. **Crash‑free** — < 0.3 % crash rate in chat module (30‑day rolling).  
70. **Downtime fallback** — If LLM provider down, show banner “AI temporarily unavailable” and disable send.  
71. **Circuit breaker** — Three consecutive 5xx responses tripping opens breaker 2 min; retries after.  
72. **Retry queue** — Offline send queue persists across app restarts.  
73. **Load test** — Sustains 1 000 concurrent chats / node with p95 latency < 800 ms.  
74. **Error logging** — Sentry captures unhandled exceptions with breadcrumbs of last 5 actions.  
75. **Observability** — Dashboard displays token usage, latency, error rate, moderation flags in real‑time.  