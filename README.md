# Stored Cross-Site Scripting (XSS) in Tag Field

<table>
  <tr>
    <td width="150" rowspan="2">
      <a href="https://github.com/mistio/mist-ce" target="_blank">
        <img src="https://avatars.githubusercontent.com/u/1569127?s=200&v=4" alt="Summer Pearl Logo" width="120"/>
      </a>
    </td>
    <td>
      <h1>Mist Community Edition</h1>
      <h3> An Open-Source Multicloud Management Platform</h3>
    </td>
  </tr>
  <tr>
    <td>
      <table>
        <tr>
          <td>
            🔗 <a href="https://github.com/mistio/mist-ce" target="_blank">Mist Github Repository</span></a>
          </td>
          <td style="padding-left: 15px;">
            🚀 <a href="https://github.com/mistio/mist-ce/releases/tag/v4.7.2" target="_blank"> Patched Version (v4.7.2) </span></a>
          </td>
        </tr>
      </table>
    </td>
  </tr>
</table>

## 📜 Description
Mist Community Edition (CE) versions prior to 4.7.2 fail to sanitize user-controlled input in tag value fields across multiple resource types, including Machines, Volumes, Zones, Images, Keys, and Scripts. Authenticated attackers can inject persistent JavaScript payloads via crafted tags, which execute automatically when victims view affected resources in the web interface.

## 🔍 Affected Versions

| Status       | Version         |
|--------------|-----------------|
| 🔴 Vulnerable |  ≤ `4.7.1`      |
| 🟢  Fixed     |  &nbsp;&nbsp;`4.7.2`      |   

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

This vulnerability was discovered by **Alex Perrakis** (Stolichnayer).

## 🔗 References:
- [Mist CE Github Repository](https://github.com/mistio/mist-ce)
- [Patched Version (v4.7.2)](https://github.com/mistio/mist-ce/releases/tag/v4.7.2)
- [Fix Commit](https://github.com/mistio/mist.api/commit/db10ecb62ac832c1ed4924556d167efb9bc07fad)

