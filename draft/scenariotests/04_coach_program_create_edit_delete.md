**Date:** 2025‑08‑02  
**File:** 04_coach_program_create_edit_delete.md  
**Purpose:** Validate that a coach can create, edit, and delete **Courses → Chapters → Modules (with quizzes)**, manage access, and preview the final program.

---

# Test Scenario – Program (Course) Authoring Flow

## 0  Pre‑conditions
- Coach is signed‑in and on the **Coach Dashboard**  
- No blocking pop‑ups; stable internet connection  

---

## A  Course List (Coach Dashboard)

1. **Tap “Add Course”**  
   - **Course Name** input  
     - Required  
     - 3–100 characters  
     - Letters, numbers, spaces, punctuation `.,:;!?‑()` only  
   - **Course Thumbnail** (optional)  
     - Accepts .jpg / .png  
     - Max 10 MB; min 600 × 400 px  
   - **Create / Save** button  
     - Disabled until required fields valid  
     - After tap, new course appears in list with trash‑can and edit icons  

2. **Edit Course** (pencil icon)  
   - Opens same form pre‑filled; changes persist after save  

3. **Delete Course** (trash icon)  
   - Confirmation dialog text: *“This will delete all chapters and modules.”*  
   - “Delete” button disabled until checkbox *“I understand”* checked  
   - After delete, course is removed from list  

---

## B  Inside a Course

### Add Chapter

1. **Tap “Add Chapter”**  
   - **Title** input  
     - Required  
     - 3–120 characters  
     - Letters, numbers, spaces, punctuation `.,:;!?‑()` only  
   - **Add** button → chapter row appears with:  
     - Title text  
     - Edit (pencil) icon  
     - Delete (trash) icon  
     - Collapse/expand arrow  

### Edit / Delete / Re‑order Chapters

2. **Edit** – pencil opens dialog identical to *Add Chapter*; changes save  
3. **Delete** – trash prompts irreversible warning, removes chapter and its modules  
4. **Re‑order** – drag handle (or up/down arrow) moves chapter; order saves on reload  

---

## C  Managing Modules within a Chapter

### Add Module

1. **Open a chapter → Tap “+ Add Module”**  
   - **Title** *(required)*  
     - 3–120 characters; letters, numbers, spaces, punctuation  
   - **Description** *(required)*  
     - Rich‑text area opens after “Add Description”  
     - 10–2 000 characters; supports bold/italic lists  
   - **Banner Image** *(optional)*  
     - .jpg / .png, < 10 MB, landscape 16:9 recommended  
   - **Upload Video** *(optional – choose one)*  
     - **Video file**: .mp4 / .mov, < 500 MB, duration ≤ 30 min  
     - **YouTube URL**: must match `https://www.youtube.com/watch?v=*`  
   - **Upload Resources** *(optional multiple)*  
     - .pdf / docx / pptx / zip; each < 100 MB  
   - **Set Up Quiz** button opens quiz builder (see section D)  
   - **Add New Module** button saves; module row appears under chapter with:  
     - Edit, delete, drag icons  

### Edit / Delete / Re‑order Modules

2. **Edit** – pencil re‑opens full module form; changes save  
3. **Delete** – trash asks *“Delete module permanently?”* confirmation  
4. **Re‑order** – drag handle changes order; persists on reload  

---

## D  Quiz Builder (inside a Module)

1. **Tap “Set Up Quiz”** → quiz panel opens  
2. **Tap “+ Add Questions”** → modal form:  
   - **Question Text** *(required)*  
     - 5–255 characters  
   - **Option Text** *(required, per option)*  
     - 1–120 characters  
     - Tap **Add** to append; minimum 2 options, maximum 6  
   - **Correct Answer** dropdown *(required once ≥ 2 options added)*  
   - **Add** button saves question; list increments  
3. Repeat step 2 to add additional questions (unbounded)  
4. **Back** closes modal; quiz summary shows question count  
5. Quiz auto‑saves with module on “Add New Module” / “Save Changes”  

---

## E  Access Control & Metadata

1. **Access Control → “+ Add User”**  
   - Search bar min 2 characters  
   - List returns matching users; tap to add  
   - Added user chip shows avatar, email, remove (×) icon  
2. **Progress** toggle  
   - ON shows completion % for each assigned user  
3. **Unlock Timing** dropdown  
   - Options: **Immediately**, **1 day after enrolment**, **Scheduled date**  
   - Selecting **Scheduled date** opens date‑picker (yyyy‑mm‑dd validation)  
4. **Preview Course** button  
   - Loads read‑only learner view in new tab; close returns to builder  

---

## F  Deleting Assets

| Asset | Action | Expected Confirmation |
|-------|--------|-----------------------|
| Course | Trash icon in course list | *“Are you sure?”* + **Delete** |
| Chapter | Trash icon in chapter row | *“Are you sure?”* + **Delete** |
| Module | Trash icon in module row | *“Are you sure?”* + **Delete** |
| Quiz Question | Trash icon next to question in quiz list | *“Are you sure?”* + **Remove** |

After confirmation, asset disappears from UI and is not present after page refresh.

---

## G  Expected Outcome
- New course with chapters, modules, resources, quizzes is created without errors  
- Edited titles, descriptions, and media persist after reload  
- Deleted items are permanently removed and cannot be reopened  
- Access control limits course visibility to assigned users  
- Preview accurately reflects latest saved state  

---

**End of file**