## AI Note Feature Test Cases

| Case ID | Case Name                                 | Expected Result                                              | Actual Result                          | Success (Yes/No) |
|---------|-------------------------------------------|-------------------------------------------------------------|----------------------------------------|------------------|
| TC-001  | Auto-add Note Name Format                 | New note name auto-filled with MMHHDDMMYY-RND format         | No auto-add text                       | No               |
| TC-002  | Note Name Character Limit                 | Note name limited to 25 characters                           | No limit                               | No               |
| TC-003  | Filter Button Functionality               | Filter button opens filter options                           | Nothing happens                        | No               |
| TC-004  | Notes List Order                          | Notes list ordered by newest created                         | Not ordered by newest                  | No               |
| TC-005  | Generate Sample Transcript Navigation     | Stays on edit transcript screen after generating sample      | Navigates to previous screen           | No               |
| TC-006  | Generate Multiple Sample Transcripts      | Can generate new sample transcript after first try           | Can't generate after first try          | No               |
| TC-007  | Specify Topic for Generated Content       | Can specify topic for Transcription, Note, and Instruction   | Can't specify topic                    | No               |
| TC-008  | Apply AI Bot Instructions                | Clicking paper-plane icon applies instructions               | Does nothing                           | No               |
| TC-009  | Bot Response to Multiple Generations      | Bot provides answers for all generated items                 | Bot struggles to provide answer         | No               |
| TC-010  | Share Button with No Clients              | Shows error or message when no clients                       | Spins forever                          | No               |
| TC-011  | AI Response Markdown Formatting           | AI response formatted as markdown                            | Double stars (**) appear mid-text       | No               |
| TC-012  | Previous Button on Edit Instructions      | Previous button navigates to previous step                   | Does nothing when clicked               | No               |
| TC-013  | Scroll AI Note Details Tab (Phone)        | Can scroll AI Note Details tab on phone                      | Can't scroll                           | No               |