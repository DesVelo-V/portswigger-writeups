# Reflected XSS into HTML Context with Nothing Encoded   > **Lab URL:** https://portswigger.net/web-security/cross-site-scripting/reflected/lab-html-context-nothing-encoded

## Lab Information - **Completed:** July 2026

- **Platform:** PortSwigger Web Security Academy
- **Category:** Cross-Site Scripting (XSS)
- **Difficulty:** Apprentice
- **Status:** Solved ✅

---

# Objective

The objective of this lab was to identify and exploit a Reflected Cross-Site Scripting (XSS) vulnerability in the application's search functionality.

---

# Methodology

## Step 1: Testing User Input Reflection

I started by searching for a normal string to understand how the application handled user input.

**Input**

```text
Yousef
```

I noticed that my input appeared both in the page content and in the URL. This indicated that the application reflected user-controlled input back to the client.

---

## Step 2: Testing HTML Rendering

Since the application reflected my input, I wanted to determine whether it rendered HTML or displayed it as plain text.

**Payload**

```html
<b>Yousef</b>
```

The word **Yousef** appeared in bold, confirming that the browser interpreted my input as HTML rather than displaying it as plain text.

This increased my suspicion that the application might also be vulnerable to Cross-Site Scripting (XSS).

---

## Step 3: Testing JavaScript Execution

After confirming that HTML rendering was possible, I tested whether JavaScript execution was also allowed.

**Payload**

```html
<script>alert(1)</script>
```

The browser displayed an alert dialog, confirming that JavaScript execution was possible.

This verified the existence of a **Reflected Cross-Site Scripting (XSS)** vulnerability.

---

# Proof of Concept

The following payload successfully executed JavaScript in the browser:

```html
<script>alert(1)</script>
```

The successful execution of the payload confirmed the vulnerability.

---

# Root Cause

The application reflects user input directly into the HTML response without applying proper output encoding or sanitization.

As a result, the browser interprets user-controlled input as executable HTML and JavaScript.

---

# Impact

- Execute arbitrary JavaScript in the victim's browser.
- Modify page content.
- Perform phishing attacks.
- Steal sensitive information if additional conditions are met.
- Perform actions on behalf of authenticated users.

---

# Remediation

- Apply proper output encoding.
- Escape HTML special characters before rendering user input.
- Validate and sanitize user input where appropriate.
- Implement a strong Content Security Policy (CSP).

---

# What I Learned

- Reflected input does not always mean an XSS vulnerability.
- Testing HTML rendering is an important step before attempting JavaScript execution.
- Browsers execute injected JavaScript when user input is rendered without proper output encoding.
- Understanding the application's behavior is more valuable than memorizing payloads.

---

## Disclaimer

This write-up was created for educational purposes using the PortSwigger Web Security Academy training platform.

All testing was performed in a controlled lab environment.
