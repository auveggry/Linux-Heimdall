<div align="center">
<a href="https://github.com/auveggry/Linux-Heimdall">
<img src="https://ptpimg.me/my2mi2.jpg" alt="北欧神话中的守护神海姆达尔的艺术图" style="max-width: 800px; width: 100%; border-radius: 8px;">
</a>
<br><br>
<h3 style="color: #6BDBAD;">项目命名缘由：神话与技术的交汇</h3>
<p>在北欧神话中，守护神海姆达尔以其超凡的感知力和警惕性著称。本项目借其之名，旨在强调其核心使命：<br>为Linux内核构建一个不知疲倦、洞察秋毫、且反应迅速的终极守护者。</p>
<h1>海姆达尔计划</h1>
<h2>Linux Heimdall</h2>
</div>

<div align="center">
<a href="https://github.com/auveggry/Linux-Heimdall/blob/main/LICENSE" target="_blank">
<img src="https://img.shields.io/badge/license-GPLv3-blue.svg?style=for-the-badge" alt="许可证">
</a>
<a href="https://github.com/auveggry/Linux-Heimdall/pulls" target="_blank">
<img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge" alt="欢迎PR">
</a>
<a href="#" target="_blank">
<img src="https://img.shields.io/badge/Linux%20Kernel-6.16-orange?style=for-the-badge" alt="内核版本">
</a>
<a href="https://github.com/auveggry/Linux-Heimdall" target="_blank">
<img src="https://img.shields.io/github/stars/auveggry/Linux-Heimdall?style=for-the-badge" alt="GitHub stars">
</a>
<br>
<a href="README_zh-CN.md" target="_blank">
<img src="https://img.shields.io/badge/阅读简体中文版本-brightgreen.svg?style=for-the-badge" alt="中文版">
</a>
<a href="README_ja-JP.md" target="_blank">
<img src="https://img.shields.io/badge/日本語版を読む-blue.svg?style=for-the-badge" alt="日文版">
</a>
</div>

<p align="center">
<a href="#part1">缺口分析</a> •
<a href="#part2">架构蓝图</a> •
<a href="#part3">实施研究</a> •
<a href="#part4">实证验证</a> •
<a href="#part5">战略价值</a> •
<a href="#part6">结论展望</a>
</p>

<div id="part1"></div>
<h3 align="center">第一部分: 完整性缺口分析</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="2">
<h4 align="center">1.1 安全启动的幻象：信任链的断裂点</h4>
</td>
</tr>
<tr>
<td width="50%" align="center" valign="top">
<p><b><font color="#4ADE80">启动时验证</font></b></p>
<p>UEFI Firmware<br>↓<br>Bootloader<br>↓<br>Kernel Loaded</p>
<p>⚡️ <b><font color="#F87171">信任断裂</font></b> ⚡️</p>
<p>Runtime Vulnerable</p>
</td>
<td width="50%" valign="top">
<ul>
<li>🛡️ <b><font color="#4ADE80">阶段一：启动时验证</font></b><br><blockquote>UEFI固件验证引导加载器和内核的签名，确保启动过程的初始纯洁性。</blockquote></li>
<li>🏁 <b><font color="#FBBF24">阶段二：信任交接</font></b><br><blockquote>内核成功加载后，安全启动的使命完成。信任链在此刻交接，但传统上并未延续。</blockquote></li>
<li>🚨 <b><font color="#F87171">阶段三：运行时风险暴露</font></b><br><blockquote>所有用户空间的应用、库和配置文件都处于无监控状态，为攻击者留下了广阔的攻击面。</blockquote></li>
</ul>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<h4 align="center">1.2 运行时威胁：系统内部的背叛</h4>
<p align="center">
<b><font color="#4ADE80">事前: 合法执行</font></b><br>
💻<br>
<code>/bin/sudo</code><br>
✅
</p>
<p align="center">
🦠→ 🔓 → 😭<br>
<small><font color="#F87171">恶意软件注入</font></small>
</p>
<p align="center">
<b><font color="#F87171">事后: 恶意行为</font></b><br>
💀<br>
<code>/bin/sudo</code> (内容已被篡改)
</p>
<blockquote><b>关键漏洞：内核的盲点</b><br>传统内核在执行文件时，信任的是文件的<b>路径</b>而非<b>内容</b>。它无法感知到该路径指向的文件内容已被恶意替换。</blockquote>
</td>
<td width="50%" valign="top">
<h4 align="center">1.3 离线威胁：“邪恶女仆”攻击</h4>
<p align="center"><b>攻击者路径</b><br>👻 (物理接触) → 💾 (离线挂载) → 📝 (篡改文件)</p>
<br>
<blockquote><b>关键漏洞：仅有IMA的系统为何会失效？</b><br>攻击者不仅修改了文件内容，还利用离线权限，重新计算并覆盖了文件的“合法”哈希值。</blockquote>
<pre><code># 1. 替换合法文件为恶意程序
echo 'malware' > /bin/sudo

2. 重新计算并伪造新的“合法”哈希值
new_hash=$(sha256sum /bin/sudo)
setfattr -n security.ima -v "$new_hash" /bin/sudo</code></pre>

<p align="center"><font color="#FCD34D">当系统重启，IMA会错误地信任被篡改的文件！</font></p>
</td>
</tr>
</tbody>
</table>
<hr>

<div id="part2"></div>
<h3 align="center">第二部分: 零信任内核架构蓝图</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="4">
<h4 align="center">2.1 信任链原则：建立不可动摇的基石</h4>
<p align="center">
⚓ 硬件信任根 (TPM 2.0)<br>
↓<br>
安全启动 (UKI) → 内核空间 (IMA/EVM) → 运行时软件
</p>
<blockquote><p align="center">一个安全的系统必须建立在一条信任链之上，其起点是物理上不可更改的硬件信任根。<br>海姆达尔计划的核心就是将这条链延伸至系统的每一个角落。</p></blockquote>
</td>
</tr>
<tr>
<td colspan="4">
<h4 align="center">2.2 可验证完整性的四大支柱</h4>
</td>
</tr>
<tr>
<td width="25%" align="center" valign="top">🕵️<br><b>IMA</b><br><small>运行时哨兵</small><br><blockquote>评估文件<b><font color="#4ADE80">内容</font></b>是否被篡改。</blockquote></td>
<td width="25%" align="center" valign="top">🔗<br><b>EVM</b><br><small>离线防御者</small><br><blockquote>保护文件<b><font color="#FBBF24">元数据</font></b>不被伪造。</blockquote></td>
<td width="25%" align="center" valign="top">🛡️<br><b>TPM 2.0</b><br><small>硬件锚点</small><br><blockquote>提供防篡改的<b><font color="#60A5FA">密钥存储</font></b>与<b><font color="#60A5FA">测量日志</font></b>。</blockquote></td>
<td width="25%" align="center" valign="top">📦<br><b>UKI</b><br><small>原子化启动</small><br><blockquote>将<b><font color="#A78BFA">安全策略</font></b>与内核一同签名。</blockquote></td>
</tr>
<tr>
<td colspan="4">
<h4 align="center">2.3 协同作战：一个统一的防御体系</h4>
<p align="center"><b>场景: 用户执行 <code>sudo ls</code></b></p>
<ol>
<li><b>🚀 启动时: 信任锚定</b><br><blockquote>TPM检查<font color="#60A5FA">PCR7</font>值，确认安全启动状态后，解封EVM密钥。</blockquote></li>
<li><b>🔑 第1步: EVM验证元数据</b><br><blockquote>内核使用解封的密钥，验证<font color="#FBBF24">EVM签名</font>，确保IMA哈希可信。</blockquote></li>
<li><b>🕵️ 第2步: IMA评估文件内容</b><br><blockquote>内核计算文件实时哈希，并与可信的<font color="#4ADE80">IMA哈希</font>对比。</blockquote></li>
</ol>
<p align="center">✅ <b><font color="#4ADE80">全部通过:</font></b> 允许执行 &nbsp;|&nbsp; ❌ <b><font color="#F87171">任何一步失败:</font></b> 拒绝访问</p>
</td>
</tr>
</tbody>
</table>
<hr>

<div id="part3"></div>
<h3 align="center">第三部分: 实施案例研究</h3>
<table width="100%">
<tbody>
<tr>
<td width="50%" valign="top">
<h4 align="center">3.1 定制核心：铸造安全基石</h4>
<p align="center">⚙️ → 🛡️ → 🚦 → 💎</p>
<p align="center"><small>通用内核 → 加固 → 开启 → 强化核心</small></p>
<blockquote><small>此流程遵循“最小权限”原则，通过加固和开启安全模块，将通用内核重塑为一个专为安全而生的、最小化的可信计算基。</small></blockquote>
</td>
<td width="50%" valign="top">
<h4 align="center">3.2 分层密钥管理策略</h4>
<p align="center">🏛️ → ✍️ → 🧠 → 🛡️</p>
<p align="center"><small>创建根信任 → 签发工作密钥 → 嵌入内核 → 硬件密封</small></p>
<blockquote><small>此策略将软件层面的信任（IMA CA）与硬件锚定的信任（EVM密钥）分离又结合，构建了一个既灵活又坚固的加密骨干。</small></blockquote>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<h4 align="center">3.3 分阶段部署策略</h4>
<p align="center">🧐 → 🏷️ → 🧬 → 🚦</p>
<p align="center"><small>审计模式 → 修复与标记 → 验证基线 → 强制执行</small></p>
<blockquote><small>这种渐进式方法确保了从宽松到严格的安全策略过渡是平滑且可控的，最大限度地减少了对生产环境的冲击。</small></blockquote>
</td>
<td width="50%" valign="top">
<h4 align="center">3.4 不可变启动：固化安全策略</h4>
<p align="center">📦 → ✍️ → 🚀 → 🛡️</p>
<p align="center"><small>打包 → 签名 → 加载 → 验证</small></p>
<blockquote><small>此流程将安全策略本身变成一个受硬件保护的加密对象，彻底关闭了通过修改引导参数来绕过安全机制的后门。</small></blockquote>
</td>
</tr>
</tbody>
</table>
<hr>

<div id="part4"></div>
<h3 align="center">第四部分: 实证验证与安全分析</h3>
<table width="100%">
<tbody>
<tr>
<td width="50%" valign="top">
<h4 align="center">4.1 场景一：运行时攻击</h4>
<p align="center">🌕 → ✍️ → 🚫 → 🛡️</p>
<p align="center"><small>初始状态 → 攻击行为 → 执行尝试 → IMA拦截</small></p>
<blockquote><small>此演示证明IMA评估机制能有效阻止对受保护文件的任何运行时篡改，确保了可执行文件的完整性。</small></blockquote>
</td>
<td width="50%" valign="top">
<h4 align="center">4.2 场景二：离线攻击</h4>
<p align="center">👻 → 📝 → 🔑 → 🛡️</p>
<p align="center"><small>离线篡改 → 伪造哈希 → 攻击失败点 → EVM防御</small></p>
<blockquote><small>此分析证明了EVM与TPM的协同作用是防御离线攻击的关键，它保护了信任链中最脆弱的一环——元数据。</small></blockquote>
</td>
</tr>
</tbody>
</table>
<hr>

<div id="part5"></div>
<h3 align="center">第五部分: 战略价值与应用前景</h3>
<table width="100%">
<tbody>
<tr>
<td width="50%" valign="top">
<h4 align="center">5.1 内核级零信任架构</h4>
<ul>
<li><b>🤔 从不信任，永远验证:</b><br><blockquote><small>系统不再假定内部文件可信，每次访问都需实时验证。</small></blockquote></li>
<li><b>🏰 假设泄露:</b><br><blockquote><small>防御内置于系统底层，而非依赖脆弱的边界。</small></blockquote></li>
<li><b>👮 最小权限:</b><br><blockquote><small>即便是root也无法执行被篡改的代码，限制破坏范围。</small></blockquote></li>
</ul>
</td>
<td width="50%" valign="top">
<h4 align="center">5.2 赋能远程证明</h4>
<ul><li><b>⚡ → ✍️ → 📨 → 🌀</b><br><blockquote><small>挑战 → 引用 → 响应 → 验证</small></blockquote></li></ul>
<h4 align="center">5.3 在高风险环境中的应用</h4>
<ul>
<li>☁️ <b>云计算:</b> <small>确保VM镜像完整性。</small></li>
<li>🏭 <b>关键基础设施:</b> <small>锁定工控系统软件。</small></li>
<li>🛰️ <b>物联网 (IoT):</b> <small>保证海量设备固件安全。</small></li>
<li>💳 <b>金融服务:</b> <small>保护交易软件。</small></li>
</ul>
</td>
</tr>
</tbody>
</table>
<hr>

<div id="part6"></div>
<h3 align="center">第六部分: 结论与展望</h3>
<table width="100%">
<tbody>
<tr>
<td width="50%" valign="top">
<h4 align="center">6.1 成果总结</h4>
<ul>
<li><b>🔗 端到端信任链:</b> <blockquote>成功构建了从硬件加电到应用程序运行的、完整且可验证的信任链。</blockquote></li>
<li><b>🛡️ 深度防御:</b> <blockquote>有效抵御了包括运行时代码注入和离线物理篡改在内的多种高级威胁。</blockquote></li>
<li><b>🎯 零信任落地:</b> <blockquote>将零信任安全理念在操作系统核心层面进行了切实的工程化落地。</blockquote></li>
</ul>
</td>
<td width="50%" valign="top">
<h4 align="center">6.2 未来展望</h4>
<ul>
<li><b>📡 集成远程证明:</b> <blockquote>与Keylime等验证器集成，实现自动化信任监控。</blockquote></li>
<li><b>🔬 细粒度策略:</b> <blockquote>为特定应用（如数据库）定制更精确的保护策略。</blockquote></li>
<li><b>⏱️ 性能基准测试:</b> <blockquote>量化不同策略对系统性能的影响，指导部署。</blockquote></li>
</ul>
</td>
</tr>
</tbody>
</table>
