# App Settings & Options Scenario

## Purpose
Describes the user experience when accessing and interacting with the Settings menu in the SelfFull app, including available options and expected behaviors. Notes any known issues based on recent testing.

---

## Scenario: Accessing and Using App Settings

**Given:**  
- The user has installed and logged into the SelfFull app.

**When:**  
- The user opens the Settings menu.

**Then:**  
- The user sees the following options:
  1. Update social bio
  2. Change password
  3. Edit contact info
  4. Tutorial page
  5. Submit a bug
  6. Submit a feature request
  7. Review data privacy & terms
  8. Explore our website
  9. Delete your profile
  10. Log out

---

### Interactions & Expected Results

1. **Update social bio**  
   - User can update their social bio/profile.  
   - *Works as expected.*

2. **Change password**  
   - User is able to change their password.  
   - *Known issue: "Change password" label is not clickable; navigation arrows are inconsistent.*

3. **Edit contact info**  
   - User is able to edit their contact information.  
   - *Known issue: "Edit contact info" label is not clickable; edit button is off-center and not needed; cannot edit fields immediately.*

4. **Tutorial page**  
   - User can view a tutorial for app features.  
   - *Known issues: No exit button; must scroll entire page to exit; next/previous buttons are inconsistent or missing.*

5. **Submit a bug**  
   - User can submit a bug report, including screenshots or videos.  
   - *Known issue: Only one screenshot or video can be uploaded per bug report.*

6. **Submit a feature request**  
   - User can submit a feature request, including screenshots.  
   - *Known issue: Only one screenshot can be uploaded per feature request.*

7. **Review data privacy & terms**  
   - User can review privacy policy and terms of service.  
   - *Works as expected.*

8. **Explore our website**  
   - User can visit the SelfFull website via provided link.  
   - *Works as expected.*

9. **Delete your profile**  
   - User can delete their profile and associated data.  
   - *Works as expected.*

10. **Log out**  
    - User can log out of the app.  
    - *Works as expected.*

---

## End