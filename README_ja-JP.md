<div align="center">
<a href="https://github.com/auveggry/Linux-Heimdall">
<img src="https://ptpimg.me/my2mi2.jpg" alt="北欧神話の守護神ヘイムダルのアートワーク" style="max-width: 800px; width: 100%; border-radius: 8px;">
</a>
<br><br>
<h3 style="color: #6BDBAD;">プロジェクト名の由来：神話と技術の交差点</h3>
<p>北欧神話において、守護神ヘイムダルはその超人的な知覚力と警戒心で知られています。このプロジェクトはその名にちなんで、その中心的な使命を強調しています：<br>Linuxカーネルのために、疲れを知らず、すべてを見通し、迅速に反応する究極の守護者を構築すること。</p>
<h1>ヘイムダル計画</h1>
<h2>Linux Heimdall</h2>
</div>

<div align="center">
<a href="https://github.com/auveggry/Linux-Heimdall/blob/main/LICENSE" target="_blank">
<img src="https://img.shields.io/badge/license-GPLv3-blue.svg?style=for-the-badge" alt="ライセンス">
</a>
<a href="https://github.com/auveggry/Linux-Heimdall/pulls" target="_blank">
<img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=for-the-badge" alt="PR歓迎">
</a>
<a href="#" target="_blank">
<img src="https://img.shields.io/badge/Linux%20Kernel-6.16.6-orange?style=for-the-badge" alt="カーネルバージョン">
</a>
<a href="https://github.com/auveggry/Linux-Heimdall" target="_blank">
<img src="https://img.shields.io/badge/GitHub-Stars-informational?style=for-the-badge" alt="GitHub stars">
</a>
<br>
<a href="README_zh-CN.md" target="_blank">
<img src="https://img.shields.io/badge/中国語版を読む-brightgreen.svg?style=for-the-badge" alt="中国語版">
</a>
<a href="README_ja-JP.md" target="_blank">
<img src="https://img.shields.io/badge/日本語版を読む-blue.svg?style=for-the-badge" alt="日本語版">
</a>
<br>
<a href="https://sakurame.eu.org/2025/08/07/privacy/%E4%B8%80%E4%B8%AA%E5%BC%80%E6%BA%90%E7%9A%84Linux%E5%86%85%E6%A0%B8%E5%AE%89%E5%85%A8%E5%BC%BA%E5%8C%96%E9%A1%B9%E7%9B%AE/" target="_blank">
<img src="https://img.shields.io/badge/ブログで全文を読む-00A859?style=for-the-badge" alt="ブログで読む">
</a>
<br>
<a href="https://github.com/auveggry/Linux-Heimdall/releases/download/Stable/Linux-Heimdall.HandBook.ZH_CN.pdf" target="_blank">
<img src="https://img.shields.io/badge/中文-ハンドブック-blueviolet?style=for-the-badge" alt="中文ハンドブック">
</a>
<a href="https://github.com/auveggry/Linux-Heimdall/releases/download/Stable/Linux-Heimdall.HandBook.en_US.pdf" target="_blank">
<img src="https://img.shields.io/badge/English-HandBook-blueviolet?style=for-the-badge" alt="English Handbook">
</a>
<a href="https://github.com/auveggry/Linux-Heimdall/releases/download/Stable/Linux-Heimdall.HandBook.ja_JP.pdf" target="_blank">
<img src="https://img.shields.io/badge/日本語-ハンドブック-blueviolet?style=for-the-badge" alt="日本語ハンドブック">
</a>
<h3 align="center" style="color: #81C784;"><i>迅速に開始するために、<a href="https://github.com/auveggry/Linux-Heimdall/releases" style="color: #96f999;">リリース・ページ</a>をご覧ください。そこには、完全なハンドブックと、プリコンパイル済みの Stable および Hardened カーネルが提供されています。</i></h3>
</div>

<p align="center">
<a href="#part1">ギャップ分析</a> •
<a href="#part2">アーキテクチャ設計図</a> •
<a href="#part3">実装研究</a> •
<a href="#part4">実証検証</a> •
<a href="#part5">戦略的価値</a> •
<a href="#part6">結論と展望</a>
</p>

<div id="part1"></div>
<h3 align="center">第一部: ギャップ分析</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="2">
<h4 align="center">1.1 セキュアブートの幻想：信頼の連鎖の断絶点</h4>
</td>
</tr>
<tr>
<td width="50%" align="center" valign="top">
<p><b><font color="#4ADE80">起動時検証</font></b></p>
<p>UEFI Firmware<br>↓<br>Bootloader<br>↓<br>Kernel Loaded</p>
<p>⚡️ <b><font color="#F87171">信頼の断絶</font></b> ⚡️</p>
<p>Runtime Vulnerable</p>
</td>
<td width="50%" valign="top">
<ul>
<li>🛡️ <b><font color="#4ADE80">フェーズ1：起動時検証</font></b><br><blockquote>UEFIファームウェアはブートローダーとカーネルの署名を検証し、起動プロセスの初期の純粋性を保証します。</blockquote></li>
<li>🏁 <b><font color="#FBBF24">フェーズ2：信頼の引き継ぎ</font></b><br><blockquote>カーネルが正常にロードされると、セキュアブートの使命は完了します。信頼の連鎖はこの時点で引き継がれますが、従来は延長されませんでした。</blockquote></li>
<li>🚨 <b><font color="#F87171">フェーズ3：ランタイムのリスク暴露</font></b><br><blockquote>すべてのユーザースペースのアプリケーション、ライブラリ、設定ファイルは監視されない状態にあり、攻撃者に広大な攻撃対象領域を残しています。</blockquote></li>
</ul>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<h4 align="center">1.2 ランタイムの脅威：システム内部からの裏切り</h4>
<p align="center">
<b><font color="#4ADE80">事前: 正当な実行</font></b><br>
💻<br>
<code>/bin/sudo</code><br>
✅
</p>
<p align="center">
🦠→ 🔓 → 😭<br>
<small><font color="#F87171">マルウェア注入</font></small>
</p>
<p align="center">
<b><font color="#F87171">事後: 悪意のある動作</font></b><br>
💀<br>
<code>/bin/sudo</code> (内容は改ざん済み)
</p>
<blockquote><b>重要な脆弱性：カーネルの死角</b><br>従来のカーネルはファイルの<b>内容</b>ではなく<b>パス</b>を信頼します。そのパスが指すファイルの内容が悪意を持って置き換えられたことを感知できません。</blockquote>
</td>
<td width="50%" valign="top">
<h4 align="center">1.3 オフラインの脅威：「邪悪なメイド」攻撃</h4>
<p align="center"><b>攻撃者の経路</b><br>👻 (物理的接触) → 💾 (オフラインマウント) → 📝 (ファイル改ざん)</p>
<br>
<blockquote><b>重要な脆弱性：IMAのみのシステムはなぜ失敗するのか？</b><br>攻撃者はファイルの内容を変更するだけでなく、オフライン権限を利用してファイルの「正当な」ハッシュ値を再計算し、上書きします。</blockquote>
<pre><code># 1. 正当なファイルを悪意のあるプログラムに置き換える
echo 'malware' > /bin/sudo

2. 新しい「正当な」ハッシュを再計算して偽造する
new_hash=$(sha256sum /bin/sudo)
setfattr -n security.ima -v "$new_hash" /bin/sudo</code></pre>

<p align="center"><font color="#FCD34D">システムが再起動すると、IMAは改ざんされたファイルを誤って信頼してしまいます！</font></p>
</td>
</tr>
</tbody>
</table>
<hr>

<div id="part2"></div>
<h3 align="center">第二部: ゼロトラスト・カーネル・アーキテクチャ設計図</h3>
<table width="100%">
<tbody>
<tr>
<td colspan="4">
<h4 align="center">2.1 信頼の連鎖の原則：揺るぎない礎の構築</h4>
<p align="center">
⚓ ハードウェアの信頼の起点 (TPM 2.0)<br>
↓<br>
セキュアブート (UKI) → カーネル空間 (IMA/EVM) → ランタイムソフトウェア
</p>
<blockquote><p align="center">安全なシステムは、物理的に変更不可能なハードウェアの信頼の起点を始点とする信頼の連鎖の上に構築されなければなりません。<br>ヘイムダル計画の核心は、この連鎖をシステムの隅々まで拡張することです。</p></blockquote>
</td>
</tr>
<tr>
<td colspan="4">
<h4 align="center">2.2 検証可能な完全性の四本柱</h4>
</td>
</tr>
<tr>
<td width="25%" align="center" valign="top">🕵️<br><b>IMA</b><br><small>ランタイムの番人</small><br><blockquote>ファイルの<b><font color="#4ADE80">内容</font></b>が改ざんされていないか評価します。</blockquote></td>
<td width="25%" align="center" valign="top">🔗<br><b>EVM</b><br><small>オフラインの防御者</small><br><blockquote>ファイルの<b><font color="#FBBF24">メタデータ</font></b>が偽造されるのを防ぎます。</blockquote></td>
<td width="25%" align="center" valign="top">🛡️<br><b>TPM 2.0</b><br><small>ハードウェアの錨</small><br><blockquote>改ざん防止の<b><font color="#60A5FA">鍵ストレージ</font></b>と<b><font color="#60A5FA">測定ログ</font></b>を提供します。</blockquote></td>
<td width="25%" align="center" valign="top">📦<br><b>UKI</b><br><small>アトミックな起動</small><br><blockquote><b><font color="#A78BFA">セキュリティポリシー</font></b>をカーネルと共に署名します。</blockquote></td>
</tr>
<tr>
<td colspan="4">
<h4 align="center">2.3 連携作戦：統一された防御システム</h4>
<p align="center"><b>シナリオ: ユーザーが <code>sudo ls</code> を実行</b></p>
<ol>
<li><b>🚀 起動時: 信頼の固定</b><br><blockquote>TPMは<font color="#60A5FA">PCR7</font>の値をチェックし、セキュアブートの状態を確認した後、EVMキーをアンシールします。</blockquote></li>
<li><b>🔑 ステップ1: EVMがメタデータを検証</b><br><blockquote>カーネルはアンシールされたキーを使用して<font color="#FBBF24">EVM署名</font>を検証し、IMAハッシュが信頼できることを保証します。</blockquote></li>
<li><b>🕵️ ステップ2: IMAがファイル内容を評価</b><br><blockquote>カーネルはファイルのリアルタイムハッシュを計算し、信頼できる<font color="#4ADE80">IMAハッシュ</font>と比較します。</blockquote></li>
</ol>
<p align="center">✅ <b><font color="#4ADE80">すべて通過:</font></b> 実行を許可 &nbsp;|&nbsp; ❌ <b><font color="#F87171">いずれかのステップで失敗:</font></b> アクセスを拒否</p>
</td>
</tr>
</tbody>
</table>
<hr>

<div id="part3"></div>
<h3 align="center">第三部: 実装研究</h3>
<table width="100%">
<tbody>
<tr>
<td width="50%" valign="top">
<h4 align="center">3.1 コアのカスタマイズ：セキュリティの礎を築く</h4>
<p align="center">⚙️ → 🛡️ → 🚦 → 💎</p>
<p align="center"><small>汎用カーネル → 強化 → 有効化 → 強化コア</small></p>
<blockquote><small>このプロセスは「最小権限」の原則に従い、汎用カーネルをセキュリティ専用の最小化された信頼できるコンピューティングベースに再構築します。</small></blockquote>
</td>
<td width="50%" valign="top">
<h4 align="center">3.2 階層的な鍵管理戦略</h4>
<p align="center">🏛️ → ✍️ → 🧠 → 🛡️</p>
<p align="center"><small>ルート信頼の作成 → 作業鍵の発行 → カーネルへの埋め込み → ハードウェアによる封印</small></p>
<blockquote><small>この戦略は、ソフトウェアレベルの信頼（IMA CA）とハードウェアに固定された信頼（EVMキー）を分離しつつ組み合わせ、柔軟かつ堅牢な暗号化バックボーンを構築します。</small></blockquote>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<h4 align="center">3.3 段階的な展開戦略</h4>
<p align="center">🧐 → 🏷️ → 🧬 → 🚦</p>
<p align="center"><small>監査モード → 修正とラベリング → ベースラインの検証 → 強制実行</small></p>
<blockquote><small>この段階的なアプローチは、緩やかなポリシーから厳格なポリシーへの移行をスムーズかつ制御可能にし、本番環境への影響を最小限に抑えます。</small></blockquote>
</td>
<td width="50%" valign="top">
<h4 align="center">3.4 不変の起動：セキュリティポリシーの固定化</h4>
<p align="center">📦 → ✍️ → 🚀 → 🛡️</p>
<p align="center"><small>パッケージ化 → 署名 → ロード → 検証</small></p>
<blockquote><small>このプロセスは、セキュリティポリシー自体をハードウェアで保護された暗号オブジェクトに変え、ブートパラメータを変更してセキュリティメカニズムをバイパスするバックドアを完全に閉じます。</small></blockquote>
</td>
</tr>
</tbody>
</table>
<hr>

<div id="part4"></div>
<h3 align="center">第四部: 実証検証とセキュリティ分析</h3>
<table width="100%">
<tbody>
<tr>
<td width="50%" valign="top">
<h4 align="center">4.1 シナリオ1：ランタイム攻撃</h4>
<p align="center">🌕 → ✍️ → 🚫 → 🛡️</p>
<p align="center"><small>初期状態 → 攻撃行為 → 実行試行 → IMAによる阻止</small></p>
<blockquote><small>このデモは、IMA評価メカニズムが保護されたファイルへのランタイム改ざんを効果的に防ぎ、実行ファイルの完全性を保証することを示しています。</small></blockquote>
</td>
<td width="50%" valign="top">
<h4 align="center">4.2 シナリオ2：オフライン攻撃</h4>
<p align="center">👻 → 📝 → 🔑 → 🛡️</p>
<p align="center"><small>オフライン改ざん → ハッシュ偽造 → 攻撃失敗点 → EVMによる防御</small></p>
<blockquote><small>この分析は、EVMとTPMの相乗効果がオフライン攻撃に対する防御の鍵であり、信頼の連鎖の最も脆弱なリンクであるメタデータを保護することを示しています。</small></blockquote>
</td>
</tr>
</tbody>
</table>
<hr>

<div id="part5"></div>
<h3 align="center">第五部: 戦略的価値と応用展望</h3>
<table width="100%">
<tbody>
<tr>
<td width="50%" valign="top">
<h4 align="center">5.1 カーネルレベルのゼロトラスト・アーキテクチャ</h4>
<ul>
<li><b>🤔 信頼せず、常に検証する:</b><br><blockquote><small>システムはもはや内部ファイルが信頼できるとは仮定せず、すべてのアクセスにリアルタイムの検証が必要です。</small></blockquote></li>
<li><b>🏰 侵害を想定する:</b><br><blockquote><small>防御は脆弱な境界に依存するのではなく、システムのコアに組み込まれています。</small></blockquote></li>
<li><b>👮 最小権限:</b><br><blockquote><small>rootでさえ改ざんされたコードを実行できず、潜在的な損害の範囲を制限します。</small></blockquote></li>
</ul>
</td>
<td width="50%" valign="top">
<h4 align="center">5.2 リモートアテステーションの実現</h4>
<ul><li><b>⚡ → ✍️ → 📨 → 🌀</b><br><blockquote><small>チャレンジ → クォート → レスポンス → 検証</small></blockquote></li></ul>
<h4 align="center">5.3 高リスク環境での応用</h4>
<ul>
<li>☁️ <b>クラウドコンピューティング:</b> <small>VMイメージの完全性を保証します。</small></li>
<li>🏭 <b>重要インフラ:</b> <small>産業用制御システム（ICS）ソフトウェアをロックダウンします。</small></li>
<li>🛰️ <b>モノのインターネット (IoT):</b> <small>大量のデバイスのファームウェアを保護します。</small></li>
<li>💳 <b>金融サービス:</b> <small>取引ソフトウェアを保護します。</small></li>
</ul>
</td>
</tr>
</tbody>
</table>
<hr>

<div id="part6"></div>
<h3 align="center">第六部: 結論と展望</h3>
<table width="100%">
<tbody>
<tr>
<td width="50%" valign="top">
<h4 align="center">6.1 成果のまとめ</h4>
<ul>
<li><b>🔗 エンドツーエンドの信頼の連鎖:</b> <blockquote>ハードウェアの電源投入からアプリケーションの実行まで、完全で検証可能な信頼の連鎖を正常に構築しました。</blockquote></li>
<li><b>🛡️ 多層防御:</b> <blockquote>ランタイムのコードインジェクションやオフラインの物理的改ざんなど、複数の高度な脅威を効果的に防御しました。</blockquote></li>
<li><b>🎯 ゼロトラストの実現:</b> <blockquote>ゼロトラストのセキュリティ概念をオペレーティングシステムのコアレベルで実践的に実装しました。</blockquote></li>
</ul>
</td>
<td width="50%" valign="top">
<h4 align="center">6.2 将来の展望</h4>
<ul>
<li><b>📡 リモートアテステーションの統合:</b> <blockquote>Keylimeなどの検証ツールと統合し、自動化された信頼監視を実現します。</blockquote></li>
<li><b>🔬 きめ細やかなポリシー:</b> <blockquote>特定のアプリケーション（例：データベース）向けに、より正確な保護ポリシーをカスタマイズします。</blockquote></li>
<li><b>⏱️ パフォーマンスのベンチマーク:</b> <blockquote>さまざまなセキュリティポリシーがシステムパフォーマンスに与える影響を定量化し、展開をガイドします。</blockquote></li>
</ul>
</td>
</tr>
</tbody>
</table>
