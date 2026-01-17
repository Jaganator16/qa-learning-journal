# Week 1 — Examples

## Table of contents
- [Day 1 — Yahoo login page](#day-1--yahoo-login-page)
  - [Test ideas (v1 — my first draft)](#test-ideas-v1--my-first-draft)
  - [Test ideas (v2 — refined with AI feedback)](#test-ideas-v2--refined-with-ai-feedback)
  - [Executed tests](#executed-tests)
  - [Bug report](#bug-report)
- [Day 2 - Lidl login page](#day-2---lidl-login-page)
  - [Test ideas](#test-ideas)
  - [Executed tests](#executed-tests-1)
  - [Bugs](#bugs)
  - [Items that need rewriting](#items-that-need-rewriting)
- [Day 3 — Thomann contact page](#day-3--thomann-contact-page)
  - [Test ideas](#test-ideas-2)
  - [Review notes (rewritten / reviewed by AI)](#review-notes-rewritten--reviewed-by-ai)
  - [Executed tests](#executed-tests-2)
  - [Review: step rewrite rationale](#review-step-rewrite-rationale)  
  
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

## Day 2 - [Lidl login page](https://accounts.lidl.com/Account/Login?ReturnUrl=%2Fconnect%2Fauthorize%2Fcallback%3Fcountry_code%3DGB%26response_type%3Dcode%26client_id%3Dgreatbritainretailclient%26scope%3Dopenid%2520profile%2520Lidl.Authentication%2520offline_access%26state%3DFFVZM63x2SMloHHWpLTH0hxg8kFHXuKfuiDHuDS0Kvs%253D%26redirect_uri%3Dhttps%253A%252F%252Fwww.lidl.co.uk%252Fuser-api%252Fsignin-oidc%26nonce%3DdhYeqjREegv9rzcMhR_EF64LIS9rqTibZJ_lf3RRJSA%26step%3Dlogin%26language%3Den-GB#login)


---

## Test ideas

### Positive

1. **Test:** Enter valid username and password  
   **Expected:** User is authenticated and taken to Lidl home page

2. **Test:** Log in with your phone number button works  
   **Expected:** User is taken to a phone number log in page

3. **Test:** "Forgot password" link works  
   **Expected:** User is taken to a password recovery page where an email or phone number is required

4. **Test:** Register link works  
   **Expected:** User is taken to an account creation page

5. **Test:** Show your password button works  
   **Expected:** When clicked, password is toggled from readable to hidden

### Negative

1. **Test:** Click log in with empty username  
   **Expected:** Validation is shown and the user is not taken to the next page

2. **Test:** Invalid username/format  
   **Expected:** Validation is shown and the user is not taken to the next step

3. **Test:** Incorrect password is entered  
   **Expected:** Account is not authenticated, error message displays, user remains on step

4. **Test:** Register with credentials already associated with an account  
   **Expected:** Validation shows username is already in use, user does not proceed

---

## Executed tests

### Test: Incorrect password is entered
**Steps:** Enter valid email, enter incorrect password  
**Expected:** Account is not authenticated, error message displays, user remains on step  
**Result:** PASS — User does not proceed. Validation reads:  
> “Invalid email or password incorrect. Try again or select ‘Forgot your password?’”

---

### Test: Register with credentials already associated with an account
**Steps:** Click Register, enter email address, enter password, click Next  
**Expected:** Validation shows username is already in use, user does not proceed  
**Result:** PASS — User is taken to a page that says:

> This email is already registered to a Lidl Plus account  
> Please log in, or if you haven’t already registered with jagobouffler@gmail.com, please contact Customer Care.

Buttons shown:
- Log in
- Contact Customer Care

---

### Test: Log in with your phone number button works
**Steps:** Click the Log in with your phone number button  
**Expected:** User is taken to a phone number log in page  
**Result:** PASS — User is taken to a page where they enter their phone number, then their password

---

## Bugs
No bugs to report.

---

## Items that need rewriting

### Positive 1

**Rewritten test:** Log in with valid email/username and password  
**Expected:** User is authenticated and a signed-in state is visible (e.g., account page loads or user menu shows the user is signed in).  

**Why:**  
“Taken to Lidl home page” may not be the actual redirect target; using an observable signed-in indicator makes it testable across different return URLs.

---

### Positive 3

**Rewritten test:** “Forgot your password?” link navigates to password recovery  
**Expected:** User is taken to a password recovery page where they can start reset using an email address or phone number (as offered).  

**Why:**  
Clarifies observable destination and avoids over-specifying exactly what’s required if the page options vary.

---

### Positive 5

**Rewritten test:** “Show password” control toggles password visibility  
**Expected:** Clicking toggles the password field between masked and visible, and the control state changes accordingly (e.g., icon/label).  

**Why:**  
Current expected outcome is reversed (“toggled from readable to hidden”); also adding a visible indicator makes it clearly observable.

---

### Negative 1

**Rewritten test:** Attempt login with empty username/email and any password state  
**Expected:** Inline validation is shown for the username/email field and login does not proceed (user remains on the login page).  

**Why:**  
“Click log in with empty username” is vague; specifying the observable validation and that navigation does not occur improves testability.

---

### Negative 2

**Rewritten test:** Enter an invalid email/username format and attempt login  
**Expected:** Format validation is shown (if supported) and login does not proceed.  

**Why:**  
“Invalid username/format” is unclear; making it explicitly about format and observable validation improves clarity.

---

### Negative 3

**Rewritten test:** Attempt login with valid email/username and incorrect password  
**Expected:** Authentication fails, an error message is displayed, and user remains on the login page.  

**Why:**  
“User remains on step” is ambiguous; “remains on the login page” is observable.

---

### Negative 4

**Rewritten test:** Attempt to register with an email already associated with an account  
**Expected:** User is prevented from completing registration and is shown a clear message that the email is already registered, with a path to log in or contact support (if offered).  

**Why:**  
“Validation shows username is already in use” may not match the actual message (email-based); this keeps it accurate and observable.

---

### Executed test wording tweak

**Executed:** Incorrect password is entered  

**Rewritten result statement (optional clarity only):**  
PASS — Login did not proceed; error message displayed and user remained on the login page.

**Why:**  
Replaces “not taken to next page” with an observable state.

Everything else looks clear and testable, and no new tests were added since nothing critical is missing for this set.

## Day 3 — [Thomann contact page](https://www.thomann.co.uk/compinfo_contact.html)

---

## Test ideas

### Positive

1. **Test:** Accordion control toggles sections  
   **Expected:** Clicking on the header for each section of the accordion closes and reopens that section.

2. **Test:** Log in button leads to log in page  
   **Expected:** The user is taken to a log in page after clicking the log in button.

3. **Test:** Normally open accordion is open after refresh  
   **Expected:** When the user refreshes the page, any sections of the accordion that were closed should reopen.

4. **Test:** “Closed” sign updates during the companies opening hours  
   **Expected:** During the closed hours, the sign says “Closed”; during the opening hours listed in the section, the sign will say “Open”.

5. **Test:** Selecting product categories updates photos, numbers and emails  
   **Steps:** User clicks on the category, a dropdown appears, the user selects a different category.  
   **Expected:** The user sees different photos of that category’s specialists, with their phone number and email.

6. **Test:** Email links lead to mailto:  
   **Expected:** The user clicks on an email link and is lead to their default service in a compose mail box with the “To” section filled.

7. **Test:** Specialist department links lead to individual page  
   **Expected:** The user clicks on a specialist department link (e.g. Drums) and is taken to a page specific to that department.

8. **Test:** Entering a valid phone number in the arrange a return call section  
   **Expected:** Upon entering a valid phone number according to the region chosen, the state of the greyed out “Book” button changes and can be clicked.

### Negative

1. **Test:** State of Open/Closed sign after changing system time settings  
   **Expected:** The sign does not rely on the user’s time settings and remains the same.

2. **Test:** Invalid telephone number is entered in arrange a return call  
   **Expected:** Format validation is shown and the “Book” button remains greyed out.

3. **Test:** Enter an invalid customer number in the arrange a return call section  
   **Expected:** Format validation is shown and the user cannot proceed.

---

## Review notes (rewritten / reviewed by AI)

### Positive

1. **Accordion control toggles sections — Acceptable**  
   **Expected:** Clicking on the header for each section of the accordion closes and reopens that section.

2. **Log in button leads to log in page — Acceptable**  
   **Expected:** The user is taken to a log in page after clicking the log in button.

3. **Normally open accordion is open after refresh — Needs change**  
   **Revised expected:** When the user refreshes the page, any accordion sections that were closed are open again.  
   **Why:** Keeps the original intent but makes the expected state explicit and directly observable.

4. **“Closed” sign updates during the companies opening hours — Needs change**  
   **Revised expected:** Outside the listed opening hours the sign shows “Closed”; during the listed opening hours it shows “Open”.  
   **Why:** Fixes grammar and removes repetition while keeping the same behaviour.

5. **Selecting product categories updates photos, numbers and emails — Needs change**  
   **Revised steps:** Click the category, open the dropdown, select a different category.  
   **Revised expected:** Photos and contact details (phone number and email) update to match the selected category.  
   **Why:** Steps were unclear and the expected result is more observable without relying on examples.

6. **Email links lead to mailto: — Needs change**  
   **Revised expected:** Clicking an email link opens the default email app with a new draft and the “To” field pre-filled.  
   **Why:** Corrects phrasing and improves observability.

7. **Specialist department links lead to individual page — Acceptable**  
   **Expected:** The user clicks on a specialist department link (e.g. Drums) and is taken to a page specific to that department.

8. **Entering a valid phone number in the arrange a return call section — Needs change**  
   **Revised expected:** Entering a valid phone number for the selected region enables the “Book” button so it can be clicked.  
   **Why:** Makes the observable change explicit rather than relying on colour.

### Negative

1. **State of Open/Closed sign after changing system time settings — Needs change**  
   **Revised expected:** Changing the user’s system time does not change the Open/Closed sign state.  
   **Why:** Makes the assertion direct and observable.

2. **Invalid telephone number is entered in arrange a return call — Needs change**  
   **Revised expected:** Format validation is shown and the “Book” button remains disabled.  
   **Why:** “Disabled” is more testable than colour-based assumptions.

3. **Enter an invalid customer number in the arrange a return call section — Acceptable**  
   **Expected:** Format validation is shown and the user cannot proceed.

---

## Executed tests

### Test: State of Open/Closed sign after changing system time settings
**Steps:** Change the user’s system time settings, return to the page, and refresh.  
**Expected:** Changing the user’s system time does not change the Open/Closed sign state.  
**Result:** PASS

### Test: Enter an invalid customer number in the arrange a return call section
**Steps:** Enter an invalid customer number, deselect the box.  
**Expected:** Format validation is shown and the user cannot proceed.  
**Result:** PASS

### Test: Normally open accordion is open after refresh
**Steps:** Close all accordion sections, refresh the page, observe the state of the accordion.  
**Expected:** When the user refreshes the page, any accordion sections that were closed are open again.  
**Result:** PASS

---

## Review: step rewrite rationale

### Test: State of Open/Closed sign after changing system time settings — Needs change

**Issue:**  
The original steps included aligning the system time zone and time to match Thomann’s opening hours, introducing unnecessary complexity and weakening the assertion.

**Revised steps:**  
Change the user’s system time settings, return to the page, and refresh.

**Why:**  
The test intent is to verify that the sign does not rely on the user’s system time. Matching the opening hours risks contradicting that intent and makes the test harder to reason about.
