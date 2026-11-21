# Standard Jira Defect Ticket Template

Copy and paste this template into Jira / GitHub Issues when logging defects:

---

```markdown
### Summary
[What Happens] on [Screen / Component] when [User Action / Condition]

---

### Issue Details
- **Issue Type:** [Functional | GUI | Performance | Security]
- **Severity:** [Critical | Major | Medium | Minor]
- **Priority:** [P1 - Blocker | P2 - High | P3 - Medium | P4 - Low]
- **Target Platform:** [Web | Android | iOS | Chrome Extension]
- **Tested Build / Release:** v1.4.2-staging (Commit: abc1234)

---

### Environment
- **Device Model:** Samsung Galaxy S23+ / PC Desktop
- **Operating System:** Android 14 (OneUI 6.0) / Windows 11 Pro 23H2
- **Browser:** Google Chrome Version 145.0.7632.117 (Official Build) (64-bit)
- **Network Condition:** Stable Wi-Fi / Throttled Fast 3G / Cellular LTE

---

### Pre-conditions
1. User has an active account on `staging-app.example.com`.
2. User is logged in under the `Trial Plan`.
3. Shopping cart contains at least 1 item.

---

### Steps to Reproduce
1. Navigate to `https://staging-app.example.com/checkout`.
2. Enter valid billing details.
3. In the coupon input field, paste test promo code `DISCOUNT_100`.
4. Click on the **"Apply Code"** button.
5. Immediately click on **"Proceed to Payment"**.

---

### Expected Result
The coupon should be validated or return an error alert, and the user should be routed to payment processing without unexpected errors.

---

### Actual Result
The application freezes on a white screen with an unhandled runtime exception: `TypeError: Cannot read properties of undefined (reading 'discountAmount')`. Console logs indicate an unhandled 500 internal server error.

---

### Test Data Used
- User Account: `test_qa_tier1@domain.com`
- Test Card: `4242 4242 4242 4242`
- Promo Code: `DISCOUNT_100`

---

### Attachments & Evidence
- Screenshot: `[Attached: error_console_trace.png]`
- Screen Recording: `[Attached: bug_reproduction_flow.mp4]`
```
