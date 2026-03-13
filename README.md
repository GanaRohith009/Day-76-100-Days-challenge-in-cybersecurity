# Day-76-100-Days-challenge-in-cybersecurity
## Day 76: JS-Based Token Validation Bypass

### Objective
To demonstrate how client-side token generation can be reverse-engineered and bypassed if not properly validated on the server.

### Lab Environment
* **Platform:** DVWA (Damn Vulnerable Web Application)
* **Tools:** Browser DevTools, Burp Suite (Repeater), MD5/ROT13 Generators.

### Execution Steps
1. **Initial Recon:** Attempted to modify the `phrase` parameter in a POST request. The server returned an `Invalid Token` error.
2. **Code Inspection:** Analyzed the frontend JavaScript. Found a function that takes the input phrase and processes it:
   * **Step A:** Apply `ROT13` substitution.
   * **Step B:** Apply `MD5` hashing to the result.
3. **Manual Validation:** Used the default phrase "changeme" to verify the logic.
   * `ROT13("changeme")` ➔ `punatrzr`
   * `MD5("punatrzr")` ➔ Matches the token observed in the request.
4. **Exploitation:**
   * Created a new payload.
   * Generated a corresponding MD5(ROT13(payload)) token.
   * Injected both into the request via Burp Suite.
   * **Result:** Validation Bypassed.

### Conclusion
This lab reinforces the principle that **the client is untrusted territory.** All security-critical logic—especially integrity checks and authentication—must be performed on the server.
