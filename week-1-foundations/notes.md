# Week 1 — Foundations (Notes)

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
