<div align="center">
<a href="https://github.com/auveggry/Linux-Heimdall">
<img src="https://ptpimg.me/my2mi2.jpg" alt="Artwork of Heimdall, the guardian god in Norse mythology" style="max-width: 800px; width: 100%; border-radius: 8px;">
</a>
<br><br>
<h3 style="color: #6BDBAD;">Project's Name: The Intersection of Mythology and Technology</h3>
<p>In Norse mythology, the guardian god Heimdall is known for his extraordinary perception and vigilance. This project is named after him to emphasize its core mission:<br>To build a tireless, all-seeing, and rapidly responsive ultimate guardian for the Linux kernel.</p>
<h1>Project Heimdall</h1>
<h2>Linux Heimdall</h2>
</div>

<div align="center">
<a href="https://github.com/auveggry/Linux-Heimdall/blob/main/LICENSE" target="_blank">
<img src="https://img.shields.io/badge/license-GPLv3-blue.svg?style=for-the-badge" alt="License">
</a>
<a href="https://github.com/auveggry/Linux-Heimdall/pulls" target="_blank">
<img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge" alt="PRs Welcome">
</a>
<a href="#" target="_blank">
<img src="https://img.shields.io/badge/Linux%20Kernel-6.18.1-orange?style=for-the-badge" alt="Kernel Version">
</a>
<a href="https://github.com/auveggry/Linux-Heimdall" target="_blank">
<img src="https://img.shields.io/badge/GitHub-Stars-informational?style=for-the-badge" alt="GitHub stars">
</a>
<br>
<a href="README_zh-CN.md" target="_blank">
<img src="https://img.shields.io/badge/Read%20in%20Chinese-brightgreen.svg?style=for-the-badge" alt="Chinese Version">
</a>
<a href="README_ja-JP.md" target="_blank">
<img src="https://img.shields.io/badge/Read%20in%20Japanese-blue.svg?style=for-the-badge" alt="Japanese Version">
</a>
<br>
<a href="https://sakurame.eu.org/2025/08/07/privacy/%E4%B8%80%E4%B8%AA%E5%BC%80%E6%BA%90%E7%9A%84Linux%E5%86%85%E6%A0%B8%E5%AE%89%E5%85%A8%E5%BC%BA%E5%8C%96%E9%A1%B9%E7%9B%AE/" target="_blank">
<img src="https://img.shields.io/badge/Read%20Full%20Article%20on%20Blog-00A859?style=for-the-badge" alt="Read on Blog">
</a>
<br>
<a href="https://github.com/auveggry/Linux-Heimdall/releases/download/Stable/Linux-Heimdall.HandBook.ZH_CN.pdf" target="_blank">
<img src="https://img.shields.io/badge/Chinese-HandBook-blueviolet?style=for-the-badge" alt="Chinese Handbook">
</a>
<a href="https://github.com/auveggry/Linux-Heimdall/releases/download/Stable/Linux-Heimdall.HandBook.en_US.pdf" target="_blank">
<img src="https://img.shields.io/badge/English-HandBook-blueviolet?style=for-the-badge" alt="English Handbook">
</a>
<a href="https://github.com/auveggry/Linux-Heimdall/releases/download/Stable/Linux-Heimdall.HandBook.ja_JP.pdf" target="_blank">
<img src="https://img.shields.io/badge/Japanese-HandBook-blueviolet?style=for-the-badge" alt="Japanese Handbook">
</a>
<h3 align="center" style="color: #81C784;"><i>To get started quickly, please check the <a href="https://github.com/auveggry/Linux-Heimdall/releases" style="color: #96f999;">Releases Page</a>, which provides the full handbook as well as pre-compiled Stable and Hardened kernels.</i></h3>
</div>

<p align="center">
<a href="#part1">Gap Analysis</a> •
<a href="#part2">Architecture Blueprint</a> •
<a href="#part3">Implementation Study</a> •
<a href="#part4">Empirical Verification</a> •
<a href="#part5">Strategic Value</a> •
<a href="#part6">Conclusion & Outlook</a>
</p>

<div id="part1"></div>
<h3 align="center">Part 1: Gap Analysis</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="2">
<h4 align="center">1.1 The Illusion of Secure Boot: The Break in the Chain of Trust</h4>
</td>
</tr>
<tr>
<td width="50%" align="center" valign="top">
<p><b><font color="#4ADE80">Boot-time Verification</font></b></p>
<p>UEFI Firmware<br>↓<br>Bootloader<br>↓<br>Kernel Loaded</p>
<p>⚡️ <b><font color="#F87171">Trust Broken</font></b> ⚡️</p>
<p>Runtime Vulnerable</p>
</td>
<td width="50%" valign="top">
<ul>
<li>🛡️ <b><font color="#4ADE80">Phase 1: Boot-time Verification</font></b><br><blockquote>The UEFI firmware verifies the signatures of the bootloader and kernel, ensuring the initial integrity of the boot process.</blockquote></li>
<li>🏁 <b><font color="#FBBF24">Phase 2: Trust Handover</font></b><br><blockquote>Once the kernel is successfully loaded, the mission of Secure Boot is complete. The chain of trust is handed over at this moment but is not traditionally extended.</blockquote></li>
<li>🚨 <b><font color="#F87171">Phase 3: Runtime Risk Exposure</font></b><br><blockquote>All user-space applications, libraries, and configuration files are left unmonitored, leaving a vast attack surface for attackers.</blockquote></li>
</ul>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<h4 align="center">1.2 Runtime Threats: Betrayal from Within</h4>
<p align="center">
<b><font color="#4ADE80">Before: Legitimate Execution</font></b><br>
💻<br>
<code>/bin/sudo</code><br>
✅
</p>
<p align="center">
🦠→ 🔓 → 😭<br>
<small><font color="#F87171">Malware Injection</font></small>
</p>
<p align="center">
<b><font color="#F87171">After: Malicious Action</font></b><br>
💀<br>
<code>/bin/sudo</code> (Content has been tampered with)
</p>
<blockquote><b>Key Vulnerability: The Kernel's Blind Spot</b><br>The traditional kernel trusts a file's <b>path</b>, not its <b>content</b>. It cannot perceive that the content at a legitimate path has been maliciously replaced.</blockquote>
</td>
<td width="50%" valign="top">
<h4 align="center">1.3 Offline Threats: The "Evil Maid" Attack</h4>
<p align="center"><b>Attacker's Path</b><br>👻 (Physical Access) → 💾 (Offline Mount) → 📝 (Tamper with Files)</p>
<br>
<blockquote><b>Key Vulnerability: Why does a system with only IMA fail?</b><br>The attacker not only modifies the file content but also uses offline privileges to recalculate and overwrite the file's "legitimate" hash value.</blockquote>
<pre><code># 1. Replace the legitimate file with a malicious program
echo 'malware' > /bin/sudo

2. Recalculate and forge a new "legitimate" hash
new_hash=$(sha256sum /bin/sudo)
setfattr -n security.ima -v "$new_hash" /bin/sudo</code></pre>

<p align="center"><font color="#FCD34D">When the system reboots, IMA will mistakenly trust the tampered file!</font></p>
</td>
</tr>
</tbody>
</table>
<hr>

<div id="part2"></div>
<h3 align="center">Part 2: Zero Trust Kernel Architecture Blueprint</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="4">
<h4 align="center">2.1 Principle of Trust Chain: Building an Unshakable Foundation</h4>
<p align="center">
⚓ Hardware Root of Trust (TPM 2.0)<br>
↓<br>
Secure Boot (UKI) → Kernel Space (IMA/EVM) → Runtime Software
</p>
<blockquote><p align="center">A secure system must be built on a chain of trust, starting from a physically unalterable hardware root of trust.<br>The core of Project Heimdall is to extend this chain to every corner of the system.</p></blockquote>
</td>
</tr>
<tr>
<td colspan="4">
<h4 align="center">2.2 The Four Pillars of Verifiable Integrity</h4>
</td>
</tr>
<tr>
<td width="25%" align="center" valign="top">🕵️<br><b>IMA</b><br><small>Runtime Sentinel</small><br><blockquote>Appraises whether file <b><font color="#4ADE80">content</font></b> has been tampered with.</blockquote></td>
<td width="25%" align="center" valign="top">🔗<br><b>EVM</b><br><small>Offline Defender</small><br><blockquote>Protects file <b><font color="#FBBF24">metadata</font></b> from being forged.</blockquote></td>
<td width="25%" align="center" valign="top">🛡️<br><b>TPM 2.0</b><br><small>Hardware Anchor</small><br><blockquote>Provides tamper-proof <b><font color="#60A5FA">key storage</font></b> and <b><font color="#60A5FA">measurement logs</font></b>.</blockquote></td>
<td width="25%" align="center" valign="top">📦<br><b>UKI</b><br><small>Atomic Boot</small><br><blockquote>Signs the <b><font color="#A78BFA">security policy</font></b> along with the kernel.</blockquote></td>
</tr>
<tr>
<td colspan="4">
<h4 align="center">2.3 Synergistic Operations: A Unified Defense System</h4>
<p align="center"><b>Scenario: A user executes <code>sudo ls</code></b></p>
<ol>
<li><b>🚀 At Boot: Anchoring Trust</b><br><blockquote>The TPM checks the <font color="#60A5FA">PCR7</font> value and, after confirming the secure boot state, unseals the EVM key.</blockquote></li>
<li><b>🔑 Step 1: EVM Verifies Metadata</b><br><blockquote>The kernel uses the unsealed key to verify the <font color="#FBBF24">EVM signature</font>, ensuring the IMA hash is trustworthy.</blockquote></li>
<li><b>🕵️ Step 2: IMA Appraises File Content</b><br><blockquote>The kernel calculates the file's real-time hash and compares it with the trusted <font color="#4ADE80">IMA hash</font>.</blockquote></li>
</ol>
<p align="center">✅ <b><font color="#4ADE80">All Pass:</font></b> Access Permitted &nbsp;|&nbsp; ❌ <b><font color="#F87171">Any Step Fails:</font></b> Access Denied</p>
</td>
</tr>
</tbody>
</table>
<hr>

<div id="part3"></div>
<h3 align="center">Part 3: Implementation Case Study</h3>
<table width="100%">
<tbody>
<tr>
<td width="50%" valign="top">
<h4 align="center">3.1 Customizing the Core: Forging the Security Cornerstone</h4>
<p align="center">⚙️ → 🛡️ → 🚦 → 💎</p>
<p align="center"><small>Generic Kernel → Harden → Enable → Reinforced Core</small></p>
<blockquote><small>This process follows the principle of "least privilege," transforming a general-purpose kernel into a minimal, security-focused trusted computing base.</small></blockquote>
</td>
<td width="50%" valign="top">
<h4 align="center">3.2 Layered Key Management Strategy</h4>
<p align="center">🏛️ → ✍️ → 🧠 → 🛡️</p>
<p align="center"><small>Create Root Trust → Issue Working Keys → Embed in Kernel → Seal with Hardware</small></p>
<blockquote><small>This strategy separates and combines software-level trust (IMA CA) with hardware-anchored trust (EVM key) to build a flexible yet robust cryptographic backbone.</small></blockquote>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<h4 align="center">3.3 Phased Deployment Strategy</h4>
<p align="center">🧐 → 🏷️ → 🧬 → 🚦</p>
<p align="center"><small>Audit Mode → Fix & Label → Validate Baseline → Enforce</small></p>
<blockquote><small>This gradual approach ensures a smooth and controllable transition from a lenient to a strict security policy, minimizing impact on the production environment.</small></blockquote>
</td>
<td width="50%" valign="top">
<h4 align="center">3.4 Immutable Boot: Solidifying Security Policies</h4>
<p align="center">📦 → ✍️ → 🚀 → 🛡️</p>
<p align="center"><small>Bundle → Sign → Load → Verify</small></p>
<blockquote><small>This process turns the security policy itself into a hardware-protected cryptographic object, completely closing the backdoor of bypassing security mechanisms by modifying boot parameters.</small></blockquote>
</td>
</tr>
</tbody>
</table>
<hr>

<div id="part4"></div>
<h3 align="center">Part 4: Empirical Verification & Security Analysis</h3>
<table width="100%">
<tbody>
<tr>
<td width="50%" valign="top">
<h4 align="center">4.1 Scenario 1: Runtime Attack</h4>
<p align="center">🌕 → ✍️ → 🚫 → 🛡️</p>
<p align="center"><small>Initial State → Attack Action → Execution Attempt → IMA Intercepts</small></p>
<blockquote><small>This demonstrates that the IMA appraisal mechanism can effectively prevent any runtime tampering of protected files, ensuring the integrity of executables.</small></blockquote>
</td>
<td width="50%" valign="top">
<h4 align="center">4.2 Scenario 2: Offline Attack</h4>
<p align="center">👻 → 📝 → 🔑 → 🛡️</p>
<p align="center"><small>Offline Tampering → Forge Hash → Point of Failure → EVM Defends</small></p>
<blockquote><small>This analysis proves that the synergy between EVM and TPM is key to defending against offline attacks, as it protects the most vulnerable link in the trust chain—the metadata.</small></blockquote>
</td>
</tr>
</tbody>
</table>
<hr>

<div id="part5"></div>
<h3 align="center">Part 5: Strategic Value & Application Prospects</h3>
<table width="100%">
<tbody>
<tr>
<td width="50%" valign="top">
<h4 align="center">5.1 Kernel-Level Zero Trust Architecture</h4>
<ul>
<li><b>🤔 Never Trust, Always Verify:</b><br><blockquote><small>The system no longer assumes internal files are trustworthy; every access requires real-time verification.</small></blockquote></li>
<li><b>🏰 Assume Breach:</b><br><blockquote><small>Defense is built into the system's core, not reliant on a fragile perimeter.</small></blockquote></li>
<li><b>👮 Least Privilege:</b><br><blockquote><small>Even root cannot execute tampered code, limiting the scope of potential damage.</small></blockquote></li>
</ul>
</td>
<td width="50%" valign="top">
<h4 align="center">5.2 Empowering Remote Attestation</h4>
<ul><li><b>⚡ → ✍️ → 📨 → 🌀</b><br><blockquote><small>Challenge → Quote → Respond → Verify</small></blockquote></li></ul>
<h4 align="center">5.3 Applications in High-Risk Environments</h4>
<ul>
<li>☁️ <b>Cloud Computing:</b> <small>Ensure VM image integrity.</small></li>
<li>🏭 <b>Critical Infrastructure:</b> <small>Lock down ICS software.</small></li>
<li>🛰️ <b>Internet of Things (IoT):</b> <small>Secure firmware for mass devices.</small></li>
<li>💳 <b>Financial Services:</b> <small>Protect transaction software.</small></li>
</ul>
</td>
</tr>
</tbody>
</table>
<hr>

<div id="part6"></div>
<h3 align="center">Part 6: Conclusion & Outlook</h3>
<table width="100%">
<tbody>
<tr>
<td width="50%" valign="top">
<h4 align="center">6.1 Summary of Achievements</h4>
<ul>
<li><b>🔗 End-to-End Chain of Trust:</b> <blockquote>Successfully built a complete and verifiable chain of trust from hardware power-on to application execution.</blockquote></li>
<li><b>🛡️ Defense in Depth:</b> <blockquote>Effectively defended against multiple advanced threats, including runtime code injection and offline physical tampering.</blockquote></li>
<li><b>🎯 Zero Trust Implementation:</b> <blockquote>Practically implemented the Zero Trust security concept at the core level of the operating system.</blockquote></li>
</ul>
</td>
<td width="50%" valign="top">
<h4 align="center">6.2 Future Outlook</h4>
<ul>
<li><b>📡 Integrate Remote Attestation:</b> <blockquote>Integrate with verifiers like Keylime to achieve automated trust monitoring.</blockquote></li>
<li><b>🔬 Fine-Grained Policies:</b> <blockquote>Customize more precise protection policies for specific applications (e.g., databases).</blockquote></li>
<li><b>⏱️ Performance Benchmarking:</b> <blockquote>Quantify the impact of different security policies on system performance to guide deployment.</blockquote></li>
</ul>
</td>
</tr>
</tbody>
</table>
