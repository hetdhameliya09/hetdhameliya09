import os

html_content = r'''<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Het N Dhameliya | Full-Stack Developer & AI/ML Engineer</title>
  <meta name="description" content="Portfolio & GitHub Profile of Het N Dhameliya - Full-Stack Developer (Django, React, Vite) and AI/ML Application Builder." />
  
  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;500;600&family=Outfit:wght@300;400;500;600;700;800;900&family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet" />
  
  <!-- Font Awesome Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" />

  <style>
    :root {
      --bg-dark: #070913;
      --bg-card: rgba(15, 18, 37, 0.65);
      --bg-card-hover: rgba(26, 31, 62, 0.85);
      --border-color: rgba(139, 92, 246, 0.18);
      --border-glow: rgba(139, 92, 246, 0.5);
      --primary: #8b5cf6;
      --primary-glow: #a78bfa;
      --secondary: #6366f1;
      --accent-cyan: #06b6d4;
      --accent-emerald: #10b981;
      --accent-amber: #f59e0b;
      --accent-pink: #ec4899;
      --text-main: #f3f4f6;
      --text-muted: #9ca3af;
      --text-dim: #6b7280;
      --font-heading: 'Outfit', sans-serif;
      --font-body: 'Plus Jakarta Sans', sans-serif;
      --font-code: 'Fira Code', monospace;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background-color: var(--bg-dark);
      color: var(--text-main);
      font-family: var(--font-body);
      overflow-x: hidden;
      line-height: 1.6;
      position: relative;
    }

    /* Custom Scrollbar */
    ::-webkit-scrollbar {
      width: 8px;
    }
    ::-webkit-scrollbar-track {
      background: #070913;
    }
    ::-webkit-scrollbar-thumb {
      background: #312e81;
      border-radius: 4px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #6366f1;
    }

    /* Background Ambient Canvas & Mesh */
    #ambient-canvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      pointer-events: none;
      z-index: 0;
    }

    .glow-orb {
      position: fixed;
      border-radius: 50%;
      filter: blur(130px);
      pointer-events: none;
      z-index: 0;
      opacity: 0.35;
      animation: floatOrb 18s ease-in-out infinite alternate;
    }
    .orb-1 {
      width: 550px;
      height: 550px;
      background: radial-gradient(circle, #7c3aed, transparent 70%);
      top: -100px;
      left: -100px;
    }
    .orb-2 {
      width: 600px;
      height: 600px;
      background: radial-gradient(circle, #4f46e5, transparent 70%);
      bottom: 5%;
      right: -150px;
      animation-delay: -6s;
    }
    .orb-3 {
      width: 450px;
      height: 450px;
      background: radial-gradient(circle, #06b6d4, transparent 70%);
      top: 45%;
      left: 50%;
      transform: translate(-50%, -50%);
      opacity: 0.15;
      animation-delay: -12s;
    }

    @keyframes floatOrb {
      0% { transform: translate(0, 0) scale(1); }
      50% { transform: translate(40px, 60px) scale(1.1); }
      100% { transform: translate(-30px, -40px) scale(0.95); }
    }

    /* Cursor Spotlight */
    #cursor-spotlight {
      position: fixed;
      width: 600px;
      height: 600px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(139, 92, 246, 0.08), transparent 70%);
      pointer-events: none;
      transform: translate(-50%, -50%);
      z-index: 1;
      transition: opacity 0.3s;
    }

    /* Layout Container */
    .app-container {
      position: relative;
      z-index: 2;
      max-width: 1280px;
      margin: 0 auto;
      padding: 0 24px;
    }

    /* Glass Effect Utilities */
    .glass-panel {
      background: var(--bg-card);
      backdrop-filter: blur(20px);
      -webkit-backdrop-filter: blur(20px);
      border: 1px solid var(--border-color);
      border-radius: 20px;
      transition: all 0.35s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .glass-panel:hover {
      border-color: var(--border-glow);
      box-shadow: 0 12px 40px -10px rgba(139, 92, 246, 0.25);
    }

    /* Top Sticky Navbar */
    .navbar-wrapper {
      position: fixed;
      top: 16px;
      left: 0;
      width: 100%;
      z-index: 100;
      display: flex;
      justify-content: center;
      padding: 0 20px;
    }
    .navbar {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 20px;
      padding: 10px 24px;
      background: rgba(11, 14, 29, 0.82);
      backdrop-filter: blur(24px);
      -webkit-backdrop-filter: blur(24px);
      border: 1px solid rgba(139, 92, 246, 0.25);
      border-radius: 9999px;
      max-width: 1100px;
      width: 100%;
      box-shadow: 0 10px 35px rgba(0, 0, 0, 0.4);
    }
    .nav-brand {
      display: flex;
      align-items: center;
      gap: 10px;
      font-family: var(--font-heading);
      font-weight: 800;
      font-size: 1.25rem;
      color: #fff;
      text-decoration: none;
      letter-spacing: -0.5px;
    }
    .brand-glow {
      background: linear-gradient(135deg, #a78bfa, #6366f1, #38bdf8);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }
    .nav-links {
      display: flex;
      align-items: center;
      gap: 6px;
      list-style: none;
    }
    .nav-links a {
      color: var(--text-muted);
      text-decoration: none;
      font-size: 0.88rem;
      font-weight: 500;
      padding: 7px 14px;
      border-radius: 9999px;
      transition: all 0.2s ease;
    }
    .nav-links a:hover, .nav-links a.active {
      color: #fff;
      background: rgba(139, 92, 246, 0.18);
    }
    .nav-actions {
      display: flex;
      align-items: center;
      gap: 10px;
    }
    .btn-nav-primary {
      background: linear-gradient(135deg, #7c3aed, #4f46e5);
      color: #fff;
      border: none;
      padding: 8px 18px;
      border-radius: 9999px;
      font-size: 0.85rem;
      font-weight: 600;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 8px;
      transition: all 0.25s ease;
      box-shadow: 0 4px 15px rgba(124, 58, 237, 0.35);
      text-decoration: none;
    }
    .btn-nav-primary:hover {
      transform: translateY(-1px);
      box-shadow: 0 6px 20px rgba(124, 58, 237, 0.55);
      filter: brightness(1.1);
    }
    .btn-mode-toggle {
      background: rgba(255, 255, 255, 0.06);
      border: 1px solid rgba(255, 255, 255, 0.12);
      color: #e2e8f0;
      padding: 8px 14px;
      border-radius: 9999px;
      font-size: 0.82rem;
      font-weight: 600;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 6px;
      transition: all 0.2s;
    }
    .btn-mode-toggle:hover {
      background: rgba(139, 92, 246, 0.2);
      border-color: var(--primary);
    }

    /* Hero Section */
    .hero-section {
      padding-top: 140px;
      padding-bottom: 70px;
      text-align: center;
      position: relative;
    }
    .status-pill {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 6px 18px;
      border-radius: 9999px;
      background: rgba(16, 185, 129, 0.1);
      border: 1px solid rgba(16, 185, 129, 0.3);
      color: #34d399;
      font-size: 0.84rem;
      font-weight: 600;
      margin-bottom: 24px;
      box-shadow: 0 0 20px rgba(16, 185, 129, 0.15);
      animation: pulseGlow 2.5s infinite;
    }
    .status-dot {
      width: 8px;
      height: 8px;
      border-radius: 50%;
      background: #10b981;
      box-shadow: 0 0 10px #10b981;
    }
    @keyframes pulseGlow {
      0%, 100% { transform: scale(1); opacity: 1; }
      50% { transform: scale(1.02); opacity: 0.85; }
    }

    .hero-title {
      font-family: var(--font-heading);
      font-size: clamp(2.8rem, 6vw, 4.6rem);
      font-weight: 900;
      letter-spacing: -1.5px;
      line-height: 1.1;
      margin-bottom: 18px;
    }
    .gradient-text {
      background: linear-gradient(135deg, #ffffff 15%, #c4b5fd 50%, #818cf8 80%, #38bdf8 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      display: inline-block;
    }
    .typing-container {
      font-family: var(--font-code);
      font-size: clamp(1.1rem, 2.5vw, 1.45rem);
      color: var(--primary-glow);
      min-height: 40px;
      margin-bottom: 28px;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 6px;
    }
    .cursor-blink {
      display: inline-block;
      width: 3px;
      height: 1.2em;
      background-color: var(--primary-glow);
      animation: blink 0.8s infinite;
    }
    @keyframes blink {
      0%, 100% { opacity: 1; }
      50% { opacity: 0; }
    }

    .hero-badges-row {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 12px;
      margin-bottom: 36px;
    }
    .hero-badge {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 8px 16px;
      border-radius: 12px;
      background: rgba(255, 255, 255, 0.04);
      border: 1px solid rgba(255, 255, 255, 0.09);
      font-size: 0.85rem;
      font-weight: 600;
      color: #e2e8f0;
      transition: all 0.25s ease;
    }
    .hero-badge:hover {
      background: rgba(139, 92, 246, 0.15);
      border-color: var(--primary);
      transform: translateY(-2px);
    }
    .hero-badge i {
      color: var(--primary-glow);
    }

    .hero-cta-group {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 16px;
    }
    .btn-hero {
      padding: 13px 28px;
      border-radius: 14px;
      font-weight: 700;
      font-size: 0.96rem;
      text-decoration: none;
      display: inline-flex;
      align-items: center;
      gap: 10px;
      transition: all 0.25s ease;
      cursor: pointer;
    }
    .btn-hero-primary {
      background: linear-gradient(135deg, #7c3aed, #4f46e5);
      color: #fff;
      box-shadow: 0 10px 30px rgba(124, 58, 237, 0.4);
      border: none;
    }
    .btn-hero-primary:hover {
      transform: translateY(-2px);
      box-shadow: 0 15px 35px rgba(124, 58, 237, 0.6);
      filter: brightness(1.1);
    }
    .btn-hero-secondary {
      background: rgba(255, 255, 255, 0.05);
      color: #f1f5f9;
      border: 1px solid rgba(255, 255, 255, 0.15);
      backdrop-filter: blur(10px);
    }
    .btn-hero-secondary:hover {
      background: rgba(255, 255, 255, 0.1);
      border-color: rgba(255, 255, 255, 0.3);
      transform: translateY(-2px);
    }

    /* Section Headings */
    .section-header {
      text-align: center;
      margin-bottom: 50px;
      position: relative;
    }
    .section-tag {
      font-family: var(--font-code);
      text-transform: uppercase;
      letter-spacing: 2px;
      font-size: 0.8rem;
      font-weight: 600;
      color: var(--primary-glow);
      margin-bottom: 8px;
      display: inline-block;
    }
    .section-title {
      font-family: var(--font-heading);
      font-size: clamp(2rem, 3.5vw, 2.75rem);
      font-weight: 800;
      letter-spacing: -0.8px;
      color: #fff;
    }
    .section-subtitle {
      color: var(--text-muted);
      max-width: 650px;
      margin: 10px auto 0;
      font-size: 1rem;
    }

    /* Terminal & Bio Section */
    .terminal-window {
      background: #0c0f24;
      border: 1px solid rgba(139, 92, 246, 0.28);
      border-radius: 18px;
      overflow: hidden;
      box-shadow: 0 20px 50px rgba(0, 0, 0, 0.5), 0 0 30px rgba(139, 92, 246, 0.1);
      margin-bottom: 80px;
    }
    .terminal-header {
      background: #121633;
      padding: 12px 18px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      border-bottom: 1px solid rgba(255, 255, 255, 0.06);
    }
    .terminal-dots {
      display: flex;
      gap: 7px;
    }
    .t-dot {
      width: 12px;
      height: 12px;
      border-radius: 50%;
    }
    .t-red { background: #ef4444; }
    .t-yellow { background: #eab308; }
    .t-green { background: #22c55e; }
    .terminal-title {
      font-family: var(--font-code);
      font-size: 0.8rem;
      color: var(--text-muted);
      display: flex;
      align-items: center;
      gap: 6px;
    }
    .terminal-tabs {
      display: flex;
      gap: 6px;
    }
    .t-tab-btn {
      background: transparent;
      border: none;
      color: var(--text-muted);
      font-family: var(--font-code);
      font-size: 0.78rem;
      padding: 4px 10px;
      border-radius: 6px;
      cursor: pointer;
      transition: all 0.2s;
    }
    .t-tab-btn.active, .t-tab-btn:hover {
      color: #fff;
      background: rgba(139, 92, 246, 0.2);
    }
    .terminal-body {
      padding: 24px;
      font-family: var(--font-code);
      font-size: 0.92rem;
      line-height: 1.7;
      color: #cbd5e1;
    }
    .t-prompt {
      color: #38bdf8;
    }
    .t-cmd {
      color: #f1f5f9;
      font-weight: 600;
    }
    .t-output {
      margin-top: 12px;
      margin-bottom: 20px;
      color: #94a3b8;
    }
    .json-key { color: #c084fc; }
    .json-str { color: #86efac; }
    .json-arr { color: #67e8f9; }

    /* Tech Stack Arsenal */
    .stack-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 24px;
      margin-bottom: 80px;
    }
    .stack-category-card {
      padding: 28px;
      background: var(--bg-card);
      border: 1px solid var(--border-color);
      border-radius: 20px;
      backdrop-filter: blur(16px);
      transition: all 0.35s ease;
      position: relative;
      overflow: hidden;
    }
    .stack-category-card:hover {
      transform: translateY(-5px);
      border-color: var(--border-glow);
      box-shadow: 0 16px 35px -10px rgba(139, 92, 246, 0.25);
    }
    .category-header {
      display: flex;
      align-items: center;
      gap: 14px;
      margin-bottom: 20px;
    }
    .category-icon-box {
      width: 46px;
      height: 46px;
      border-radius: 14px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.25rem;
      background: linear-gradient(135deg, rgba(139, 92, 246, 0.2), rgba(99, 102, 241, 0.1));
      color: var(--primary-glow);
      border: 1px solid rgba(139, 92, 246, 0.3);
    }
    .category-name {
      font-family: var(--font-heading);
      font-size: 1.2rem;
      font-weight: 700;
      color: #fff;
    }
    .skill-badges-container {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
    }
    .skill-pill {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 8px 14px;
      background: rgba(255, 255, 255, 0.035);
      border: 1px solid rgba(255, 255, 255, 0.08);
      border-radius: 10px;
      font-size: 0.84rem;
      font-weight: 600;
      color: #e2e8f0;
      transition: all 0.25s ease;
    }
    .skill-pill:hover {
      background: rgba(139, 92, 246, 0.18);
      border-color: var(--primary);
      transform: scale(1.04);
    }
    .skill-pill img {
      width: 20px;
      height: 20px;
    }

    /* Featured Projects */
    .projects-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(360px, 1fr));
      gap: 30px;
      margin-bottom: 80px;
    }
    .project-card {
      background: var(--bg-card);
      border: 1px solid var(--border-color);
      border-radius: 24px;
      padding: 32px;
      backdrop-filter: blur(20px);
      transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      position: relative;
      overflow: hidden;
    }
    .project-card::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      height: 3px;
      background: linear-gradient(90deg, #7c3aed, #6366f1, #06b6d4);
      opacity: 0;
      transition: opacity 0.3s;
    }
    .project-card:hover {
      transform: translateY(-8px);
      border-color: rgba(139, 92, 246, 0.45);
      box-shadow: 0 20px 45px -12px rgba(124, 58, 237, 0.35);
    }
    .project-card:hover::before {
      opacity: 1;
    }
    .project-top {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      margin-bottom: 16px;
    }
    .project-badge {
      display: inline-block;
      font-family: var(--font-code);
      font-size: 0.72rem;
      font-weight: 700;
      text-transform: uppercase;
      letter-spacing: 1px;
      padding: 5px 12px;
      border-radius: 9999px;
      background: rgba(139, 92, 246, 0.15);
      color: var(--primary-glow);
      border: 1px solid rgba(139, 92, 246, 0.3);
    }
    .project-link-icon {
      width: 40px;
      height: 40px;
      border-radius: 50%;
      background: rgba(255, 255, 255, 0.05);
      border: 1px solid rgba(255, 255, 255, 0.1);
      display: flex;
      align-items: center;
      justify-content: center;
      color: #fff;
      text-decoration: none;
      transition: all 0.25s;
    }
    .project-link-icon:hover {
      background: var(--primary);
      transform: rotate(45deg);
    }
    .project-title {
      font-family: var(--font-heading);
      font-size: 1.5rem;
      font-weight: 800;
      color: #fff;
      margin-bottom: 12px;
      line-height: 1.25;
    }
    .project-desc {
      color: var(--text-muted);
      font-size: 0.94rem;
      margin-bottom: 20px;
      line-height: 1.6;
    }
    .project-features {
      list-style: none;
      margin-bottom: 24px;
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 8px;
    }
    .project-features li {
      font-size: 0.83rem;
      color: #cbd5e1;
      display: flex;
      align-items: center;
      gap: 7px;
    }
    .project-features li i {
      color: var(--accent-cyan);
      font-size: 0.75rem;
    }
    .project-tech-tags {
      display: flex;
      flex-wrap: wrap;
      gap: 7px;
      margin-bottom: 24px;
    }
    .tech-tag {
      font-family: var(--font-code);
      font-size: 0.76rem;
      font-weight: 600;
      padding: 4px 10px;
      border-radius: 6px;
      background: rgba(255, 255, 255, 0.04);
      color: #c4b5fd;
      border: 1px solid rgba(139, 92, 246, 0.15);
    }
    .btn-repo {
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      width: 100%;
      padding: 12px;
      border-radius: 12px;
      background: rgba(255, 255, 255, 0.04);
      border: 1px solid rgba(255, 255, 255, 0.1);
      color: #fff;
      text-decoration: none;
      font-size: 0.88rem;
      font-weight: 600;
      transition: all 0.25s ease;
    }
    .btn-repo:hover {
      background: rgba(139, 92, 246, 0.25);
      border-color: var(--primary);
    }

    /* AI / ML Architecture Matrix */
    .ai-matrix-card {
      background: linear-gradient(135deg, rgba(20, 24, 54, 0.8), rgba(12, 15, 34, 0.8));
      border: 1px solid rgba(139, 92, 246, 0.3);
      border-radius: 24px;
      padding: 36px;
      margin-bottom: 80px;
      box-shadow: 0 15px 40px rgba(0, 0, 0, 0.4);
    }
    .pipeline-steps {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 16px;
      margin-bottom: 36px;
      position: relative;
    }
    .pipeline-step {
      background: rgba(255, 255, 255, 0.03);
      border: 1px solid rgba(255, 255, 255, 0.08);
      border-radius: 16px;
      padding: 20px;
      text-align: center;
      transition: all 0.3s;
    }
    .pipeline-step:hover {
      background: rgba(139, 92, 246, 0.15);
      border-color: var(--primary);
      transform: translateY(-4px);
    }
    .step-num {
      width: 28px;
      height: 28px;
      border-radius: 50%;
      background: var(--primary);
      color: #fff;
      font-size: 0.8rem;
      font-weight: 700;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 12px;
    }
    .step-title {
      font-family: var(--font-heading);
      font-weight: 700;
      font-size: 1.05rem;
      color: #fff;
      margin-bottom: 6px;
    }
    .step-desc {
      font-size: 0.82rem;
      color: var(--text-muted);
    }

    .matrix-table {
      width: 100%;
      border-collapse: collapse;
      font-size: 0.92rem;
    }
    .matrix-table th {
      text-align: left;
      padding: 14px 18px;
      background: rgba(255, 255, 255, 0.04);
      color: var(--primary-glow);
      font-family: var(--font-heading);
      font-weight: 700;
      border-bottom: 1px solid rgba(255, 255, 255, 0.08);
    }
    .matrix-table td {
      padding: 14px 18px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.05);
      color: #cbd5e1;
    }
    .matrix-table tr:hover td {
      background: rgba(139, 92, 246, 0.06);
    }
    .status-tag {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      padding: 4px 10px;
      border-radius: 6px;
      background: rgba(16, 185, 129, 0.15);
      color: #34d399;
      font-size: 0.78rem;
      font-weight: 600;
    }

    /* GitHub Stats & Analytics Hub */
    .analytics-section {
      margin-bottom: 80px;
    }
    .stats-cards-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
      gap: 24px;
      margin-bottom: 24px;
    }
    .stat-img-card {
      background: var(--bg-card);
      border: 1px solid var(--border-color);
      border-radius: 20px;
      padding: 24px;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
      transition: all 0.3s ease;
    }
    .stat-img-card:hover {
      border-color: var(--border-glow);
      transform: translateY(-4px);
      box-shadow: 0 12px 35px rgba(124, 58, 237, 0.2);
    }
    .stat-img-card img {
      max-width: 100%;
      height: auto;
      border-radius: 12px;
    }

    /* Focus YAML Interactive Card */
    .focus-card {
      background: #0d111d;
      border: 1px solid rgba(139, 92, 246, 0.3);
      border-radius: 20px;
      padding: 28px;
      font-family: var(--font-code);
      margin-bottom: 80px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.4);
    }
    .focus-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 20px;
      padding-bottom: 12px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.08);
    }
    .yaml-tree {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 20px;
    }
    .yaml-branch {
      background: rgba(255, 255, 255, 0.02);
      border: 1px solid rgba(255, 255, 255, 0.05);
      border-radius: 14px;
      padding: 16px;
    }
    .yaml-branch-title {
      color: #38bdf8;
      font-size: 0.95rem;
      font-weight: 700;
      margin-bottom: 10px;
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .yaml-item {
      font-size: 0.84rem;
      color: #cbd5e1;
      margin-bottom: 6px;
      display: flex;
      align-items: center;
      gap: 6px;
    }
    .yaml-item::before {
      content: "•";
      color: var(--primary-glow);
    }

    /* Contact / Connect Section */
    .connect-section {
      text-align: center;
      padding: 60px 24px;
      background: linear-gradient(180deg, rgba(15, 18, 37, 0.5) 0%, rgba(10, 12, 26, 0.9) 100%);
      border: 1px solid var(--border-color);
      border-radius: 30px;
      margin-bottom: 80px;
      position: relative;
      overflow: hidden;
    }
    .connect-title {
      font-family: var(--font-heading);
      font-size: 2.2rem;
      font-weight: 800;
      color: #fff;
      margin-bottom: 12px;
    }
    .connect-subtitle {
      color: var(--text-muted);
      max-width: 550px;
      margin: 0 auto 30px;
    }
    .social-links-row {
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 14px;
    }
    .social-btn {
      display: inline-flex;
      align-items: center;
      gap: 10px;
      padding: 12px 24px;
      border-radius: 14px;
      background: rgba(255, 255, 255, 0.05);
      border: 1px solid rgba(255, 255, 255, 0.1);
      color: #fff;
      text-decoration: none;
      font-weight: 600;
      font-size: 0.92rem;
      transition: all 0.25s ease;
    }
    .social-btn:hover {
      background: rgba(139, 92, 246, 0.25);
      border-color: var(--primary);
      transform: translateY(-3px);
      box-shadow: 0 8px 25px rgba(124, 58, 237, 0.3);
    }

    /* Footer */
    footer {
      border-top: 1px solid rgba(255, 255, 255, 0.08);
      padding: 30px 0 50px;
      text-align: center;
      color: var(--text-dim);
      font-size: 0.85rem;
    }

    /* Markdown Drawer / GitHub Modal */
    .modal-overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      background: rgba(5, 7, 15, 0.85);
      backdrop-filter: blur(12px);
      z-index: 1000;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 20px;
      opacity: 0;
      pointer-events: none;
      transition: all 0.3s ease;
    }
    .modal-overlay.active {
      opacity: 1;
      pointer-events: auto;
    }
    .modal-card {
      background: #0d111d;
      border: 1px solid rgba(139, 92, 246, 0.4);
      border-radius: 20px;
      max-width: 900px;
      width: 100%;
      max-height: 88vh;
      display: flex;
      flex-direction: column;
      box-shadow: 0 25px 60px rgba(0, 0, 0, 0.8), 0 0 40px rgba(139, 92, 246, 0.2);
      transform: scale(0.95);
      transition: transform 0.3s ease;
    }
    .modal-overlay.active .modal-card {
      transform: scale(1);
    }
    .modal-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 18px 24px;
      border-bottom: 1px solid rgba(255, 255, 255, 0.08);
    }
    .modal-body {
      padding: 20px 24px;
      overflow-y: auto;
      font-family: var(--font-code);
      font-size: 0.86rem;
      color: #cbd5e1;
      white-space: pre-wrap;
      background: #090c16;
      user-select: text;
    }
    .modal-footer {
      display: flex;
      align-items: center;
      justify-content: flex-end;
      gap: 12px;
      padding: 16px 24px;
      border-top: 1px solid rgba(255, 255, 255, 0.08);
    }

    /* Toast Notification */
    .toast {
      position: fixed;
      bottom: 24px;
      right: 24px;
      background: linear-gradient(135deg, #10b981, #059669);
      color: #fff;
      padding: 12px 22px;
      border-radius: 12px;
      font-weight: 600;
      font-size: 0.9rem;
      display: flex;
      align-items: center;
      gap: 8px;
      box-shadow: 0 10px 25px rgba(16, 185, 129, 0.4);
      z-index: 2000;
      transform: translateY(100px);
      opacity: 0;
      transition: all 0.3s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .toast.show {
      transform: translateY(0);
      opacity: 1;
    }

    /* Mobile Responsive adjustments */
    @media (max-width: 768px) {
      .nav-links { display: none; }
      .hero-title { font-size: 2.5rem; }
      .project-features { grid-template-columns: 1fr; }
      .projects-grid { grid-template-columns: 1fr; }
      .terminal-tabs { display: none; }
    }
  </style>
</head>
<body>

  <!-- Ambient Glow Orbs -->
  <div class="glow-orb orb-1"></div>
  <div class="glow-orb orb-2"></div>
  <div class="glow-orb orb-3"></div>

  <!-- Ambient Canvas Background -->
  <canvas id="ambient-canvas"></canvas>

  <!-- Cursor Spotlight -->
  <div id="cursor-spotlight"></div>

  <!-- Top Sticky Navigation -->
  <header class="navbar-wrapper">
    <nav class="navbar">
      <a href="#hero" class="nav-brand">
        <i class="fa-solid fa-code" style="color: #8b5cf6;"></i>
        <span>Het<span class="brand-glow">.dev</span></span>
      </a>

      <ul class="nav-links">
        <li><a href="#about">About</a></li>
        <li><a href="#skills">Tech Stack</a></li>
        <li><a href="#projects">Projects</a></li>
        <li><a href="#aiml">AI / ML</a></li>
        <li><a href="#analytics">GitHub Stats</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>

      <div class="nav-actions">
        <button class="btn-mode-toggle" id="open-readme-btn" title="View Clean GitHub Profile Markdown">
          <i class="fa-brands fa-markdown"></i>
          <span>GitHub README</span>
        </button>
        <a href="https://github.com/hetdhameliya09" target="_blank" class="btn-nav-primary">
          <i class="fa-brands fa-github"></i>
          <span>Follow</span>
        </a>
      </div>
    </nav>
  </header>

  <!-- Main Container -->
  <main class="app-container">

    <!-- HERO SECTION -->
    <section id="hero" class="hero-section">
      <div class="status-pill">
        <span class="status-dot"></span>
        <span>Open To Full-Stack &amp; AI/ML Opportunities</span>
      </div>

      <h1 class="hero-title">
        Hi, I'm <span class="gradient-text">Het N Dhameliya</span>
      </h1>

      <div class="typing-container">
        <span id="typing-text"></span>
        <span class="cursor-blink"></span>
      </div>

      <div class="hero-badges-row">
        <div class="hero-badge">
          <i class="fa-solid fa-graduation-cap"></i>
          <span>Engineering Student</span>
        </div>
        <div class="hero-badge">
          <i class="fa-solid fa-layer-group"></i>
          <span>Full-Stack Development</span>
        </div>
        <div class="hero-badge">
          <i class="fa-solid fa-brain"></i>
          <span>AI / ML Applications</span>
        </div>
        <div class="hero-badge">
          <i class="fa-solid fa-server"></i>
          <span>Django &amp; React Architect</span>
        </div>
      </div>

      <div class="hero-cta-group">
        <a href="#projects" class="btn-hero btn-hero-primary">
          <i class="fa-solid fa-rocket"></i>
          <span>Explore Featured Projects</span>
        </a>
        <button class="btn-hero btn-hero-secondary" id="quick-copy-md">
          <i class="fa-regular fa-copy"></i>
          <span>Copy Fixed GitHub Markdown</span>
        </button>
      </div>
    </section>

    <!-- INTERACTIVE TERMINAL & BIO SECTION -->
    <section id="about">
      <div class="section-header">
        <span class="section-tag">// IDENTITY &amp; PHILOSOPHY</span>
        <h2 class="section-title">Engineering Practical Systems</h2>
        <p class="section-subtitle">
          Building real-world software across full-stack architectures, data-driven backends, and machine learning decision systems.
        </p>
      </div>

      <div class="terminal-window">
        <div class="terminal-header">
          <div class="terminal-dots">
            <span class="t-dot t-red"></span>
            <span class="t-dot t-yellow"></span>
            <span class="t-dot t-green"></span>
          </div>
          <div class="terminal-title">
            <i class="fa-solid fa-terminal"></i>
            <span>het@workstation: ~/portfolio (zsh)</span>
          </div>
          <div class="terminal-tabs">
            <button class="t-tab-btn active" onclick="switchTermTab('bio')">bio.json</button>
            <button class="t-tab-btn" onclick="switchTermTab('skills')">stack.config</button>
            <button class="t-tab-btn" onclick="switchTermTab('goals')">mission.yaml</button>
          </div>
        </div>

        <div class="terminal-body" id="term-body">
          <p><span class="t-prompt">het@workstation:~$</span> <span class="t-cmd">cat bio.json</span></p>
          <div class="t-output" id="term-content">
{
  <span class="json-key">"name"</span>: <span class="json-str">"Het N Dhameliya"</span>,
  <span class="json-key">"role"</span>: <span class="json-str">"Full-Stack Developer &amp; AI/ML Project Builder"</span>,
  <span class="json-key">"focus"</span>: <span class="json-str">"Backend systems, modern frontend UI/UX, and data-driven intelligence"</span>,
  <span class="json-key">"stack_highlights"</span>: [
    <span class="json-arr">"Django"</span>, <span class="json-arr">"Django REST Framework"</span>, <span class="json-arr">"React"</span>, <span class="json-arr">"Vite"</span>, <span class="json-arr">"Python"</span>, <span class="json-arr">"Scikit-Learn"</span>, <span class="json-arr">"Tailwind CSS"</span>
  ],
  <span class="json-key">"philosophy"</span>: <span class="json-str">"Turning real-world enterprise &amp; agricultural workflows into robust, usable digital products."</span>,
  <span class="json-key">"open_to"</span>: [
    <span class="json-arr">"Full-Stack Development"</span>,
    <span class="json-arr">"Django / Python Backend Engineering"</span>,
    <span class="json-arr">"React &amp; Modern Frontend Engineering"</span>,
    <span class="json-arr">"AI / ML Application Development"</span>,
    <span class="json-arr">"Open Source &amp; Product Engineering"</span>
  ]
}
          </div>
        </div>
      </div>
    </section>

    <!-- TECH STACK ARSENAL -->
    <section id="skills">
      <div class="section-header">
        <span class="section-tag">// ARSENAL &amp; CAPABILITIES</span>
        <h2 class="section-title">Technical Expertise</h2>
        <p class="section-subtitle">
          Battle-tested toolset for crafting scalable backends, performant user interfaces, and intelligent pipelines.
        </p>
      </div>

      <div class="stack-grid">
        <!-- Languages -->
        <div class="stack-category-card">
          <div class="category-header">
            <div class="category-icon-box">
              <i class="fa-solid fa-code"></i>
            </div>
            <h3 class="category-name">Languages</h3>
          </div>
          <div class="skill-badges-container">
            <span class="skill-pill"><img src="https://skillicons.dev/icons?i=python" alt="Python" /> Python</span>
            <span class="skill-pill"><img src="https://skillicons.dev/icons?i=js" alt="JavaScript" /> JavaScript (ES6+)</span>
            <span class="skill-pill"><img src="https://skillicons.dev/icons?i=html" alt="HTML5" /> HTML5</span>
            <span class="skill-pill"><img src="https://skillicons.dev/icons?i=css" alt="CSS3" /> CSS3</span>
          </div>
        </div>

        <!-- Frontend -->
        <div class="stack-category-card">
          <div class="category-header">
            <div class="category-icon-box">
              <i class="fa-brands fa-react"></i>
            </div>
            <h3 class="category-name">Frontend</h3>
          </div>
          <div class="skill-badges-container">
            <span class="skill-pill"><img src="https://skillicons.dev/icons?i=react" alt="React" /> React.js</span>
            <span class="skill-pill"><img src="https://skillicons.dev/icons?i=vite" alt="Vite" /> Vite</span>
            <span class="skill-pill"><img src="https://skillicons.dev/icons?i=tailwind" alt="Tailwind" /> Tailwind CSS</span>
            <span class="skill-pill"><img src="https://skillicons.dev/icons?i=bootstrap" alt="Bootstrap" /> Bootstrap 5</span>
            <span class="skill-pill"><i class="fa-solid fa-chart-pie" style="color:#f59e0b;"></i> Chart.js</span>
          </div>
        </div>

        <!-- Backend & Databases -->
        <div class="stack-category-card">
          <div class="category-header">
            <div class="category-icon-box">
              <i class="fa-solid fa-server"></i>
            </div>
            <h3 class="category-name">Backend &amp; Databases</h3>
          </div>
          <div class="skill-badges-container">
            <span class="skill-pill"><img src="https://skillicons.dev/icons?i=django" alt="Django" /> Django</span>
            <span class="skill-pill"><i class="fa-solid fa-network-wired" style="color:#6366f1;"></i> Django REST Framework</span>
            <span class="skill-pill"><img src="https://skillicons.dev/icons?i=postgres" alt="Postgres" /> PostgreSQL</span>
            <span class="skill-pill"><img src="https://skillicons.dev/icons?i=sqlite" alt="SQLite" /> SQLite</span>
            <span class="skill-pill"><i class="fa-solid fa-key" style="color:#10b981;"></i> JWT Authentication</span>
          </div>
        </div>

        <!-- AI/ML & Engineering Tools -->
        <div class="stack-category-card">
          <div class="category-header">
            <div class="category-icon-box">
              <i class="fa-solid fa-brain"></i>
            </div>
            <h3 class="category-name">AI / ML &amp; DevOps</h3>
          </div>
          <div class="skill-badges-container">
            <span class="skill-pill"><i class="fa-solid fa-microchip" style="color:#ec4899;"></i> Scikit-Learn</span>
            <span class="skill-pill"><i class="fa-solid fa-tree" style="color:#10b981;"></i> Random Forest ML</span>
            <span class="skill-pill"><img src="https://skillicons.dev/icons?i=git" alt="Git" /> Git &amp; GitHub</span>
            <span class="skill-pill"><img src="https://skillicons.dev/icons?i=vscode" alt="VSCode" /> VS Code</span>
            <span class="skill-pill"><img src="https://skillicons.dev/icons?i=npm" alt="NPM" /> NPM</span>
            <span class="skill-pill"><i class="fa-solid fa-spider" style="color:#38bdf8;"></i> Web Scraping</span>
          </div>
        </div>
      </div>
    </section>

    <!-- FEATURED PROJECTS SHOWCASE -->
    <section id="projects">
      <div class="section-header">
        <span class="section-tag">// CRAFTED WORK &amp; SYSTEMS</span>
        <h2 class="section-title">Featured Projects</h2>
        <p class="section-subtitle">
          Real-world applications built from scratch with robust architecture and modern user experiences.
        </p>
      </div>

      <div class="projects-grid">
        <!-- Project 1: AgroSense -->
        <div class="project-card">
          <div>
            <div class="project-top">
              <span class="project-badge">Full-Stack + AI / ML</span>
              <a href="https://github.com/hetdhameliya09/Smart-Agriculture-Assistant-Platform" target="_blank" class="project-link-icon" title="View on GitHub">
                <i class="fa-solid fa-arrow-up-right-from-square"></i>
              </a>
            </div>
            <h3 class="project-title">🌾 AgroSense — Smart Agriculture Platform</h3>
            <p class="project-desc">
              An end-to-end agricultural decision-support system featuring machine learning crop recommendation and yield prediction, role-based portals, live agricultural news, market rates, and automated PDF certification.
            </p>
            <ul class="project-features">
              <li><i class="fa-solid fa-circle-check"></i> ML Crop Recommendation</li>
              <li><i class="fa-solid fa-circle-check"></i> Random Forest Yield Prediction</li>
              <li><i class="fa-solid fa-circle-check"></i> Farmer, Officer &amp; Admin Roles</li>
              <li><i class="fa-solid fa-circle-check"></i> JWT Secured Auth</li>
              <li><i class="fa-solid fa-circle-check"></i> Automated PDF Certificates</li>
              <li><i class="fa-solid fa-circle-check"></i> Web Scraping Engine</li>
            </ul>
            <div class="project-tech-tags">
              <span class="tech-tag">Python</span>
              <span class="tech-tag">Django</span>
              <span class="tech-tag">DRF</span>
              <span class="tech-tag">React</span>
              <span class="tech-tag">Vite</span>
              <span class="tech-tag">Tailwind</span>
              <span class="tech-tag">Scikit-Learn</span>
            </div>
          </div>
          <a href="https://github.com/hetdhameliya09/Smart-Agriculture-Assistant-Platform" target="_blank" class="btn-repo">
            <i class="fa-brands fa-github"></i>
            <span>Inspect Repository</span>
          </a>
        </div>

        <!-- Project 2: VendorBridge -->
        <div class="project-card">
          <div>
            <div class="project-top">
              <span class="project-badge">Enterprise ERP / SRM</span>
              <a href="https://github.com/hetdhameliya09/VendorBridge" target="_blank" class="project-link-icon" title="View on GitHub">
                <i class="fa-solid fa-arrow-up-right-from-square"></i>
              </a>
            </div>
            <h3 class="project-title">🏢 VendorBridge — Procurement &amp; SRM</h3>
            <p class="project-desc">
              Comprehensive Django-powered procurement management software covering the complete lifecycle: supplier onboarding, RFQ generation, quotation matrix comparison, multi-tier approvals, purchase orders, and PDF invoicing.
            </p>
            <ul class="project-features">
              <li><i class="fa-solid fa-circle-check"></i> Vendor Onboarding &amp; Vetting</li>
              <li><i class="fa-solid fa-circle-check"></i> RFQ &amp; Quotation Engine</li>
              <li><i class="fa-solid fa-circle-check"></i> Quotation Comparison Matrix</li>
              <li><i class="fa-solid fa-circle-check"></i> Multi-level Approvals</li>
              <li><i class="fa-solid fa-circle-check"></i> Purchase Orders &amp; Invoices</li>
              <li><i class="fa-solid fa-circle-check"></i> Interactive Chart.js Analytics</li>
            </ul>
            <div class="project-tech-tags">
              <span class="tech-tag">Python</span>
              <span class="tech-tag">Django</span>
              <span class="tech-tag">Bootstrap 5</span>
              <span class="tech-tag">Chart.js</span>
              <span class="tech-tag">SQLite</span>
              <span class="tech-tag">PDF Invoicing</span>
            </div>
          </div>
          <a href="https://github.com/hetdhameliya09/VendorBridge" target="_blank" class="btn-repo">
            <i class="fa-brands fa-github"></i>
            <span>Inspect Repository</span>
          </a>
        </div>

        <!-- Project 3: SEM IV FSD-II -->
        <div class="project-card">
          <div>
            <div class="project-top">
              <span class="project-badge">Modern Frontend</span>
              <a href="https://github.com/hetdhameliya09/SEM_IV_FSD-II" target="_blank" class="project-link-icon" title="View on GitHub">
                <i class="fa-solid fa-arrow-up-right-from-square"></i>
              </a>
            </div>
            <h3 class="project-title">⚛️ SEM IV FSD-II — React &amp; Vite Architectures</h3>
            <p class="project-desc">
              Curated repository of modular full-stack frontend patterns, component lifecycles, event dispatching, client-side routing, and state management implementations built with React and Vite.
            </p>
            <ul class="project-features">
              <li><i class="fa-solid fa-circle-check"></i> Modular Component System</li>
              <li><i class="fa-solid fa-circle-check"></i> Dynamic Props &amp; State Trees</li>
              <li><i class="fa-solid fa-circle-check"></i> Client-Side SPA Routing</li>
              <li><i class="fa-solid fa-circle-check"></i> Modern ES6+ JavaScript</li>
              <li><i class="fa-solid fa-circle-check"></i> High-Speed Vite Toolchain</li>
              <li><i class="fa-solid fa-circle-check"></i> Clean Architecture Patterns</li>
            </ul>
            <div class="project-tech-tags">
              <span class="tech-tag">React</span>
              <span class="tech-tag">Vite</span>
              <span class="tech-tag">JavaScript</span>
              <span class="tech-tag">HTML5/CSS3</span>
              <span class="tech-tag">State Management</span>
            </div>
          </div>
          <a href="https://github.com/hetdhameliya09/SEM_IV_FSD-II" target="_blank" class="btn-repo">
            <i class="fa-brands fa-github"></i>
            <span>Inspect Repository</span>
          </a>
        </div>
      </div>
    </section>

    <!-- AI / ML EXPERTISE & PIPELINE -->
    <section id="aiml">
      <div class="section-header">
        <span class="section-tag">// MACHINE LEARNING INTEGRATION</span>
        <h2 class="section-title">AI / ML Applied Intelligence</h2>
        <p class="section-subtitle">
          Bridging statistical modeling with production-ready full-stack applications for real-time inference.
        </p>
      </div>

      <div class="ai-matrix-card">
        <!-- Interactive Workflow Pipeline -->
        <div class="pipeline-steps">
          <div class="pipeline-step">
            <span class="step-num">1</span>
            <h4 class="step-title">Data Ingestion</h4>
            <p class="step-desc">Collecting agricultural metrics, soil parameters, weather datasets &amp; web scraped insights.</p>
          </div>
          <div class="pipeline-step">
            <span class="step-num">2</span>
            <h4 class="step-title">Model Training</h4>
            <p class="step-desc">Tuning Scikit-Learn Random Forest estimators for high-accuracy crop &amp; yield prediction.</p>
          </div>
          <div class="pipeline-step">
            <span class="step-num">3</span>
            <h4 class="step-title">REST Inference API</h4>
            <p class="step-desc">Serving optimized inference endpoints through Django REST Framework with JWT authentication.</p>
          </div>
          <div class="pipeline-step">
            <span class="step-num">4</span>
            <h4 class="step-title">Decision UI</h4>
            <p class="step-desc">Delivering actionable recommendations and downloadable PDF certificates to farmers &amp; officers.</p>
          </div>
        </div>

        <!-- Capability Matrix Table -->
        <table class="matrix-table">
          <thead>
            <tr>
              <th>Domain</th>
              <th>Status</th>
              <th>Technical Implementation</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td><strong>Machine Learning</strong></td>
              <td><span class="status-tag"><i class="fa-solid fa-check"></i> Applied</span></td>
              <td>Scikit-Learn based pipeline and model lifecycle integration.</td>
            </tr>
            <tr>
              <td><strong>Crop Recommendation</strong></td>
              <td><span class="status-tag"><i class="fa-solid fa-check"></i> Applied</span></td>
              <td>Random Forest multi-class classification for agronomic recommendations.</td>
            </tr>
            <tr>
              <td><strong>Yield Estimation</strong></td>
              <td><span class="status-tag"><i class="fa-solid fa-check"></i> Applied</span></td>
              <td>Regression model predicting agricultural output based on real parameters.</td>
            </tr>
            <tr>
              <td><strong>Data-Driven Systems</strong></td>
              <td><span class="status-tag"><i class="fa-solid fa-check"></i> Applied</span></td>
              <td>Full-stack bridging: Model Training &rarr; REST API &rarr; React Dashboard.</td>
            </tr>
          </tbody>
        </table>
      </div>
    </section>

    <!-- GITHUB ANALYTICS & ACTIVITY HUB -->
    <section id="analytics" class="analytics-section">
      <div class="section-header">
        <span class="section-tag">// LIVE METRICS &amp; ACTIVITY</span>
        <h2 class="section-title">GitHub Analytics &amp; Activity</h2>
        <p class="section-subtitle">
          Real-time insights and contribution tracking from <a href="https://github.com/hetdhameliya09" target="_blank" style="color: var(--primary-glow); text-decoration: underline;">@hetdhameliya09</a>.
        </p>
      </div>

      <!-- Stats Cards -->
      <div class="stats-cards-grid">
        <div class="stat-img-card">
          <img src="https://github-readme-stats.vercel.app/api?username=hetdhameliya09&show_icons=true&theme=tokyonight&hide_border=true&bg_color=0D1117&title_color=8B5CF6&icon_color=6366F1&text_color=C4B5FD" alt="GitHub Stats" loading="lazy" />
        </div>
        <div class="stat-img-card">
          <img src="https://github-readme-streak-stats.herokuapp.com/?user=hetdhameliya09&theme=tokyonight&hide_border=true&background=0D1117&ring=8B5CF6&fire=6366F1&currStreakLabel=C4B5FD" alt="GitHub Streak" loading="lazy" />
        </div>
        <div class="stat-img-card">
          <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=hetdhameliya09&layout=compact&theme=tokyonight&hide_border=true&bg_color=0D1117&title_color=8B5CF6&text_color=C4B5FD" alt="Top Languages" loading="lazy" />
        </div>
      </div>

      <!-- Activity Graph Card -->
      <div class="stat-img-card" style="margin-bottom: 24px;">
        <img src="https://github-readme-activity-graph.vercel.app/graph?username=hetdhameliya09&bg_color=0D1117&color=C4B5FD&line=8B5CF6&point=6366F1&area=true&hide_border=true" alt="Contribution Graph" style="width: 100%;" loading="lazy" />
      </div>

      <!-- Trophies & Contribution Grid -->
      <div class="stats-cards-grid">
        <div class="stat-img-card">
          <img src="https://github-profile-trophy.vercel.app/?username=hetdhameliya09&theme=discord&no-frame=true&no-bg=true&margin-w=8&column=4" alt="GitHub Trophies" loading="lazy" />
        </div>
        <div class="stat-img-card">
          <img src="https://raw.githubusercontent.com/hetdhameliya09/hetdhameliya09/output/github-contribution-grid-snake.svg" alt="GitHub Contribution Snake" onerror="this.src='https://via.placeholder.com/600x200/0d1117/8b5cf6?text=GitHub+Contribution+Snake'" loading="lazy" />
        </div>
      </div>
    </section>

    <!-- CURRENT FOCUS (YAML STYLE) -->
    <section>
      <div class="focus-card">
        <div class="focus-header">
          <span style="color: #a78bfa; font-weight: 700;">⚡ current_focus.yaml</span>
          <span style="color: #64748b; font-size: 0.8rem;">Status: Actively Coding</span>
        </div>

        <div class="yaml-tree">
          <div class="yaml-branch">
            <div class="yaml-branch-title"><i class="fa-solid fa-book-open"></i> Learning:</div>
            <div class="yaml-item">Advanced Full-Stack Engineering</div>
            <div class="yaml-item">Distributed Backend Architecture</div>
            <div class="yaml-item">AI/ML Production Deployment</div>
            <div class="yaml-item">Modern Reactive Interfaces</div>
          </div>

          <div class="yaml-branch">
            <div class="yaml-branch-title"><i class="fa-solid fa-hammer"></i> Building:</div>
            <div class="yaml-item">Full-Stack Django Applications</div>
            <div class="yaml-item">Enterprise Workflow &amp; SRM Systems</div>
            <div class="yaml-item">AI-Powered Decision Support Systems</div>
            <div class="yaml-item">Dynamic Analytics Dashboards</div>
          </div>

          <div class="yaml-branch">
            <div class="yaml-branch-title"><i class="fa-solid fa-compass"></i> Exploring:</div>
            <div class="yaml-item">Scalable Web Microservices</div>
            <div class="yaml-item">Real-time ML Model Inference</div>
            <div class="yaml-item">Automated PDF &amp; Document Engines</div>
            <div class="yaml-item">Cloud Deployment &amp; CI/CD</div>
          </div>
        </div>
      </div>
    </section>

    <!-- CONTACT & CONNECT HUB -->
    <section id="contact">
      <div class="connect-section">
        <h2 class="connect-title">Let's Build Something Extraordinary</h2>
        <p class="connect-subtitle">
          Interested in collaborating, discussing full-stack projects, or exploring software engineering opportunities? Let's connect!
        </p>

        <div class="social-links-row">
          <a href="https://github.com/hetdhameliya09" target="_blank" class="social-btn">
            <i class="fa-brands fa-github" style="color: #8b5cf6;"></i>
            <span>GitHub Profile</span>
          </a>
          <button class="social-btn" id="copy-contact-btn">
            <i class="fa-solid fa-envelope" style="color: #06b6d4;"></i>
            <span>hetdhameliya09</span>
          </button>
          <a href="https://github.com/hetdhameliya09?tab=repositories" target="_blank" class="social-btn">
            <i class="fa-solid fa-folder-open" style="color: #10b981;"></i>
            <span>All Repositories</span>
          </a>
        </div>
      </div>
    </section>

  </main>

  <!-- FOOTER -->
  <footer>
    <div class="app-container">
      <p>Designed &amp; Engineered with ❤️ by <strong>Het N Dhameliya</strong> • Full-Stack &amp; AI/ML Developer</p>
      <p style="margin-top: 6px; font-size: 0.78rem;">Built with Vanilla CSS, Canvas Animations &amp; Pure Modern Web Standards.</p>
    </div>
  </footer>

  <!-- MARKDOWN VIEWER MODAL -->
  <div class="modal-overlay" id="readme-modal">
    <div class="modal-card">
      <div class="modal-header">
        <div style="display: flex; align-items: center; gap: 10px;">
          <i class="fa-brands fa-markdown" style="color: #8b5cf6; font-size: 1.3rem;"></i>
          <div>
            <h3 style="font-family: var(--font-heading); color: #fff; font-size: 1.1rem; margin: 0;">Clean GitHub Profile README</h3>
            <p style="color: #94a3b8; font-size: 0.78rem; margin: 0;">Fixed emoji encodings, polished markdown &amp; badges ready for GitHub</p>
          </div>
        </div>
        <button id="close-modal-btn" style="background: none; border: none; color: #94a3b8; font-size: 1.2rem; cursor: pointer;">
          <i class="fa-solid fa-xmark"></i>
        </button>
      </div>

      <div class="modal-body" id="raw-markdown-content"></div>

      <div class="modal-footer">
        <button class="btn-mode-toggle" id="modal-close-btn2">Close</button>
        <button class="btn-nav-primary" id="copy-modal-md-btn">
          <i class="fa-regular fa-copy"></i>
          <span>Copy Markdown</span>
        </button>
      </div>
    </div>
  </div>

  <!-- TOAST NOTIFICATION -->
  <div class="toast" id="toast">
    <i class="fa-solid fa-circle-check"></i>
    <span id="toast-msg">Copied to clipboard!</span>
  </div>

  <!-- JAVASCRIPT LOGIC -->
  <script>
    // Clean, perfectly encoded GitHub README Markdown template (without any mojibake!)
    const CLEAN_MARKDOWN = `<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f0c29,50:302b63,100:24243e&height=220&section=header&text=Het%20N%20Dhameliya&fontSize=48&fontColor=ffffff&animation=fadeIn&fontAlignY=38" width="100%"/>
</p>

<p align="center">
  <a href="https://git.io/typing-svg">
    <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=600&size=22&duration=3000&pause=900&color=8B5CF6&center=true&vCenter=true&width=750&lines=Full-Stack+Developer;Django+%7C+React+Developer;AI%2FML+Project+Builder;Software+Engineering+Enthusiast;Building+Practical+Digital+Products" alt="Typing SVG"/>
  </a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Engineering-Student-7C3AED?style=for-the-badge&labelColor=111827"/>
  <img src="https://img.shields.io/badge/Full--Stack-Development-6366F1?style=for-the-badge&labelColor=111827"/>
  <img src="https://img.shields.io/badge/AI%2FML-Projects-8B5CF6?style=for-the-badge&labelColor=111827"/>
</p>

<p align="center">
  <a href="https://github.com/hetdhameliya09">
    <img src="https://img.shields.io/badge/GitHub-hetdhameliya09-6366F1?style=for-the-badge&logo=github&logoColor=white&labelColor=111827"/>
  </a>
  <img src="https://komarev.com/ghpvc/?username=hetdhameliya09&style=for-the-badge&color=7C3AED&label=PROFILE+VIEWS"/>
</p>

---

## 👨‍💻 About Me

I am an engineering-focused developer building practical full-stack applications with an emphasis on backend systems, modern frontend development, data-driven features, and product-oriented engineering.

My GitHub work includes Django-based applications, React/Vite development, REST APIs, authentication and role-based access control, procurement workflows, analytics dashboards, web scraping, and machine-learning-powered decision support systems.

I enjoy turning real-world workflows into usable software — from enterprise procurement and supplier management to smart agriculture, analytics, and AI-assisted decision systems.

### 🎯 Open To

- Full-Stack Development
- Django / Python Development
- React Development
- Backend & REST API Engineering
- AI / ML Application Development
- Software Engineering Projects
- Open Source Collaboration

---

## ⚡ Tech Stack

### Languages
<p>
  <img src="https://skillicons.dev/icons?i=python,js,html,css" />
</p>

### Frontend
<p>
  <img src="https://skillicons.dev/icons?i=react,vite,tailwind,bootstrap" />
</p>

### Backend & Databases
<p>
  <img src="https://skillicons.dev/icons?i=django,sqlite,postgres" />
</p>

### Tools & DevOps
<p>
  <img src="https://skillicons.dev/icons?i=git,github,vscode,npm" />
</p>

---

## 🤖 AI / ML Expertise

| Domain | Proficiency | Details |
|---|---|---|
| Machine Learning | ✅ Applied | Scikit-Learn based application development |
| Crop Recommendation | ✅ Applied | Random Forest based recommendation workflow |
| Yield Prediction | ✅ Applied | ML-powered agricultural yield estimation |
| Data-Driven Applications | ✅ Applied | Integrating ML models into full-stack applications |
| ML Inference | ✅ Applied | Application-level model training and prediction workflows |

---

# 🚀 Featured Projects

## 🌾 AgroSense — Smart Agriculture Assistant Platform
A full-stack decision-support platform built around agricultural workflows.

### Technologies
\`Python\` \`Django\` \`Django REST Framework\` \`React\` \`Vite\` \`Tailwind CSS\` \`Scikit-Learn\`

### Key Features
- 🌾 Crop recommendation
- 📈 Yield prediction
- 🤖 Random Forest ML models
- 🔐 JWT authentication
- 👨‍🌾 Farmer role
- 👨‍💼 Agriculture Officer role
- 🛡️ Admin role
- 📰 Agricultural news
- 📊 Market prices
- 📜 Government schemes
- 📈 Analytics dashboards
- 📄 PDF yield certificates
- 🕷️ Web scraping

🔗 **Repository**: https://github.com/hetdhameliya09/Smart-Agriculture-Assistant-Platform

---

## 🏢 VendorBridge — Procurement & Supplier Relationship Management
A Django-based ERP/SRM application covering vendor onboarding, RFQs, quotation management, approvals, purchase orders, invoices and analytics.

### Technologies
\`Python\` \`Django\` \`Bootstrap 5\` \`Chart.js\` \`SQLite\`

### Key Features
- 👥 Vendor management
- 📝 Vendor onboarding
- 📋 RFQ creation
- 📑 Quotation management
- ⚖️ Quotation comparison
- 🛡️ Approval workflows
- 📦 Purchase orders
- 🧾 Supplier invoices
- 📄 PDF invoice generation
- 📊 Analytics dashboard

🔗 **Repository**: https://github.com/hetdhameliya09/VendorBridge

---

## ⚛️ SEM IV FSD-II
Full-stack development coursework and practical implementations using React/Vite.

### Topics
- React components
- Props & State
- Events & Handlers
- Routing
- JavaScript ES6+
- Vite Toolchain
- Frontend Architecture

🔗 **Repository**: https://github.com/hetdhameliya09/SEM_IV_FSD-II

---

# 💼 Experience & Projects

## Software Engineering & Full-Stack Development Projects
Building and experimenting with full-stack applications through academic and independent software projects.

### Core Capabilities
- Design and develop Django applications
- Build React/Vite frontend interfaces
- Develop REST APIs with DRF
- Implement JWT authentication & Role-Based Access Control
- Integrate machine-learning models into web pipelines
- Build analytics dashboards
- Develop web-scraping utilities
- Work with relational databases (PostgreSQL, SQLite)

---

# 🏆 Achievements

| Recognition | Details |
|---|---|
| Full-Stack Projects | Built multiple end-to-end applications spanning frontend, backend, databases and workflows. |
| AI/ML Integration | Integrated machine-learning models into an agricultural decision-support application. |
| Enterprise Workflow Engineering | Developed procurement workflows covering vendors, RFQs, quotations, approvals, purchase orders and invoices. |
| Modern Web Development | Worked with Django, DRF, React/Vite, Tailwind CSS, Bootstrap and Chart.js. |

---

# 📊 GitHub Analytics

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=hetdhameliya09&show_icons=true&theme=tokyonight&hide_border=true&bg_color=0D1117&title_color=8B5CF6&icon_color=6366F1&text_color=C4B5FD" height="180"/>
  <img src="https://github-readme-streak-stats.herokuapp.com/?user=hetdhameliya09&theme=tokyonight&hide_border=true&background=0D1117&ring=8B5CF6&fire=6366F1&currStreakLabel=C4B5FD" height="180"/>
</p>

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=hetdhameliya09&layout=compact&theme=tokyonight&hide_border=true&bg_color=0D1117&title_color=8B5CF6&text_color=C4B5FD" height="180"/>
</p>

---

# 🏆 GitHub Trophies

<p align="center">
  <img src="https://github-profile-trophy.vercel.app/?username=hetdhameliya09&theme=discord&no-frame=true&no-bg=true&margin-w=8&column=7"/>
</p>

---

# 📈 Contribution Activity

<p align="center">
  <img src="https://github-readme-activity-graph.vercel.app/graph?username=hetdhameliya09&bg_color=0D1117&color=C4B5FD&line=8B5CF6&point=6366F1&area=true&hide_border=true" width="100%"/>
</p>

---

# 🐍 Contribution Snake

<p align="center">
  <img src="https://raw.githubusercontent.com/hetdhameliya09/hetdhameliya09/output/github-contribution-grid-snake.svg" alt="GitHub Contribution Snake"/>
</p>

---

# 🎯 Current Focus

\`\`\`yaml
Learning:
  - Advanced Full-Stack Engineering
  - Backend Architecture
  - AI/ML Application Development
  - Modern React Development

Building:
  - Full-Stack Django Applications
  - Enterprise Workflow Systems
  - AI-Powered Decision Support Applications

Exploring:
  - Machine Learning Integration
  - Data-Driven Products
  - Scalable Web Application Architecture

Open To:
  - Software Engineering Projects
  - Full-Stack Development Opportunities
  - AI/ML Application Projects
  - Open Source Collaboration
\`\`\``;

    // Toast Function
    function showToast(message) {
      const toast = document.getElementById('toast');
      const toastMsg = document.getElementById('toast-msg');
      toastMsg.innerText = message;
      toast.classList.add('show');
      setTimeout(() => {
        toast.classList.remove('show');
      }, 3000);
    }

    // Typing Effect
    const words = [
      "Full-Stack Developer",
      "Django & React Specialist",
      "AI/ML Project Builder",
      "Enterprise System Architect",
      "Crafting Practical Digital Solutions"
    ];
    let i = 0;
    let timer;

    function typingEffect() {
      let word = words[i].split("");
      var loopTyping = function() {
        if (word.length > 0) {
          document.getElementById('typing-text').innerHTML += word.shift();
        } else {
          setTimeout(deletingEffect, 2000);
          return false;
        }
        timer = setTimeout(loopTyping, 75);
      };
      loopTyping();
    }

    function deletingEffect() {
      let word = words[i].split("");
      var loopDeleting = function() {
        if (word.length > 0) {
          word.pop();
          document.getElementById('typing-text').innerHTML = word.join("");
        } else {
          if (words.length > (i + 1)) {
            i++;
          } else {
            i = 0;
          }
          setTimeout(typingEffect, 400);
          return false;
        }
        timer = setTimeout(loopDeleting, 35);
      };
      loopDeleting();
    }
    typingEffect();

    // Ambient Canvas Particle Constellations
    const canvas = document.getElementById('ambient-canvas');
    const ctx = canvas.getContext('2d');
    let width, height;
    let particles = [];

    function resizeCanvas() {
      width = canvas.width = window.innerWidth;
      height = canvas.height = window.innerHeight;
    }
    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    class Particle {
      constructor() {
        this.x = Math.random() * width;
        this.y = Math.random() * height;
        this.vx = (Math.random() - 0.5) * 0.6;
        this.vy = (Math.random() - 0.5) * 0.6;
        this.radius = Math.random() * 1.8 + 0.5;
        this.color = Math.random() > 0.5 ? 'rgba(139, 92, 246, ' : 'rgba(99, 102, 241, ';
        this.alpha = Math.random() * 0.5 + 0.2;
      }
      update() {
        this.x += this.vx;
        this.y += this.vy;
        if (this.x < 0 || this.x > width) this.vx *= -1;
        if (this.y < 0 || this.y > height) this.vy *= -1;
      }
      draw() {
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2);
        ctx.fillStyle = this.color + this.alpha + ')';
        ctx.fill();
      }
    }

    for (let j = 0; j < 55; j++) {
      particles.push(new Particle());
    }

    function animateParticles() {
      ctx.clearRect(0, 0, width, height);
      for (let a = 0; a < particles.length; a++) {
        particles[a].update();
        particles[a].draw();
        for (let b = a + 1; b < particles.length; b++) {
          let dist = Math.hypot(particles[a].x - particles[b].x, particles[a].y - particles[b].y);
          if (dist < 120) {
            ctx.beginPath();
            ctx.moveTo(particles[a].x, particles[a].y);
            ctx.lineTo(particles[b].x, particles[b].y);
            ctx.strokeStyle = 'rgba(139, 92, 246, ' + (0.15 * (1 - dist / 120)) + ')';
            ctx.lineWidth = 0.6;
            ctx.stroke();
          }
        }
      }
      requestAnimationFrame(animateParticles);
    }
    animateParticles();

    // Cursor Spotlight
    const spotlight = document.getElementById('cursor-spotlight');
    window.addEventListener('mousemove', (e) => {
      spotlight.style.left = e.clientX + 'px';
      spotlight.style.top = e.clientY + 'px';
    });

    // Terminal Tabs Switcher
    const tabContents = {
      bio: `{
  <span class="json-key">"name"</span>: <span class="json-str">"Het N Dhameliya"</span>,
  <span class="json-key">"role"</span>: <span class="json-str">"Full-Stack Developer &amp; AI/ML Project Builder"</span>,
  <span class="json-key">"focus"</span>: <span class="json-str">"Backend systems, modern frontend UI/UX, and data-driven intelligence"</span>,
  <span class="json-key">"stack_highlights"</span>: [
    <span class="json-arr">"Django"</span>, <span class="json-arr">"Django REST Framework"</span>, <span class="json-arr">"React"</span>, <span class="json-arr">"Vite"</span>, <span class="json-arr">"Python"</span>, <span class="json-arr">"Scikit-Learn"</span>, <span class="json-arr">"Tailwind CSS"</span>
  ],
  <span class="json-key">"philosophy"</span>: <span class="json-str">"Turning real-world enterprise &amp; agricultural workflows into robust, usable digital products."</span>
}`,
      skills: `<span style="color:#f59e0b;"># Stack Configuration</span>
[Languages]
Python = "3.x (Advanced Backend & ML)"
JavaScript = "ES6+, Modern React Ecosystem"
HTML5_CSS3 = "Semantic, Responsive, Modern Web Standards"

[Frameworks]
Backend = "Django, Django REST Framework"
Frontend = "React, Vite, Tailwind CSS, Bootstrap 5"
Data_ML = "Scikit-Learn, Random Forest Classifier/Regressor"
Databases = "PostgreSQL, SQLite"`,
      goals: `<span style="color:#06b6d4;"># Developer Mission</span>
objective: "Build high-impact digital systems combining resilient backend services with sleek user interfaces."
open_roles:
  - "Full-Stack Software Engineer"
  - "Python & Django Backend Developer"
  - "React Frontend Engineer"
  - "AI/ML Solutions Builder"`
    };

    function switchTermTab(tabKey) {
      document.querySelectorAll('.t-tab-btn').forEach(btn => btn.classList.remove('active'));
      event.target.classList.add('active');
      document.getElementById('term-content').innerHTML = tabContents[tabKey];
    }

    // Modal Markdown Management
    const readmeModal = document.getElementById('readme-modal');
    const openReadmeBtn = document.getElementById('open-readme-btn');
    const closeModalBtn = document.getElementById('close-modal-btn');
    const closeModalBtn2 = document.getElementById('modal-close-btn2');
    const copyModalMdBtn = document.getElementById('copy-modal-md-btn');
    const quickCopyBtn = document.getElementById('quick-copy-md');
    const rawMarkdownContent = document.getElementById('raw-markdown-content');
    const copyContactBtn = document.getElementById('copy-contact-btn');

    rawMarkdownContent.textContent = CLEAN_MARKDOWN;

    function openModal() {
      readmeModal.classList.add('active');
    }
    function closeModal() {
      readmeModal.classList.remove('active');
    }

    openReadmeBtn.addEventListener('click', openModal);
    closeModalBtn.addEventListener('click', closeModal);
    closeModalBtn2.addEventListener('click', closeModal);
    readmeModal.addEventListener('click', (e) => {
      if (e.target === readmeModal) closeModal();
    });

    // Copy to Clipboard actions
    function copyMarkdown() {
      navigator.clipboard.writeText(CLEAN_MARKDOWN).then(() => {
        showToast('✨ Clean GitHub Markdown copied to clipboard!');
      });
    }

    copyModalMdBtn.addEventListener('click', copyMarkdown);
    quickCopyBtn.addEventListener('click', copyMarkdown);

    copyContactBtn.addEventListener('click', () => {
      navigator.clipboard.writeText('https://github.com/hetdhameliya09').then(() => {
        showToast('🔗 GitHub profile link copied!');
      });
    });

    // 3D Card Hover Tilt Effect
    document.querySelectorAll('.project-card, .stack-category-card').forEach(card => {
      card.addEventListener('mousemove', (e) => {
        const rect = card.getBoundingClientRect();
        const x = e.clientX - rect.left - rect.width / 2;
        const y = e.clientY - rect.top - rect.height / 2;
        card.style.transform = `perspective(1000px) rotateX(${-y * 0.03}deg) rotateY(${x * 0.03}deg) translateY(-6px)`;
      });
      card.addEventListener('mouseleave', () => {
        card.style.transform = 'perspective(1000px) rotateX(0) rotateY(0) translateY(0)';
      });
    });
  </script>
</body>
</html>
'''

target_path = r"c:\Users\Het\OneDrive\Desktop\git.html"
with open(target_path, "w", encoding="utf-8") as f:
    f.write(html_content)

print(f"Successfully generated extraordinary portfolio & GitHub profile at {target_path}")

