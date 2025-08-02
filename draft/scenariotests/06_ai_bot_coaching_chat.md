**Date:** 2025‑08‑02  
**File:** 06_ai_bot_coaching_chat.md  
**Purpose:** Confirm that coaches and clients can converse with the **AIAI Assistant** by text and (on mobile) speech‑to‑text, that responses render correctly, and that ancillary actions (audio playback, copy, refresh) work as intended.

---

# Test Scenario – AI Coaching Chat

## 0  Pre‑conditions
- User is signed‑in  
- Stable internet connection (≥ 2 Mbps)  

---

## A  Open Chat

1. **Tap “Chat With AI”** in sidebar  
   - URL path `/chatAIScreen` loads without 404  
   - Header text “Chat with AI✨” visible  
   - Refresh icon (⟳) top‑right present and enabled  

2. **Initial assistant message**  
   - Bubble text “Hello! How can I assist you today?” appears in ≤ 2 s  
   - Speaker button (🔊) inside bubble visible  
   - Sub‑label “Generated with AI” and **Copy response** link shown  

---

## B  Send Text Message (Desktop & Mobile)

| Checkpoint | Validation Rules | Expected Result |
|------------|------------------|-----------------|
| **Message input field** | Placeholder “Write a message …” | Field gains focus on tap / click |
| Characters | Min 1, Max 2 048 | Counter turns red if limit exceeded |
| Allowed charset | UTF‑8; emojis; punctuation; no script tags `<script>` | Unsafe chars escaped |
| Line breaks | Shift + Enter inserts newline | Message retains formatting in bubble |
| **Send button** | Solid arrow icon | Disabled when input empty; becomes active on valid text |
| Submit via Enter | Enter key without Shift sends | Same behaviour as button |
| Loading state | Spinner replaces arrow ≤ 500 ms | Spinner disappears after response |

3. **Assistant response**  
   - Appears in new bubble beneath user message  
   - Average latency ≤ 5 s  
   - Long responses auto‑scroll chat to latest bubble  

4. **Copy response link**  
   - Copies exact text to clipboard (paste into Notes to verify)  
   - Toast *“Copied”* displayed  

---

## C  Speech‑to‑Text (Mobile Only)

| Step | Detail | Expected |
|------|--------|----------|
| **Microphone icon** | Located inside message field, right side | Visible when keyboard closed |
| Tap icon | OS microphone permission prompt if first time | Choose **Allow** |
| Recording | Level meter animates while speaking | Transcribed text appears live in input |
| Stop recording | Auto stops on 3 s silence **or** tap icon again | Icon reverts; transcription ready for edit |
| Validation | Same min / max / charset rules as text | Errors shown inline |
| Send | Tap arrow | Message bubble shows spoken text |

---

## D  Text‑to‑Speech Playback (All Platforms)

1. **Tap speaker button (🔊)** in any assistant bubble  
   - Audio plays via system output  
   - Second tap pauses playback  
   - Navigating away stops audio  

2. **Volume / route change**  
   - Adjust device volume → playback volume changes  
   - Connect Bluetooth headset → audio routes correctly  

---

## E  Refresh Conversation

1. **Tap refresh icon (⟳)**  
   - Tap **refresh icon (⟳)** → chat history empties; initial assistant greeting reappears  

---

## F  Error Handling

| Scenario | Trigger | Expected UI |
|----------|---------|-------------|
| Backend timeout | Simulate by disabling internet, send message | Error toast *“Unable to reach server”*; retry icon in bubble |
| Invalid token | Force logout while tab open | Redirect to Sign In screen |
| Character overflow | > 2 048 chars pasted | Inline error “Character limit exceeded” |

---

## 1  Expected Outcome
- Users can exchange unlimited messages with AI within validation limits  
- Speech‑to‑text reliably captures input on mobile when permission granted  
- Audio playback and copy actions work on every assistant response  
- Refresh clears history without residual data  

---

**End of file**