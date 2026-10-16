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
