# Week 1 — Foundations (Notes)

## Table of contents
- [Day 1 - Yahoo login page](#day-1---yahoo-login-page)
  - [What I learned in day 1](#what-i-learned-in-day-1)
  - [Validation observation (Yahoo)](#validation-observation-yahoo)
- [Day 2 - Lidl login page](#day-2---lidl-login-page)
  - [What I learned in day 2](#what-i-learned-in-day-2)
- [Day 3 - Thomann contact page](#day-3---thomann-contact-page)
  - [What I learned in day 3](#what-i-learned-in-day-3)
- [Day 4 - James Brown shop](#day-4---james-brown-shop)
  - [What I learned in day 4](#what-i-learned-in-day-4)
- [Day 5 - Hub - St Ives](#day-5---hub---st-ives)
  - [What I learned in day 5](#what-i-learned-in-day-5)
  
---

## Day 1 - [Yahoo login page](https://login.yahoo.com/?.src=ym&pspid=159600001&activity=mail-direct&.lang=en-GB&.intl=uk&.done=https%3A%2F%2Fuk.mail.yahoo.com%2Fd%2Flogin)

### What I learned in day 1
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

---

## Day 2 - [Lidl login page](https://accounts.lidl.com/Account/Login?ReturnUrl=%2Fconnect%2Fauthorize%2Fcallback%3Fcountry_code%3DGB%26response_type%3Dcode%26client_id%3Dgreatbritainretailclient%26scope%3Dopenid%2520profile%2520Lidl.Authentication%2520offline_access%26state%3DFFVZM63x2SMloHHWpLTH0hxg8kFHXuKfuiDHuDS0Kvs%253D%26redirect_uri%3Dhttps%253A%252F%252Fwww.lidl.co.uk%252Fuser-api%252Fsignin-oidc%26nonce%3DdhYeqjREegv9rzcMhR_EF64LIS9rqTibZJ_lf3RRJSA%26step%3Dlogin%26language%3Den-GB#login)

### What I learned in day 2

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

---

## Day 3 - [Thomann contact page](https://www.thomann.co.uk/compinfo_contact.html)

### What I learned in day 3

1. **Do not introduce assumptions during review**  
   Rewrites must not add assumptions about default states or internal behaviour (e.g. accordion defaults). Test intent should be preserved exactly as written unless it is unclear or incorrect.

2. **Prefer common tester language when it is already precise**  
   Terms widely understood in testing contexts can be clearer than technically “correct” alternatives. Replacing familiar phrasing with abstract wording can reduce clarity rather than improve it.

3. **Keep steps aligned with the test’s core assertion**  
   Steps should support the assertion being tested and avoid unnecessary complexity that could weaken or confuse the purpose of the test.

4. **Challenge feedback that does not improve the test**  
   Review feedback should be questioned if it does not clearly increase precision, observability, or reproducibility. Not all suggested changes are improvements.

5. **Clarity is about shared understanding, not formality**  
   A test is clear if another tester can execute it consistently without interpretation, even if the language is informal.

## Day 4 - [James Brown shop](https://shop.jamesbrown.com/products/living-in-america-world-tour-t-shirt-x3ctjb067?variant=42018518401093)

### What I learned in day 4

1. **Avoid mixing step and expected-result wording**  
   Errors occurred when outcomes were labelled as “Revised” instead of clearly being treated as expected results. Keeping steps, expected results, and revisions clearly separated avoids confusion during execution and review.

2. **Use a single, explicit action to submit forms**  
   Phrases like “click to proceed” caused ambiguity. Tests are clearer when the submission action is stated once and unambiguously (e.g. “submit the form”).

3. **Keep terminology consistent within a test**  
   Inconsistent terms (e.g. “news letter” vs “newsletter”) can introduce uncertainty. Using one consistent label throughout improves clarity and reduces interpretation errors.

---

 ## Day 5 - Hub - St Ives

### What I learned in day 5

- Test failures are not automatically bugs; they often need validation before being promoted.
- Bug reports should focus on observable behaviour, not assumptions or intent.
- Removing irrelevant detail (e.g. “fake” data) improves clarity and reproducibility.
- Clear expected vs actual behaviour is more important than perfect certainty.
- Writing assumed bugs is still valuable practice for structure and precision.
- **Expected results should state a blocking condition when testing enforcement**  
  When testing verification or security, expectations should clearly state what action is prevented until a condition is met.  
