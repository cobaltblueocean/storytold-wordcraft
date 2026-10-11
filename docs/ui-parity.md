# UI parity with Microsoft Word

> **Last reviewed:** 2026-10-10 · **Last updated:** 2026-10-11 · **Change:** trivial (Customize Ribbon and the Quick Access Toolbar, #379; previously: major, first version; ribbon, dialogs, shortcuts and on-canvas interaction measured from `crates/ui-egui` and the command registry) · **Target:** Microsoft Word (Microsoft 365) for Mac 16.113.4

How WordCraft looks and feels next to Word: ribbon, dialogs, panes, keyboard, mouse and touch.
Typing behaviour has its own checklist ([`typing-parity.md`](typing-parity.md)). All assets are our
own (`AGENTS.md`: no Microsoft iconography, ever).

**Dimension: ~65% (estimated), 65–100 h to full** (the sum of the rows below; dialog depth is counted here, not under features).

| Area | WordCraft | Word | Parity | Hours |
|---|---|---|---|---|
| Ribbon tabs and groups | All Word tabs including contextual Table Design/Layout, Picture Format, Shape Format, Header & Footer, Equation; ribbon overflow (#43, #129). Draw tab: Select, Eraser, Pen, Pencil, Highlighter with colour and thickness (#307); missing: Lasso, Add Pen, Ink to Shape/Math, Ink Replay | Same plus Draw | 85% | (Draw in features) |
| Keytips (Alt / ⌃⌥ letters) | ✅ (#43) | ✅ | 85% | 1–2 |
| Mini-toolbar on selection | ✅ (#43) | ✅ | 80% | 1–2 |
| Quick Access Toolbar | AutoSave, then the user's commands (Save, Undo, Redo by default); add, remove and reorder from its … menu (common commands, More Commands…), right-click on any ribbon button, or Customize Ribbon; saved per user (#379, #376). Not shown below the ribbon | customizable | 90% | 0.5 |
| Customize Ribbon / Customize Keyboard | Customize Keyboard (#368): categories, a command's keys, press a combination to see which command uses it, Assign / Remove / Reset All; custom keys override built-ins, removed built-ins do nothing, saved per user; `tools.customizeKeyboard` for agents. Customize Ribbon (#379): show, hide and reorder tabs, custom tabs and custom groups (on any tab) holding any commands, rename, remove, Reset; right-click on the ribbon; saved per user; `tools.customizeRibbon` for agents. Built-in tabs can't be renamed; no import/export file | ✅ | 85% | 1–2 |
| Keyboard shortcuts | **125** commands bound in `CommandSpec::key`, 144 key combinations (measured on Linux/Windows); styles, spacing, symbols, fields, views, mail merge (#330); field keys Alt+F9, Shift+F9, Ctrl+Shift+F9, Ctrl+F11, Ctrl+Shift+F11, F11, Shift+F11 (#339); Alt+Shift+arrows (move paragraphs, promote/demote), Shift+F5 Go Back and Alt+X (#343). Missing: en dash on the numeric keypad | ~250 default shortcuts | ~70% | 2–4 |
| Modal dialogs | **36** (`Dialog` enum: Font, Paragraph, Tabs, Borders and Shading, Find, Go To, Insert Table, Table Properties, Page Setup, Link, Bookmark, Word Count, Zoom, Watermark, New Style, Modify Style, Manage Styles, Table Style, Commands, Paste Special, About, Save Changes, Password, Encrypt with Password, Define New Multilevel List, Track Changes Options; Columns, Symbol with Special Characters, Field (#321); Field code (#339); mail merge Recipients, Insert Merge Field, Find Recipient, Rules, Match Fields, Check for Errors) plus panes and menus for the rest | ~100 (Caption, Index, TOC options, Citation, Compare, Protect, Language, Hyphenation, Line Numbers, Envelopes, Labels, AutoCorrect, Options panes…) | ~40% | 20–30 |
| Task panes (Navigation, Styles, Comments, Reviewing, Format Picture/Shape, Thesaurus, Accessibility, Clipboard, Selection) | Navigation, Styles, Comments, Thesaurus, Accessibility, Read Aloud, Zotero; Style Inspector (#236); Clipboard pane (#264) open | all | 70% | 4–6 |
| Context menus (right-click) | text, spelling suggestions, fields (Update Field, Edit Field…, Toggle Field Codes, #339); objects and tables partial | rich per context | 55% | 3–5 |
| Backstage (Home, New, Open, Info, Save As, Print, Share, Export, Options) | Home and New separate (#254), Info properties kept (#268) | | 68% | 4–6 |
| Rulers: indents, tabs, margins, table columns | indents draggable (one undo, #62); tabs; table column drag pending (#49) | ✅ | 70% | 2–3 |
| On-canvas objects: select, drag, resize handles, nudge | ✅ tested (#228) | ✅ | 75% | — |
| Rotation handle, crop handles on canvas, alignment guides, smart guides | rotation handle (Shift: 15° steps), turned frames resize along their axes (#332); crop handles and guides missing | ✅ | 25% | 3–5 |
| Selection: word/sentence/paragraph clicks, Shift extend, F8 extend mode, column (Alt+drag, #237) | ✅ | ✅ | 85% | 1 |
| Zoom: Ctrl+scroll, pinch (#179), zoom buttons (#232), pages side by side when zoomed out (#251) | ✅ | ✅ | 85% | — |
| Touchpad smooth/inertial scroll | ✅ (#252) | ✅ | 90% | — |
| Status bar (page x of y, words, language, view buttons, zoom slider) | ✅ | ✅ | 80% | — |
| Interface themes (light, dark, system #249, follows OS changes live #311), dark page separate from the interface theme (#194, #312) | ✅ | ✅ | 90% | — |
| Interface size (File › Options › General, 80–200 %, on top of the system display scale; `ui.interfaceSize`) (#475) | ✅ | system display scaling only | 100% | — |
| Platform conventions (macOS menus/traffic lights #255, Windows title bar, Linux CSD on Wayland #78) | partial | native | 70% | 3–5 |
| Screen readers (VoiceOver, Narrator, Orca) | AccessKit on, document canvas exposure untested | full | 25% | 10–15 |
| Right-to-left (mirrored) interface | ❌ | ✅ (Arabic, Hebrew Word) | 0% | in localization |

## Revision history

| Date | Change | Summary |
|---|---|---|
| 2026-10-11 | trivial | Customize Ribbon (custom tabs and groups, hidden and reordered tabs) and a customizable Quick Access Toolbar with a working … menu (#379, #376) |
| 2026-10-11 | trivial | Customize Keyboard dialog (Tools › Customize Keyboard, File › Options › Keyboard shortcuts): custom keys override built-ins and persist (#368) |
| 2026-10-11 | minor | Keyboard shortcuts 101 → 125 commands (#330): Reset Paragraph/Character Formatting, symbols, DATE/TIME/PAGE fields, view switches, Word Count, mail merge, F4 Repeat now reachable |
| 2026-10-11 | trivial | Collapsed duplicate rows left by parallel merges |
| 2026-10-11 | trivial | Dialogs keep their top edge in place when switching tabs (Paragraph, Font, Borders and Shading…): only the bottom edge moves (#507) |
| 2026-10-11 | trivial | Interface size setting in File › Options › General (80–200 %), kept between runs and applied on top of the system's display scale; `ui.interfaceSize` for agents (#475) |
| 2026-10-11 | trivial | Font box (ribbon and mini toolbar): typing lists the matching fonts (prefix first, then any part of the name); Up/Down, Enter or a click picks one, Escape cancels (#359) |
| 2026-10-11 | trivial | Field codes (#339): View › Field Codes (Alt+F9), Toggle Field Codes (Shift+F9), a field-code popup (double-click, right-click › Edit Field…; Ctrl+F9 opens the Field dialog), unlink/lock/unlock and next/previous field keys; field items in the context menu |
| 2026-10-10 | trivial | Tabs dialog (Paragraph › Tabs…, double-click a ruler tab) and Borders and Shading with Borders, Page Border and Shading tabs (#320) |
| 2026-10-10 | trivial | Columns (presets, unequal widths, line between, apply to), Symbol (font coverage grid by Unicode subset, recently used, character code, Special Characters) and Field (categories, options, field codes) dialogs (#321) |
| 2026-10-10 | trivial | Define New Multilevel List (all nine levels, live preview, `list.define`) and Track Changes Options (show, balloons, insertion/deletion marks and colours, changed-line bars; `review.trackingOptions`, saved per user) (#328) |
| 2026-10-10 | trivial | Shortcuts: Alt+Shift+Up/Down move paragraphs, Alt+Shift+Left/Right promote/demote (⌃⇧ arrows on macOS), Shift+F5 Go Back, Alt+X Toggle Unicode (#343) |
| 2026-10-10 | trivial | Rotation handle on pictures, shapes and text boxes; Rotate menu (90° and flips) and a Rotation box in Picture/Shape Format › Size (#332) |
| 2026-10-10 | trivial | System interface theme keeps following OS appearance changes (no longer pins the macOS window); Dark page no longer darkens the interface (#311, #312) |
| 2026-10-10 | trivial | AutoSave switch greyed out with a tooltip saying why where AutoSave can't save; Save As from it (#196, #176) |
| 2026-10-10 | trivial | Table Properties dialog and Table Layout Height/Width boxes (#44) |
| 2026-10-10 | minor | Merged main: Style Inspector, Column Selection, zoom buttons, inertial scrolling, File Info landed |
| 2026-10-10 | major | First version: ribbon, dialog, shortcut and interaction inventory |
| 2026-10-10 | trivial | Draw tab tools and Review › Hide Ink (#307) |
