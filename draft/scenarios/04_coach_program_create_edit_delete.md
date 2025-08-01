# Coach Program: Create, Edit, and Delete Scenario

## Purpose
Describes the user experience for coaches creating, editing, and deleting courses/programs in the SelfFull app, including expected behaviors and known issues from recent testing.

---

## Scenario: Coach Course Management

**Given:**  
- The coach is logged into the SelfFull app or web platform.

**When:**  
1. The coach navigates to the dashboard or course management section.
2. The coach creates a new course/program.
3. The coach adds chapters and modules to the course.
4. The coach adds descriptions to modules.
5. The coach previews modules and chapters.
6. The coach edits course content as needed.
7. The coach deletes a course/program.

**Then:**  
- The coach can manage courses, chapters, and modules.
- The following issues may be encountered:
  - Chapter slider stacks onto module sliders (should not stack).
  - Preview menu is not sized correctly while reading a module.
  - Description does not auto-open when navigating to a module.
  - Course creation screen layout: too much space taken by SelfFull logo (should use most of the screen for editing).
- All other course management actions work as expected.

---

## End of