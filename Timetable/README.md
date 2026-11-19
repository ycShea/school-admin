# Timetable PDF → Excel

🔗 **[Click here to access the Live Tool](https://ycshea.github.io/HkugacAdmin/SchoolTimeTable/)**

A single-page web tool that turns the two PDF timetables exported from **aSc Timetables** (the **Class PDF** and the **Teacher PDF**) into **Excel files**:

- a **database workbook** (teacher database, class lessons, teacher lookup, summary, notes);
- a file of **class timetables** (one sheet per class) and a file of **teacher timetables** (one sheet per teacher);
- a separate **Free lesson attendance** file.

Everything runs in your browser. The PDFs are read on your computer and are **not uploaded anywhere**.

> Prefer everything inside one Google Sheet? See the [Google Sheets version](https://github.com/ycShea/HkugacAdmin/blob/main/SchoolTimeTable/Spreadsheet%20Version/README.md).

---

## Contents

- [Quick start](#quick-start)
- [What you get](#what-you-get)
- [Free lesson attendance](#free-lesson-attendance)
- [How teachers, venues and subjects are matched](#how-teachers-venues-and-subjects-are-matched)
- [Checks shown while importing](#checks-shown-while-importing)
- [Limitations](#limitations)
- [FAQ](#faq)
- [Privacy and hosting](#privacy-and-hosting)
- [Customising](#customising)

---

## Quick start

1. Open the [live tool](https://ycshea.github.io/HkugacAdmin/SchoolTimeTable/).
2. **Step 1:** choose the **Class PDF**, then the **Teacher PDF**. Both are required.
3. **Step 2:** check the file names (they are proposed from the PDF names) and keep or untick the timetable files. See [the options](#the-options-in-step-2).
4. Click **Import** and wait for the green **All done.** line. Three download links appear right after it: the database file, the class timetables and the teacher timetables.
5. Click **Open Free lesson attendance ▶** if you also want the [Free lesson attendance](#free-lesson-attendance) file.

### The options in step 2

| Option | What it does |
|---|---|
| Database file | Name of the database workbook (default `<Class PDF name>_database`) |
| Also create the two timetable files | Ticked by default. Untick it to make only the database file |
| Class file | Default `<Class PDF name>_class_timetables` |
| Teacher file | Default `<Teacher PDF name>_teacher_timetables` |

The file names can be edited. Two files cannot have the same name, and Import stays disabled until the names are different.

### File-name and content checks

- **File-name check (a warning):** the Class PDF's name should contain “Class” (for example `2627_T1_Class_v9.pdf`) and the Teacher PDF's name should contain “Teacher”. If not, a warning appears under that box, and it says so when the two files look swapped. You can still import.
- **Content check (stops the import):** the Class PDF must show class names such as S1H on its pages, and the Teacher PDF must show names such as “CHAN Clara (Chinese)”. If not, the import stops with a message and nothing is made.

---

## What you get

| File | Contents |
|---|---|
| `<Class PDF name>_database.xlsx` | Five sheets, in this order: `Teacher DB`, `Class Lessons`, `Teacher Lookup`, `DB Summary`, `Notes` |
| `<Class PDF name>_class_timetables.xlsx` | One sheet per class, in the order of the pages in the Class PDF |
| `<Teacher PDF name>_teacher_timetables.xlsx` | One sheet per teacher, in the order of the pages in the Teacher PDF |
| `<Class PDF name>_free_lesson_attendance.xlsx` | One sheet, `Free lesson attendance` (made from the Free lesson attendance window) |

### The database workbook

| Sheet | Contents |
|---|---|
| `Teacher DB` | One row per teacher, day and period: Teacher, Day, Period, Class, Venue, Co-teaching (Y or N), Lesson/Meeting/Support, Subject, Time, Teachers sharing this venue, Pairing, Teacher Name |
| `Class Lessons` | One row per lesson per class, as printed in the Class PDF (Class, Day, Period start, Periods, Time, Subject, Teachers, Venue) |
| `Teacher Lookup` | Teacher code, name and department (read from the Teacher PDF) |
| `DB Summary` | How many rows have no venue or subject of their own, by subject (formulas over `Teacher DB`) |
| `Notes` | The rules, the sheets, and the cross-check of the two PDFs |

- A double period is two rows in `Teacher DB`, one per period.
- In `Teacher DB` the Class column holds the classes of the lesson as printed, for example `S2H/S2K/S2U`.
- **Lesson / Meeting / Support:** a card with classes is a *Lesson*. A card whose name contains “Meeting” is a *Meeting*. A card whose name contains “SUPPORT” is *Support*. For meetings and support the Subject column holds the name printed on the card.
- `Co-teaching` and `DB Summary` are formulas. Excel calculates them when the file is opened.
- `Teacher DB` already contains every lesson row of the class data (the page checks that the two PDFs agree, see [the cross-check](#checks-shown-while-importing)).

### The class timetables file

Each sheet has the days `A1`–`B5` across the top and the periods `1`–`7` down the side. Each class sheet has two tables with the same structure:

- the **blue table** at the top (rows 1–8) shows the subject;
- the **green table** in **rows 11–18** shows more detail. Each cell holds the subject, the teachers and the venue on separate lines, for example `ICT` / `LG / MH` / `207A`.

Double periods fill both periods in both tables.

### The teacher timetables file

The sheet name is the teacher code. Each cell holds the subject, the classes and the venue on separate lines. Cell A1 is the teacher code and the full name is in A10. If a teacher has two lessons in the same period, both are shown.

---

## Free lesson attendance

A separate Excel file with one row per class, day and period, where the subject is written as `Class-Subject`:

| Subject | Day | Period |
|---|---|---|
| S4A-MA | A1 | 1 |
| S5C-E1 | A1 | 1 |
| S5H-E3 | A1 | 1 |
| S6A-E2 | A1 | 1 |
| S4A-EN | A1 | 2 |

**How to make it.** After an import, click **Open Free lesson attendance ▶**. A window opens over the page:

1. **Levels.** Tick the levels you want. **S4–S6** are ticked by default; you can also tick S1–S3. **Select all** and **Unselect all** next to the heading tick or clear all six levels.
2. **Map the electives.** Shown only when needed, see below.
3. **File name** (default `<Class PDF name>_free_lesson_attendance`), then **Create the Excel file**. A download link appears in the window and in the log.

The rows are sorted by day (`A1`…`B5`), then period, then class A–Z. A double period gives two rows. Free periods give no row.

**How the subject is written**

| Subject in the class PDF | Shown as |
|---|---|
| `CHI`, `EN`, `MA`, `CSD`, `HD`, `PE` (also `OPT1`, `OPT2`, `CASTLE`, `MS`) | As printed, for example `S4A-OPT1`, `S6C-CSD` |
| An elective block lesson (S4E2, S5E1, S6E2…) | `E2`, `E1`, `E2`… (the level is dropped) |
| The one other elective of a class that has blocks | The missing number: **E1 in S4** (blocks are E2 and E3), **E3 in S5 and S6** (blocks are E1 and E2) |
| The electives of a class with no blocks (today S5C and S6A) | Chosen by you in the mapping table |
| S1–S3 subjects | As printed, for example `S1H-ICT` |

**E1, E2 and E3** are names for groups of electives: a group can hold one subject or several. Every class in S4–S6 has three elective lines, which are E1, E2 and E3.

**The mapping table.** For a class that has no block lessons, the numbers cannot be worked out from the timetable, so you choose them. There is one table per level, listing the subjects of the classes it applies to. The defaults are **PHY or EC/PHY → E1, CHEM → E2, BIO → E3**, listed in that order. Choose **As printed** to leave a subject unchanged.

**Warnings and confirmation.** The window shows a warning, in red, if a subject is left unmapped or if two subjects of one class get the same number (for example `S5C: EC/PHY and BIO are both mapped to E1.`). If a warning exists when you click **Create the Excel file**, it asks **Create the file anyway?** and waits for **Yes, create it anyway** or **No, go back**.

**Making it again.** The window warns that the file was already created and that creating it again replaces it. Importing again clears it.

---

## How teachers, venues and subjects are matched

Where a lesson lists several teachers, venues and subjects, they are matched **by position**.

> `AF / HC / SYC` with venues `601,602,603` means AF uses 601, HC uses 602 and SYC uses 603.
> Subjects work the same way: `CH/BIO` with `TH / NYC` and `604,213` means TH teaches CH in 604, and NYC teaches BIO in 213.

| Situation | What happens |
|---|---|
| Same number of teachers and venues | Matched by position |
| **One** venue (or subject) | Every teacher shares it |
| **More teachers than venues** (or subjects), with more than one venue | The first teachers are matched by position. Each remaining teacher gets the full venue list, a **line break**, then the full teacher list (for example `301,302,303,207B,311,308,409` ⏎ `AH / NC / DW / EL / CK / STC / AYI / CT / HH`). Subjects work the same way (`EC/PEDSE` ⏎ `ALC / EL / HH`). These rows are flagged in the **Pairing** column |
| **Group sessions**: `HD`, `MS`, `CASTLE`, `OPT1`, `OPT2`, `OPT3`… | **Not matched.** Every teacher row shows the full venue list |
| A lesson drawn side by side in a clash cell (the PDF does not print its teachers) | The teacher list is taken from the same lesson on another teacher's page. If that is not possible, the venue is not matched and the row is flagged |

**Co-teaching** is `Y` when more than one teacher uses the same venue in the same lesson, otherwise `N`.

- Group sessions are `Y`.
- For a teacher with no venue of their own, the count in “Teachers sharing this venue” is an estimate (at least 2).
- Meetings and support are `N`.

**Teacher codes.** The Teacher PDF shows each teacher's full name but not their initials. The page works the initials out: they are the code that appears in every lesson on that teacher's page. Where several teachers always teach together, codes already taken by other pages are removed. A teacher page with no lessons has no code.

---

## Checks shown while importing

| Check | Where |
|---|---|
| Every class-day adds up to 7 periods, with no overlapping lessons | Class PDF |
| Every lesson was placed and every teacher has a code; pages with no lessons are shown in red | Teacher PDF |
| **Cross-check:** the Teacher PDF and the Class PDF agree on every lesson row (same teacher, day, period, classes, venue, subject and co-teaching) | Both. The result is also written to the `Notes` sheet |

---

## Limitations

- Built and tested for the **HKUGA College 2026–27 Term 1** aSc exports: landscape, a 10-day cycle `A1`–`B5`, 7 periods. The page reads the PDF by text position and font size, so a different print layout may need the layout constants in `index.html` adjusted.
- Free periods have no row.
- Where a teacher has two lessons in the same period, both are listed.
- In grouped lessons (for example EN or MA across several classes) the PDF does not say which teacher takes which class, so each teacher is listed against every class in the group.
- Teacher codes are worked out from the PDF rather than printed in it. Check the `Teacher Lookup` sheet.
- The page needs an internet connection to load two libraries from cdnjs.
- Each import starts from scratch: the page does not keep anything between visits.

---

## FAQ

**Is my PDF uploaded?**
No. Everything runs in your browser.

**Why does a cell show a venue list, then a line break, then a list of teachers?**
That teacher has no venue (or subject) of their own: the lesson has more teachers than venues (or subjects). See [the matching rules](#how-teachers-venues-and-subjects-are-matched).

**Why are the venues of HD, MS, CASTLE and OPT not matched to teachers?**
They are whole-level group sessions, so every teacher row shows the full venue list. You can change which subjects are treated this way (see [Customising](#customising)).

**Why do I have to map the electives of S5C and S6A?**
Their timetables show the subjects (for example EC/PHY, BIO, CHEM) and no E1/E2/E3 block lessons, so the group of each subject is not in the PDF. The defaults are PHY or EC/PHY → E1, CHEM → E2, BIO → E3.

**Why does a teacher appear against every class in a group lesson?**
The PDF lists all the teachers of a lesson on every class page and does not say who takes which class.

**A teacher has no code. Why?**
Their page has no lessons, so there is nothing to work the code out from.

**Can I use it for another school or another layout?**
Only if the PDF has the same print layout. Otherwise the layout constants need adjusting (see below).

---

## Privacy and hosting

- The PDFs stay in your browser. Teacher names are read from the Teacher PDF while the page is open and are not stored in the page or anywhere else.
- The repository needs only `index.html`, which is served at `/SchoolTimeTable/`. It uses [pdf.js 3.11.174](https://mozilla.github.io/pdf.js/) and [ExcelJS 4.4.0](https://github.com/exceljs/exceljs), loaded from cdnjs.

## Customising

All settings are at the top of the script in `index.html`:

| Setting | What it controls |
|---|---|
| `GROUP_RE` | The subject codes treated as group sessions (default `HD`, `MS`, `CASTLE`, `OPT…`) |
| `X`, `Y` | Column and row edges of the class timetable grid. `TX` is the column edges for teacher pages |
| `DAYS`, `TIMES` | Day codes and period times |
| `FREE_CORE` | Subjects shown as printed in Free lesson attendance (default CHI, EN, MA, CSD, HD, PE, CASTLE, MS, OPT…) |
| `FREE_BLOCK` | Elective block codes, such as S4E2 or S5E1 |
| `freeDefaultE` | The default mapping offered for electives (PHY or EC/PHY → E1, CHEM → E2, BIO → E3) |
| `DB_ORDER` | The order of the sheets in the database workbook |
