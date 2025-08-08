<div align="center">

Linux Heimdall (海姆达尔计划)
<p>
<img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License">
<img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt="PRs Welcome">
<img src="https://img.shields.io/badge/Linux%20Kernel-6.x-orange" alt="Kernel Version">
<img src="https://img.shields.io/github/stars/auveggry/Linux-Heimdall?style=social" alt="GitHub stars">
</p>

一个基于 IMA/EVM + TPM 2.0 + UKI 的开源 Linux 内核安全强化架构，旨在构建从硬件到运行时的端到端可验证信任链。

<br>

<img src="https://upload.wikimedia.org/wikipedia/commons/7/7b/Nils_Asplund_-_Heimdal.jpg" alt="Heimdall Art" width="700"/>

<em style="color: #9CA3AF;">项目命名缘由：在北欧神话中，守护神海姆达尔以其超凡的感知力和警惕性著称。本项目借其之名，旨在强调其核心使命——为Linux内核构建一个不知疲倦、洞察秋毫、且反应迅速的终极守护者。</em>
</div>

<!-- Section-based Navigation -->

<table width="100%">
<tr align="center">
<td><a href="#-第一部分-完整性缺口分析">缺口分析</a></td>
<td><a href="#-第二部分-零信任内核架构蓝图">架构蓝图</a></td>
<td><a href="#-第三部分-实施案例研究">实施研究</a></td>
<td><a href="#-第四部分-实证验证与安全分析">实证验证</a></td>
<td><a href="#-第五部分-战略价值与应用前景">战略价值</a></td>
<td><a href="#-第六部分-结论与展望">结论展望</a></td>
</tr>
</table>

<a id="-第一部分-完整性缺口分析">🛡️ 第一部分: 完整性缺口分析</a>
1.1 安全启动的幻象：信任链的断裂点
<table>
<tr>
<td width="45%" valign="top">
<div align="center">
<br>
<div style="background-color: #166534; color: white; border-radius: 8px; padding: 10px; width: 200px; text-align: center; font-weight: bold;">UEFI Firmware</div>
<div style="color: #007A42; font-size: 24px; font-weight: bold;">↓</div>
<div style="background-color: #166534; color: white; border-radius: 8px; padding: 10px; width: 200px; text-align: center; font-weight: bold;">Bootloader</div>
<div style="color: #007A42; font-size: 24px; font-weight: bold;">↓</div>
<div style="background-color: #166534; color: white; border-radius: 8px; padding: 10px; width: 200px; text-align: center; font-weight: bold;">Kernel Loaded</div>
<div style="color: #DC2626; font-size: 24px; font-weight: bold;">⚡️</div>
<div style="background-color: #991B1B; color: white; border-radius: 8px; padding: 10px; width: 200px; text-align: center; font-weight: bold;">Runtime Vulnerable</div>
<br>
</div>
</td>
<td valign="top">
<ul>
<li>
<p>🛡️ <strong><font color="#4ADE80">阶段一：启动时验证</font></strong><br>
<small style="color: #9CA3AF;">UEFI固件验证引导加载器和内核的签名，确保启动过程的初始纯洁性。</small></p>
</li>
<li>
<p>🏁 <strong><font color="#FBBF24">阶段二：信任交接</font></strong><br>
<small style="color: #9CA3AF;">内核成功加载后，安全启动的使命完成。信任链在此刻交接，但传统上并未延续。</small></p>
</li>
<li>
<p>🚨 <strong><font color="#F87171">阶段三：运行时风险暴露</font></strong><br>
<small style="color: #9CA3AF;">所有用户空间的应用、库和配置文件都处于无监控状态，为攻击者留下了广阔的攻击面。</small></p>
</li>
</ul>
</td>
</tr>
</table>

1.2 运行时威胁 & 1.3 离线威胁
<table>
<tr>
<td width="50%" valign="top">
<h4 align="center"><font color="#00A859">1.2 运行时威胁：系统内部的背叛</font></h4>
<table width="100%">
<tr align="center">
<td><strong><font color="#4ADE80">事前: 合法执行</font></strong><br>💻<br><code>/bin/sudo</code><br><small>内核验证路径和权限</small><br>✅</td>
<td><br>🦠<br>→<br><small><font color="#F87171">恶意注入</font></small></td>
<td><strong><font color="#F87171">事后: 恶意行为</font></strong><br>💀<br><code>/bin/sudo</code><br><small>内容已被篡改</small><br>🔓</td>
</tr>
</table>
<blockquote>
<p>🚨 <strong>关键漏洞：内核的盲点</strong><br>
<small>传统内核在执行文件时，信任的是文件的<strong>路径</strong>而非<strong>内容</strong>。它检查用户是否有权限执行 <code>/bin/sudo</code>，但它无法感知到该路径指向的文件内容已被恶意替换。这是运行时完整性保护的核心动机。</small></p>
</blockquote>
</td>
<td width="50%" valign="top">
<h4 align="center"><font color="#00A859">1.3 离线威胁：“邪恶女仆”攻击</font></h4>
<div align="center">
<p>👻 物理接触 → 💾 离线挂载 → 📝 篡改文件</p>
</div>
<blockquote>
<p>🚨 <strong>关键漏洞：仅有IMA的系统为何会失效？</strong><br>
<small>攻击者不仅修改了文件内容，还利用离线权限，重新计算并覆盖了文件的“合法”哈希值。</small>
<pre><code style="color: #F87171;"># 1. echo 'malware' > /bin/sudo

2. new_hash=$(sha256sum /bin/sudo)
3. setfattr -n security.ima -v $new_hash /bin/sudo
</code></pre>
<small><font color="#FCD34D">当系统重启后，IMA会发现哈希匹配，从而错误地信任了被篡改的文件！</font></small></p>
</blockquote>
</td>
</tr>
</table>

<a id="-第二部分-零信任内核架构蓝图">🗺️ 第二部分: 零信任内核架构蓝图</a>
2.1 信任链原则：建立不可动摇的基石
<div align="center">
<p>⚓<br><strong>硬件信任根 (TPM 2.0)</strong></p>
<p>↓</p>
<p><strong>安全启动 (UKI)</strong> → <strong>内核空间 (IMA/EVM)</strong> → <strong>运行时软件</strong></p>
<p><small style="color: #9CA3AF;">一个安全的系统必须建立在一条信任链之上，其起点是物理上不可更改的硬件信任根。<br>海姆达尔计划的核心就是将这条链延伸至系统的每一个角落。</small></p>
</div>

2.2 可验证完整性的四大支柱
<table width="100%">
<tr align="center">
<td width="25%">🕵️<br><strong>IMA</strong><br><small>运行时哨兵</small><hr><small>评估文件<font color="#4ADE80"><strong>内容</strong></font>是否被篡改。</small></td>
<td width="25%">🔗<br><strong>EVM</strong><br><small>离线防御者</small><hr><small>保护文件<font color="#FBBF24"><strong>元数据</strong></font>不被伪造。</small></td>
<td width="25%">🛡️<br><strong>TPM 2.0</strong><br><small>硬件锚点</small><hr><small>提供防篡改的<font color="#60A5FA"><strong>密钥存储</strong></font>与<font color="#60A5FA"><strong>测量日志</strong></font>。</small></td>
<td width="25%">📦<br><strong>UKI</strong><br><small>原子化启动</small><hr><small>将<font color="#A78BFA"><strong>安全策略</strong></font>与内核一同签名，防止绕过。</small></td>
</tr>
</table>

2.3 协同作战：一个统一的防御体系
<div align="center">
<p><strong>场景: 用户执行 <code>sudo ls</code></strong></p>
</div>

🚀 启动时: 信任锚定<br>
<small>TPM检查<font color="#60A5FA"><strong>PCR7</strong></font>值，确认安全启动状态后，解封EVM密钥。</small>

<div align="center">↓</div>

🔑 第1步: EVM验证元数据<br>
<small>内核使用解封的密钥，验证<font color="#FBBF24"><strong>EVM签名</strong></font>。此举确保文件的IMA哈希值本身是可信的。</small>

<div align="center">↓</div>

🕵️ 第2步: IMA评估文件内容<br>
<small>内核计算文件实时哈希，并与可信的<font color="#4ADE80"><strong>IMA哈希</strong></font>对比。</small>

<div align="center">↓</div>

<table width="100%">
<tr>
<td align="center" width="50%" style="background-color: rgba(22, 101, 52, 0.2); border: 1px solid #22C55E; border-radius: 8px;">
<p><strong><font color="#4ADE80">✅ 全部通过</font></strong><br><small>允许执行</small></p>
</td>
<td align="center" width="50%" style="background-color: rgba(153, 27, 27, 0.2); border: 1px solid #EF4444; border-radius: 8px;">
<p><strong><font color="#F87171">❌ 任何一步失败</font></strong><br><small>拒绝访问</small></p>
</td>
</tr>
</table>

<a id="-第三部分-实施案例研究">🛠️ 第三部分: 实施案例研究</a>
<table>
<tr>
<td width="50%" valign="top" style="border: 1px solid #005A34; border-radius: 8px; padding: 10px;">
<h4 align="center"><font color="#00A859">3.1 定制核心：铸造安全基石</font></h4>
<table width="100%">
<tr align="center">
<td>⚙️<br><strong>起点</strong><br><small>通用内核</small></td>
<td>→</td>
<td>🛡️<br><strong>加固</strong><br><small>移除非必需模块</small></td>
<td>→</td>
<td>🚦<br><strong>开启</strong><br><small>激活IMA/EVM</small></td>
<td>→</td>
<td>💎<br><strong>终点</strong><br><small>强化核心</small></td>
</tr>
</table>
</td>
<td width="50%" valign="top" style="border: 1px solid #005A34; border-radius: 8px; padding: 10px;">
<h4 align="center"><font color="#00A859">3.2 分层密钥管理策略</font></h4>
<table width="100%">
<tr align="center">
<td>🏛️<br><strong>1. 创建根信任</strong><br><small>建立离线IMA根CA</small></td>
<td>→</td>
<td>✍️<br><strong>2. 签发工作密钥</strong><br><small>用于日常签名</small></td>
</tr>
<tr align="center">
<td>🧠<br><strong>3. 嵌入内核</strong><br><small>将根CA公钥编译</small></td>
<td>→</td>
<td>🛡️<br><strong>4. 硬件密封</strong><br><small>用TPM密封EVM密钥</small></td>
</tr>
</table>
</td>
</tr>
<tr>
<td width="50%" valign="top" style="border: 1px solid #005A34; border-radius: 8px; padding: 10px;">
<h4 align="center"><font color="#00A859">3.3 分阶段部署策略</font></h4>
<table width="100%">
<tr align="center">
<td>🧐<br><strong>1. 审计模式</strong><br><small><code>log</code></small></td>
<td>→</td>
<td>🏷️<br><strong>2. 修复与标记</strong><br><small><code>fix</code></small></td>
<td>→</td>
<td>✅<br><strong>3. 验证基线</strong><br><small>检查日志</small></td>
<td>→</td>
<td>🚦<br><strong>4. 强制执行</strong><br><small><code>enforce</code></small></td>
</tr>
</table>
</td>
<td width="50%" valign="top" style="border: 1px solid #005A34; border-radius: 8px; padding: 10px;">
<h4 align="center"><font color="#00A859">3.4 不可变启动：固化安全策略</font></h4>
<table width="100%">
<tr align="center">
<td>📦<br><strong>1. 打包</strong><br><small>内核+策略+Initrd</small></td>
<td>→</td>
<td>✍️<br><strong>2. 签名</strong><br><small>使用安全启动密钥</small></td>
<td>→</td>
<td>🚀<br><strong>3. 加载</strong><br><small>引导程序加载</small></td>
<td>→</td>
<td>🛡️<br><strong>4. 验证</strong><br><small>UEFI固件验证</small></td>
</tr>
</table>
</td>
</tr>
</table>

<a id="-第四部分-实证验证与安全分析">🔬 第四部分: 实证验证与安全分析</a>
<table>
<tr>
<td width="50%" valign="top" style="border: 1px solid #005A34; border-radius: 8px; padding: 10px;">
<h4 align="center"><font color="#00A859">4.1 场景一：运行时攻击</font></h4>
<p align="center">✅ 初始状态 → ✍️ 攻击行为 → 🚫 执行尝试 → 🛡️ <strong>IMA 拦截</strong></p>
<hr>
<small>此演示证明IMA评估机制能有效阻止对受保护文件的任何运行时篡改，确保了可执行文件的完整性。</small>
</td>
<td width="50%" valign="top" style="border: 1px solid #005A34; border-radius: 8px; padding: 10px;">
<h4 align="center"><font color="#00A859">4.2 场景二：离线攻击</font></h4>
<p align="center">👻 离线篡改 → 📝 伪造哈希 → 🔑 攻击失败 → 🛡️ <strong>EVM 防御</strong></p>
<hr>
<small>此分析证明了EVM与TPM的协同作用是防御离线攻击的关键，它保护了信任链中最脆弱的一环——元数据。</small>
</td>
</tr>
</table>

<a id="-第五部分-战略价值与应用前景">🚀 第五部分: 战略价值与应用前景</a>
<table>
<tr>
<td width="33%" valign="top">
<h4 align="center"><font color="#00A859">5.1 内核级零信任架构</font></h4>
<ul>
<li>🤔 <strong>从不信任，永远验证</strong></li>
<li>🏰 <strong>假设泄露</strong></li>
<li>👮 <strong>最小权限</strong></li>
</ul>
</td>
<td width="33%" valign="top">
<h4 align="center"><font color="#00A859">5.2 赋能远程证明</font></h4>
<ol>
<li>❓ <strong>挑战</strong>: 验证者发送随机数</li>
<li>✍️ <strong>引用</strong>: TPM对PCR和随机数签名</li>
<li>📨 <strong>响应</strong>: 发送引用和IMA日志</li>
<li>✅ <strong>验证</strong>: 验证者重放日志并比对</li>
</ol>
</td>
<td width="33%" valign="top">
<h4 align="center"><font color="#00A859">5.3 在高风险环境中的应用</font></h4>
<p align="center">
☁️ 云计算 &nbsp;&nbsp; 🏭 关键基础设施<br>
🛰️ 物联网(IoT) &nbsp;&nbsp; 💳 金融服务
</p>
</td>
</tr>
</table>

<a id="-第六部分-结论与展望">🏁 第六部分: 结论与展望</a>
<table>
<tr>
<td width="50%" valign="top">
<h4 align="center"><font color="#00A859">6.1 成果总结</font></h4>
<blockquote>
<p>🔗 <strong>端到端信任链</strong><br>
🛡️ <strong>深度防御</strong><br>
🎯 <strong>零信任落地</strong></p>
</blockquote>
</td>
<td width="50%" valign="top">
<h4 align="center"><font color="#00A859">6.2 未来展望</font></h4>
<table width="100%">
<tr align="center">
<td>📡<br>集成远程证明</td>
<td>🔬<br>细粒度策略</td>
<td>⏱️<br>性能基准测试</td>
</tr>
</table>
</td>
</tr>
</table>
