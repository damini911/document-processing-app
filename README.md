Act as a Senior QA Engineer, Pension Testing SME, and Python Code Reviewer.

Your task is to perform a complete verification of the MOA Valuation Package Assembly application.

DO NOT modify code.

ONLY audit, validate, trace, and report.

=================================================

GOAL

=================================================

Confirm that the application implementation matches the Operations requirements and SOP documents.

Verify all extraction logic, business rules, document filtering, section ordering, bookmark logic, filename generation, Action Required logic, and 403(b) behavior.

=================================================

TRACE COMPLETE WORKFLOW

=================================================

Validate the workflow:

Input PDFs

    ↓

PDF Classification

    ↓

Field Extraction

    ↓

PlanProfile Creation

    ↓

Rules Engine

    ↓

Section Inclusion/Exclusion

    ↓

Document Ordering

    ↓

Bookmarks

    ↓

Final PDF

For each stage provide:

- Input

- Output

- Code Location

- Validation Result

- Any Risk

=================================================

VERIFY FIELD EXTRACTION

=================================================

Confirm where each field is derived from:

Plan Number

Plan Name

Plan Type

Plan Year Start

Plan Year End

HCE Current

HCE Future

Top Heavy

Top Heavy %

ACP Method

ACP Failed

ADP Failed

402(g) Failed

415 Failed

Returns Required

Returns Already Processed

Variance Report

Annual Allocation

ACP QNEC

ADP QNEC

402(g) After 4/15

For each field show:

Field

Source File

Extraction Method

Code Location

Confidence Level

=================================================

VERIFY 403(b) RULES

=================================================

Confirm implementation of:

1. HCE/KEY renamed to HCE

2. ACP bookmark used instead of ADP/ACP bookmark

3. ADP-only references suppressed where required

4. Top Heavy removed when:

   "403b N/A"

5. Missing detailed 410(b) report is allowed

6. Universal Availability wording retained

Report pass/fail for each rule.

=================================================

VERIFY ACTION REQUIRED PAGE

=================================================

Validate:

Rule A

If:

402(g) fail OR 415 fail

Then:

Compliance Failure wording appears

--------------------------------------------

Rule B

If:

ACP/ADP fail

AND returns required

AND Prior method

Then:

Prior Method wording appears

--------------------------------------------

Rule C

If:

ACP/ADP fail

AND returns required

AND Current method

Then:

Current Method wording appears

--------------------------------------------

Rule D

If:

Top Heavy > 60%

Then:

Top Heavy wording appears

--------------------------------------------

Rule E

If:

Variance exists

OR Annual Allocation = Yes

Then:

Contribution wording appears

--------------------------------------------

Rule F

If no action items exist

Then show ONLY:

"NO IMMEDIATE ACTION REQUIRED"

Verify exact implementation.

=================================================

VERIFY FAILURE LETTER LOGIC

=================================================

ACP Failure Notice

Include only if:

- ACP Fail

- Returns Required

- Current Method

Otherwise remove.

--------------------------------------------

402(g) Sample Letter

Include only if:

- 402(g) Fail

- NOT after 4/15

Otherwise remove.

--------------------------------------------

415 Failure Letter

Include only if:

- 415 Fail

Otherwise remove.

--------------------------------------------

ACP Return Letter

Include only if:

- ACP Fail

- Returns Required

Otherwise remove.

Verify implementation.

=================================================

VERIFY SECTION ORDERING

=================================================

Validate ordering against sections.yaml

and business rules.

Verify conditional sections:

Cover Letter

Test Summary

Action Required

Important Information

Compliance Overview

Contribution Analysis

HCE

Future HCE

ACP

402(g)

410(b)

401(a)(4)

ABPT

BRF

414(s)

415

Top Heavy

Census

For each section provide:

Include Conditions

Exclude Conditions

Order Position

=================================================

VERIFY BOOKMARK RULES

=================================================

Check bookmark generation.

Verify:

Cover Letter

Test Summary

Contribution Analysis

HCE

Future HCE

ACP Test

402(g)

410(b)

401(a)(4)

ABPT

BRF

414(s)

415

Top Heavy

Census

Report:

Bookmark Name

Creation Condition

Code Location

=================================================

VERIFY FILENAME LOGIC

=================================================

For:

07/01/2025 – 06/30/2026

Expected:

800643_2025-Valuation.pdf

Confirm that beginning plan year is used.

=================================================

TRACE TEST PLAN 800643

=================================================

Simulate plan 800643.

Produce:

{

  "plan_type": "",

  "testing_method": "",

  "hce_current": "",

  "hce_future": "",

  "top_heavy": "",

  "top_heavy_percent": "",

  "adp_failed": "",

  "acp_failed": "",

  "fail_402g": "",

  "fail_415": "",

  "returns_required": "",

  "selected_sections": [],

  "removed_sections": [],

  "bookmarks": []

}

=================================================

FINAL REPORT

=================================================

Provide:

1. Working correctly

2. Potential defects

3. Missing business rules

4. Incorrect assumptions

5. Risk areas

6. Test cases still needed

7. Overall confidence score (0-100%)

DO NOT modify files.

DO NOT write code.

ONLY perform a verification audit.

 

---------------------------
Act as a Senior Python Architect, QA Engineer, and Pension Valuation SME.

DO NOT modify code.

Perform a complete static audit of the MOA Valuation Package Assembly application.

Assume that no sample files are available.

You must validate the implementation by tracing the code paths, configuration files, models, rules, and service interactions.

==================================================

OBJECTIVE

==================================================

Determine whether the application correctly implements the MOA valuation package requirements.

Do not require actual PDF files.

Analyze only source code and configuration.

==================================================

REQUIREMENTS TO VERIFY

==================================================

1. PLAN TYPE RULES

Verify how plan_type is determined and consumed.

Specifically verify 403(b) behavior:

- HCE/KEY becomes HCE

- ACP bookmark instead of ADP/ACP bookmark

- ADP-only notices suppressed

- Top Heavy often removed when marked "403b N/A"

- Missing 410(b) report is allowed

- Universal Availability language preserved

Show where each rule is implemented.

==================================================

2. ACTION REQUIRED LOGIC

==================================================

Verify code implements:

Compliance wording appears when:

    402(g) failure OR 415 failure

    AND returns still required

PRIOR wording appears when:

    ADP/ACP failed

    AND prior method

    AND returns required

CURRENT wording appears when:

    ADP/ACP failed

    AND current method

    AND returns required

Top Heavy wording appears when:

    top heavy > 60%

Contribution wording appears when:

    annual allocation

    OR variance report

If no action items exist:

    ONLY

    "NO IMMEDIATE ACTION REQUIRED"

Trace implementation and provide pass/fail assessment.

==================================================

3. FAILURE LETTER LOGIC

==================================================

Verify:

ACP Failure Notice

Include only when:

    ACP Fail

    Returns Required

    Current Method

Otherwise remove.

--------------------------------------

402(g) Sample Letter

Include only when:

    402(g) Fail

    AND NOT after 4/15

Otherwise remove.

--------------------------------------

415 Sample Letter

Include only when:

    415 Fail

Otherwise remove.

--------------------------------------

Excess Summary

Only when applicable.

Identify exact code implementing these rules.

==================================================

4. FIELD SOURCE AUDIT

==================================================

Build a matrix:

Field

Expected Source

Actual Source In Code

Code Location

Verify:

plan_type

plan_number

plan_year

testing_method

hce_current

hce_future

top_heavy

top_heavy_percent

adp_failed

acp_failed

fail_402g

fail_415

returns_required

variance_report

annual_allocation

adp_qnec

acp_qnec

402g_after_deadline

Highlight any fields that are inferred from PDFs but should come from Excel.

==================================================

5. PLAN PROFILE AUDIT

==================================================

Trace every property of PlanProfile.

For each property:

- Where set

- Where modified

- Where consumed

- Whether default values could cause incorrect assembly

Identify nullable fields that may silently create wrong output.

==================================================

6. RULES ENGINE AUDIT

==================================================

Review rules_engine.py.

Produce:

Rule Name

Input Fields

Decision

Output

Risk

Verify no rule includes a document simply because it exists.

Confirm decisions are business-rule driven.

==================================================

7. SECTION ORDERING AUDIT

==================================================

Review:

sections.yaml

package_map.yaml

file_order.py

package_builder.py

Generate:

Section

Required?

Conditional?

Inclusion Rule

Exclusion Rule

Order

Validate:

Cover Letter

Test Summary

Action Required

Important Information

Compliance Overview

Contribution Analysis

HCE

Future HCE

ACP

402(g)

410(b)

401(a)(4)

ABPT

BRF

414(s)

415

Top Heavy

Census

==================================================

8. BOOKMARK AUDIT

==================================================

Review bookmark generation.

For every bookmark:

Bookmark Name

Creation Condition

Code Location

Verify alignment with SOP.

==================================================

9. RESULT SUMMARY AUDIT

==================================================

Review field_patterns.py and pdf_extractor.py.

Determine whether extraction patterns match likely MOA reports.

Pay special attention to:

ACP

ADP

402(g)

415

410(b)

Identify regexes likely to fail because of report wording differences.

==================================================

10. RISK ANALYSIS

==================================

field_patterns.py

    ↓

pdf_extractor.py

    ↓

PlanProfile

    ↓

rules_engine.py

    ↓

action_required.py

    ↓

package_builder.py

# document-processing-app
A modular document processing and validation platform.

Now I can clearly see why you're saying the result is not as expected.

I compared your generated file ​pdf icon 800643_UNKNOWN-Valuation (1).pdf against the expected file ​pdf icon 800643_2025-Valuation.pdf. [800643_UNK...uation (1) | PDF]

The biggest issue
Your automation is keeping all conditional failure pages, even though the plan passed all tests.

From your generated file:

Page 3
Contains:

IMMEDIATE ACTION REQUIRED - COMPLIANCE TEST FAILURE

IMMEDIATE ACTION REQUIRED - ACP TEST FAILURE

IMMEDIATE ACTION REQUIRED - CONTRIBUTIONS

[800643_UNK...uation (1) | PDF]

Page 4
Contains:

IMMEDIATE ACTION REQUIRED - ACP PRIOR METHOD TEST FAILURE

NO IMMEDIATE ACTION IS REQUIRED AT THIS TIME

[800643_UNK...uation (1) | PDF]

For this plan:

ACP = Pass

402(g) = Pass

415(c) = Pass

410(b) = Pass

[800643_UNK...uation (1) | PDF]

Therefore the expected package should contain only:

NO IMMEDIATE ACTION IS REQUIRED AT THIS TIME

and all failure paragraphs should be removed.

Incorrect pages included
Your generated PDF includes:

ACP failure letter
Page 6

SAMPLE/DRAFT Communication to Participant

ACP nondiscrimination testing failure

[800643_UNK...uation (1) | PDF]

Should be removed.

ACP excess return notice
Page 11

Failed Compliance Testing Excess Return Notice

Current method testing

[800643_UNK...uation (1) | PDF]

Should be removed.

415 failure information
Page 12

Annual Additions (IRC 415) Test Failure Information

[800643_UNK...uation (1) | PDF]

Should be removed.

402(g) failure sample letter
Page 13

withdrawn from your plan account as the 402(g) Deferral Limit has been exceeded

[800643_UNK...uation (1) | PDF]

Should be removed.

415 failure sample letter
Page 14

Annual Additions (IRC 415) limit has been exceeded

[800643_UNK...uation (1) | PDF]

Should be removed.

Root cause
Your automation appears to be assembling based on:

PDF exists

=> Include PDF

Instead of:

PDF exists

+

Business rule satisfied

=> Include PDF

The business rule for this plan is:

ACP_PASS = True

DEFERRAL_PASS = True

LIMIT415_PASS = True

So:

REMOVE:

    ACP Failure Notice

    ACP Return Notice

    ACP Sample Letter

    402g Sample Letter

    415 Failure Information

    415 Sample Letter

Second issue
Your automation is not removing unused Action Required text.

Current output:

IMMEDIATE ACTION REQUIRED....

IMMEDIATE ACTION REQUIRED....

IMMEDIATE ACTION REQUIRED....

NO IMMEDIATE ACTION REQUIRED....

[800643_UNK...uation (1) | PDF]

Expected:

NO IMMEDIATE ACTION REQUIRED AT THIS TIME

only.

This likely means your text-removal logic is not firing.

Third issue
Wrong document order

Your generated PDF order is:

Cover Letter

Test Summary

Action Required

Failure Pages

Overview

More Failure Pages

Contribution Analysis

HCE

...

[800643_UNK...uation (1) | PDF]

Expected order is:

Cover Letter

Test Summary

Action Required

Important Information

Compliance Overview

Contribution Analysis

HCE

Future HCE

ACP

402(g)

415

Census

The failure-related documents should not be inserted between Action Required and Contribution Analysis for this plan.

Fourth issue
Missing "Important Information" page

Expected PDF contains:

Year End Recap: Important Information

with selected bullets. This appears immediately after Action Required.

Your generated PDF does not contain this page at all. [800643_UNK...uation (1) | PDF]

This means either:

the source PDF wasn't identified correctly, or
classification logic failed.
What rule should drive these decisions?
For this plan I would create:

rules = {

    "acp_pass": True,

    "402g_pass": True,

    "415_pass": True,

    "plan_type": "403b",

    "hce_current": True,

    "hce_future": True,

    "top_heavy": False,

}

Then:

if acp_pass:

    remove_acp_failure_notice()

    remove_acp_return_notice()

    remove_acp_sample_letter()

if pass_402g:

    remove_402g_letter()

if pass_415:

    remove_415_failure_notice()

    remove_415_letter()

if no_failures:

    keep_only_no_action_required()

What I would debug first
I would place logging around the Result Summary parser and verify it extracts:

{

    "410b": "Pass",

    "402g": "Pass",

    "415": "Pass",

    "ACP": "Pass"

}

Because if your parser fails to read those values, the app will assume:

unknown = include everything

which is exactly what your output looks like.

My strongest suspicion is that the Result Summary PDF is not being used to control page removal, or the pass/fail extraction from the summary page is failing, causing all conditional templates to remain in the assembled package.

------------------------------------------

You are a senior Python architect and pension valuation domain analyst.

Analyze the entire MOA valuation package assembly workflow.

Context:

Current issue:

The application successfully merges PDFs but includes pages that should be removed based on business rules.

Example:

Plan Type = 403(b)

ACP Method = Current

HCE Current = Yes

HCE Future = Yes

Top Heavy = 403b N/A

Result Summary shows:

410(b) = Pass

402(g) = Pass

415(c) = Pass

ACP = Pass

Expected package:

- Cover Letter

- Test Summary

- Action Required (only "No Immediate Action Required")

- Year End Recap

- Compliance Overview

- Contribution Analysis

- HCE

- Future HCE

- ACP Test

- 402(g)

- 415

- Census

Should NOT include:

- ACP Failure Notice

- ACP Sample Letter

- ACP Return Letter

- 402(g) Sample Letter

- 415 Failure Information

- 415 Sample Letter

- Excess Summary

- Top Heavy Section

Current application includes many failure-related pages.

TASKS

1. Review the following files:

services/orchestrator.py

services/pdf_extractor.py

services/rules_engine.py

services/action_required.py

services/package_builder.py

services/file_order.py

services/plan_profile_service.py

models/plan_profile.py

config/field_patterns.py

config/rules.yaml

config/403b.yaml

config/sections.yaml

config/package_map.yaml

config/paragraphs.yaml

2. Produce a report showing:

Business Rule

Source Field

Code Location

Current Logic

Expected Logic

Gap

3. Verify every field source.

Use this source-of-truth matrix:

Excel Fields:

- plan_type

- hce_current

- hce_future

- top_heavy

- acp_method

- acp_reclassified

- annual_allocation

Result Summary Fields:

- adp_pass_fail

- acp_pass_fail

- fail_402g

- fail_415

- fail_410b

- top_heavy_percent

ACP Report:

- QNEC amounts

- returns required

402(g) Report:

- after_4_15 exception

Variance Report:

- existence only

4. Validate these rules:

Rule A:

If ACP Pass:

remove ACP failure notices

remove ACP sample letters

remove ACP return letters

Rule B:

If 402(g) Pass:

remove 402(g) sample letter

Rule C:

If 415 Pass:

remove 415 sample letter

remove 415 failure information

Rule D:

If Top Heavy = "403b N/A":

remove Top Heavy section

Rule E:

If no failures exist:

Action Required page must contain only:

"NO IMMEDIATE ACTION REQUIRED"

Rule F:

403(b) plans:

- ADP bookmarks should not be created

- HCE/KEY becomes HCE

- ACP bookmark instead of ADP/ACP bookmark

- missing detailed 410(b) report is allowed

Rule G:

Filename must use beginning plan year:

07/01/2025 - 06/30/2026

=> 2025

5. Trace the exact decision path for:

Plan 800643

Produce:

{

  "plan_type": "...",

  "hce_current": ...,

  "hce_future": ...,

  "top_heavy": ...,

  "acp_method": "...",

  "acp_failed": ...,

  "fail_402g": ...,

  "fail_415": ...,

  "returns_required": ...,

  "selected_sections": [...],

  "removed_sections": [...]

}

6. Look for logic that:

- includes pages merely because a PDF exists

instead of

- including pages because the business rule says to keep them

7. Generate a code fix plan with exact file names, functions, and code locations that need modification.

Do not make assumptions.

Trace values from extraction -> PlanProfile -> Rules Engine -> Assembly.

---------------

Add debug logging to the valuation assembly process.

Before assembly, generate profile_debug.json containing:

{

  "plan_type": "",

  "testing_method": "",

  "hce_current": false,

  "hce_future": false,

  "top_heavy": false,

  "top_heavy_percent": null,

  "adp_failed": false,

  "acp_failed": false,

  "fail_402g": false,

  "fail_415": false,

  "returns_required": false,

  "variance_report": false,

  "contributions_required": false,

  "fail_402g_after_deadline": false,

  "selected_sections": [],

  "removed_sections": []

}

Output this file for every assembly run.

Then trace exactly why each section was included or excluded.
