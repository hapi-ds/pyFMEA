# Why pyFMEA?
Why do you need a Python module for an FMEA when there are plenty of Excel templates available?

Yes, you have to elaborate a bit and go into detail here. The "modern" FMEA, according to the AIAG handbook, consists of 7 steps:

1. Planning
2. Structure Analysis
3. Function Analysis
4. Failure Analysis
5. Risk Analysis and Prioritization
6. Optimization
7. Results Documentation

The aforementioned Excel templates fulfill all these functions in one. This also allows for very good management (assessment and tracking) of risks. However, the failure analysis itself is no longer as easily achievable as it originally was – even before Excel existed. This might be surprising, as the tabular format also comes from the original, very effective FMEAs – but there's a small, yet very significant difference. The original idea behind FMEA was to break down the problem – starting from a design element or a function of a part/process – into very small and therefore manageable "chunks" and to proceed only in small steps. The following scheme was used for this:

- Step 1: Copy the blank table template (only the header is filled in).
- Step 2: Enter exactly ONE (obvious/first) failure into the "Failure" column.
- Step 3: Based on this one failure, enter all possible failure effects that come to mind into the "Failure Effect" column.
- Step 4: Based on this one failure, enter all possible failure causes into the "Failure Cause" column.
- Step 5: Take a new, blank table template (header is filled in).
- Step 6: Transfer one of the identified failure causes or failure effects into the "Failure" column and then, as in Step 3 and 4, fill in the "Failure Effect" and "Failure Cause" columns for this one failure.
- Step 7: Repeat Step 5 for each of the failure effects and failure causes from the first sheet.
- Step 8: Repeat Step 5 for all sheets until you reach a failure cause or failure effect that requires no further iteration.

This results in a very detailed analysis. All failures, failure effects, and failure causes are "comprehensible" and can also be checked for completeness and supplemented by others, page by page. The problem with this, in turn, is that you have many failure chains spread across many sheets, which are then difficult to assess or manage. So, you have to choose between a rock and a hard place.

A common remedy is to carry out the failure analysis using other tools – for example, creating an Ishikawa diagram for each line.

With pyFMEA, I am trying to re-enable the original form of failure analysis while also preserving all the steps of the modern FMEA process without increasing the effort involved. The basic idea is to use a PDF form for entering failure effects and causes for ONE failure. The PDF is then iteratively supplemented with the identified FEs & FCs as new failure input forms.

In detail, I have envisioned the following workflow:

- In the first step, a Word template is filled out. This contains all the basic information (corresponding to FMEA steps 1 to 3).
- In the next step, pyFMEA generates the first version of the FMEA PDF from the word-file, which contains a form page for each listed focus function/process into which the primary failures can be entered.
- In the next pyFMEA call, a failure-form-page is generated for each identified failure, into which FEs and FCs can be entered.
- The next call, in turn, generates further new failure-form-pages for all found FEs and FCs as failures where new FEs and FCs can be inserted.
- The previous step is repeated until, finally, the last FE or FC is reached (marked in form).
- At this point, the failure chains are exported to a standard Excel FMEA template, in which the assessment and tracking are carried out.

Additional functions such as exporting to JSON, NetworkX, etc., and a mechanism for revising/updating the risk analysis are planned.
