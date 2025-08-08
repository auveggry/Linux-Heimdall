<div style="background-color: #0F1A13; color: #E5E7EB; font-family: 'Noto Sans SC', sans-serif; padding: 20px; line-height: 1.6;">

<!-- HEADER -->

<div style="text-align: center; margin-bottom: 2rem;">
<img src="https://upload.wikimedia.org/wikipedia/commons/7/7b/Nils_Asplund_-_Heimdal.jpg" alt="北欧神话中的守护神海姆达尔的艺术图" style="max-width: 800px; width: 100%; border-radius: 8px; border: 2px solid #005A34; box-shadow: 0 8px 24px rgba(0,0,0,0.4);">
</div>

<div style="max-width: 48rem; margin: 0 auto 3rem auto; text-align: center;">
<h3 style="font-size: 1.25rem; font-weight: bold; color: #6BDBAD;">项目命名缘由：神话与技术的交汇</h3>
<p style="font-size: 0.875rem; margin-top: 0.5rem; color: #9CA3AF;">在北欧神话中，守护神海姆达尔以其超凡的感知力和警惕性著称。本项目借其之名，旨在强调其核心使命：为Linux内核构建一个不知疲倦、洞察秋毫、且反应迅速的终极守护者。</p>
</div>

<h1 style="font-size: 3.75rem; font-weight: bold; text-align: center; color: white; text-shadow: 0 0 8px rgba(0, 168, 89, 0.8), 0 0 10px rgba(0, 168, 89, 0.6);">海姆达尔计划</h1>
<h2 style="font-size: 2.25rem; font-weight: bold; text-align: center; color: white; margin-top: 0.5rem;">Linux Heimdall</h2>

<!-- GITHUB LINK -->

<div style="text-align: center; padding: 2rem 0; border-top: 1px solid #005A34; border-bottom: 1px solid #005A34; margin: 3rem auto; max-width: 1100px;">
<p style="font-weight: bold; font-size: 1.25rem; color: white; margin:0;">Linux Heimdall</p>
<p style="color: #6BDBAD; margin: 0.5rem 0 0 0;">一个开源的Linux内核安全强化项目</p>
<a href="https://github.com/auveggry/Linux-Heimdall" target="_blank" style="display: inline-block; margin-top: 1rem; padding: 0.5rem 1.5rem; background-color: #00A859; color: white; font-weight: bold; border-radius: 8px; text-decoration: none;">在 GitHub 上查看</a>
</div>

<!-- NAVIGATION (using table for layout) -->

<div id="nav-container" style="max-width: 1100px; margin: 0 auto 3rem auto; background: linear-gradient(to bottom, #1b2d24, #0f1a13); border: 1px solid #005A34; border-radius: 12px; padding: 8px;">
<table style="width: 100%; border-collapse: collapse;">
<tbody>
<tr>
<td style="text-align: center; padding: 0;"><a href="#part1" style="color: #E5E7EB; text-decoration: none; display: block; padding: 8px 12px; border-radius: 8px;">缺口分析</a></td>
<td style="text-align: center; padding: 0;"><a href="#part2" style="color: #E5E7EB; text-decoration: none; display: block; padding: 8px 12px; border-radius: 8px;">架构蓝图</a></td>
<td style="text-align: center; padding: 0;"><a href="#part3" style="color: #E5E7EB; text-decoration: none; display: block; padding: 8px 12px; border-radius: 8px;">实施研究</a></td>
<td style="text-align: center; padding: 0;"><a href="#part4" style="color: #E5E7EB; text-decoration: none; display: block; padding: 8px 12px; border-radius: 8px;">实证验证</a></td>
<td style="text-align: center; padding: 0;"><a href="#part5" style="color: #E5E7EB; text-decoration: none; display: block; padding: 8px 12px; border-radius: 8px;">战略价值</a></td>
<td style="text-align: center; padding: 0;"><a href="#part6" style="color: #E5E7EB; text-decoration: none; display: block; padding: 8px 12px; border-radius: 8px;">结论展望</a></td>
</tr>
</tbody>
</table>
</div>

<!-- PART 1: GAP ANALYSIS -->

<div id="part1" style="padding-top: 4rem; margin-top: -4rem;">
<h3 style="font-size: 1.875rem; font-weight: bold; text-align: center; margin-bottom: 2.5rem; color: white; text-shadow: 0 0 8px rgba(0, 168, 89, 0.8), 0 0 10px rgba(0, 168, 89, 0.6);">第一部分: 完整性缺口分析</h3>
<div style="background-color: #1B2D24; border: 1px solid #005A34; padding: 1.5rem; border-radius: 8px; margin-bottom: 2rem;">
<h4 style="font-size: 1.5rem; font-weight: bold; text-align: center; color: #00A859; margin-bottom: 1.5rem; margin-top:0;">1.1 安全启动的幻象：信任链的断裂点</h4>
<table style="width: 100%; border-collapse: collapse;">
<tbody>
<tr>
<td style="width: 50%; vertical-align: middle; text-align: center; padding-right: 2rem;">
<div style="padding: 0.75rem; background-color: #166534; border-radius: 8px; width: 14rem; text-align: center; font-weight: bold; margin: 0 auto;">UEFI Firmware</div>
<div style="width: 2px; height: 2rem; background-color: #007A42; margin: 0 auto;"></div>
<div style="padding: 0.75rem; background-color: #166534; border-radius: 8px; width: 14rem; text-align: center; font-weight: bold; margin: 0 auto;">Bootloader</div>
<div style="width: 2px; height: 2rem; background-color: #007A42; margin: 0 auto;"></div>
<div style="padding: 0.75rem; background-color: #166534; border-radius: 8px; width: 14rem; text-align: center; font-weight: bold; margin: 0 auto;">Kernel Loaded</div>
<div style="width: 100%; max-width: 14rem; height: 0.5rem; margin: 0.75rem auto; display: flex; align-items: center; justify-content: center;">
<div style="flex-grow: 1; height: 1px; background-color: #DC2626;"></div>
<span style="font-size: 1.875rem; color: #DC2626; background-color: #1B2D24; padding-left: 0.5rem; padding-right: 0.5rem;">⚡️</span>
<div style="flex-grow: 1; height: 1px; background-color: #DC2626;"></div>
</div>
<div style="padding: 0.75rem; background-color: #991B1B; border-radius: 8px; width: 14rem; text-align: center; font-weight: bold; margin: 0 auto;">Runtime Vulnerable</div>
</td>
<td style="width: 50%; vertical-align: middle;">
<ul style="list-style: none; padding: 0; margin: 0; display: flex; flex-direction: column; gap: 1.5rem;">
<li style="display: flex; align-items: flex-start;"><span style="font-size: 1.875rem; margin-right: 1rem; line-height: 1.2;">🛡️</span><div><h5 style="font-weight: bold; color: #4ADE80; margin:0;">阶段一：启动时验证</h5><p style="font-size: 0.875rem; color: #9CA3AF; margin:0.25rem 0 0 0;">UEFI固件验证引导加载器和内核的签名，确保启动过程的初始纯洁性。</p></div></li>
<li style="display: flex; align-items: flex-start;"><span style="font-size: 1.875rem; margin-right: 1rem; line-height: 1.2;">🏁</span><div><h5 style="font-weight: bold; color: #FBBF24; margin:0;">阶段二：信任交接</h5><p style="font-size: 0.875rem; color: #9CA3AF; margin:0.25rem 0 0 0;">内核成功加载后，安全启动的使命完成。信任链在此刻交接，但传统上并未延续。</p></div></li>
<li style="display: flex; align-items: flex-start;"><span style="font-size: 1.875rem; margin-right: 1rem; line-height: 1.2;">🚨</span><div><h5 style="font-weight: bold; color: #F87171; margin:0;">阶段三：运行时风险暴露</h5><p style="font-size: 0.875rem; color: #9CA3AF; margin:0.25rem 0 0 0;">所有用户空间的应用、库和配置文件都处于无监控状态，为攻击者留下了广阔的攻击面。</p></div></li>
</ul>
</td>
</tr>
</tbody>
</table>
</div>
<table style="width: 100%; border-collapse: collapse; border-spacing: 0;">
<tbody>
<tr>
<td style="width: 50%; padding-right: 1rem; vertical-align: top;">
<div style="background-color: #1B2D24; border: 1px solid #005A34; padding: 1.5rem; border-radius: 8px; height: 100%;">
<h4 style="font-size: 1.5rem; font-weight: bold; text-align: center; color: #00A859; margin-bottom: 1rem; margin-top:0;">1.2 运行时威胁：系统内部的背叛</h4>
<table style="width: 100%; text-align: center; margin-top: 1.5rem;">
<tbody>
<tr>
<td style="vertical-align: top; width: 38%;">
<h5 style="font-weight: bold; color: #4ADE80; margin:0;">事前: 合法执行</h5>
<p style="font-size: 2.25rem; margin: 0.5rem 0;">💻</p>
<p style="font-family: monospace; font-size: 0.75rem; background-color: #374151; padding: 0.25rem; border-radius: 4px; display: inline-block; margin:0;">/bin/sudo</p>
<p style="font-size: 0.75rem; margin-top: 0.25rem; color: #9CA3AF;">内核验证路径和权限</p>
<p style="font-size: 1.5rem; margin-top: 0.5rem; color: #4ADE80;">✅</p>
</td>
<td style="vertical-align: middle; width: 24%;">
<div style="position: relative; line-height: 1;">
<div style="font-size: 2.25rem; color: #F87171;">→</div>
<div style="position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); background-color: #1B2D24; padding: 0 0.25rem;">
<p style="font-size: 2rem; margin:0;">🦠</p>
</div>
</div>
<p style="font-size: 0.75rem; color: #F87171; margin-top: 0.5rem;">恶意软件注入</p>
</td>
<td style="vertical-align: top; width: 38%;">
<h5 style="font-weight: bold; color: #F87171; margin:0;">事后: 恶意行为</h5>
<p style="font-size: 2.25rem; margin: 0.5rem 0;">💀</p>
<p style="font-family: monospace; font-size: 0.75rem; background-color: rgba(153, 27, 27, 0.8); padding: 0.25rem; border-radius: 4px; display: inline-block; margin:0;">/bin/sudo</p>
<p style="font-size: 0.75rem; margin-top: 0.25rem; color: #9CA3AF;">内容已被篡改</p>
<p style="font-size: 1.5rem; margin-top: 0.5rem; color: #F87171;">🔓</p>
</td>
</tr>
</tbody>
</table>
<div style="width: 100%; text-align: center; font-size: 1.5rem; margin: 0.75rem 0; color: #F87171;">↓</div>
<h5 style="font-weight: bold; color: #F87171; text-align: center; margin-bottom: 0.5rem;">关键漏洞：内核的盲点</h5>
<div style="background-color: rgba(0,0,0,0.5); padding: 1rem; border-radius: 8px; border: 1px solid #F87171; text-align: center;">
<p style="font-size: 0.875rem; margin:0;">传统内核在执行文件时，信任的是文件的路径而非内容。它检查用户是否有权限执行<code style="font-family: monospace; font-size: 0.75rem; color: #E5E7EB; background-color: #374151; padding: 2px 4px; border-radius: 4px;">/bin/sudo</code>，但它无法感知到该路径指向的文件内容已被恶意替换。这是运行时完整性保护的核心动机。</p>
</div>
</div>
</td>
<td style="width: 50%; padding-left: 1rem; vertical-align: top;">
<div style="background-color: #1B2D24; border: 1px solid #005A34; padding: 1.5rem; border-radius: 8px; height: 100%;">
<h4 style="font-size: 1.5rem; font-weight: bold; text-align: center; color: #00A859; margin-bottom: 1rem; margin-top:0;">1.3 离线威胁：“邪恶女仆”攻击</h4>
<div style="margin-top: 1.5rem;">
<h5 style="font-weight: bold; color: #FBBF24; text-align: center; margin-bottom: 0.5rem;">攻击者路径</h5>
<table style="width: 100%; text-align: center;">
<tbody>
<tr>
<td><p style="font-size: 1.875rem; margin:0;">👻</p><p style="margin:0; font-size: 0.875rem;">物理接触</p></td>
<td style="font-size: 1.5rem; color: #6B7280;">→</td>
<td><p style="font-size: 1.875rem; margin:0;">💾</p><p style="margin:0; font-size: 0.875rem;">离线挂载</p></td>
<td style="font-size: 1.5rem; color: #6B7280;">→</td>
<td><p style="font-size: 1.875rem; margin:0;">📝</p><p style="margin:0; font-size: 0.875rem;">篡改文件</p></td>
</tr>
</tbody>
</table>
<div style="width: 100%; text-align: center; font-size: 1.5rem; margin: 0.75rem 0; color: #F87171;">↓</div>
<h5 style="font-weight: bold; color: #F87171; text-align: center; margin-bottom: 0.5rem;">关键漏洞：仅有IMA的系统为何会失效？</h5>
<div style="background-color: rgba(0,0,0,0.5); padding: 1rem; border-radius: 8px; border: 1px solid #F87171;">
<p style="font-size: 0.875rem; margin-top: 0; margin-bottom: 0.5rem;">攻击者不仅修改了文件内容，还利用离线权限，重新计算并覆盖了文件的“合法”哈希值。</p>
<div style="font-family: monospace; font-size: 0.75rem; color: #F87171; background: #111827; padding: 10px; border-radius: 5px; text-align: left;">
<p style="margin:0;">1. # echo 'malware' > /bin/sudo</p>
<p style="margin:0.25rem 0;">2. # new_hash=$(sha256sum /bin/sudo)</p>
<p style="margin:0;">3. # setfattr -n security.ima -v $new_hash /bin/sudo</p>
</div>
<p style="font-size: 0.875rem; margin-top: 0.75rem; margin-bottom: 0; text-align: center; color: #FCD34D;">当系统重启后，IMA会发现哈希匹配，从而错误地信任了被篡改的文件！</p>
</div>
</div>
</div>
</td>
</tr>
</tbody>
</table>
</div>

<!-- PART 2: ARCHITECTURE BLUEPRINT -->

<div id="part2" style="padding-top: 4rem; margin-top: -4rem;">
<h3 style="font-size: 1.875rem; font-weight: bold; text-align: center; margin-bottom: 3rem; color: white; text-shadow: 0 0 8px rgba(0, 168, 89, 0.8), 0 0 10px rgba(0, 168, 89, 0.6);">第二部分: 零信任内核架构蓝图</h3>
<div style="background-color: #1B2D24; border: 1px solid #005A34; padding: 1.5rem; border-radius: 8px; margin-bottom: 2rem;">
<h4 style="font-size: 1.5rem; font-weight: bold; text-align: center; color: #00A859; margin-bottom: 1rem; margin-top:0;">2.1 信任链原则：建立不可动摇的基石</h4>
<div style="text-align: center;">
<div style="display: inline-block; padding: 1rem; background-color: #0F1A13; border-radius: 8px;">
<p style="font-size: 3rem; margin: 0;">⚓</p>
<p style="font-weight: bold; font-size: 1.125rem; margin-top: 0.5rem;">硬件信任根 (TPM 2.0)</p>
</div>
<div style="font-size: 2.25rem; color: #6B7280; font-weight: 200; margin: 0.5rem 0;">↓</div>
<table style="width: auto; margin: 0 auto; border-spacing: 0.5rem; border-collapse: separate;">
<tbody>
<tr>
<td style="padding: 0.75rem; background-color: #166534; border-radius: 8px; width: 12rem; text-align:center;">安全启动 (UKI)</td>
<td style="font-size: 1.5rem; color: #6B7280; vertical-align: middle;">→</td>
<td style="padding: 0.75rem; background-color: #15803D; border-radius: 8px; width: 12rem; text-align:center;">内核空间</td>
<td style="font-size: 1.5rem; color: #6B7280; vertical-align: middle;">→</td>
<td style="padding: 0.75rem; background-color: #16A34A; border-radius: 8px; width: 12rem; text-align:center;">运行时软件</td>
</tr>
</tbody>
</table>
</div>
<p style="text-align: center; margin-top: 1.5rem; color: #D1D5DB;">一个安全的系统必须建立在一条信任链之上，其起点是物理上不可更改的硬件信任根。海姆达尔计划的核心就是将这条链延伸至系统的每一个角落。</p>
</div>
<div style="background-color: #1B2D24; border: 1px solid #005A34; padding: 1.5rem; border-radius: 8px; margin-bottom: 2rem;">
<h4 style="font-size: 1.5rem; font-weight: bold; text-align: center; color: #00A859; margin-bottom: 1.5rem; margin-top:0;">2.2 可验证完整性的四大支柱</h4>
<table style="width: 100%; border-collapse: collapse; border-spacing: 0;">
<tbody>
<tr>
<td style="width: 25%; padding: 0 0.75rem; vertical-align: top;">
<div style="text-align: center; padding: 1rem; background-color: #0F1A13; border-radius: 8px; height: 100%;"><p style="font-size: 2.25rem; margin:0;">🕵️</p><h5 style="font-weight: bold; margin-top: 0.5rem;">IMA</h5><p style="font-size: 0.75rem; color: #9CA3AF; margin-bottom: 0.5rem;">运行时哨兵</p><p style="font-size: 0.875rem; margin:0;">评估文件<strong style="color: #4ADE80;">内容</strong>是否被篡改。</p></div>
</td>
<td style="width: 25%; padding: 0 0.75rem; vertical-align: top;">
<div style="text-align: center; padding: 1rem; background-color: #0F1A13; border-radius: 8px; height: 100%;"><p style="font-size: 2.25rem; margin:0;">🔗</p><h5 style="font-weight: bold; margin-top: 0.5rem;">EVM</h5><p style="font-size: 0.75rem; color: #9CA3AF; margin-bottom: 0.5rem;">离线防御者</p><p style="font-size: 0.875rem; margin:0;">保护文件<strong style="color: #FBBF24;">元数据</strong>（包括IMA哈希）不被伪造。</p></div>
</td>
<td style="width: 25%; padding: 0 0.75rem; vertical-align: top;">
<div style="text-align: center; padding: 1rem; background-color: #0F1A13; border-radius: 8px; height: 100%;"><p style="font-size: 2.25rem; margin:0;">🛡️</p><h5 style="font-weight: bold; margin-top: 0.5rem;">TPM 2.0</h5><p style="font-size: 0.75rem; color: #9CA3AF; margin-bottom: 0.5rem;">硬件锚点</p><p style="font-size: 0.875rem; margin:0;">提供防篡改的<strong style="color: #60A5FA;">密钥存储</strong>与<strong style="color: #60A5FA;">测量日志</strong>。</p></div>
</td>
<td style="width: 25%; padding: 0 0.75rem; vertical-align: top;">
<div style="text-align: center; padding: 1rem; background-color: #0F1A13; border-radius: 8px; height: 100%;"><p style="font-size: 2.25rem; margin:0;">📦</p><h5 style="font-weight: bold; margin-top: 0.5rem;">UKI</h5><p style="font-size: 0.75rem; color: #9CA3AF; margin-bottom: 0.5rem;">原子化启动</p><p style="font-size: 0.875rem; margin:0;">将<strong style="color: #A78BFA;">安全策略</strong>与内核一同签名，防止绕过。</p></div>
</td>
</tr>
</tbody>
</table>
</div>
<div style="background-color: #1B2D24; border: 1px solid #005A34; padding: 2rem; border-radius: 8px;">
<h4 style="font-size: 1.5rem; font-weight: bold; text-align: center; color: #00A859; margin-bottom: 1.5rem; margin-top:0;">2.3 协同作战：一个统一的防御体系</h4>
<div style="border: 2px dashed #005A34; padding: 1.5rem; border-radius: 8px; max-width: 80%; margin: 0 auto;">
<div style="text-align: center; margin-bottom: 1.5rem;"><p style="font-weight: bold; font-size: 1.125rem;">场景: 用户执行 <code style="background-color: rgba(0,0,0,0.5); padding: 0.25rem 0.5rem; border-radius: 4px; color: #E5E7EB; font-family: monospace;">sudo ls</code></p></div>
<div style="display: flex; flex-direction: column; align-items: center; text-align: center; gap: 0;">
<div style="background-color: #1B2D24; border: 1px solid #005A34; padding: 1rem; border-radius: 8px; width: 100%;"><h5 style="font-weight: bold; font-size: 1.125rem; color: #6BDBAD; margin:0;">🚀 启动时: 信任锚定</h5><p style="font-size: 0.75rem; margin:0.25rem 0 0 0; color: #9CA3AF;">TPM检查<strong style="color: #60A5FA;">PCR7</strong>值，确认安全启动状态后，解封EVM密钥。</p></div>
<div style="width: 2px; height: 1rem; background-color: #005A34; margin: 0.5rem auto;"></div>
<div style="background-color: #1B2D24; border: 1px solid #005A34; padding: 1rem; border-radius: 8px; width: 100%;"><h5 style="font-weight: bold; font-size: 1.125rem; color: #6BDBAD; margin:0;">🔑 第1步: EVM验证元数据</h5><p style="font-size: 0.75rem; margin:0.25rem 0 0 0; color: #9CA3AF;">内核使用解封的密钥，验证<strong style="color: #FBBF24;">EVM签名</strong>。此举确保文件的IMA哈希值本身是可信的。</p></div>
<div style="width: 2px; height: 1rem; background-color: #005A34; margin: 0.5rem auto;"></div>
<div style="background-color: #1B2D24; border: 1px solid #005A34; padding: 1rem; border-radius: 8px; width: 100%;"><h5 style="font-weight: bold; font-size: 1.125rem; color: #6BDBAD; margin:0;">🕵️ 第2步: IMA评估文件内容</h5><p style="font-size: 0.75rem; margin:0.25rem 0 0 0; color: #9CA3AF;">内核计算文件实时哈希，并与可信的<strong style="color: #4ADE80;">IMA哈希</strong>对比。</p></div>
<div style="width: 2px; height: 1rem; background-color: #005A34; margin: 0.5rem auto;"></div>
<table style="width: 100%; border-spacing: 1rem; margin-top: 0.5rem; border-collapse: separate;">
<tbody>
<tr>
<td style="width: 50%; padding: 1rem; border-radius: 8px; text-align: center; background-color: rgba(22, 101, 52, 0.5); border: 1px solid #22C55E;"><p style="font-size: 1.25rem; font-weight: bold; color: #4ADE80; margin:0;">✅ 全部通过</p><p style="font-size: 0.875rem; margin:0.25rem 0 0 0;">允许执行</p></td>
<td style="width: 50%; padding: 1rem; border-radius: 8px; text-align: center; background-color: rgba(153, 27, 27, 0.5); border: 1px solid #EF4444;"><p style="font-size: 1.25rem; font-weight: bold; color: #F87171; margin:0;">❌ 任何一步失败</p><p style="font-size: 0.875rem; margin:0.25rem 0 0 0;">拒绝访问</p></td>
</tr>
</tbody>
</table>
</div>
</div>
</div>
</div>

<!-- PART 3: IMPLEMENTATION -->

<div id="part3" style="padding-top: 4rem; margin-top: -4rem;">
<h3 style="font-size: 1.875rem; font-weight: bold; text-align: center; margin-bottom: 3rem; color: white; text-shadow: 0 0 8px rgba(0, 168, 89, 0.8), 0 0 10px rgba(0, 168, 89, 0.6);">第三部分: 实施案例研究</h3>
<table style="width: 100%; border-spacing: 2rem; border-collapse: separate;">
<tbody>
<tr>
<td style="width: 50%; background-color: #1B2D24; border: 1px solid #005A34; padding: 1.5rem; border-radius: 8px; vertical-align: top;">
<h4 style="font-size: 1.25rem; font-weight: bold; text-align: center; color: #00A859; margin-top: 0; margin-bottom: 1rem;">3.1 定制核心：铸造安全基石</h4>
<table style="width: 100%; text-align: center; margin-top: 1rem;">
<tbody>
<tr>
<td><p style="font-size: 1.875rem; margin:0;">⚙️</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">起点: 通用内核</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">功能丰富但攻击面大</p></td>
<td><p style="font-size: 1.875rem; margin:0;">🛡️</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">加固</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">移除非必需模块</p></td>
<td><p style="font-size: 1.875rem; margin:0;">🚦</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">开启</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">激活IMA/EVM/TPM</p></td>
<td><p style="font-size: 1.875rem; margin:0;">💎</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">终点: 强化核心</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">精简、坚固、安全</p></td>
</tr>
</tbody>
</table>
<p style="font-size: 0.75rem; margin-top: 1.5rem; text-align: center; color: #9CA3AF;">此流程遵循“最小权限”原则，通过加固和开启安全模块，将通用内核重塑为一个专为安全而生的、最小化的可信计算基。</p>
</td>
<td style="width: 50%; background-color: #1B2D24; border: 1px solid #005A34; padding: 1.5rem; border-radius: 8px; vertical-align: top;">
<h4 style="font-size: 1.25rem; font-weight: bold; text-align: center; color: #00A859; margin-top: 0; margin-bottom: 1rem;">3.2 分层密钥管理策略</h4>
<table style="width: 100%; text-align: center; margin-top: 1rem;">
<tbody>
<tr>
<td><p style="font-size: 1.875rem; margin:0;">🏛️</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">1. 创建根信任</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">建立离线IMA根CA</p></td>
<td><p style="font-size: 1.875rem; margin:0;">✍️</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">2. 签发工作密钥</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">用于日常文件签名</p></td>
<td><p style="font-size: 1.875rem; margin:0;">🧠</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">3. 嵌入内核</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">将根CA公钥编译进去</p></td>
<td><p style="font-size: 1.875rem; margin:0;">🛡️</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">4. 硬件密封</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">用TPM密封EVM密钥</p></td>
</tr>
</tbody>
</table>
<p style="font-size: 0.75rem; margin-top: 1.5rem; text-align: center; color: #9CA3AF;">此策略将软件层面的信任（IMA CA）与硬件锚定的信任（EVM密钥）分离又结合，构建了一个既灵活又坚固的加密骨干。</p>
</td>
</tr>
<tr>
<td style="width: 50%; background-color: #1B2D24; border: 1px solid #005A34; padding: 1.5rem; border-radius: 8px; vertical-align: top;">
<h4 style="font-size: 1.25rem; font-weight: bold; text-align: center; color: #00A859; margin-top: 0; margin-bottom: 1rem;">3.3 分阶段部署策略</h4>
<table style="width: 100%; text-align: center; margin-top: 1rem;">
<tbody>
<tr>
<td><p style="font-size: 1.875rem; margin:0;">🧐</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">1. 审计模式</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">ima_appraise=log</p></td>
<td><p style="font-size: 1.875rem; margin:0;">🏷️</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">2. 修复与标记</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">ima_appraise=fix</p></td>
<td><p style="font-size: 1.875rem; margin:0;">✅</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">3. 验证基线</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">检查日志确保无误</p></td>
<td><p style="font-size: 1.875rem; margin:0;">🚦</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">4. 强制执行</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">ima_appraise=enforce</p></td>
</tr>
</tbody>
</table>
<p style="font-size: 0.75rem; margin-top: 1.5rem; text-align: center; color: #9CA3AF;">这种渐进式方法确保了从宽松到严格的安全策略过渡是平滑且可控的，最大限度地减少了对生产环境的冲击。</p>
</td>
<td style="width: 50%; background-color: #1B2D24; border: 1px solid #005A34; padding: 1.5rem; border-radius: 8px; vertical-align: top;">
<h4 style="font-size: 1.25rem; font-weight: bold; text-align: center; color: #00A859; margin-top: 0; margin-bottom: 1rem;">3.4 不可变启动：固化安全策略</h4>
<table style="width: 100%; text-align: center; margin-top: 1rem;">
<tbody>
<tr>
<td><p style="font-size: 1.875rem; margin:0;">📦</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">1. 打包</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">内核+安全策略+Initrd</p></td>
<td><p style="font-size: 1.875rem; margin:0;">✍️</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">2. 签名</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">使用安全启动密钥</p></td>
<td><p style="font-size: 1.875rem; margin:0;">🚀</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">3. 加载</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">引导加载程序加载</p></td>
<td><p style="font-size: 1.875rem; margin:0;">🛡️</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">4. 验证</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">UEFI固件验证签名</p></td>
</tr>
</tbody>
</table>
<p style="font-size: 0.75rem; margin-top: 1.5rem; text-align: center; color: #9CA3AF;">此流程将安全策略本身变成一个受硬件保护的加密对象，彻底关闭了通过修改引导参数来绕过安全机制的后门。</p>
</td>
</tr>
</tbody>
</table>
</div>

<!-- PART 4: VALIDATION -->

<div id="part4" style="padding-top: 4rem; margin-top: -4rem;">
<h3 style="font-size: 1.875rem; font-weight: bold; text-align: center; margin-bottom: 3rem; color: white; text-shadow: 0 0 8px rgba(0, 168, 89, 0.8), 0 0 10px rgba(0, 168, 89, 0.6);">第四部分: 实证验证与安全分析</h3>
<table style="width: 100%; border-spacing: 2rem; border-collapse: separate;">
<tbody>
<tr>
<td style="width: 50%; background-color: #1B2D24; border: 1px solid #005A34; padding: 1.5rem; border-radius: 8px; vertical-align: top;">
<h4 style="font-size: 1.5rem; font-weight: bold; text-align: center; color: #00A859; margin-top: 0; margin-bottom: 1rem;">4.1 场景一：运行时攻击</h4>
<table style="width: 100%; text-align: center; margin-top: 1rem;">
<tbody>
<tr>
<td><p style="font-size: 1.875rem; margin:0;">✅</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">1. 初始状态</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">/usr/bin/ls 文件受IMA保护</p></td>
<td><p style="font-size: 1.875rem; margin:0;">✍️</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">2. 攻击行为</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">攻击者篡改文件内容</p></td>
<td><p style="font-size: 1.875rem; margin:0;">🚫</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">3. 执行尝试</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">用户或系统尝试运行</p></td>
<td><p style="font-size: 1.875rem; margin:0;">🛡️</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">4. IMA 拦截</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">哈希不匹配，访问被拒绝</p></td>
</tr>
</tbody>
</table>
<p style="font-size: 0.75rem; margin-top: 1.5rem; text-align: center; color: #9CA3AF;">此演示证明IMA评估机制能有效阻止对受保护文件的任何运行时篡改，确保了可执行文件的完整性。</p>
</td>
<td style="width: 50%; background-color: #1B2D24; border: 1px solid #005A34; padding: 1.5rem; border-radius: 8px; vertical-align: top;">
<h4 style="font-size: 1.5rem; font-weight: bold; text-align: center; color: #00A859; margin-top: 0; margin-bottom: 1rem;">4.2 场景二：离线攻击</h4>
<table style="width: 100%; text-align: center; margin-top: 1rem;">
<tbody>
<tr>
<td><p style="font-size: 1.875rem; margin:0;">👻</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">1. 离线篡改</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">攻击者修改/bin/sudo</p></td>
<td><p style="font-size: 1.875rem; margin:0;">📝</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">2. 伪造哈希</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">攻击者更新security.ima</p></td>
<td><p style="font-size: 1.875rem; margin:0;">🔑</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">3. 攻击失败点</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">无法伪造EVM签名(密钥被TPM密封)</p></td>
<td><p style="font-size: 1.875rem; margin:0;">🛡️</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">4. EVM 防御</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">开机后EVM检测到签名无效</p></td>
</tr>
</tbody>
</table>
<p style="font-size: 0.75rem; margin-top: 1.5rem; text-align: center; color: #9CA3AF;">此分析证明了EVM与TPM的协同作用是防御离线攻击的关键，它保护了信任链中最脆弱的一环——元数据。</p>
</td>
</tr>
</tbody>
</table>
</div>

<!-- PART 5: STRATEGIC VALUE -->

<div id="part5" style="padding-top: 4rem; margin-top: -4rem;">
<h3 style="font-size: 1.875rem; font-weight: bold; text-align: center; margin-bottom: 3rem; color: white; text-shadow: 0 0 8px rgba(0, 168, 89, 0.8), 0 0 10px rgba(0, 168, 89, 0.6);">第五部分: 战略价值与应用前景</h3>
<div style="display: flex; flex-direction: column; gap: 2rem;">
<div style="background-color: #1B2D24; border: 1px solid #005A34; padding: 1.5rem; border-radius: 8px;">
<h4 style="font-size: 1.5rem; font-weight: bold; text-align: center; color: #00A859; margin-top: 0; margin-bottom: 1rem;">5.1 内核级零信任架构</h4>
<div style="max-width: 80%; margin: 0 auto; display: flex; flex-direction: column; align-items: center; text-align: center; gap: 1rem; margin-top: 1rem;">
<div style="background-color: #0F1A13; border: 1px solid #005A34; padding: 1rem; border-radius: 8px; width: 100%;"><h5 style="font-weight: bold; font-size: 1.125rem; color: #6BDBAD; margin:0;">🤔 原则一: 从不信任，永远验证</h5><p style="font-size: 0.75rem; color: #9CA3AF; margin: 0.25rem 0 0 0;">系统不再假定内部文件可信，每次访问都需实时验证。</p></div>
<div style="background-color: #0F1A13; border: 1px solid #005A34; padding: 1rem; border-radius: 8px; width: 100%;"><h5 style="font-weight: bold; font-size: 1.125rem; color: #6BDBAD; margin:0;">🏰 原则二: 假设泄露</h5><p style="font-size: 0.75rem; color: #9CA3AF; margin: 0.25rem 0 0 0;">防御内置于系统底层，而非依赖脆弱的边界。</p></div>
<div style="background-color: #0F1A13; border: 1px solid #005A34; padding: 1rem; border-radius: 8px; width: 100%;"><h5 style="font-weight: bold; font-size: 1.125rem; color: #6BDBAD; margin:0;">👮 原则三: 最小权限</h5><p style="font-size: 0.75rem; color: #9CA3AF; margin: 0.25rem 0 0 0;">即便是root也无法执行被篡改的代码，限制破坏范围。</p></div>
</div>
</div>
<div style="background-color: #1B2D24; border: 1px solid #005A34; padding: 1.5rem; border-radius: 8px;">
<h4 style="font-size: 1.5rem; font-weight: bold; text-align: center; color: #00A859; margin-top: 0; margin-bottom: 1rem;">5.2 赋能远程证明</h4>
<table style="width: 100%; text-align: center; margin-top: 1rem;">
<tbody>
<tr>
<td><p style="font-size: 1.875rem; margin:0;">❓</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">1. 挑战</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">验证者发送随机数</p></td>
<td><p style="font-size: 1.875rem; margin:0;">✍️</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">2. 引用</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">TPM对PCR和随机数签名</p></td>
<td><p style="font-size: 1.875rem; margin:0;">📨</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">3. 响应</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">发送引用和IMA日志</p></td>
<td><p style="font-size: 1.875rem; margin:0;">✅</p><p style="font-weight: bold; font-size: 0.875rem; margin: 0.25rem 0;">4. 验证</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">验证者重放日志并比对</p></td>
</tr>
</tbody>
</table>
</div>
<div style="background-color: #1B2D24; border: 1px solid #005A34; padding: 1.5rem; border-radius: 8px;">
<h4 style="font-size: 1.5rem; font-weight: bold; text-align: center; color: #00A859; margin-top: 0; margin-bottom: 1rem;">5.3 在高风险环境中的应用</h4>
<table style="width: 100%; text-align: center; margin-top: 1rem;">
<tbody>
<tr>
<td><p style="font-size: 2.25rem; margin:0;">☁️</p><p style="font-weight: bold; font-size: 0.875rem; margin-top: 0.5rem;">云计算</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">确保VM镜像完整性，为客户提供可信证明。</p></td>
<td><p style="font-size: 2.25rem; margin:0;">🏭</p><p style="font-weight: bold; font-size: 0.875rem; margin-top: 0.5rem;">关键基础设施</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">锁定工控系统软件，防止未经授权的变更。</p></td>
<td><p style="font-size: 2.25rem; margin:0;">🛰️</p><p style="font-weight: bold; font-size: 0.875rem; margin-top: 0.5rem;">物联网 (IoT)</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">保证海量设备固件安全，实现可信远程管理。</p></td>
<td><p style="font-size: 2.25rem; margin:0;">💳</p><p style="font-weight: bold; font-size: 0.875rem; margin-top: 0.5rem;">金融服务</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">保护交易软件，提供不可变的审计追踪。</p></td>
</tr>
</tbody>
</table>
</div>
</div>
</div>

<!-- PART 6: CONCLUSION -->

<div id="part6" style="padding-top: 4rem; margin-top: -4rem;">
<h3 style="font-size: 1.875rem; font-weight: bold; text-align: center; margin-bottom: 3rem; color: white; text-shadow: 0 0 8px rgba(0, 168, 89, 0.8), 0 0 10px rgba(0, 168, 89, 0.6);">第六部分: 结论与展望</h3>
<div style="display: flex; flex-direction: column; gap: 2rem;">
<div style="background-color: #1B2D24; border: 1px solid #005A34; padding: 1.5rem; border-radius: 8px;">
<h4 style="font-size: 1.5rem; font-weight: bold; text-align: center; color: #00A859; margin-top: 0; margin-bottom: 1rem;">6.1 成果总结</h4>
<div style="max-width: 80%; margin: 0 auto; display: flex; flex-direction: column; align-items: center; text-align: center; gap: 1rem; margin-top: 1rem;">
<div style="background-color: #0F1A13; border: 1px solid #005A34; padding: 1rem; border-radius: 8px; width: 100%;"><h5 style="font-weight: bold; font-size: 1.125rem; color: #6BDBAD; margin:0;">🔗 端到端信任链</h5><p style="font-size: 0.75rem; color: #9CA3AF; margin: 0.25rem 0 0 0;">成功构建了从硬件加电到应用程序运行的、完整且可验证的信任链。</p></div>
<div style="background-color: #0F1A13; border: 1px solid #005A34; padding: 1rem; border-radius: 8px; width: 100%;"><h5 style="font-weight: bold; font-size: 1.125rem; color: #6BDBAD; margin:0;">🛡️ 深度防御</h5><p style="font-size: 0.75rem; color: #9CA3AF; margin: 0.25rem 0 0 0;">有效抵御了包括运行时代码注入和离线物理篡改在内的多种高级威胁。</p></div>
<div style="background-color: #0F1A13; border: 1px solid #005A34; padding: 1rem; border-radius: 8px; width: 100%;"><h5 style="font-weight: bold; font-size: 1.125rem; color: #6BDBAD; margin:0;">🎯 零信任落地</h5><p style="font-size: 0.75rem; color: #9CA3AF; margin: 0.25rem 0 0 0;">将零信任安全理念在操作系统核心层面进行了切实的工程化落地。</p></div>
</div>
</div>
<div style="background-color: #1B2D24; border: 1px solid #005A34; padding: 1.5rem; border-radius: 8px;">
<h4 style="font-size: 1.5rem; font-weight: bold; text-align: center; color: #00A859; margin-top: 0; margin-bottom: 1rem;">6.2 未来展望</h4>
<table style="width: 100%; text-align: center; margin-top: 1rem;">
<tbody>
<tr>
<td><p style="font-size: 2.25rem; margin:0;">📡</p><p style="font-weight: bold; font-size: 0.875rem; margin-top: 0.5rem;">集成远程证明</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">与Keylime等验证器集成，实现自动化信任监控。</p></td>
<td><p style="font-size: 2.25rem; margin:0;">🔬</p><p style="font-weight: bold; font-size: 0.875rem; margin-top: 0.5rem;">细粒度策略</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">为特定应用（如数据库）定制更精确的保护策略。</p></td>
<td><p style="font-size: 2.25rem; margin:0;">⏱️</p><p style="font-weight: bold; font-size: 0.875rem; margin-top: 0.5rem;">性能基准测试</p><p style="font-size: 0.75rem; color: #9CA3AF; margin:0;">量化不同策略对系统性能的影响，指导部署。</p></td>
</tr>
</tbody>
</table>
</div>
</div>
</div>

</div>
