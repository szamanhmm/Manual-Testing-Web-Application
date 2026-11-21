# Test Case Specification Template

### Test Suite: Authentication & Account Security
**Module:** User Sign-up & Email Validation  
**Author:** Saifuz Zaman (QA Lead)  
**Execution Type:** Manual Functional Testing  

---

| Test Case ID | Test Scenario | Pre-conditions | Test Steps | Test Data | Expected Result | Actual Result | Status |
| :---: | :--- | :--- | :--- | :--- | :--- | :--- | :---: |
| `TC_AUTH_01` | Verify valid registration with standard credentials | User not logged in; landing on `/signup` | 1. Enter valid email.<br>2. Enter compliant password.<br>3. Click "Sign Up". | Email: `valid_user@test.com`<br>Pass: `P@ssword123!` | Account created; verification email dispatched; user routed to verify screen. | As expected. | **PASS** |
| `TC_AUTH_02` | Verify password rejection when missing special character | User on `/signup` | 1. Enter valid email.<br>2. Enter password without symbols.<br>3. Click "Sign Up". | Pass: `Password123` | Inline validation error: *"Password must contain at least one special character."* | Error appeared correctly. | **PASS** |
| `TC_AUTH_03` | Verify rejection when entering invalid email syntax | User on `/signup` | 1. Enter email missing domain suffix.<br>2. Enter valid password.<br>3. Submit form. | Email: `user@example` | Form submission prevented; *"Please enter a valid email address"* shown. | Submission blocked; alert shown. | **PASS** |
| `TC_AUTH_04` | Verify system prevents login before email verification | Registered but unverified account exists | 1. Navigate to `/login`.<br>2. Enter unverified credentials.<br>3. Click "Log In". | Account: `unverified@test.com` | Access denied; prompt to verify email with "Resend Verification" link. | Direct access allowed without email verification. | **FAIL** `(Bug B_06)` |
| `TC_AUTH_05` | Verify input behavior on leading/trailing whitespace | User on `/login` | 1. Enter email with leading space.<br>2. Enter correct password.<br>3. Click "Log In". | Email: `  user@test.com` | Email sanitized automatically; login successful. | Login failed with "User not found". | **FAIL** |
| `TC_AUTH_06` | Verify throttling on 5 consecutive failed login attempts | Active registered account | 1. Attempt login with wrong password 5 times. | Pass: `WrongPass1`, `WrongPass2`... | Account locked for 15 minutes; reCAPTCHA triggered. | As expected; account locked. | **PASS** |
