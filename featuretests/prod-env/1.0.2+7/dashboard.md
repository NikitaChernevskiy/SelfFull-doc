## Dashboard Testing – Web App on PC

| Case ID | Case Name                                   | Expected Result                                                      | Actual Result                                  | Success (Yes/No) |
|---------|---------------------------------------------|--------------------------------------------------------------------- |------------------------------------------------|------------------|
| DB-001  | Screen Navigation Button Visibility         | Unselected icons are clearly visible on light background             | Icons are too light and hard to see             | No               |
| DB-002  | Onboarding Upload Video Button Style        | Upload video button is prominent and matches other buttons           | Small "+" on right wall, not visible or styled  | No               |
| DB-003  | Program Duration Input Type                 | Program duration uses date input                                     | Uses weeks input, not date                      | No               |
| DB-004  | Milestone Number Input Type                 | Milestone number uses number input                                   | Not a number input                              | No               |
| DB-005  | Custom Milestone Interval Input Type        | Custom milestone interval uses date input                            | Not a date input                                | No               |
| DB-006  | Invalid Format Error Handling               | Error message shown for invalid format, no auto-change to 0          | Fields auto-change to 0 after save              | No               |
| DB-007  | Focus Area Image Required Indicator         | Required* star shown if image is required                            | No Required* star                               | No               |
| DB-008  | Closing Message Button Style                | Upload video/materials buttons are prominent and match design        | Buttons are small "+" and not visible           | No               |
| DB-009  | Onboarding Edit Save Warning                | Always shows SAVE button and pop-up if quitting without saving       | No SAVE button or pop-up warning                | No               |
| DB-010  | Notification Schedule Display               | Selected time/date appears under choice with edit button             | No display of selected time/date                | No               |
| DB-011  | Dual Picker Time Format                    | Simple time entry, no overload of functionality                      | Dual picker format is overloaded                | No               |
| DB-012  | AM/PM Selector Usage                       | No AM/PM selector, uses 24-hour format or dropdown                   | AM/PM selector present, unnecessary             | No               |
| DB-013  | Time Input Dropdown                        | Time input is dropdown with hour intervals, editable by number input | Not a dropdown, not editable as described       | No               |
| DB-014  | Invite Users Email Validation               | Only valid emails accepted in invite box                             | Any text can be entered                         | No               |

## Dashboard Testing – Web App on Phone

| Case ID | Case Name                                   | Expected Result                                                      | Actual Result                                  | Success (Yes/No) |
|---------|---------------------------------------------|--------------------------------------------------------------------- |------------------------------------------------|------------------|
| DBP-001 | Invite Users Instructions Size/Scroll       | Instructions fit screen and can be scrolled                          | Instructions too large, links cut off, can't scroll | No            |

## Dashboard Testing – Application on Phone

| Case ID | Case Name                                   | Expected Result                                                      | Actual Result                                  | Success (Yes/No) |
|---------|---------------------------------------------|--------------------------------------------------------------------- |------------------------------------------------|------------------|
| DBA-001 | No New Bugs                                 | No new errors; same as web app                                       | No new errors; same as