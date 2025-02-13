# CVE-2025-MIST-XSS  
## Stored Cross-Site Scripting (XSS) in Tag Field

## 📜 Description
**Mist Community Edition (CE) v4.7.1** contains a **Stored Cross-Site Scripting (XSS)** vulnerability within its tag functionality. Mist resources, including **Machines, Volumes, Zones, Images, Keys, and Scripts**, support user-defined tags in key-value format. The vulnerability resides in the **value field** of these tags, where malicious JavaScript code can be injected and persistently stored. When a user views the resource listing page, the injected script is executed due to the application’s failure to properly sanitize user input.

## 📌 Affected Version
- Mist Community Edition (CE) v4.7.1
- Other versions prior to v4.7.1 may also be affected

## ⚠️ Disclaimer
This project is intended for **educational and ethical research purposes only**. Unauthorized testing on systems without explicit permission is illegal. Use responsibly and only on systems you own or have permission to test.

## 💻 Exploit Details

### 🔹 **Stored XSS Exploitation**
The injected script remains stored within the Mist interface and is triggered when an authenticated user navigates to the resource listing page. This can lead to:
- **Automatic JavaScript execution in the victim’s browser**
- **Session hijacking and user impersonation**
- **Potential privilege escalation and persistent access**

## 🛠️ Steps to Reproduce

### 1️⃣ Insert Malicious Payload into a Tag
For example, add the following payload as a **tag value** within a Mist resource:
```html
<iframe src="javascript:alert('Clouds')"></iframe>
```
<img src="/assets/mist_adding_xss.png" width="700">

### 2️⃣ Save Tag
- Click the **Save** button to store the tag.
- The malicious payload is now stored within the Mist resource.

<img src="/assets/mist_tag_1.png">

### 3️⃣ Trigger the Exploit
- Navigate to the **resource listing page** where the tag is displayed.
- The payload executes automatically, triggering the JavaScript.
- This vulnerability can be combined with **CSRF attacks** for further exploitation.
  
<img src="/assets/mist_xss_alert.png" width="700">

## 🎬 Demonstration Video

<a href="https://www.youtube.com/watch?v=HNcb-oYFdVg" target="_blank">
  <img src="https://img.youtube.com/vi/HNcb-oYFdVg/maxresdefault.jpg" width="700" height="380"/>
</a>

## 🧑‍💻 Discovery
The **CVE-2025-XXXX** vulnerability was discovered by **Alex Perrakis (Stolichnayer)**.

## 🔗 **References:**
- [Mist CE Github Repository](https://github.com/mistio/mist-ce)

