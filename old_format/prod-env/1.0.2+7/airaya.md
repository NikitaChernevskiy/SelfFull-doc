## AI Testing – Web App on PC

| Case ID | Case Name                              | Expected Result                                                      | Actual Result                                  | Success (Yes/No) |
|---------|----------------------------------------|--------------------------------------------------------------------- |------------------------------------------------|------------------|
| AI-001  | Input Box Resizing on Enter            | Input box stays same size when pressing enter                        | Input box increases in height; background image moves up | No               |
| AI-002  | Message Disappears After Send          | Sent message disappears from input area immediately                  | Message stays until AI response is received     | No               |
| AI-003  | New Chat Memory                        | AI does not remember previous chats with other users                 | AI remembers past interactions; only clearing history helps | No               |
| AI-004  | Design After Reload                    | Design remains consistent after reload                               | Design changes after reload, returns to normal after clicking | No               |
| AI-005  | Error Message in Chat                  | Bot displays error message in chat if sending/receiving fails        | No error message shown in chat                  | No               |
| AI-006  | Timeout Handling                       | Bot says something went wrong if no answer after 60 seconds          | No timeout message shown                        | No               |
| AI-007  | TTS Speed for Big Texts                | Big texts are processed quickly for TTS                              | TTS takes too long for big texts                | No               |
| AI-008  | TTS Resume Behavior                    | Resuming TTS continues from where paused                             | After pausing/resuming twice, TTS restarts from beginning and waits again | No               |

## AI Testing – Web App on Phone

| Case ID | Case Name                              | Expected Result                                                      | Actual Result                                  | Success (Yes/No) |
|---------|----------------------------------------|--------------------------------------------------------------------- |------------------------------------------------|------------------|
| AIP-001 | TTS First Play Error                   | TTS works on first play                                              | "Not allowed error" on first play; works on second | No               |
| AIP-002 | Chat Bubble Cutoff                     | Chat bubbles fit screen size                                         | Chat bubbles are cut off                        | No               |

## AI Testing – Application on Phone

| Case ID | Case Name                              | Expected Result                                                      | Actual Result                                  | Success (Yes/No) |
|---------|----------------------------------------|--------------------------------------------------------------------- |------------------------------------------------|------------------|
| AIA-001 | Bug Parity with Web                    | No new errors; same as web app                                       | No new errors; same as web app                  |