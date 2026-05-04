<template>
  <div style="display:none" aria-hidden="true"></div>
</template>
<style>
/* ===== 全局暗色背景 & 定位修复 ===== */
.slidev-page {
  position: relative !important;
  overflow: hidden !important;
  background: #0b1121 !important;
  color: #e2e8f0;
}
.slidev-layout,
.slidev-layout.default {
  position: relative !important;
  background: transparent !important;
  width: 100% !important;
  height: 100% !important;
  padding: 0 !important;
  margin: 0 !important;
  box-sizing: border-box !important;
}
/* 缩小幻灯片内容，适配 UnoCSS py-10 的 40px 内边距 */
.slide-cover, .slide-overview, .slide-recursive, .slide-backward,
.slide-equation, .slide-code, .slide-summary {
  transform: scale(0.85) !important;
  transform-origin: center center !important;
}

/* ===== SLIDE 1: 封面 ===== */
.stars-bg {
  position: absolute; inset: 0;
  background: radial-gradient(ellipse at 30% 40%, rgba(99,102,241,0.12) 0%, transparent 60%),
              radial-gradient(ellipse at 70% 60%, rgba(16,185,129,0.08) 0%, transparent 60%);
}
@keyframes orbit-spin {
  from { transform: translate(-50%, -50%) rotate(0deg); }
  to   { transform: translate(-50%, -50%) rotate(360deg); }
}
@keyframes orbit-spin-rev {
  from { transform: translate(-50%, -50%) rotate(0deg); }
  to   { transform: translate(-50%, -50%) rotate(-360deg); }
}
.cover-orbit {
  position: absolute; top: 50%; left: 50%;
  width: 500px; height: 500px; border-radius: 50%;
  border: 1px solid rgba(99,102,241,0.3);
  animation: orbit-spin 12s linear infinite;
}
.cover-orbit::after {
  content: '';
  position: absolute;
  top: -6px; left: calc(50% - 6px);
  width: 12px; height: 12px;
  border-radius: 50%;
  background: #e0e7ff;
  box-shadow: 0 0 16px #818cf8, 0 0 32px #6366f1;
}
.cover-orbit-2 {
  width: 380px; height: 380px;
  border-color: rgba(16,185,129,0.25);
  animation: orbit-spin-rev 15s linear infinite;
}
.cover-orbit-2::after {
  content: '';
  position: absolute;
  top: -5px; left: calc(50% - 5px);
  width: 10px; height: 10px;
  border-radius: 50%;
  background: #d1fae5;
  box-shadow: 0 0 14px #34d399, 0 0 28px #10b981;
}
.cover-content { position: relative; z-index: 1; }
.cover-badge {
  display: inline-block; padding: 6px 20px; border-radius: 20px;
  border: 1px solid rgba(99,102,241,0.4); color: #a5b4fc;
  font-size: 14px; letter-spacing: 2px; margin-bottom: 16px;
}
.cover-title {
  font-size: 52px; font-weight: 800; line-height: 1.2;
  background: linear-gradient(135deg, #e2e8f0 0%, #a5b4fc 100%);
  -webkit-background-clip: text; -webkit-text-fill-color: transparent;
  margin-bottom: 8px;
}
.cover-subtitle {
  font-size: 18px; color: rgba(148,163,184,0.7); letter-spacing: 4px;
  margin-bottom: 28px;
}
.cover-chapters { display: flex; gap: 8px; flex-wrap: wrap; justify-content: center; }
.cover-chip {
  padding: 5px 14px; border-radius: 14px; font-size: 12px;
  border: 1px solid rgba(255,255,255,0.08); color: rgba(148,163,184,0.6);
}
.cover-chip.active-chip {
  border-color: rgba(99,102,241,0.5); color: #a5b4fc;
  background: rgba(99,102,241,0.1);
}

/* ===== SLIDE 2: 迭代策略总览 ===== */
.slide-overview { display: flex; align-items: center; }
.bg-circuit { position: absolute; inset: 0; opacity: 0.25; }
.overview-left {
  width: 38%; display: flex; flex-direction: column; justify-content: center;
  padding: 40px; position: relative; z-index: 1;
}
.overview-left-badge {
  display: inline-block; padding: 4px 14px; border-radius: 12px;
  border: 1px solid rgba(16,185,129,0.3); color: #34d399;
  font-size: 12px; margin-bottom: 12px; width: fit-content;
}
.overview-left-title {
  font-size: 34px; font-weight: 700; line-height: 1.2; color: #f1f5f9;
}
.overview-left-divider {
  width: 60px; height: 2px; background: linear-gradient(90deg, #10b981, transparent);
  margin: 16px 0;
}
.overview-left-sub {
  font-size: 14px; color: rgba(148,163,184,0.8); line-height: 1.6;
}
.overview-right {
  flex: 1; display: flex; flex-direction: column; justify-content: center;
  gap: 12px; padding: 40px 40px 40px 0; position: relative; z-index: 1;
}
.ov-card {
  display: flex; align-items: center; gap: 14px;
  background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.06);
  border-radius: 12px; padding: 16px 20px;
}
.ov-icon {
  width: 40px; height: 40px; border-radius: 10px; display: flex;
  align-items: center; justify-content: center; font-size: 18px; font-weight: 700;
  flex-shrink: 0;
}
.icon-green { background: rgba(16,185,129,0.15); color: #34d399; }
.icon-purple { background: rgba(168,85,247,0.15); color: #c084fc; }
.icon-amber { background: rgba(245,158,11,0.15); color: #fbbf24; }
.ov-card-title { font-size: 15px; font-weight: 600; color: #f1f5f9; }
.ov-card-desc { font-size: 12px; color: rgba(148,163,184,0.7); line-height: 1.5; margin-top: 2px; }
.ov-card-tag {
  margin-left: auto; font-size: 10px; padding: 3px 10px; border-radius: 10px;
  border: 1px solid rgba(255,255,255,0.06); color: rgba(148,163,184,0.4);
  flex-shrink: 0;
}

/* ===== 通用分区标题 ===== */
.sec-header { display: flex; align-items: baseline; gap: 12px; padding: 20px 36px 0; position: relative; z-index: 1; }
.sec-num {
  font-size: 28px; font-weight: 800; font-family: 'JetBrains Mono', monospace;
  background: linear-gradient(135deg, #6366f1, #a5b4fc);
  -webkit-background-clip: text; -webkit-text-fill-color: transparent;
}
.sec-title { font-size: 22px; font-weight: 700; color: #f1f5f9; }
.sec-tag {
  font-size: 11px; color: rgba(148,163,184,0.5); border: 1px solid rgba(255,255,255,0.06);
  padding: 2px 10px; border-radius: 10px;
}

/* ===== SLIDE 3: 递推法 ===== */
.bg-fib { position: absolute; inset: 0; opacity: 0.08; }
.slide-recursive { display: flex; flex-direction: column; }
.rec-grid {
  display: flex; gap: 20px; padding: 16px 36px 24px; position: relative; z-index: 1;
}
.rec-col { flex: 1; display: flex; flex-direction: column; gap: 12px; }
.problem-box {
  background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.07);
  border-radius: 12px; padding: 14px; font-size: 13px; color: rgba(203,213,225,0.8);
  line-height: 1.6;
}
.prob-title { font-size: 14px; font-weight: 600; color: #f1f5f9; margin-bottom: 4px; }
.fib-cell { text-align: center; }
.fib-num {
  width: 44px; height: 44px; border-radius: 50%; display: flex;
  align-items: center; justify-content: center;
  font-family: 'JetBrains Mono', monospace; font-size: 17px; font-weight: 700;
}
.fib-base { background: rgba(255,255,255,0.05); color: rgba(203,213,225,0.6); }
.fib-hi { background: rgba(245,158,11,0.15); color: #fbbf24; border: 1px solid rgba(245,158,11,0.2); }
.fib-month { font-size: 10px; color: rgba(148,163,184,0.4); margin-top: 4px; }
.fib-arrow { color: rgba(148,163,184,0.3); font-family: 'JetBrains Mono', monospace; }
.formula-label { font-size: 11px; color: rgba(16,185,129,0.6); text-transform: uppercase; letter-spacing: 1px; }
.formula-box-dark {
  background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.07);
  border-radius: 12px; padding: 14px;
}
.formula-main {
  font-family: 'JetBrains Mono', monospace; font-size: 16px; font-weight: 600;
  color: #34d399; margin: 6px 0;
}
.formula-sub {
  font-size: 12px; color: rgba(148,163,184,0.6); line-height: 1.6; margin-top: 4px;
}
.code-box-dark {
  background: rgba(0,0,0,0.3); border: 1px solid rgba(255,255,255,0.06);
  border-radius: 10px; padding: 12px 14px; overflow: hidden;
}
.code-box-dark pre {
  margin: 0; font-family: 'JetBrains Mono', monospace; font-size: 11.5px;
  line-height: 1.7; color: #cbd5e1;
}
.code-box-label {
  font-size: 10px; color: rgba(148,163,184,0.4); margin-bottom: 6px;
  text-transform: uppercase; letter-spacing: 1px;
}

/* Syntax highlighting */
.kw { color: #c084fc; }
.var { color: #fbbf24; }
.num { color: #fb923c; }
.op { color: #67e8f9; }
.cm { color: rgba(148,163,184,0.45); }
.str { color: #34d399; }
.fn { color: #60a5fa; }

/* ===== SLIDE 4: 倒推法 ===== */
.bg-binary { position: absolute; inset: 0; }
.slide-backward { display: flex; flex-direction: column; }
.binary-col {
  position: absolute; top: 0; bottom: 0; writing-mode: vertical-lr;
  font-family: 'JetBrains Mono', monospace; font-size: 10px;
  color: rgba(16,185,129,0.06); letter-spacing: 2px;
}
.bw-grid { display: flex; gap: 20px; padding: 12px 36px 24px; position: relative; z-index: 1; }
.bw-col { flex: 1; display: flex; flex-direction: column; gap: 12px; }
.bw-card {
  background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.07);
  border-radius: 12px; padding: 16px;
}
.bw-card-a { border-left: 2px solid rgba(168,85,247,0.3); }
.bw-card-b { border-left: 2px solid rgba(59,130,246,0.3); }
.bw-card-c { border-left: 2px solid rgba(16,185,129,0.3); }
.bw-label { font-size: 13px; font-weight: 600; color: #f1f5f9; margin-bottom: 8px; }
.compare-row { display: flex; align-items: center; gap: 10px; margin-bottom: 8px; }
.compare-icon {
  width: 32px; height: 32px; border-radius: 8px; display: flex;
  align-items: center; justify-content: center; font-size: 14px; font-weight: 700;
  flex-shrink: 0;
}
.ci-green { background: rgba(16,185,129,0.15); color: #34d399; }
.ci-purple { background: rgba(168,85,247,0.15); color: #c084fc; }
.compare-text { font-size: 13px; color: rgba(203,213,225,0.8); }
.monkey-steps { display: flex; flex-direction: column; gap: 8px; }
.monkey-step { display: flex; align-items: center; gap: 12px; }
.monkey-day {
  width: 34px; height: 34px; border-radius: 50%; display: flex;
  align-items: center; justify-content: center; font-size: 14px; font-weight: 700;
  background: rgba(168,85,247,0.15); border: 1px solid rgba(168,85,247,0.3);
  color: #c084fc; flex-shrink: 0;
}
.monkey-text { font-size: 13px; color: rgba(203,213,225,0.8); }
.monkey-code {
  font-family: 'JetBrains Mono', monospace; font-size: 12px; padding: 8px 12px;
  background: rgba(168,85,247,0.08); border-radius: 8px; color: #c084fc;
}
.pascal-vis { display: flex; flex-direction: column; align-items: center; gap: 4px; margin-bottom: 10px; }
.pascal-row { display: flex; gap: 8px; }
.pascal-cell {
  width: 32px; height: 32px; border-radius: 6px; display: flex;
  align-items: center; justify-content: center;
  font-family: 'JetBrains Mono', monospace; font-size: 13px;
}
.pascal-cell.bright { background: rgba(59,130,246,0.2); color: #60a5fa; }
.pascal-cell.lit { background: rgba(255,255,255,0.04); color: rgba(203,213,225,0.6); }
.pascal-formula {
  font-family: 'JetBrains Mono', monospace; font-size: 13px; color: #60a5fa;
  text-align: center;
}
.compare-code-grid { display: flex; gap: 12px; }
.ccode-label { font-size: 12px; font-weight: 600; }
.ccode-block {
  font-family: 'JetBrains Mono', monospace; font-size: 11px; line-height: 1.7;
  padding: 10px 12px; border-radius: 8px;
}
.ccode-bad { background: rgba(239,68,68,0.08); color: rgba(203,213,225,0.7); border: 1px solid rgba(239,68,68,0.15); }
.ccode-good { background: rgba(16,185,129,0.08); color: rgba(203,213,225,0.8); border: 1px solid rgba(16,185,129,0.15); }
.ccode-cm { color: rgba(148,163,184,0.4); }

/* ===== SLIDE 5: 迭代法解方程 ===== */
.bg-converge { position: absolute; inset: 0; opacity: 0.08; }
.eq-grid {
  display: flex; gap: 16px; padding: 12px 36px 16px; position: relative; z-index: 1;
  flex: 1;
}
.eq-method {
  flex: 1; background: rgba(255,255,255,0.02); border: 1px solid rgba(255,255,255,0.06);
  border-radius: 14px; overflow: hidden; display: flex; flex-direction: column;
}
.eq-method-header {
  padding: 12px 16px; font-weight: 700; font-size: 15px;
  display: flex; align-items: center; gap: 8px;
}
.eq-method-header.h-red { background: rgba(239,68,68,0.1); color: #f87171; border-bottom: 1px solid rgba(239,68,68,0.15); }
.eq-method-header.h-blue { background: rgba(59,130,246,0.1); color: #60a5fa; border-bottom: 1px solid rgba(59,130,246,0.15); }
.eq-method-header.h-amber { background: rgba(245,158,11,0.1); color: #fbbf24; border-bottom: 1px solid rgba(245,158,11,0.15); }
.eq-method-body { padding: 14px 16px; font-size: 12px; color: rgba(203,213,225,0.7); }
.eq-idea { line-height: 1.5; margin-bottom: 10px; }
.eq-formula {
  font-family: 'JetBrains Mono', monospace; font-size: 13px; padding: 10px 12px;
  background: rgba(0,0,0,0.25); border-radius: 8px; margin-bottom: 10px;
  line-height: 1.7; color: #cbd5e1;
}
.heq { color: #f87171; }
.heq2 { color: #60a5fa; }
.heq3 { color: #fbbf24; }
.eq-steps { display: flex; flex-direction: column; gap: 6px; }
.eq-step { display: flex; align-items: flex-start; gap: 10px; }
.eq-dot {
  width: 6px; height: 6px; border-radius: 50%; margin-top: 4px; flex-shrink: 0;
}
.eq-dot-r { background: #f87171; }
.eq-dot-b { background: #60a5fa; }
.eq-dot-a { background: #fbbf24; }
.eq-bottom-bar {
  display: flex; align-items: center; gap: 16px; padding: 10px 36px 16px;
  position: relative; z-index: 1;
}
.eq-bottom-label { font-size: 12px; color: rgba(148,163,184,0.6); }
.eq-bottom-formula {
  font-family: 'JetBrains Mono', monospace; font-size: 13px; color: #cbd5e1;
  padding: 8px 14px; background: rgba(59,130,246,0.06); border-radius: 8px;
  border: 1px solid rgba(59,130,246,0.12);
}

/* ===== SLIDE 6 & 7: 代码实现 ===== */
.bg-codegrid { pointer-events: none; user-select: none; }
.code-dual-grid {
  display: flex; gap: 20px; padding: 12px 36px 24px;
  position: relative; z-index: 1; flex: 1;
}
.code-file {
  flex: 1; background: rgba(0,0,0,0.35); border: 1px solid rgba(255,255,255,0.06);
  border-radius: 12px; overflow: hidden; display: flex; flex-direction: column;
}
.code-file-header {
  display: flex; align-items: center; gap: 10px; padding: 10px 14px;
  background: rgba(255,255,255,0.03); border-bottom: 1px solid rgba(255,255,255,0.04);
}
.code-file-dots { display: flex; gap: 5px; }
.cfd { width: 10px; height: 10px; border-radius: 50%; }
.cfd-r { background: #ef4444; }
.cfd-y { background: #f59e0b; }
.cfd-g { background: #10b981; }
.code-file-name {
  font-size: 11px; color: rgba(148,163,184,0.5);
  font-family: 'JetBrains Mono', monospace;
}
.code-file-body { padding: 12px 14px; flex: 1; }
.code-file-body pre {
  margin: 0; font-family: 'JetBrains Mono', monospace; font-size: 12px;
  line-height: 1.8; color: #cbd5e1;
}
.lnum { color: rgba(148,163,184,0.22); margin-right: 10px; user-select: none; }

/* ===== SLIDE 8: 总结 ===== */
.bg-graph { position: absolute; inset: 0; opacity: 0.15; }
.sum-header { text-align: center; padding: 24px 36px 0; position: relative; z-index: 1; }
.sum-title { font-size: 32px; font-weight: 700; color: #f1f5f9; letter-spacing: 1px; }
.sum-sub { font-size: 13px; color: rgba(148,163,184,0.5); margin-top: 4px; }
.sum-divider {
  width: 80px; height: 2px;
  background: linear-gradient(90deg, transparent, #6366f1, transparent);
  margin: 14px auto 0;
}
.sum-grid {
  display: flex; gap: 20px; padding: 20px 40px 16px;
  position: relative; z-index: 1; flex: 1;
}
.sum-card {
  flex: 1; background: rgba(255,255,255,0.03); border: 1px solid rgba(255,255,255,0.06);
  border-radius: 14px; padding: 20px;
}
.sum-card-top { display: flex; align-items: center; gap: 10px; margin-bottom: 14px; }
.sum-card-icon {
  width: 38px; height: 38px; border-radius: 10px; display: flex;
  align-items: center; justify-content: center; font-size: 18px; font-weight: 700;
}
.si-green { background: rgba(16,185,129,0.15); color: #34d399; }
.si-purple { background: rgba(168,85,247,0.15); color: #c084fc; }
.si-amber { background: rgba(245,158,11,0.15); color: #fbbf24; }
.sum-card-title { font-size: 17px; font-weight: 600; color: #f1f5f9; }
.sum-card-items { display: flex; flex-direction: column; gap: 8px; }
.sum-item { display: flex; align-items: center; gap: 10px; font-size: 13px; color: rgba(203,213,225,0.7); }
.sum-dot { width: 6px; height: 6px; border-radius: 50%; flex-shrink: 0; }
.sd-g { background: #34d399; }
.sd-p { background: #c084fc; }
.sd-a { background: #fbbf24; }
.sum-footer {
  text-align: center; padding: 10px 36px 20px; font-size: 12px;
  color: rgba(148,163,184,0.4); position: relative; z-index: 1;
}

/* ===== 通用 ===== */
strong { color: #fff; }
</style>
