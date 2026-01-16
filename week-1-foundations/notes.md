# Week 1 — Foundations (Notes)

## Table of contents
- [Day 1 - Yahoo login page](#day-1---yahoo-login-page)
  - [What I learned](#what-i-learned)
  - [Validation observation (Yahoo)](#validation-observation-yahoo)
## Day 1 - [Yahoo login page](https://login.yahoo.com/?.src=ym&pspid=159600001&activity=mail-direct&.lang=en-GB&.intl=uk&.done=https%3A%2F%2Fuk.mail.yahoo.com%2Fd%2Flogin)
### What I learned
- Write from an outside perspective (“User is redirected…”, not “I…”)  
- Include steps when needed (especially for anything involving sessions like “Stay signed in”)  
- Avoid colour-based assertions (“red text”) — say “error message shown near field”  
- Don’t speculate (“perhaps/usually”) — write only what I can verify  
- Avoid browser-dependent claims (autofill/field clearing) unless explicitly testing the browser  
- Keep each test focused on one behaviour  
- Prefer observable outcomes: stays on page / can’t proceed / error shown / redirects

### Validation observation (Yahoo)
- Empty input and invalid-format input returned the same message (“Sorry, we don’t recognise this email address.”)
- Expected would usually differ:
  - Empty: “Enter your email/username”
  - Invalid format: “Enter a valid email address”

# Week 1 — Foundations (Notes)

## Today’s learnings

1. **Be precise about observable outcomes**  
   Tests should avoid vague destinations such as “next page” or “home page”. Outcomes are stronger when they are anchored to observable states, such as a visible signed-in indicator, an error message being shown, or the page not changing.

2. **Avoid ambiguous wording such as “works” or “step”**  
   Terms like “button works” or “remains on step” do not clearly describe behaviour. Clear tests state exactly what action occurs and what does not occur.

3. **Match expected results to actual system behaviour**  
   Expected results should reflect what the system does, not an assumed validation message or mechanism. Correct behaviour can still be mismatched with an inaccurate expectation.

4. **Separate test idea quality from execution quality**  
   Test execution can be correct even when test wording needs improvement. Writing clear, neutral, testable cases is a distinct skill from running the tests themselves.

5. **Small wording changes can significantly improve test strength**  
   Minor adjustments—removing ambiguity, tightening scope, or clarifying outcomes—can materially improve test quality without requiring a full rewrite.
