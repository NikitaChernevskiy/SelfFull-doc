SelfFull universal Mobile App Standards: Coach Program (Course / Chapter / Module) Lifecycle Requirements  
v1.0 – 31 July 2025  

---

## Why We Need This Document  
The **Course Builder** is the revenue engine for SelfFull. Clear, measurable rules for creating, editing, and deleting courses—plus their nested chapters and modules—ensure that every coach can publish high‑quality learning paths without friction, while protecting clients from broken links or orphaned content. These standards align Product, Design, Engineering, and QA under one contract, speeding release cycles and providing auditors with a complete trace of content lifecycle governance.

---

## Course‑Level Requirements (1 – 15)

1. **Create Course CTA**  
   “+ Add Course” button visible on Coach Dashboard Courses card; enabled only when coach has ≤ 20 active courses.  

2. **Mandatory fields**  
   Course Name (max 60 chars), Hero Image (16:9, min 1280 × 720, ≤ 2 MB), Short Description (≤ 160 chars), Long Description (Markdown, 200–4 000 chars).  

4. **Draft state**  
   New course starts as **Draft** and is invisible to clients until Published; dashboard label “Draft” with grey badge.  

5. **Publish guard**  
   Publish button disabled until ≥ 1 chapter and ≥ 1 module exist and hero image uploaded.  

6. **Autosave**  
   Draft autosaves after any field blur or every 10 s of idle typing; failure shows red toast ≤ 100 chars.  

8. **Delete rule**  
   Course deletion allowed only when no active clients enrolled; else “Archive” soft‑delete for historical access.  

9. **Confirmation modal**  
   Deleting shows 2‑step confirmation with course name in input field; irreversible copy ≤ 120 chars.  

10. **Thumbnail preview**  
    Hero image renders responsive preview; alt text auto‑filled with Course Name.  

12. **Accessibility**  
    All form inputs have visible labels and ARIA descriptions; keyboard navigation order logical.  

13. **Latency**  
    Create, update, publish endpoints respond < 1 s (P95) on 4G.  

14. **Error copy**  
    Server errors show toast with generic copy + Request ID; no stack traces.  

15. **Undo window**  
    Immediately after delete, snackbar with “Undo” appears for 5 s; restores course if clicked.  

---

## Chapter‑Level Requirements (16 – 30)

16. **Add Chapter**  
    “+ Add Chapter” button appears at bottom of chapter list; new chapter labeled “Untitled Chapter” until renamed.  

17. **Chapter fields**  
    Chapter Title (max 80 chars) required; optional Summary (≤ 300 chars).  

18. **Drag‑reorder**  
    Chapters draggable via 8‑dot handle; order persists on blur.  

19. **Collapse / Expand**  
    Clicking chapter header toggles module list; state remembered per coach session.  

20. **Unique numbering**  
    Chapters auto‑number (1, 2, 3…) based on position; renumbers after reorder.  

21. **Delete guard**  
    Chapter cannot be deleted while containing modules; coach must move/delete modules first.  

23. **Accessibility**  
    Drag‑reorder supports keyboard: Move Up / Down buttons appear in focus mode.  

24. **Latency**  
    Adding or renaming chapter round‑trip < 500 ms.  

25. **Undo**  
    Deleting chapter shows 5 s undo snackbar; restores with modules intact.  

26. **Empty state**  
    If no chapters, display illustration + text “Add your first chapter to begin”.  

27. **Error copy**  
    Attempt to delete last remaining chapter while modules exist shows modal “Please move or delete modules first”.  

28. **Bulk expand/collapse**  
    “Expand All / Collapse All” buttons provided when > 3 chapters.  

29. **Autosave**  
    Title edits autosave on blur; unsaved indicator ● disappears after success.  

30. **WCAG**  
    Chapter header color contrast ≥ 4.5 : 1 in light & dark themes.  

---

## Module‑Level Requirements (31 – 55)

31. **Add Module**  
    “+ Add Module” inside selected chapter inserts module at end; default title “Untitled Module”.  

32. **Standalone Module**  
    “Add Standalone Module” button adds module outside any chapter; appears at bottom of list.  

33. **Module fields**  
    Module Title (≤ 80 chars) **required**; Description (Markdown, 50–2 000 chars) optional; Quiz block optional.  

34. **Quiz builder**  
    Each quiz supports 1–10 questions; question text ≤ 200 chars; up to 5 answer options; one correct flag.  

35. **Icons**  
    Edit ✏️ and Delete 🗑️ icons appear on module hover; 24 dp, hit target 48 dp.  

36. **Delete confirmation**  
    Deleting module prompts “Are you sure?” modal with title; module cannot be undone once snackbar expires (5 s).  

37. **Drag‑reorder**  
    Modules reorder within chapter via drag; cannot drag across chapters—must use Move To menu.  

38. **Move To…**  
    Context menu lists other chapters; selecting moves module, renumbers automatically.  

39. **Description preview**  
    Markdown description renders toggle Preview / Edit; preview sanitizes HTML.  

40. **Quiz placeholder**  
    Empty quiz area shows “Add your first question” button.  

41. **Quiz validation**  
    Cannot publish course if any module has quiz with < 1 question or question missing correct answer.  

42. **Autosave**  
    Description and quiz edits autosave every 10 s or on blur.  

43. **File uploads**  
    Description supports embedded images: JPEG/PNG/WebP ≤ 1 MB each, max 10 per module.  

44. **Accessibility**  
    Module edit panel reachable via Tab sequence; quiz radio buttons exposed to screen readers.  

45. **Latency**  
    Add / delete / update module responses < 700 ms (P95).  

46. **Error handling**  
    If save fails, red toast + inline “Retry” button; unsaved indicator remains.  

48. **Duplicate**  
    “Duplicate Module” option copies title, description, quiz; appends “(copy)” to title; duplicate lands below original.  

49. **Unsaved warning**  
    Navigating away with unsaved module changes prompts modal “Discard or Save draft?”.  

50. **WCAG**  
    Quiz option contrast ≥ 4.5 : 1; focus ring visible.  

51. **Progress indicators**  
    Saving shows inline spinner next to title; spinner disappears on success.  

52. **Markdown help**  
    “Show Sample” link opens cheat‑sheet modal (< 2 KB).  

53. **Search filter**  
    Search box filters modules by title in real time; highlights matches.  

55. **Undo delete**  
    Module deletion snackbar with Undo (5 s); restores at original position.  

---

## Access Control & Client Sync Requirements (56 – 65)

56. **Enrollment check**  
    Publishing new modules triggers real‑time push to enrolled clients; fallback polling every 30 min.  

57. **Permission model**  
    Only Coach role may create/edit/delete; Admin can force‑publish.  

61. **Client migration**  
    Deleting a module that clients completed keeps progress stats but removes access; dashboard shows “Archived”.  

62. **Rate limit**  
    API limits to 30 writes/min per user to prevent spam.  

63. **GDPR**  
    Course content must not contain PII; server strips accidental email addresses in Markdown (regex).  

64. **Localization**  
    Course builder UI strings from i18n files; content fields stored UTF‑8 without modification.  