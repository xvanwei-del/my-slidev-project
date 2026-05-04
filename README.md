---
theme: default
css: ./style.css
title: 基本的算法策略 - 迭代算法
---

<!-- 第1页：封面页 -->
<div class="deck-wrapper">
  <div class="slide-container">
    <div class="slide slide-cover active" id="slide-1">
      <div class="stars-bg"></div>
      <div class="cover-orbit"></div>
      <div class="cover-orbit cover-orbit-2"></div>
      <div class="cover-content">
        <div class="cover-badge">Chapter 4</div>
        <div class="cover-title">基本的算法策略<br>迭代算法</div>
        <div class="cover-subtitle">Algorithm Design & Analysis</div>
        <div class="cover-chapters">
          <div class="cover-chip active-chip">4.1 迭代算法</div>
          <div class="cover-chip">4.2 蛮力法</div>
          <div class="cover-chip">4.3 分而治之</div>
          <div class="cover-chip">4.4 贪婪算法</div>
          <div class="cover-chip">4.5 动态规划</div>
        </div>
      </div>
    </div>
  </div>
</div>

---

<!-- 第2页：迭代策略总览 -->
<div class="deck-wrapper">
  <div class="slide-container">
    <div class="slide slide-overview active" id="slide-2">
      <div class="overview-left">
        <div class="overview-left-title">迭代算法<br>核心思想</div>
        <div class="overview-left-sub">用旧值算新值<br>一般用于数值计算<br><br>控制方式：<br>· 固定次数结束<br>· 特定条件结束</div>
      </div>
      <div class="overview-right">
        <div class="ov-card">
          <div class="ov-icon icon-green">→</div>
          <div>
            <div class="ov-card-title">递推法（正推）</div>
            <div class="ov-card-desc">由前向后解问题，利用已知初值逐步推算后续值</div>
          </div>
        </div>
        <div class="ov-card">
          <div class="ov-icon icon-purple">←</div>
          <div>
            <div class="ov-card-title">倒推法（逆推）</div>
            <div class="ov-card-desc">从结果出发，反向推算起始条件</div>
          </div>
        </div>
        <div class="ov-card">
          <div class="ov-icon icon-amber">≈</div>
          <div>
            <div class="ov-card-title">迭代法解方程</div>
            <div class="ov-card-desc">逐步逼近，构造收敛数列求方程近似根</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

---

<!-- 第3页：递推法（斐波那契） -->
<div class="deck-wrapper">
  <div class="slide-container">
    <div class="slide slide-recursive active" id="slide-3">
      <div class="sec-header">
        <div class="sec-num">4.1</div>
        <div class="sec-title">递推法 — 斐波那契数列（兔子问题）</div>
        <div class="sec-tag">Forward Iteration</div>
      </div>
      <div class="rabbit-grid">
        <div class="rabbit-left">
          <div class="problem-box">
            <strong>问题：</strong>一对兔子从出生后第三个月起每月生一对，假若兔子只生不死，一月份抱来一对刚出生的兔子，问一年中每月各有多少对？
          </div>
          <div class="formula-box">
            <div class="formula-label">迭代关系式</div>
            <div class="formula-main">yₙ = yₙ₋₁ + yₙ₋₂</div>
            <div class="formula-sub">初始条件：y₁ = y₂ = 1，n ≥ 3</div>
          </div>
          <div class="formula-box">
            <div class="formula-label">循环不变式</div>
            <div class="formula-sub" style="background:#f0fdf4;border-left:3px solid #10b981;font-size:12px;padding:8px 10px">
              设 a=前2月，b=前1月，c=当前<br>
              每轮：a←b，b←c，c←a+b
            </div>
          </div>
        </div>
        <div style="display:flex;flex-direction:column;gap:10px">
          <div class="fib-table">
            <table>
              <thead><tr>
                <th>月份</th><th>1</th><th>2</th><th>3</th><th>4</th><th>5</th><th>6</th><th>7</th>
              </tr></thead>
              <tbody>
                <tr>
                  <td style="font-weight:500;color:#374151">对数</td>
                  <td>1</td><td>1</td>
                  <td class="highlight">2</td>
                  <td class="highlight">3</td>
                  <td class="highlight">5</td>
                  <td class="highlight">8</td>
                  <td class="highlight">13</td>
                </tr>
              </tbody>
            </table>
          </div>
          <div class="code-box" style="flex:1;font-size:11px;line-height:1.7">
<span class="cm">// 迭代求斐波那契</span>
<span class="kw">int</span> <span class="var">a</span>=<span class="num">1</span>, <span class="var">b</span>=<span class="num">1</span>, <span class="var">c</span>;
<span class="kw">for</span> (<span class="var">i</span>=<span class="num">3</span>; <span class="var">i</span>&lt;=<span class="num">12</span>; <span class="var">i</span>++) {
    <span class="var">c</span> = <span class="var">a</span> + <span class="var">b</span>;
    <span class="fn">print</span>(<span class="var">i</span>, <span class="var">c</span>);
    <span class="var">a</span> = <span class="var">b</span>;
    <span class="var">b</span> = <span class="var">c</span>;
}</div>
          <div class="formula-box" style="padding:8px 12px">
            <div class="formula-label">辗转相除法 GCD</div>
            <div class="formula-sub" style="font-size:11px;line-height:1.7">
              gcd(m, n) = gcd(n, m % n)<br>
              循环直至余数为 0
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

---

<!-- 第4页：倒推法 -->
<div class="deck-wrapper">
  <div class="slide-container">
    <div class="slide slide-backward active" id="slide-4">
      <div class="sec-header">
        <div class="sec-num">4.2</div>
        <div class="sec-title">倒推法 — 从结果反推起始</div>
        <div class="sec-tag">Backward Iteration</div>
      </div>
      <div class="bw-grid">
        <div style="display:flex;flex-direction:column;gap:12px">
          <div class="bw-card bw-card-a">
            <div class="bw-label">正推 vs 倒推</div>
            <div class="compare-row">
              <div class="compare-icon ci-green">→</div>
              <div class="compare-text"><strong>正推：</strong>已知初始值，逐步推后续结果</div>
            </div>
            <div class="compare-row">
              <div class="compare-icon ci-purple">←</div>
              <div class="compare-text"><strong>倒推：</strong>已知末态，反向推算起始状态</div>
            </div>
          </div>
          <div class="bw-card bw-card-a">
            <div class="bw-label">猴子吃桃问题</div>
            <div class="bw-step-list">
              <div class="bw-step">
                <div class="bw-step-num">10</div>
                <div class="bw-step-text">第10天 <strong>1个</strong>桃</div>
              </div>
              <div class="bw-step">
                <div class="bw-step-num">9</div>
                <div class="bw-step-text">第n-1天 = <strong>(第n天 + 1) × 2</strong></div>
              </div>
              <div class="bw-step">
                <div class="bw-step-num">1</div>
                <div class="bw-step-text">倒推至第1天即为答案</div>
              </div>
            </div>
          </div>
          <div class="bw-card" style="background:rgba(16,185,129,0.08);border:1px solid rgba(16,185,129,0.25);flex:1">
            <div class="bw-label" style="color:#34d399">穿越沙漠问题</div>
            <div class="bw-step-list">
              <div class="bw-step">
                <div class="bw-step-num" style="background:rgba(16,185,129,0.2);border-color:rgba(16,185,129,0.4);color:#34d399">k</div>
                <div class="bw-step-text">第k段出发次数，走行 <strong>500/(2k-1)</strong> 公里</div>
              </div>
              <div class="bw-step">
                <div class="bw-step-num" style="background:rgba(16,185,129,0.2);border-color:rgba(16,185,129,0.4);color:#34d399">S</div>
                <div class="bw-step-text"><strong>S₁ = 500k，S₂ = S₁ - (2k-1)×x</strong></div>
              </div>
            </div>
          </div>
        </div>
        <div style="display:flex;flex-direction:column;gap:12px">
          <div class="bw-card bw-card-b">
            <div class="bw-label">杨辉三角 — 为何需要倒推？</div>
            <div class="pascal-vis" id="pascal-vis">
              <div class="pascal-row"><div class="pascal-cell bright">1</div></div>
              <div class="pascal-row"><div class="pascal-cell lit">1</div><div class="pascal-cell lit">1</div></div>
              <div class="pascal-row"><div class="pascal-cell lit">1</div><div class="pascal-cell bright">2</div><div class="pascal-cell lit">1</div></div>
              <div class="pascal-row"><div class="pascal-cell lit">1</div><div class="pascal-cell bright">3</div><div class="pascal-cell bright">3</div><div class="pascal-cell lit">1</div></div>
              <div class="pascal-row"><div class="pascal-cell lit">1</div><div class="pascal-cell lit">4</div><div class="pascal-cell bright">6</div><div class="pascal-cell lit">4</div><div class="pascal-cell lit">1</div></div>
            </div>
            <div style="font-size:11px;color:#64748b;text-align:center;margin-top:6px">a[i][j] = a[i-1][j-1] + a[i-1][j]</div>
          </div>
          <div class="bw-card bw-card-a" style="flex:1">
            <div class="bw-label">倒推避免覆盖</div>
            <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px">
              <div>
                <div style="font-size:10px;color:#ef4444;margin-bottom:4px;font-family:monospace">正推（错误）</div>
                <div style="font-family:monospace;font-size:10px;background:#1a0a0a;border:1px solid rgba(239,68,68,0.3);border-radius:6px;padding:7px;color:#fca5a5;line-height:1.7">A[j] = A[j-1] + A[j]<br>j = 2,3,...,i-1<br><span style="color:#6c7086">// 覆盖上一行数据！</span></div>
              </div>
              <div>
                <div style="font-size:10px;color:#34d399;margin-bottom:4px;font-family:monospace">倒推（正确）</div>
                <div style="font-family:monospace;font-size:10px;background:#0a1a12;border:1px solid rgba(52,211,153,0.3);border-radius:6px;padding:7px;color:#6ee7b7;line-height:1.7">A[j] = A[j-1] + A[j]<br>j = i-1,...,2<br><span style="color:#6c7086">// 从右到左安全！</span></div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

---

<!-- 第5页：迭代法解方程 -->
<div class="deck-wrapper">
  <div class="slide-container">
    <div class="slide slide-equation active" id="slide-5">
      <div class="sec-header">
        <div class="sec-num">4.3</div>
        <div class="sec-title">迭代法解方程 — 三种数值方法</div>
        <div class="sec-tag">Equation Solving</div>
      </div>
      <div class="eq-grid">
        <div class="eq-method">
          <div class="eq-method-header h-red">
            <span style="font-size:16px">∿</span> 不动点迭代
          </div>
          <div class="eq-method-body">
            <div class="eq-idea">将方程 f(x)=0 等价变形为 x=φ(x)，构造迭代序列逐步收敛</div>
            <div class="eq-formula">
              x<sub style="font-size:9px">n</sub> = <span class="highlight-eq">φ(x<sub style="font-size:9px">n-1</sub>)</span>
            </div>
            <div class="eq-steps">
              <div class="eq-step"><div class="eq-step-dot dot-red"></div><div>确定初值 x₀</div></div>
              <div class="eq-step"><div class="eq-step-dot dot-red"></div><div>构造 x=φ(x)</div></div>
              <div class="eq-step"><div class="eq-step-dot dot-red"></div><div>迭代直到 |xₙ-xₙ₋₁| &lt; ε</div></div>
            </div>
          </div>
        </div>
        <div class="eq-method">
          <div class="eq-method-header h-blue">
            <span style="font-size:16px">∂</span> 牛顿迭代法
          </div>
          <div class="eq-method-body">
            <div class="eq-idea">用切线逼近曲线，每步以切线零点作为新近似根，收敛速度快</div>
            <div class="eq-formula">
              x₁ = x₀ - <span class="highlight-eq2">f(x₀)/f'(x₀)</span>
            </div>
            <div class="eq-steps">
              <div class="eq-step"><div class="eq-step-dot dot-blue"></div><div>ax³+bx²+cx+d=0</div></div>
              <div class="eq-step"><div class="eq-step-dot dot-blue"></div><div>f₀ = horner求值</div></div>
              <div class="eq-step"><div class="eq-step-dot dot-blue"></div><div>f₁ = 导数值，迭代更新</div></div>
            </div>
          </div>
        </div>
        <div class="eq-method">
          <div class="eq-method-header h-amber">
            <span style="font-size:16px">⟨⟩</span> 二分法
          </div>
          <div class="eq-method-body">
            <div class="eq-idea">在异号区间 [a,b] 内反复对折，每次缩小一半，定位方程根</div>
            <div class="eq-formula">
              c = <span class="highlight-eq3">(a+b)/2</span><br>
              f(a)·f(c)&lt;0 → [a,c]
            </div>
            <div class="eq-steps">
              <div class="eq-step"><div class="eq-step-dot dot-amber"></div><div>前提：f(a)·f(b)&lt;0</div></div>
              <div class="eq-step"><div class="eq-step-dot dot-amber"></div><div>每轮区间减半</div></div>
              <div class="eq-step"><div class="eq-step-dot dot-amber"></div><div>直到 |f(c)| &lt; 1e-4</div></div>
            </div>
          </div>
        </div>
      </div>
      <div style="margin-top:12px;background:#fff;border-radius:10px;border:1px solid #e5e7eb;padding:10px 14px">
        <div style="font-size:11px;color:#9ca3af;font-family:monospace;margin-bottom:5px">示例方程（牛顿法）</div>
        <div style="font-family:monospace;font-size:12px;color:#374151">x³ + 2x² + 3x + 4 = 0 &nbsp;→&nbsp; <span style="color:#e11d48">f'(x) = 3x² + 4x + 3</span></div>
      </div>
    </div>
  </div>
</div>

---

<!-- 第6页：代码实现 -->
<div class="deck-wrapper">
  <div class="slide-container">
    <div class="slide slide-code active" id="slide-6">
      <div class="sec-header">
        <div class="sec-num">&lt;/&gt;</div>
        <div class="sec-title">代码实现对比</div>
        <div class="sec-tag">Code Examples</div>
      </div>
      <div class="code-tabs">
        <div class="code-tab active-tab" onclick="switchTab('gcd')">gcd.c</div>
        <div class="code-tab" onclick="switchTab('newton')">newton.c</div>
        <div class="code-tab" onclick="switchTab('bisect')">bisect.c</div>
        <div class="code-tab" onclick="switchTab('pascal')">pascal.c</div>
      </div>
      <div class="code-panel active-panel" id="tab-gcd">
<pre><span class="line-num">1</span><span class="kw">int</span> <span class="fn">gcd</span>(<span class="kw">int</span> <span class="var">a</span>, <span class="kw">int</span> <span class="var">b</span>) {
<span class="line-num">2</span>    <span class="kw">int</span> <span class="var">c</span> = <span class="var">a</span> <span class="op">%</span> <span class="var">b</span>;
<span class="line-num">3</span>    <span class="kw">while</span> (<span class="var">c</span> != <span class="num">0</span>) {
<span class="line-num">4</span>        <span class="var">a</span> = <span class="var">b</span>;    <span class="cm">// 循环不变式：gcd(a,b) = gcd(b, a%b)</span>
<span class="line-num">5</span>        <span class="var">b</span> = <span class="var">c</span>;
<span class="line-num">6</span>        <span class="var">c</span> = <span class="var">a</span> <span class="op">%</span> <span class="var">b</span>;
<span class="line-num">7</span>    }
<span class="line-num">8</span>    <span class="kw">return</span> <span class="var">b</span>;    <span class="cm">// 最大公约数</span>
<span class="line-num">9</span>}</pre>
      </div>
      <div class="code-panel" id="tab-newton">
<pre><span class="line-num">1</span><span class="kw">float</span> <span class="fn">newton</span>(<span class="kw">float</span> <span class="var">a</span>,<span class="kw">float</span> <span class="var">b</span>,<span class="kw">float</span> <span class="var">c</span>,<span class="kw">float</span> <span class="var">d</span>) {
<span class="line-num">2</span>    <span class="kw">float</span> <span class="var">x1</span>=<span class="num">1</span>, <span class="var">x0</span>, <span class="var">f0</span>, <span class="var">f1</span>;
<span class="line-num">3</span>    <span class="kw">do</span> {
<span class="line-num">4</span>        <span class="var">x0</span> = <span class="var">x1</span>;
<span class="line-num">5</span>        <span class="cm">// Horner法高效求值</span>
<span class="line-num">6</span>        <span class="var">f0</span> = ((<span class="var">a</span>*<span class="var">x0</span>+<span class="var">b</span>)*<span class="var">x0</span>+<span class="var">c</span>)*<span class="var">x0</span>+<span class="var">d</span>;
<span class="line-num">7</span>        <span class="var">f1</span> = (<span class="num">3</span>*<span class="var">a</span>*<span class="var">x0</span>+<span class="num">2</span>*<span class="var">b</span>)*<span class="var">x0</span>+<span class="var">c</span>;  <span class="cm">// 导数</span>
<span class="line-num">8</span>        <span class="var">x1</span> = <span class="var">x0</span> - <span class="var">f0</span>/<span class="var">f1</span>;  <span class="cm">// 切线零点</span>
<span class="line-num">9</span>    } <span class="kw">while</span> (<span class="fn">fabs</span>(<span class="var">x1</span>-<span class="var">x0</span>) >= <span class="num">1e-4</span>);
<span class="line-num">10</span>    <span class="kw">return</span> <span class="var">x1</span>;
<span class="line-num">11</span>}</pre>
      </div>
      <div class="code-panel" id="tab-bisect">
<pre><span class="line-num">1</span><span class="kw">float</span> <span class="var">x1</span>=<span class="num">0</span>, <span class="var">x2</span>=<span class="num">2</span>, <span class="var">x</span>, <span class="var">f</span>, <span class="var">f1</span>, <span class="var">f2</span>;
<span class="line-num">2</span><span class="cm">// 方程：x³/2 + 2x² - 8 = 0</span>
</pre>
      </div>
    </div>
  </div>
</div>

---

<!-- 第7页：总结 -->
<div class="deck-wrapper">
  <div class="slide-container">
    <div class="slide slide-summary active" id="slide-7">
      <div class="sum-title">迭代算法核心总结</div>
      <div class="sum-sub">Algorithm Design & Analysis</div>
      <div class="sum-grid">
        <div class="sum-card">
          <div class="sum-card-icon">→</div>
          <div class="sum-card-title">递推法</div>
          <div class="sum-card-items">
            <div class="sum-item"><div class="sum-dot"></div><div>正推：初值 → 后续值</div></div>
            <div class="sum-item"><div class="sum-dot"></div><div>斐波那契/辗转相除法</div></div>
            <div class="sum-item"><div class="sum-dot"></div><div>循环不变式保障正确性</div></div>
          </div>
        </div>
        <div class="sum-card">
          <div class="sum-card-icon">←</div>
          <div class="sum-card-title">倒推法</div>
          <div class="sum-card-items">
            <div class="sum-item"><div class="sum-dot"></div><div>逆推：结果 → 初始条件</div></div>
            <div class="sum-item"><div class="sum-dot"></div><div>猴子吃桃/杨辉三角</div></div>
            <div class="sum-item"><div class="sum-dot"></div><div>避免数据覆盖问题</div></div>
          </div>
        </div>
        <div class="sum-card">
          <div class="sum-card-icon">≈</div>
          <div class="sum-card-title">迭代解方程</div>
          <div class="sum-card-items">
            <div class="sum-item"><div class="sum-dot"></div><div>不动点/牛顿/二分法</div></div>
            <div class="sum-item"><div class="sum-dot"></div><div>逐步逼近，控制精度</div></div>
            <div class="sum-item"><div class="sum-dot"></div><div>牛顿法收敛速度最快</div></div>
          </div>
        </div>
      </div>
      <div class="sum-footer">
        Algorithm Design & Analysis © 2025
      </div>
    </div>
  </div>
</div>

<!-- 全局脚本（Slidev 中通过 md 嵌入） -->
<script>
// 代码标签切换逻辑
function switchTab(tabName) {
  // 隐藏所有面板
  document.querySelectorAll('.code-panel').forEach(panel => {
    panel.classList.remove('active-panel');
  });
  // 移除所有标签激活态
  document.querySelectorAll('.code-tab').forEach(tab => {
    tab.classList.remove('active-tab');
  });
  // 激活目标面板和标签
  document.getElementById(`tab-${tabName}`).classList.add('active-panel');
  event.target.classList.add('active-tab');
}

// 杨辉三角动态效果（可选）
document.addEventListener('DOMContentLoaded', () => {
  const pascalCells = document.querySelectorAll('.pascal-cell');
  pascalCells.forEach((cell, index) => {
    setTimeout(() => {
      cell.classList.add('lit');
    }, index * 100);
  });
});
</script>