---
name: testrail-test-cases
description: Generate TestRail-importable CSV test cases by visually examining a live digital banking web experience in the browser. Use this skill whenever the user wants to write, create, or generate test cases for any feature or page in their online banking platform. Triggers: "create test cases", "write test cases", "generate test cases", "TestRail", "QA test cases", "test cases for [feature]". Do NOT use for other CSV tasks or non-banking test cases.
allowed-tools: mcp__Claude_in_Chrome__tabs_context_mcp, mcp__Claude_in_Chrome__computer, mcp__Claude_in_Chrome__navigate, mcp__Claude_in_Chrome__find, mcp__Claude_in_Chrome__read_page, mcp__Claude_in_Chrome__get_page_text, Bash, Write
---

# TestRail Test Case Generator — Digital Banking

Generate importable CSV test cases for Congressional Federal Credit Union's digital banking platform by **visually examining the live browser experience**.

## When to Use This Skill

Use this skill when the user asks to:
- Create or generate test cases for a digital banking feature
- Write QA test cases for TestRail
- Produce a TestRail CSV for any online banking page or workflow

**Domain**: Congressional Federal Credit Union — Digital Banking User Experiences

---

## Step 1: Connect to the Browser

Call `tabs_context_mcp (createIfEmpty: false)` and take a screenshot to see current state.

**SAFETY RULE**: This is a live banking environment. OBSERVE ONLY — never click Submit, Save, Transfer, Confirm, or any irreversible action button.

---

## Step 2: Explore the Feature

Navigate to the feature the user specified. Use:
- `computer(screenshot)` — take screenshots to see the page
- `read_page` — get accessibility tree for element details
- `find` — locate specific elements by description
- `navigate` — go to a URL if needed

### What to Document

| Category | What to Look For |
|----------|-----------------|
| **Entry points** | All navigation paths to reach this feature |
| **Page structure** | Headings, tables, columns, sections |
| **Form elements** | Dropdowns (all options), text fields, checkboxes |
| **Actions** | Buttons, links (note labels exactly) |
| **Validation** | What happens with empty/invalid inputs |
| **States** | Different states (e.g., active vs frozen, enabled vs disabled) |
| **Error messages** | Any error or warning text |
| **Success flows** | Confirmation pages, success messages |
| **Cancel flows** | Cancel buttons, navigation away |

---

## Step 3: Plan Test Cases

Before writing, outline coverage:

1. **Happy path** — successful primary workflows
2. **Navigation/entry** — all ways to reach the feature
3. **UI verification** — page elements display correctly
4. **State variations** — each dropdown option, each state
5. **Edge cases** — empty forms, duplicate selections, invalid inputs
6. **Error handling** — validation messages
7. **Cancel flows** — canceling mid-action

Aim for **8-15 test cases** for a typical feature. Sequence tests logically (setup → action → verify → cleanup).

### Identifying Test Prerequisites

After planning your test sequence, identify which tests depend on state created by a prior test. Add prerequisite cross-references to the Preconditions field using this rule:

> **If a test case can only be attempted after another test case has already been completed (because it depends on state that test creates), reference that prior test by exact title in the Preconditions section.**

**When to add a prerequisite reference:**
- A test depends on data state created by a prior test (e.g., "Open Unfreeze page for a frozen debit card" requires "Freeze an active debit card" to have run so a card is actually frozen)
- A test picks up mid-flow from where another test left off (e.g., "Freeze an active debit card" requires "Open Freeze page for an active debit card")
- A test verifies behavior only reachable after a specific prior action

**When NOT to add a prerequisite reference:**
- The prior step is just navigation that is repeated in Steps (navigation steps are self-contained)
- The test is fully independent and can be run on its own

**Format — single prerequisite:**

    <p>User is logged in to UAT environment. [Context.] Prerequisite: complete "[Exact Test Case Title]" before attempting this test.</p>

**Format — multiple prerequisites (chain):**

    <p>User is logged in to UAT environment. [Context.] Prerequisites: complete "[Test 1 Title]" then "[Test 2 Title]" before attempting this test.</p>

---

## Step 4: Title Naming Conventions

| Pattern | Example |
|---------|---------|
| Open [Feature] page | Open Overdraft Protection page |
| View [element] for [context] | View existing overdraft sources for each account |
| Update [field] to [value] | Update primary source to SAVINGS ACCOUNT |
| Validation: [condition] | Validation: save without selecting a source |
| [Action] - [variant] | Transfer to SAVINGS ACCOUNT - success |
| [Action] via [entry point] | Navigate to Debit Card Summary via Account Summary link |
| [Action] [object] | Freeze an active debit card |
| Verify [element] display | Verify Debit Card Summary table columns |

---

## Step 5: HTML Formatting Rules

| Field | Format |
|-------|--------|
| Steps (Step) | `<ol><li>Step one.</li><li>Step two.</li></ol>` |
| Steps (Expected Result) | Same `<ol><li>` format as Steps (Step) |
| Expected Result (overall) | `<p>One sentence describing overall outcome.</p>` |
| Preconditions | `<p>User is logged in to UAT environment. [Context.] [Prerequisite if applicable.]</p>` |

- Use `&#039;` for apostrophes in HTML fields
- The "Steps" column (positions 20 and 21, duplicate header) and "Steps (Step)" (position 26) all receive the same `<ol><li>` content

---

## Step 6: Generate the CSV

### EXACT Header Row (copy verbatim)

"ID","Title","Attachments","Automation Type","Created By","Created On","Estimate","Expected Result","Forecast","Goals","Labels","Mission","Preconditions","Priority","References","Section","Section Depth","Section Description","Section Hierarchy","Steps","Steps","Steps (Additional Info)","Steps (Expected Result)","Steps (References)","Steps (Shared step ID)","Steps (Step)","Suite","Suite ID","Template","Type","Updated By","Updated On","automation_id","is_converted"

### Fixed Values Per Row

| Column | Value |
|--------|-------|
| ID | "" (empty) |
| Attachments | "" |
| Automation Type | " None" (space before None) |
| Created By/On, Estimate, Forecast, Goals, Labels, Mission, References | "" |
| Section Depth | "0" |
| Steps (Additional Info), Steps (References), Steps (Shared step ID) | "" |
| Suite | "Master" |
| Suite ID | "S4" |
| Template | "Test Case (Text)" |
| Type | "Other" |
| Updated By/On, automation_id | "" |
| is_converted | "1" |

### Variable Values Per Row

| Column | Notes |
|--------|-------|
| Title | Test case name using naming conventions above |
| Expected Result | `<p>...</p>` HTML describing overall pass condition |
| Preconditions | `<p>...</p>` HTML with login state, context, and prerequisite test reference if applicable |
| Priority | "High", "Medium", or "Low" |
| Section | Feature name (e.g., "Overdraft Protection") |
| Section Description | One sentence describing the feature purpose |
| Section Hierarchy | Same as Section |
| Steps | `<ol><li>...</li></ol>` HTML |
| Steps (duplicate col 21) | Same as Steps |
| Steps (Expected Result) | `<ol><li>...</li></ol>` HTML |
| Steps (Step) | Same as Steps |

### CSV Encoding

- csv.QUOTE_ALL — every field double-quoted
- File encoding: UTF-8

### Output Filename

    testrail_[feature-slug]_[YYYY-MM-DD].csv

---

## Step 7: Save and Report

Save the CSV with Python csv.writer(quoting=csv.QUOTE_ALL).

Also write a matching `.cfg` import mapping file alongside the CSV (same base name, `.cfg` extension):

```python
import json

cfg = {"import":{"format":"csv","version":1},"file":{"encoding":"UTF-8","delimiter":",","start_row":1,"has_header":True,"skip_empty":True},"layout":{"format":"single","break":None,"template":1},"columns":["","cases:title","","cases:custom_automation_type","","","cases:estimate","cases:custom_expected","","","cases:labels","","cases:custom_preconds","cases:priority_id","cases:refs","cases:section_id","","cases:section_desc","cases:section_hierarchy","cases:custom_steps","","","","","","","","","","cases:type_id","","","cases:custom_case_automation_id"],"values":{"1":{"remove_html":False},"3":{"mapping":{"none":""}},"7":{"remove_html":False},"10":{"remove_html":False},"12":{"remove_html":False},"13":{"mapping":{"high":"3","medium":"2"}},"14":{"remove_html":False},"17":{"remove_html":False},"18":{"remove_html":False},"19":{"remove_html":False},"29":{"mapping":{"other":"7"}},"32":{"remove_html":False}}}

cfg_path = csv_path.replace(".csv", ".cfg")
with open(cfg_path, "w", encoding="utf-8") as f:
    json.dump(cfg, f, separators=(",", ":"))
```

Tell the user both full file paths and the number of test cases generated.
