# Client Invitation and Onboarding Scenario

## Purpose
Describes the flow and known issues in the SelfFull platform when a coach invites a client to a course, including case sensitivity in email handling, onboarding steps, and navigation experience.

---

## Scenario: Client Invitation and Onboarding Flow

**Given:**  
- The coach is logged into the SelfFull app or web platform.

**When:**  
1. The coach invites a new user to join a course.  
2. The coach selects a course to which the user should be added.  
3. The coach enters the client’s email, but mistakenly includes an uppercase letter (e.g., `John.Doe@example.com`).  
4. The client receives the invitation email successfully.  
5. The client attempts to sign up using the same email, but in lowercase (e.g., `john.doe@example.com`).  
6. The system does not recognize the email due to case sensitivity.  
7. The client is required to retype the email exactly as entered by the coach (with the uppercase letter) to proceed.  
8. After entering the matching email, the client sees the onboarding message and begins the onboarding process.  
9. The client completes the onboarding flow.  
10. The client sets up their profile, including profile picture and phone number.  
11. The client navigates to the main page (courses dashboard).

**Then:**  
- The client can successfully access their courses after completing onboarding.  
- The following issue was identified:
  - **Email matching is case-sensitive**, which causes friction during signup if the coach entered the email with capital letters.

---