# Week 1 — Examples

## Table of contents
- [Day 1 — Yahoo login page](#day-1---yahoo-login-page)
  - [Test ideas (v1 — my first draft)](#test-ideas-v1--my-first-draft)
  - [Test ideas (v2 — refined with AI feedback)](#test-ideas-v2--refined-with-ai-feedback)
  - [Executed tests](#executed-tests)
  - [Bug report](#bug-report)
  
## Day 1 - [Yahoo login page](https://login.yahoo.com/?.src=ym&pspid=159600001&activity=mail-direct&.lang=en-GB&.intl=uk&.done=https%3A%2F%2Fuk.mail.yahoo.com%2Fd%2Flogin)

### Test ideas (v1 — my first draft)

Positive tests:

Test 1: Log in with correct email and password  
Expected: I'm logged in and taken to the home page

Test 2: Log in and click stay signed in  
Expected: After closing the tab and opening a new one, going to the log in page should be skipped straight to the home page

Test 3: Click Forgotten password  
Expected: Taken to a page or form where an email or phone number is entered, for a reset password link or form to be sent to the user

Test 4: Click Forgotten username  
Expected: Taken to page or form to enter a recovery email

Test 5: Click create an account  
Expected: Taken to a page where you enter all the necessary details to make an account

Test 6: Log in without ticking stay signed in  
Expected: After deleting the tab, opening a new tab and going to this page you should be expected to log in again, with no fields being auto filled.

Negative tests:

Test 7: Click next with no email or username entered  
Expected: Either a greyed out (unclickable) next button, or a "username required" message to appear in or above the username box

Test 8: Enter invalid username  
Expected: The username box to be cleared with a message in red appearing above or within saying "Incorrect username" or "user not found"

Test 9: Enter incorrect password  
Expected: The password box to be cleared with a message appearing above in red saying "incorrect password", multiple attempted create a countdown of attempts left until it is restricted with reset password (usually below) being the only option. Perhaps an email sent out to the user saying "attempted log in, was this you?".

Test 10: Create a new account with already used credentials  
Expected: After entering details and clicking create account, red text appears above the create account button and the username box saying "Account already in use" with a button for sign in and possibly forgotten password appearing


### Test ideas (v2 — refined with AI feedback)

#### Positive
1. Sign in with valid username + valid password  
   Expected: User is authenticated and redirected to Yahoo Mail (or the configured destination page).

2. Stay signed in enabled persists session  
   Steps: Sign in with “Stay signed in” checked → close browser → reopen → go to Yahoo Mail.  
   Expected: User remains signed in (no prompt to enter credentials).

3. Forgotten password link works  
   Expected: Navigates to password recovery flow (prompts for identifier and next steps).

4. Forgotten username link works  
   Expected: Navigates to username recovery flow (prompts for recovery method/details).

5. Create an account link works  
   Expected: Navigates to account creation/registration page.

6. Stay signed in disabled does not persist session  
   Steps: Sign in with “Stay signed in” unchecked → close browser → reopen → go to Yahoo Mail.  
   Expected: User is prompted to sign in again (no automatic authentication).

#### Negative
7. Click Next with empty username/email  
   Expected: Validation shown and user does not proceed to password step.

8. Enter invalid username/email format (e.g., `jago@`)  
   Expected: Validation shown for invalid format and user does not proceed.

9. Valid username + incorrect password  
   Expected: Error message shown; user remains on password step; account is not authenticated.

10. Create account with already-used identifier (on sign-up page)  
    Expected: Inline error indicates identifier is already in use; user cannot complete registration.

### Executed tests
Environment:
- Desktop: Chrome, macOS Sequoia 15.5, VPN ON, adblockers ON

Constraint:
- Account creation blocked during phone verification on desktop, so tests requiring an existing account could not be executed.

#### Test: Forgotten username link works
Result: PASS  
Notes: Navigates to account recovery page (“Let’s find your account”), prompts for recovery email.

#### Test: Click Next with empty username/email
Result: PASS (behaviour observed)  
Notes: Message shown: “Sorry, we don’t recognise this email address.”

#### Test: Enter invalid username/email format (e.g., `john@`)
Result: PASS (behaviour observed)  
Notes: Message shown: “Sorry, we don’t recognise this email address.”

### Bug report
Title: Account creation fails at phone verification on desktop; iOS proceeds but SMS not received

Steps:
1. Go to Yahoo sign up
2. Enter valid details until the “Add your phone number” step
3. Enter a valid phone number
4. Click “Receive code by text”

Expected:
A 6-digit verification code is sent by SMS and the user can enter it to continue sign-up.

Actual:
- Desktop (Chrome + Edge): Error page shown (“Something went wrong… We could not sign you in… Try again from a different device.”). User cannot proceed.
- iOS (Chrome): User can reach the step and press “Receive code by text”, but no SMS code is received.

Environments tested:
1) Desktop — Chrome — macOS Sequoia 15.5 — VPN ON — adblockers ON — 18:15  
2) Desktop — Edge — macOS Sequoia 15.5 — VPN OFF — adblockers OFF — 18:20  
3) Phone — Chrome — iOS 18.6.2 — VPN ON — 18:30  

Additional info:
- Tried twice with one number and twice with another
- No SMS received on either number; other texts arrive normally

Evidence:
- Screenshots: `week-1-foundations/screenshots/yahoo-signup-error-chrome.png` & `week-1-foundations/screenshots/yahoo-signup-error-edge.png`
- URL contained `/account/challenge/fail`
