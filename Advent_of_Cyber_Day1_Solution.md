# Advent of Cyber Day 1: Authentication Bypass Guide

## Walkthrough

### 1. Identification
- Open the target website.
- Right-click -> **Inspect** (or press `F12`).
- Go to the **Storage** tab (Firefox) or **Application** tab (Chrome).
- Look under **Cookies** and identify the session cookie.

### 2. Analysis (Decoding)
- Copy the cookie value.
- Identify the encoding (e.g., Hexadecimal).
- Decode it (e.g., using CyberChef).

### 3. Manipulation (Tampering)
- View the decoded data (JSON).
- Change the `username` field to `santa`.

### 4. Re-Encoding
- Encode the modified JSON string back into the original format (Hexadecimal).

### 5. Exploitation
- Replace the browser's cookie value with the new string.
- Refresh the page.

---

## Challenge Answers

*   **What is the name of the cookie used for authentication?**  
    `auth`
*   **In what format is the value of this cookie encoded?**  
    `Hexadecimal`
*   **Having decoded the cookie, what format is the data stored in?**  
    `JSON`
*   **What is the value of Santa's cookie?**  
    `7b22636f6d70616e79223a22546865204265737420466573746976616c20436f6d70616e79222c2022757365726e616d65223a2273616e7461227d`
*   **What is the flag you're given when the line is fully active?**  
    `THM{MjY0Yzg5NTJmY2Q1NzM1NjBmZWFhYmQy}`
