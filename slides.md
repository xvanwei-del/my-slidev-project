---
theme: default
title: 迭代算法 — 算法设计与分析
highlighter: shiki
aspectRatio: 16/9
canvasWidth: 900
---


<!-- SLIDE 1: 封面 -->
<div class="slide-cover" style="position:absolute;inset:0;transform:scale(0.90) translateY(0%);transform-origin:center center;display:flex;align-items:center;justify-content:center;text-align:center;">
  <style>
    @keyframes ring-outer { from { transform: translate(-50%,-50%) rotate(0deg); } to { transform: translate(-50%,-50%) rotate(360deg); } }
    @keyframes ring-inner { from { transform: translate(-50%,-50%) rotate(180deg); } to { transform: translate(-50%,-50%) rotate(-180deg); } }
    .orbit-ring { position: absolute; top: 50%; left: 50%; border-radius: 50%; animation: ring-outer 8s linear infinite; }
    .orbit-ring.ring2 { animation-name: ring-inner; animation-duration: 20s; }
    .dot1 { position: absolute; top: -8px; left: calc(50% - 8px); width: 16px; height: 16px; border-radius: 50%; background: #e0e7ff; box-shadow: 0 0 12px #818cf8, 0 0 24px #6366f1, 0 0 40px #4f46e5; }
    .dot2 { position: absolute; bottom: -7px; left: calc(50% - 7px); width: 14px; height: 14px; border-radius: 50%; background: #a7f3d0; box-shadow: 0 0 10px #34d399, 0 0 20px #10b981, 0 0 32px #059669; }
  </style>
  <div class="stars-bg"></div>
  <div class="orbit-ring" style="width:500px;height:500px;border:1px solid rgba(99,102,241,0.25);"><div class="dot1"></div></div>
  <div class="orbit-ring ring2" style="width:380px;height:380px;border:1px solid rgba(16,185,129,0.2);"><div class="dot2"></div></div>
  <div class="cover-content">
    <div class="cover-badge">Chapter 4</div>
    <div class="cover-title">基本的算法策略<br>迭代算法</div>
    <div class="cover-subtitle">Algorithm Design &amp; Analysis</div>
    <div class="cover-chapters">
      <div class="cover-chip active-chip">4.1 迭代算法</div>
      <div class="cover-chip">4.2 蛮力法</div>
      <div class="cover-chip">4.3 分而治之</div>
      <div class="cover-chip">4.4 贪婪算法</div>
      <div class="cover-chip">4.5 动态规划</div>
    </div>
  </div>
</div>

---

<!-- SLIDE 2: 迭代策略总览 -->
<div class="slide-overview" style="position:absolute;inset:0;transform:scale(0.78) translateY(-8%);transform-origin:center center;">
  <div class="bg-circuit">
    <svg viewBox="0 0 900 506" preserveAspectRatio="xMidYMid slice">
      <g stroke="#10b981" stroke-width="1" fill="none">
        <line x1="0" y1="80" x2="200" y2="80"/><line x1="200" y1="80" x2="200" y2="140"/>
        <line x1="200" y1="140" x2="350" y2="140"/><line x1="350" y1="140" x2="350" y2="200"/>
        <line x1="0" y1="200" x2="100" y2="200"/><line x1="100" y1="200" x2="100" y2="280"/>
        <line x1="100" y1="280" x2="400" y2="280"/><line x1="400" y1="280" x2="400" y2="350"/>
        <line x1="400" y1="350" x2="900" y2="350"/>
        <line x1="500" y1="0" x2="500" y2="120"/><line x1="500" y1="120" x2="650" y2="120"/>
        <line x1="650" y1="120" x2="650" y2="220"/><line x1="650" y1="220" x2="900" y2="220"/>
        <line x1="700" y1="0" x2="700" y2="60"/><line x1="700" y1="60" x2="850" y2="60"/>
        <line x1="850" y1="60" x2="850" y2="150"/>
        <line x1="0" y1="400" x2="300" y2="400"/><line x1="300" y1="400" x2="300" y2="450"/>
        <line x1="300" y1="450" x2="600" y2="450"/>
        <circle cx="200" cy="80" r="4" fill="#10b981"/>
        <circle cx="350" cy="140" r="4" fill="#10b981"/>
        <circle cx="100" cy="280" r="4" fill="#10b981"/>
        <circle cx="400" cy="350" r="4" fill="#10b981"/>
        <circle cx="650" cy="120" r="4" fill="#10b981"/>
        <circle cx="700" cy="60" r="4" fill="#10b981"/>
        <circle cx="300" cy="400" r="4" fill="#10b981"/>
      </g>
    </svg>
  </div>
  <div v-click class="overview-left">
    <div class="overview-left-badge">⟳ Iterative Strategy</div>
    <div class="overview-left-title">迭代算法<br>三大策略</div>
    <div class="overview-left-divider"></div>
    <div class="overview-left-sub">
      利用已知条件，通过<strong style="color:#fff">循环迭代</strong>逐步逼近目标值或终态，是工程与科学计算的核心范式。
    </div>
  </div>
  <div class="overview-right">
    <div v-click class="ov-card">
      <div class="ov-icon icon-green">→</div>
      <div>
        <div class="ov-card-title">递推法（正推）</div>
        <div class="ov-card-desc">由已知初始值，依据递推关系逐步向前推导。适用于斐波那契、GCD 等。</div>
      </div>
      <div class="ov-card-tag">Forward</div>
    </div>
    <div v-click class="ov-card">
      <div class="ov-icon icon-purple">←</div>
      <div>
        <div class="ov-card-title">倒推法（逆推）</div>
        <div class="ov-card-desc">从末态已知条件出发，反向推算初始状态。猴子吃桃、杨辉三角等。</div>
      </div>
      <div class="ov-card-tag">Backward</div>
    </div>
    <div v-click class="ov-card">
      <div class="ov-icon icon-amber">≈</div>
      <div>
        <div class="ov-card-title">迭代逼近（解方程）</div>
        <div class="ov-card-desc">构造收敛序列，逐步逼近方程精确根。不动点、牛顿法、二分法。</div>
      </div>
      <div class="ov-card-tag">Converge</div>
    </div>
  </div>
</div>

---

<!-- SLIDE 3: 递推法 -->
<div class="slide-content" style="transform: scale(0.91); transform-origin: top center;">
<div class="slide-recursive" style="position:absolute;inset:0;transform:scale(0.78) translateY(-8%);transform-origin:center center;">
  <div class="bg-fib">
    <svg viewBox="0 0 900 506" preserveAspectRatio="xMidYMid slice">
      <g fill="none" stroke="#f59e0b" stroke-width="1">
        <circle cx="450" cy="253" r="240"/><circle cx="450" cy="253" r="180"/>
        <circle cx="450" cy="253" r="120"/><circle cx="450" cy="253" r="70"/>
        <circle cx="450" cy="253" r="35"/><circle cx="450" cy="253" r="14"/>
      </g>
      <g font-family="JetBrains Mono,monospace" font-size="13" fill="#f59e0b">
        <text x="30" y="40">1, 1, 2, 3, 5, 8, 13, 21, 34, 55...</text>
        <text x="30" y="460">f(n) = f(n-1) + f(n-2)</text>
      </g>
    </svg>
  </div>
  <div v-click class="sec-header">
    <div class="sec-num">4.1</div>
    <div class="sec-title">递推法 — 由已知推未知</div>
    <div class="sec-tag">Forward Iteration</div>
  </div>
  <div class="rec-grid" style="flex:1">
    <div class="rec-col">
      <div v-click class="problem-box">
        <div class="prob-title">经典问题：兔子繁殖</div>
        每对兔子第三个月起每月生一对，<strong>第12个月共有多少对？</strong><br>
        初始：第1、2月各1对；第n月 = 第(n-1)月 + 第(n-2)月
      </div>
      <div v-click style="background:rgba(255,255,255,0.03);border:1px solid rgba(255,255,255,0.07);border-radius:12px;padding:12px;display:flex;flex-direction:column;gap:8px">
        <div class="formula-label">斐波那契数列</div>
        <div style="display:flex;align-items:center;gap:4px;flex-wrap:wrap">
          <div class="fib-cell"><div class="fib-num fib-base">1</div><div class="fib-month">m=1</div></div>
          <div class="fib-arrow">→</div>
          <div class="fib-cell"><div class="fib-num fib-base">1</div><div class="fib-month">m=2</div></div>
          <div class="fib-arrow">→</div>
          <div class="fib-cell"><div class="fib-num fib-hi">2</div><div class="fib-month">m=3</div></div>
          <div class="fib-arrow">→</div>
          <div class="fib-cell"><div class="fib-num fib-hi">3</div><div class="fib-month">m=4</div></div>
          <div class="fib-arrow">→</div>
          <div class="fib-cell"><div class="fib-num fib-hi">5</div><div class="fib-month">m=5</div></div>
          <div class="fib-arrow">→</div>
          <div class="fib-cell"><div class="fib-num fib-hi">8</div><div class="fib-month">m=6</div></div>
          <div class="fib-arrow">→</div>
          <div class="fib-cell"><div class="fib-num fib-hi">13</div><div class="fib-month">…12</div></div>
        </div>
        <div style="font-family:'JetBrains Mono',monospace;font-size:12px;color:rgba(245,158,11,0.7);padding:6px 8px;background:rgba(245,158,11,0.06);border-radius:6px">
          f(n) = f(n−1) + f(n−2) &nbsp;|&nbsp; f(1)=f(2)=1
        </div>
      </div>
      <div v-click class="formula-box-dark" style="flex:1">
        <div class="formula-label">辗转相除法 GCD</div>
        <div class="formula-main">gcd(m, n) = gcd(n, m % n)</div>
        <div class="formula-sub">
          · 循环直至余数为 0<br>
          · 循环不变式：gcd(a,b) 保持不变<br>
          · 每次迭代后 b 严格减小 → 必然终止
        </div>
      </div>
    </div>
    <div class="rec-col">
      <div v-click class="code-box-dark" style="flex:1">
        <div class="code-box-label">fib.c — 迭代求斐波那契</div>
        <pre><span class="kw">int</span> <span class="var">a</span>=<span class="num">1</span>, <span class="var">b</span>=<span class="num">1</span>, <span class="var">c</span>;
<span class="kw">for</span> (<span class="var">i</span>=<span class="num">3</span>; <span class="var">i</span>&lt;=<span class="num">12</span>; <span class="var">i</span>++) {
    <span class="var">c</span> = <span class="var">a</span> <span class="op">+</span> <span class="var">b</span>;        <span class="cm">// 递推核心</span>
    <span class="fn">printf</span>(<span class="num">"%d %d\n"</span>, <span class="var">i</span>, <span class="var">c</span>);
    <span class="var">a</span> = <span class="var">b</span>;           <span class="cm">// 滑动窗口</span>
    <span class="var">b</span> = <span class="var">c</span>;
}</pre>
      </div>
      <div v-click class="code-box-dark" style="flex:1">
        <div class="code-box-label">gcd.c — 辗转相除法</div>
        <pre><span class="kw">int</span> <span class="fn">gcd</span>(<span class="kw">int</span> <span class="var">a</span>, <span class="kw">int</span> <span class="var">b</span>) {
    <span class="kw">int</span> <span class="var">c</span> = <span class="var">a</span> <span class="op">%</span> <span class="var">b</span>;
    <span class="kw">while</span> (<span class="var">c</span> != <span class="num">0</span>) {
        <span class="var">a</span> = <span class="var">b</span>;  <span class="cm">// 循环不变式：gcd(a,b)不变</span>
        <span class="var">b</span> = <span class="var">c</span>;
        <span class="var">c</span> = <span class="var">a</span> <span class="op">%</span> <span class="var">b</span>;
    }
    <span class="kw">return</span> <span class="var">b</span>; <span class="cm">// 最大公约数</span>
}</pre>
      </div>
    </div>
  </div>
</div>
  
</div>


---

<!-- SLIDE 4: 倒推法 -->
<div class="slide-content" style="transform: scale(0.88); transform-origin: top center;">
<div class="slide-backward" style="position:absolute;inset:0;transform:scale(0.78) translateY(-8%);transform-origin:center center;">
  <div class="bg-binary">
    <div class="binary-col" style="left:5%">10110100101101001011010010</div>
    <div class="binary-col" style="left:12%">01001011010010110100101101</div>
    <div class="binary-col" style="left:20%">11010010110100101101001011</div>
    <div class="binary-col" style="left:28%">00101101001011010010110100</div>
    <div class="binary-col" style="left:72%">10110100101101001011010010</div>
    <div class="binary-col" style="left:80%">01001011010010110100101101</div>
    <div class="binary-col" style="left:88%">11010010110100101101001011</div>
    <div class="binary-col" style="left:95%">00101101001011010010110100</div>
  </div>
  <div v-click class="sec-header">
    <div class="sec-num">4.2</div>
    <div class="sec-title">倒推法 — 从结果反推起始</div>
    <div class="sec-tag">Backward Iteration</div>
  </div>
  <div class="bw-grid" style="flex:1">
    <div class="bw-col">
      <div v-click class="bw-card bw-card-a" style="flex:0 0 auto">
        <div class="bw-label">正推 vs 倒推</div>
        <div class="compare-row">
          <div class="compare-icon ci-green">→</div>
          <div class="compare-text"><strong>正推：</strong>已知初始值，逐步向后推导结果</div>
        </div>
        <div class="compare-row" style="margin-bottom:0">
          <div class="compare-icon ci-purple">←</div>
          <div class="compare-text"><strong>倒推：</strong>已知末态，反向推算起始状态</div>
        </div>
      </div>
      <div v-click class="bw-card bw-card-a" style="flex:1">
        <div class="bw-label">猴子吃桃问题</div>
        <div class="monkey-steps">
          <div class="monkey-step">
            <div class="monkey-day">10</div>
            <div class="monkey-text">第10天剩 <strong>1个</strong>桃（已知末态）</div>
          </div>
          <div class="monkey-step">
            <div class="monkey-day">n-1</div>
            <div class="monkey-text">第n-1天 = <strong>(第n天 + 1) × 2</strong></div>
          </div>
          <div class="monkey-step">
            <div class="monkey-day">←</div>
            <div class="monkey-text">逐天倒推直至第1天</div>
          </div>
          <div class="monkey-code">day[i-1] = (day[i] + 1) * 2</div>
        </div>
      </div>
      <div v-click class="bw-card bw-card-c" style="flex:1">
        <div class="bw-label">穿越沙漠建油库</div>
        <div class="monkey-steps">
          <div class="monkey-step">
            <div class="monkey-day" style="background:rgba(16,185,129,0.2);border-color:rgba(16,185,129,0.35);color:#34d399">k</div>
            <div class="monkey-text">第k段出发次数，行驶 <strong>500/(2k-1)</strong> 公里</div>
          </div>
          <div class="monkey-step">
            <div class="monkey-day" style="background:rgba(16,185,129,0.2);border-color:rgba(16,185,129,0.35);color:#34d399">S</div>
            <div class="monkey-text"><strong>S₁ = 500k，S₂ = S₁ − (2k-1)×x</strong></div>
          </div>
        </div>
      </div>
    </div>
    <div class="bw-col">
      <div v-click class="bw-card bw-card-b" style="flex:0 0 auto">
        <div class="bw-label">杨辉三角 — 为何需要倒推？</div>
        <div class="pascal-vis">
          <div class="pascal-row"><div class="pascal-cell bright">1</div></div>
          <div class="pascal-row"><div class="pascal-cell lit">1</div><div class="pascal-cell lit">1</div></div>
          <div class="pascal-row"><div class="pascal-cell lit">1</div><div class="pascal-cell bright">2</div><div class="pascal-cell lit">1</div></div>
          <div class="pascal-row"><div class="pascal-cell lit">1</div><div class="pascal-cell bright">3</div><div class="pascal-cell bright">3</div><div class="pascal-cell lit">1</div></div>
          <div class="pascal-row"><div class="pascal-cell lit">1</div><div class="pascal-cell lit">4</div><div class="pascal-cell bright">6</div><div class="pascal-cell lit">4</div><div class="pascal-cell lit">1</div></div>
        </div>
        <div class="pascal-formula">a[j] = a[j-1] + a[j]</div>
      </div>
      <div v-click class="bw-card bw-card-a" style="flex:1">
        <div class="bw-label">倒推避免数据覆盖</div>
        <div class="compare-code-grid">
          <div>
            <div class="ccode-label" style="color:#ef4444;margin-bottom:5px">✗ 正推（覆盖错误）</div>
            <div class="ccode-block ccode-bad">
              A[j] = A[j-1] + A[j]<br>
              j = 2, 3, ..., i-1<br>
              <span class="ccode-cm">// 旧数据被覆盖！</span>
            </div>
          </div>
          <div>
            <div class="ccode-label" style="color:#34d399;margin-bottom:5px">✓ 倒推（正确）</div>
            <div class="ccode-block ccode-good">
              A[j] = A[j-1] + A[j]<br>
              j = i-1, ..., 2<br>
              <span class="ccode-cm">// 从右到左安全！</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

  
</div>

---

<!-- SLIDE 5: 迭代法解方程 -->
<div class="slide-equation" style="position:absolute;inset:0;transform:scale(0.95) translateY(4%);transform-origin:center center;">
  <div class="bg-converge">
    <svg viewBox="0 0 900 506" preserveAspectRatio="xMidYMid slice">
      <g fill="none" stroke="#e11d48" stroke-width="1">
        <circle cx="800" cy="253" r="300"/>
        <circle cx="800" cy="253" r="220"/>
        <circle cx="800" cy="253" r="150"/>
        <circle cx="800" cy="253" r="90"/>
        <circle cx="800" cy="253" r="45"/>
        <circle cx="800" cy="253" r="18"/>
      </g>
      <g stroke="#3b82f6" stroke-width="0.8" stroke-dasharray="4,4" fill="none">
        <line x1="100" y1="50" x2="100" y2="456"/>
        <line x1="50" y1="253" x2="600" y2="253"/>
        <path d="M100,453 Q200,50 300,350 Q400,180 500,280 Q550,245 580,255 Q590,252 600,253" stroke-width="1.5" stroke="#3b82f6" stroke-dasharray="none"/>
      </g>
      <g font-family="JetBrains Mono,monospace" font-size="11" fill="#e11d48" opacity="0.5">
        <text x="30" y="30">f(x) = 0</text>
        <text x="30" y="460">xₙ → x*</text>
      </g>
    </svg>
  </div>
  <div v-click class="sec-header">
    <div class="sec-num">4.3</div>
    <div class="sec-title">迭代法解方程 — 三种数值方法</div>
    <div class="sec-tag">Equation Solving</div>
  </div>
  <div class="eq-grid" style="flex:1">
    <div v-click class="eq-method">
      <div class="eq-method-header h-red">
        <span style="font-size:18px">∿</span> 不动点迭代
      </div>
      <div class="eq-method-body">
        <div class="eq-idea">将方程 f(x)=0 等价变形为 x=φ(x)，构造迭代序列，当 |φ'(x)|&lt;1 时收敛</div>
        <div class="eq-formula">
          xₙ = <span class="heq">φ(xₙ₋₁)</span><br>
          终止条件：|xₙ−xₙ₋₁| &lt; ε
        </div>
        <div class="eq-steps">
          <div class="eq-step"><div class="eq-dot eq-dot-r"></div><div>确定初始值 x₀</div></div>
          <div class="eq-step"><div class="eq-dot eq-dot-r"></div><div>构造等价形式 x=φ(x)</div></div>
          <div class="eq-step"><div class="eq-dot eq-dot-r"></div><div>迭代直到收敛精度满足 ε</div></div>
          <div class="eq-step"><div class="eq-dot eq-dot-r"></div><div>需验证 |φ'(x)|&lt;1 保证收敛</div></div>
        </div>
      </div>
    </div>
    <div v-click class="eq-method">
      <div class="eq-method-header h-blue">
        <span style="font-size:18px">∂</span> 牛顿迭代法
      </div>
      <div class="eq-method-body">
        <div class="eq-idea">用切线逼近曲线，以切线零点作为新近似根，二次收敛速度极快</div>
        <div class="eq-formula">
          x₁ = x₀ − <span class="heq2">f(x₀) / f'(x₀)</span><br>
          Horner法高效求值
        </div>
        <div class="eq-steps">
          <div class="eq-step"><div class="eq-dot eq-dot-b"></div><div>ax³+bx²+cx+d=0</div></div>
          <div class="eq-step"><div class="eq-dot eq-dot-b"></div><div>f₀ = Horner求函数值</div></div>
          <div class="eq-step"><div class="eq-dot eq-dot-b"></div><div>f₁ = 导数值 3ax²+2bx+c</div></div>
          <div class="eq-step"><div class="eq-dot eq-dot-b"></div><div>迭代更新至 |x₁−x₀|&lt;1e-4</div></div>
        </div>
      </div>
    </div>
    <div v-click class="eq-method">
      <div class="eq-method-header h-amber">
        <span style="font-size:18px">⟨⟩</span> 二分法
      </div>
      <div class="eq-method-body">
        <div class="eq-idea">在异号区间 [a,b] 内反复对折，每次将搜索范围缩小一半，稳定定位方程根</div>
        <div class="eq-formula">
          c = <span class="heq3">(a+b) / 2</span><br>
          若 f(a)·f(c)&lt;0 → 根在 [a,c]
        </div>
        <div class="eq-steps">
          <div class="eq-step"><div class="eq-dot eq-dot-a"></div><div>前提：f(a)·f(b)&lt;0（异号）</div></div>
          <div class="eq-step"><div class="eq-dot eq-dot-a"></div><div>每轮区间长度减半</div></div>
          <div class="eq-step"><div class="eq-dot eq-dot-a"></div><div>直到 |f(c)| &lt; 1e-4 停止</div></div>
          <div class="eq-step"><div class="eq-dot eq-dot-a"></div><div>线性收敛，稳定但较慢</div></div>
        </div>
      </div>
    </div>
  </div>
  <div v-click class="eq-bottom-bar">
    <div class="eq-bottom-label">示例（牛顿法）</div>
    <div class="eq-bottom-formula">x³ + 2x² + 3x + 4 = 0 &nbsp;→&nbsp; <span class="heq">f'(x) = 3x² + 4x + 3</span></div>
  </div>
</div>

---

<!-- SLIDE 6: 代码实现 A — GCD + 牛顿迭代 -->
<div class="slide-code" style="position:absolute;inset:0;transform:scale(0.95) translateY(4%);transform-origin:center center;">
  <div class="bg-codegrid" style="white-space:pre;line-height:1.5;overflow:hidden;position:absolute;inset:0;padding:8px;font-family:'JetBrains Mono',monospace;font-size:10px;color:rgba(245,158,11,0.12)">for(i=0;i&lt;n;i++){   while(c!=0){    do{x0=x1;      if(f1*f2&gt;0){x1=x;f1=f;}
  a=b; b=c;           x1=x0-f0/f1;    } while(fabs(x1-x0)&gt;=1e-4);
  c=a%b; }            return b; }    else{x2=x;f2=f;} } while(fabs(f)&gt;=1e-4);
int a=1,b=1,c;        f0=((a*x0+b)*x0+c)*x0+d;    x=(x1+x2)/2; f=F(x);
for(i=3;i&lt;=12;i++){  f1=(3*a*x0+2*b)*x0+c;      A[1]=A[i]=1; for(j=i-1;j&gt;=2;j--)</div>
  <div v-click class="sec-header">
    <div class="sec-num">&lt;/&gt;</div>
    <div class="sec-title">代码实现 — GCD 与牛顿迭代</div>
    <div class="sec-tag">Code · 1/2</div>
  </div>
  <div class="code-dual-grid" style="flex:1">
    <div v-click class="code-file">
      <div class="code-file-header">
        <div class="code-file-dots">
          <div class="cfd cfd-r"></div><div class="cfd cfd-y"></div><div class="cfd cfd-g"></div>
        </div>
        <div class="code-file-name">gcd.c</div>
      </div>
      <div class="code-file-body">
        <pre><span class="lnum">1</span><span class="kw">int</span> <span class="fn">gcd</span>(<span class="kw">int</span> <span class="var">a</span>, <span class="kw">int</span> <span class="var">b</span>) {
<span class="lnum">2</span>    <span class="kw">int</span> <span class="var">c</span> = <span class="var">a</span> <span class="op">%</span> <span class="var">b</span>;
<span class="lnum">3</span>    <span class="kw">while</span> (<span class="var">c</span> != <span class="num">0</span>) {
<span class="lnum">4</span>        <span class="var">a</span> = <span class="var">b</span>;   <span class="cm">// 循环不变式：gcd(a,b)不变</span>
<span class="lnum">5</span>        <span class="var">b</span> = <span class="var">c</span>;
<span class="lnum">6</span>        <span class="var">c</span> = <span class="var">a</span> <span class="op">%</span> <span class="var">b</span>;
<span class="lnum">7</span>    }
<span class="lnum">8</span>    <span class="kw">return</span> <span class="var">b</span>; <span class="cm">// 最大公约数</span>
<span class="lnum">9</span>}</pre>
      </div>
    </div>
    <div v-click class="code-file">
      <div class="code-file-header">
        <div class="code-file-dots">
          <div class="cfd cfd-r"></div><div class="cfd cfd-y"></div><div class="cfd cfd-g"></div>
        </div>
        <div class="code-file-name">newton.c</div>
      </div>
      <div class="code-file-body">
        <pre><span class="lnum"> 1</span><span class="kw">float</span> <span class="fn">newton</span>(<span class="kw">float</span> <span class="var">a</span>, <span class="kw">float</span> <span class="var">b</span>,
<span class="lnum"> 2</span>             <span class="kw">float</span> <span class="var">c</span>, <span class="kw">float</span> <span class="var">d</span>) {
<span class="lnum"> 3</span>    <span class="kw">float</span> <span class="var">x1</span>=<span class="num">1</span>, <span class="var">x0</span>, <span class="var">f0</span>, <span class="var">f1</span>;
<span class="lnum"> 4</span>    <span class="kw">do</span> {
<span class="lnum"> 5</span>        <span class="var">x0</span> = <span class="var">x1</span>;
<span class="lnum"> 6</span>        <span class="cm">// Horner法高效求值</span>
<span class="lnum"> 7</span>        <span class="var">f0</span> = ((<span class="var">a</span>*<span class="var">x0</span>+<span class="var">b</span>)*<span class="var">x0</span>+<span class="var">c</span>)*<span class="var">x0</span>+<span class="var">d</span>;
<span class="lnum"> 8</span>        <span class="var">f1</span> = (<span class="num">3</span>*<span class="var">a</span>*<span class="var">x0</span>+<span class="num">2</span>*<span class="var">b</span>)*<span class="var">x0</span>+<span class="var">c</span>;
<span class="lnum"> 9</span>        <span class="var">x1</span> = <span class="var">x0</span> - <span class="var">f0</span>/<span class="var">f1</span>; <span class="cm">// 切线零点</span>
<span class="lnum">10</span>    } <span class="kw">while</span> (<span class="fn">fabs</span>(<span class="var">x1</span>-<span class="var">x0</span>) >= <span class="num">1e-4</span>);
<span class="lnum">11</span>    <span class="kw">return</span> <span class="var">x1</span>;
<span class="lnum">12</span>}</pre>
      </div>
    </div>
  </div>
</div>

---

<!-- SLIDE 7: 代码实现 B — 二分法 + 杨辉三角 -->
<div class="slide-code" style="position:absolute;inset:0;transform:scale(0.95) translateY(4%);transform-origin:center center;">
  <div class="bg-codegrid" style="white-space:pre;line-height:1.5;overflow:hidden;position:absolute;inset:0;padding:8px;font-family:'JetBrains Mono',monospace;font-size:10px;color:rgba(245,158,11,0.12)">for(i=0;i&lt;n;i++){   while(c!=0){    do{x0=x1;      if(f1*f2&gt;0){x1=x;f1=f;}
  a=b; b=c;           x1=x0-f0/f1;    } while(fabs(x1-x0)&gt;=1e-4);
  c=a%b; }            return b; }    else{x2=x;f2=f;} } while(fabs(f)&gt;=1e-4);
int a=1,b=1,c;        f0=((a*x0+b)*x0+c)*x0+d;    x=(x1+x2)/2; f=F(x);
for(i=3;i&lt;=12;i++){  f1=(3*a*x0+2*b)*x0+c;      A[1]=A[i]=1; for(j=i-1;j&gt;=2;j--)</div>
  <div v-click class="sec-header">
    <div class="sec-num">&lt;/&gt;</div>
    <div class="sec-title">代码实现 — 二分法与杨辉三角</div>
    <div class="sec-tag">Code · 2/2</div>
  </div>
  <div class="code-dual-grid" style="flex:1">
    <div v-click class="code-file">
      <div class="code-file-header">
        <div class="code-file-dots">
          <div class="cfd cfd-r"></div><div class="cfd cfd-y"></div><div class="cfd cfd-g"></div>
        </div>
        <div class="code-file-name">bisect.c</div>
      </div>
      <div class="code-file-body">
        <pre><span class="lnum"> 1</span><span class="kw">float</span> <span class="var">x1</span>=<span class="num">0</span>, <span class="var">x2</span>=<span class="num">2</span>, <span class="var">x</span>, <span class="var">f</span>, <span class="var">f1</span>, <span class="var">f2</span>;
<span class="lnum"> 2</span><span class="cm">// 方程：x³/2 + 2x² - 8 = 0</span>
<span class="lnum"> 3</span><span class="var">f1</span> = <span class="fn">F</span>(<span class="var">x1</span>); <span class="var">f2</span> = <span class="fn">F</span>(<span class="var">x2</span>);
<span class="lnum"> 4</span><span class="kw">if</span> (<span class="var">f1</span>*<span class="var">f2</span> &gt; <span class="num">0</span>) {
<span class="lnum"> 5</span>    <span class="fn">print</span>(<span class="str">"No root"</span>); <span class="kw">return</span>;
<span class="lnum"> 6</span>}
<span class="lnum"> 7</span><span class="kw">do</span> {
<span class="lnum"> 8</span>    <span class="var">x</span> = (<span class="var">x1</span>+<span class="var">x2</span>)/<span class="num">2</span>; <span class="cm">// 取区间中点</span>
<span class="lnum"> 9</span>    <span class="var">f</span> = <span class="fn">F</span>(<span class="var">x</span>);
<span class="lnum">10</span>    <span class="kw">if</span> (<span class="var">f1</span>*<span class="var">f</span> &gt; <span class="num">0</span>) { <span class="var">x1</span>=<span class="var">x</span>; <span class="var">f1</span>=<span class="var">f</span>; }
<span class="lnum">11</span>    <span class="kw">else</span>           { <span class="var">x2</span>=<span class="var">x</span>; <span class="var">f2</span>=<span class="var">f</span>; }
<span class="lnum">12</span>} <span class="kw">while</span> (<span class="fn">fabs</span>(<span class="var">f</span>) >= <span class="num">1e-4</span>);</pre>
      </div>
    </div>
    <div v-click class="code-file">
      <div class="code-file-header">
        <div class="code-file-dots">
          <div class="cfd cfd-r"></div><div class="cfd cfd-y"></div><div class="cfd cfd-g"></div>
        </div>
        <div class="code-file-name">pascal.c</div>
      </div>
      <div class="code-file-body">
        <pre><span class="lnum"> 1</span><span class="cm">// 杨辉三角——倒推法（一维数组）</span>
<span class="lnum"> 2</span><span class="kw">for</span> (<span class="var">i</span>=<span class="num">1</span>; <span class="var">i</span>&lt;=<span class="var">n</span>; <span class="var">i</span>++) {
<span class="lnum"> 3</span>    <span class="var">A</span>[<span class="num">1</span>] = <span class="var">A</span>[<span class="var">i</span>] = <span class="num">1</span>;
<span class="lnum"> 4</span>    <span class="cm">// 关键：j从大到小！避免覆盖</span>
<span class="lnum"> 5</span>    <span class="kw">for</span> (<span class="var">j</span>=<span class="var">i</span>-<span class="num">1</span>; <span class="var">j</span>&gt;=<span class="num">2</span>; <span class="var">j</span>--) {
<span class="lnum"> 6</span>        <span class="var">A</span>[<span class="var">j</span>] = <span class="var">A</span>[<span class="var">j</span>-<span class="num">1</span>] + <span class="var">A</span>[<span class="var">j</span>];
<span class="lnum"> 7</span>    }
<span class="lnum"> 8</span>    <span class="kw">for</span> (<span class="var">j</span>=<span class="num">1</span>; <span class="var">j</span>&lt;=<span class="var">i</span>; <span class="var">j</span>++)
<span class="lnum"> 9</span>        <span class="fn">printf</span>(<span class="str">"%4d"</span>, <span class="var">A</span>[<span class="var">j</span>]);
<span class="lnum">10</span>    <span class="fn">printf</span>(<span class="str">"\n"</span>);
<span class="lnum">11</span>}</pre>
      </div>
    </div>
  </div>
</div>

---

<!-- SLIDE 8: 总结 -->
<div class="slide-summary" style="position:absolute;inset:0;transform:scale(0.95) translateY(4%);transform-origin:center center;">
  <div class="bg-graph">
    <svg viewBox="0 0 900 506" preserveAspectRatio="xMidYMid slice">
      <g stroke="#6366f1" stroke-width="1" fill="none">
        <line x1="100" y1="100" x2="250" y2="180"/>
        <line x1="250" y1="180" x2="400" y2="120"/>
        <line x1="400" y1="120" x2="550" y2="200"/>
        <line x1="550" y1="200" x2="700" y2="150"/>
        <line x1="700" y1="150" x2="820" y2="220"/>
        <line x1="100" y1="380" x2="220" y2="300"/>
        <line x1="220" y1="300" x2="380" y2="360"/>
        <line x1="380" y1="360" x2="520" y2="290"/>
        <line x1="520" y1="290" x2="680" y2="350"/>
        <line x1="680" y1="350" x2="830" y2="300"/>
        <line x1="250" y1="180" x2="220" y2="300"/>
        <line x1="400" y1="120" x2="380" y2="360"/>
        <line x1="550" y1="200" x2="520" y2="290"/>
        <line x1="700" y1="150" x2="680" y2="350"/>
      </g>
      <g fill="#6366f1">
        <circle cx="100" cy="100" r="5"/><circle cx="250" cy="180" r="5"/>
        <circle cx="400" cy="120" r="5"/><circle cx="550" cy="200" r="5"/>
        <circle cx="700" cy="150" r="5"/><circle cx="820" cy="220" r="5"/>
        <circle cx="100" cy="380" r="5"/><circle cx="220" cy="300" r="5"/>
        <circle cx="380" cy="360" r="5"/><circle cx="520" cy="290" r="5"/>
        <circle cx="680" cy="350" r="5"/><circle cx="830" cy="300" r="5"/>
      </g>
    </svg>
  </div>
  <div v-click class="sum-header">
    <div class="sum-title">迭代算法 — 知识总结</div>
    <div class="sum-sub">Chapter 4.1 · Algorithm Design &amp; Analysis</div>
    <div class="sum-divider"></div>
  </div>
  <div class="sum-grid">
    <div v-click class="sum-card">
      <div class="sum-card-top">
        <div class="sum-card-icon si-green">→</div>
        <div class="sum-card-title">递推法</div>
      </div>
      <div class="sum-card-items">
        <div class="sum-item"><div class="sum-dot sd-g"></div><span><strong>斐波那契数列</strong></span></div>
        <div class="sum-item"><div class="sum-dot sd-g"></div><span><strong>GCD</strong> 辗转相除</span></div>
        <div class="sum-item"><div class="sum-dot sd-g"></div><span>循环不变式维护</span></div>
        <div class="sum-item"><div class="sum-dot sd-g"></div><span>正向推进，初值已知</span></div>
      </div>
    </div>
    <div v-click class="sum-card">
      <div class="sum-card-top">
        <div class="sum-card-icon si-purple">←</div>
        <div class="sum-card-title">倒推法</div>
      </div>
      <div class="sum-card-items">
        <div class="sum-item"><div class="sum-dot sd-p"></div><span><strong>猴子吃桃</strong>问题</span></div>
        <div class="sum-item"><div class="sum-dot sd-p"></div><span><strong>杨辉三角</strong>（避免覆盖）</span></div>
        <div class="sum-item"><div class="sum-dot sd-p"></div><span>穿越沙漠建油库</span></div>
        <div class="sum-item"><div class="sum-dot sd-p"></div><span>从末态反向推导</span></div>
      </div>
    </div>
    <div v-click class="sum-card">
      <div class="sum-card-top">
        <div class="sum-card-icon si-amber">≈</div>
        <div class="sum-card-title">解方程三法</div>
      </div>
      <div class="sum-card-items">
        <div class="sum-item"><div class="sum-dot sd-a"></div><span><strong>不动点迭代</strong></span></div>
        <div class="sum-item"><div class="sum-dot sd-a"></div><span><strong>牛顿切线法</strong>（二次收敛）</span></div>
        <div class="sum-item"><div class="sum-dot sd-a"></div><span><strong>二分区间法</strong>（线性收敛）</span></div>
        <div class="sum-item"><div class="sum-dot sd-a"></div><span>逐步逼近精确解</span></div>
      </div>
    </div>
  </div>
</div>
