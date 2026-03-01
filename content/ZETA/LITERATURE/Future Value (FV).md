---
connections:
reference: "[[Spreadsheet Formulas for Personal Finance]]"
tags:
  - type/note
  - theme/personal-finance
type: literature_note
created: 2025-12-03 22:20
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

> Given an initial sum, an interest rate, a periodic payment and a duration, what will the balance be after the last payment?

$$
FV = PV\times (1+r)^{nt}
$$
- FV = future value
- PV = present value
- $r$ = interest rate per period
- $n$ = number of periods
- $t$ = time in years

In Excel it can be used like this: `FV(rate, nper, pmt, pv, type)`

---

#flashcards/personal-finance

What is FV?::Future Value

What is Future Value used for?::Balance after the last payment given a duration, a periodic payment and the interest rate