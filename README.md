<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ahsanul Habib Safin — Developer · Creator · AI Builder</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Caveat:wght@400;500;600;700&family=Instrument+Serif:ital@0;1&family=DM+Mono:wght@300;400;500&family=Bebas+Neue&display=swap" rel="stylesheet">
<style>
  :root {
    --cream: #F5F0E8;
    --cream-dark: #EDE5D4;
    --ink: #1A1209;
    --ink-light: #3D2F1A;
    --rust: #C44B2B;
    --rust-light: #E8673F;
    --gold: #D4A017;
    --sage: #4A6741;
    --blue-ink: #2B4A8C;
    --paper: #FAF7F0;
    --shadow: rgba(26,18,9,0.12);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--cream);
    color: var(--ink);
    font-family: 'DM Mono', monospace;
    overflow-x: hidden;
    cursor: none;
  }

  /* CUSTOM CURSOR */
  .cursor {
    width: 12px; height: 12px;
    background: var(--rust);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9999;
    transition: transform 0.15s ease;
    mix-blend-mode: multiply;
  }
  .cursor-trail {
    width: 32px; height: 32px;
    border: 2px solid var(--rust);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9998;
    transition: all 0.35s cubic-bezier(0.25, 0.46, 0.45, 0.94);
    opacity: 0.5;
  }

  /* NOISE TEXTURE OVERLAY */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none; z-index: 9997;
    opacity: 0.6;
  }

  /* NAV */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    padding: 20px 48px;
    display: flex; align-items: center; justify-content: space-between;
    background: transparent;
    transition: background 0.4s;
  }
  nav.scrolled {
    background: rgba(245, 240, 232, 0.95);
    backdrop-filter: blur(8px);
    border-bottom: 1.5px dashed rgba(26,18,9,0.15);
  }
  .nav-logo {
    font-family: 'Caveat', cursive;
    font-size: 22px; font-weight: 700;
    color: var(--ink);
    text-decoration: none;
    letter-spacing: 0.02em;
  }
  .nav-logo span { color: var(--rust); }
  .nav-links {
    display: flex; gap: 32px; list-style: none;
  }
  .nav-links a {
    font-family: 'DM Mono', monospace;
    font-size: 11px; font-weight: 500;
    color: var(--ink-light); text-decoration: none;
    letter-spacing: 0.12em; text-transform: uppercase;
    position: relative;
    transition: color 0.2s;
  }
  .nav-links a::after {
    content: '';
    position: absolute; bottom: -3px; left: 0; right: 0;
    height: 1.5px; background: var(--rust);
    transform: scaleX(0); transition: transform 0.25s;
    transform-origin: left;
  }
  .nav-links a:hover { color: var(--rust); }
  .nav-links a:hover::after { transform: scaleX(1); }

  /* HERO */
  .hero {
    min-height: 100vh;
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 120px 48px 80px;
    position: relative;
    overflow: hidden;
    align-items: center;
    gap: 60px;
  }

  /* BIG ruled lines behind hero */
  .hero::before {
    content: '';
    position: absolute; left: 0; right: 0; top: 0; bottom: 0;
    background-image: repeating-linear-gradient(
      transparent,
      transparent 47px,
      rgba(26,18,9,0.06) 47px,
      rgba(26,18,9,0.06) 48px
    );
    pointer-events: none;
  }

  /* Red margin line */
  .hero::after {
    content: '';
    position: absolute; left: 120px; top: 0; bottom: 0;
    width: 2px;
    background: rgba(196,75,43,0.25);
    pointer-events: none;
  }

  .hero-text { position: relative; z-index: 2; }

  .hero-label {
    font-family: 'DM Mono', monospace;
    font-size: 11px; letter-spacing: 0.2em;
    text-transform: uppercase; color: var(--rust);
    margin-bottom: 20px;
    display: flex; align-items: center; gap: 12px;
    opacity: 0; animation: fadeUp 0.6s 0.2s forwards;
  }
  .hero-label::before {
    content: '';
    display: inline-block; width: 32px; height: 1.5px;
    background: var(--rust);
  }

  .hero-headline {
    font-family: 'Instrument Serif', serif;
    font-size: clamp(42px, 5vw, 72px);
    line-height: 1.08;
    font-weight: 400;
    color: var(--ink);
    margin-bottom: 20px;
    opacity: 0; animation: fadeUp 0.7s 0.35s forwards;
  }
  .hero-headline em {
    font-style: italic; color: var(--rust);
  }

  .hero-sub {
    font-family: 'Caveat', cursive;
    font-size: 22px; font-weight: 500;
    color: var(--ink-light);
    margin-bottom: 48px;
    line-height: 1.5;
    opacity: 0; animation: fadeUp 0.7s 0.5s forwards;
  }
  .hero-sub strong { color: var(--rust); }

  .hero-btns {
    display: flex; gap: 16px; flex-wrap: wrap;
    opacity: 0; animation: fadeUp 0.7s 0.65s forwards;
  }

  .btn {
    font-family: 'DM Mono', monospace;
    font-size: 12px; font-weight: 500;
    letter-spacing: 0.1em; text-transform: uppercase;
    padding: 14px 32px;
    border: 2px solid var(--ink);
    text-decoration: none;
    position: relative;
    transition: all 0.25s;
    display: inline-block;
    cursor: none;
  }
  .btn::after {
    content: '';
    position: absolute; inset: 3px 3px -3px -3px;
    border: 2px solid var(--ink);
    transition: all 0.2s;
  }
  .btn:hover { transform: translate(-2px, -2px); }
  .btn:hover::after { inset: 5px 5px -5px -5px; }

  .btn-primary {
    background: var(--ink); color: var(--cream);
  }
  .btn-primary::after { border-color: var(--rust); }
  .btn-primary:hover { background: var(--rust); border-color: var(--rust); }

  .btn-secondary {
    background: transparent; color: var(--ink);
  }
  .btn-secondary:hover { background: var(--ink); color: var(--cream); }

  /* HERO ILLUSTRATION */
  .hero-illustration {
    position: relative; z-index: 2;
    display: flex; justify-content: center; align-items: center;
    opacity: 0; animation: fadeIn 1s 0.5s forwards;
  }

  .notebook-card {
    width: 340px; height: 420px;
    background: var(--paper);
    border: 2px solid var(--ink);
    position: relative;
    box-shadow: 8px 8px 0 var(--ink);
    padding: 40px 36px 36px;
    transform: rotate(2deg);
  }
  .notebook-card::before {
    content: '';
    position: absolute; left: 44px; top: 0; bottom: 0;
    width: 2px; background: rgba(196,75,43,0.3);
  }
  .notebook-holes {
    position: absolute; left: 20px; top: 0; bottom: 0;
    display: flex; flex-direction: column;
    justify-content: space-evenly; align-items: center;
    padding: 20px 0;
  }
  .hole {
    width: 12px; height: 12px;
    border-radius: 50%;
    border: 2px solid var(--ink);
    background: var(--cream);
  }
  .nc-label {
    font-family: 'DM Mono', monospace;
    font-size: 9px; letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--rust); margin-bottom: 20px;
  }
  .nc-title {
    font-family: 'Caveat', cursive;
    font-size: 28px; font-weight: 700;
    color: var(--ink); line-height: 1.2; margin-bottom: 24px;
  }
  .nc-list {
    list-style: none;
    display: flex; flex-direction: column; gap: 10px;
  }
  .nc-list li {
    font-family: 'Caveat', cursive;
    font-size: 18px; color: var(--ink-light);
    display: flex; align-items: center; gap: 10px;
    padding-bottom: 10px;
    border-bottom: 1.5px solid rgba(26,18,9,0.1);
  }
  .nc-list li::before {
    content: '→'; color: var(--rust); font-family: 'DM Mono', monospace;
    font-size: 13px;
  }
  .nc-stamp {
    position: absolute; bottom: 30px; right: 30px;
    width: 68px; height: 68px;
    border: 3px solid var(--rust);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    text-align: center;
    transform: rotate(-12deg);
  }
  .nc-stamp span {
    font-family: 'Caveat', cursive;
    font-size: 10px; font-weight: 700;
    color: var(--rust); line-height: 1.2;
    text-transform: uppercase;
  }

  /* DOODLES */
  .doodle {
    position: absolute; pointer-events: none;
    opacity: 0; animation: fadeIn 0.8s forwards;
  }

  /* SECTION BASE */
  section {
    padding: 100px 48px;
    position: relative;
  }
  .section-inner { max-width: 1100px; margin: 0 auto; }

  .section-label {
    font-family: 'DM Mono', monospace;
    font-size: 10px; letter-spacing: 0.25em; text-transform: uppercase;
    color: var(--rust);
    display: flex; align-items: center; gap: 14px;
    margin-bottom: 16px;
  }
  .section-label::before {
    content: '';
    width: 24px; height: 1.5px; background: var(--rust);
  }

  .section-title {
    font-family: 'Instrument Serif', serif;
    font-size: clamp(38px, 4.5vw, 62px);
    font-weight: 400; line-height: 1.05;
    color: var(--ink);
    margin-bottom: 16px;
  }
  .section-title em { font-style: italic; color: var(--rust); }

  .section-desc {
    font-family: 'Caveat', cursive;
    font-size: 19px; color: var(--ink-light);
    line-height: 1.65; max-width: 520px;
    margin-bottom: 64px;
  }

  /* PROJECTS */
  .projects-section { background: var(--ink); }
  .projects-section .section-label { color: var(--rust-light); }
  .projects-section .section-label::before { background: var(--rust-light); }
  .projects-section .section-title { color: var(--cream); }
  .projects-section .section-desc { color: rgba(245,240,232,0.6); }

  .projects-section::before {
    content: '';
    position: absolute; left: 0; right: 0; top: 0; bottom: 0;
    background-image: repeating-linear-gradient(
      transparent, transparent 47px,
      rgba(245,240,232,0.04) 47px, rgba(245,240,232,0.04) 48px
    );
    pointer-events: none;
  }

  .project-featured {
    border: 2px solid rgba(245,240,232,0.2);
    padding: 52px;
    position: relative;
    margin-bottom: 32px;
    overflow: hidden;
    transition: border-color 0.3s;
  }
  .project-featured:hover { border-color: var(--rust-light); }

  .project-featured::before {
    content: '★ FEATURED';
    position: absolute; top: 20px; right: 20px;
    font-family: 'DM Mono', monospace;
    font-size: 9px; letter-spacing: 0.2em;
    color: var(--gold); border: 1px solid var(--gold);
    padding: 4px 10px;
  }

  .project-number {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 100px; color: rgba(245,240,232,0.04);
    position: absolute; top: -10px; right: 40px;
    line-height: 1; pointer-events: none;
  }

  .project-tag {
    font-family: 'DM Mono', monospace;
    font-size: 10px; letter-spacing: 0.15em; text-transform: uppercase;
    color: var(--sage); background: rgba(74,103,65,0.15);
    border: 1px solid rgba(74,103,65,0.3);
    padding: 4px 12px; display: inline-block; margin-bottom: 20px;
  }

  .project-name {
    font-family: 'Instrument Serif', serif;
    font-size: clamp(28px, 3vw, 42px); font-weight: 400;
    color: var(--cream); margin-bottom: 16px; line-height: 1.1;
  }
  .project-name em { font-style: italic; color: var(--rust-light); }

  .project-desc {
    font-family: 'Caveat', cursive;
    font-size: 18px; color: rgba(245,240,232,0.65);
    line-height: 1.7; max-width: 600px; margin-bottom: 32px;
  }

  .project-features {
    display: flex; gap: 24px; flex-wrap: wrap; margin-bottom: 36px;
  }
  .project-feature {
    font-family: 'DM Mono', monospace;
    font-size: 11px; color: rgba(245,240,232,0.5);
    display: flex; align-items: center; gap: 8px;
  }
  .project-feature::before {
    content: '◆'; font-size: 6px; color: var(--rust-light);
  }

  .project-link {
    font-family: 'DM Mono', monospace;
    font-size: 11px; letter-spacing: 0.1em; text-transform: uppercase;
    color: var(--cream); border-bottom: 1.5px solid var(--rust-light);
    text-decoration: none; padding-bottom: 2px;
    transition: color 0.2s;
  }
  .project-link:hover { color: var(--rust-light); }

  .projects-wip {
    border: 1.5px dashed rgba(245,240,232,0.15);
    padding: 32px 52px;
    display: flex; align-items: center; gap: 24px;
    color: rgba(245,240,232,0.35);
    font-family: 'Caveat', cursive; font-size: 18px;
  }
  .wip-dot {
    width: 8px; height: 8px; border-radius: 50%;
    background: var(--gold); animation: blink 2s infinite;
    flex-shrink: 0;
  }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0.2} }

  /* LAB */
  .lab-section { background: var(--cream-dark); }

  .lab-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 0;
    border: 2px solid var(--ink);
    margin-top: 20px;
  }

  .lab-item {
    padding: 36px 28px;
    border-right: 1.5px solid rgba(26,18,9,0.12);
    border-bottom: 1.5px solid rgba(26,18,9,0.12);
    position: relative;
    transition: background 0.25s;
    cursor: none;
  }
  .lab-item:hover { background: rgba(196,75,43,0.06); }
  .lab-item:last-child { border-right: none; }

  .lab-icon {
    font-size: 32px; margin-bottom: 16px; display: block;
  }
  .lab-item-title {
    font-family: 'Instrument Serif', serif;
    font-size: 20px; font-weight: 400; color: var(--ink);
    margin-bottom: 8px;
  }
  .lab-item-desc {
    font-family: 'Caveat', cursive;
    font-size: 16px; color: var(--ink-light);
    line-height: 1.6;
  }

  .lab-philosophy {
    margin-top: 52px;
    padding: 40px 48px;
    border: 2px solid var(--ink);
    background: var(--paper);
    position: relative;
    box-shadow: 5px 5px 0 rgba(26,18,9,0.12);
    display: flex; align-items: center; gap: 40px;
  }
  .lab-philosophy::before {
    content: '"';
    font-family: 'Instrument Serif', serif;
    font-size: 120px; color: rgba(196,75,43,0.12);
    position: absolute; top: -20px; left: 20px;
    line-height: 1; pointer-events: none;
  }
  .lab-philosophy-text {
    font-family: 'Instrument Serif', serif;
    font-size: 24px; font-style: italic;
    color: var(--ink); line-height: 1.5;
  }
  .lab-philosophy-note {
    font-family: 'DM Mono', monospace;
    font-size: 10px; color: var(--rust); letter-spacing: 0.1em;
    text-transform: uppercase; margin-top: 12px;
  }

  /* WRITING */
  .writing-section { background: var(--paper); }

  .writing-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 24px; margin-top: 20px;
  }

  .writing-card {
    border: 1.5px solid rgba(26,18,9,0.15);
    padding: 36px 32px;
    background: var(--cream);
    position: relative;
    transition: transform 0.2s, box-shadow 0.2s;
    cursor: none;
  }
  .writing-card:hover {
    transform: translate(-3px, -3px);
    box-shadow: 6px 6px 0 rgba(26,18,9,0.15);
  }

  .writing-topic {
    font-family: 'DM Mono', monospace;
    font-size: 9px; letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--rust); margin-bottom: 16px;
  }
  .writing-title {
    font-family: 'Instrument Serif', serif;
    font-size: 22px; font-weight: 400; color: var(--ink);
    line-height: 1.3; margin-bottom: 12px;
  }
  .writing-excerpt {
    font-family: 'Caveat', cursive;
    font-size: 16px; color: var(--ink-light);
    line-height: 1.65;
  }
  .writing-card-num {
    position: absolute; bottom: 20px; right: 24px;
    font-family: 'Bebas Neue', sans-serif;
    font-size: 48px; color: rgba(26,18,9,0.05);
    line-height: 1;
  }

  /* ABOUT */
  .about-section { background: var(--cream); }

  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1.2fr;
    gap: 80px; align-items: start; margin-top: 20px;
  }

  .about-portrait {
    position: relative;
  }
  .portrait-frame {
    width: 100%; aspect-ratio: 4/5;
    border: 2px solid var(--ink);
    background: var(--cream-dark);
    position: relative;
    box-shadow: 10px 10px 0 var(--ink);
    overflow: hidden;
    display: flex; align-items: center; justify-content: center;
  }
  .portrait-placeholder {
    font-family: 'Caveat', cursive;
    font-size: 18px; color: rgba(26,18,9,0.3);
    text-align: center; padding: 20px;
  }

  /* Hand-drawn portrait SVG */
  .portrait-frame svg {
    width: 100%; height: 100%;
  }

  .portrait-caption {
    font-family: 'Caveat', cursive;
    font-size: 15px; color: var(--ink-light);
    text-align: center; margin-top: 12px;
  }
  .portrait-sticker {
    position: absolute; top: -16px; right: -16px;
    width: 64px; height: 64px;
    background: var(--rust); color: var(--cream);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-family: 'Caveat', cursive; font-size: 11px;
    font-weight: 700; text-align: center;
    text-transform: uppercase; line-height: 1.2;
    transform: rotate(15deg);
    border: 2px solid var(--ink);
  }

  .about-content .bio-text {
    font-family: 'Instrument Serif', serif;
    font-size: 22px; line-height: 1.75;
    color: var(--ink); margin-bottom: 40px;
  }
  .about-content .bio-text em { font-style: italic; color: var(--rust); }

  .about-pillars {
    display: grid; grid-template-columns: repeat(3, 1fr);
    gap: 16px; margin-bottom: 48px;
  }
  .pillar {
    padding: 24px 20px;
    border: 1.5px solid rgba(26,18,9,0.15);
    text-align: center;
    background: var(--paper);
  }
  .pillar-icon { font-size: 24px; margin-bottom: 8px; }
  .pillar-name {
    font-family: 'Caveat', cursive;
    font-size: 16px; font-weight: 700; color: var(--ink);
  }

  .about-quote {
    border-left: 3px solid var(--rust);
    padding: 20px 28px;
    background: rgba(196,75,43,0.04);
    font-family: 'Instrument Serif', serif;
    font-size: 19px; font-style: italic;
    color: var(--ink); line-height: 1.6;
  }

  /* SKILLS */
  .skills-section { background: var(--cream-dark); }

  .skills-track-wrapper {
    overflow: hidden; margin-top: 20px;
    border-top: 1.5px solid rgba(26,18,9,0.12);
    border-bottom: 1.5px solid rgba(26,18,9,0.12);
    padding: 20px 0;
    margin-bottom: 60px;
  }
  .skills-track {
    display: flex; gap: 0;
    animation: scroll-left 20s linear infinite;
    width: max-content;
  }
  @keyframes scroll-left {
    0% { transform: translateX(0); }
    100% { transform: translateX(-50%); }
  }
  .skill-pill {
    font-family: 'Caveat', cursive;
    font-size: 22px; font-weight: 700;
    color: var(--ink); padding: 0 36px;
    border-right: 2px solid rgba(26,18,9,0.12);
    white-space: nowrap;
    display: flex; align-items: center; gap: 12px;
  }
  .skill-pill::before { content: '✦'; font-size: 10px; color: var(--rust); }

  .skills-grid {
    display: grid; grid-template-columns: repeat(5, 1fr); gap: 16px;
  }
  .skill-card {
    padding: 32px 24px;
    border: 1.5px solid rgba(26,18,9,0.12);
    background: var(--paper);
    text-align: center;
    position: relative;
    transition: transform 0.2s, box-shadow 0.2s;
    cursor: none;
  }
  .skill-card:hover {
    transform: translate(-2px,-2px);
    box-shadow: 4px 4px 0 rgba(26,18,9,0.15);
    border-color: var(--rust);
  }
  .skill-card-icon { font-size: 28px; margin-bottom: 12px; }
  .skill-card-name {
    font-family: 'DM Mono', monospace;
    font-size: 11px; letter-spacing: 0.1em; text-transform: uppercase;
    color: var(--ink);
  }

  /* VISION */
  .vision-section {
    background: var(--ink);
    padding: 120px 48px;
    text-align: center;
    position: relative;
    overflow: hidden;
  }
  .vision-section::before {
    content: '';
    position: absolute; inset: 0;
    background-image: repeating-linear-gradient(
      90deg,
      transparent, transparent 119px,
      rgba(245,240,232,0.03) 119px, rgba(245,240,232,0.03) 120px
    ), repeating-linear-gradient(
      transparent, transparent 47px,
      rgba(245,240,232,0.03) 47px, rgba(245,240,232,0.03) 48px
    );
    pointer-events: none;
  }

  .vision-eyebrow {
    font-family: 'DM Mono', monospace;
    font-size: 10px; letter-spacing: 0.25em; text-transform: uppercase;
    color: var(--gold); margin-bottom: 28px;
    display: flex; align-items: center; justify-content: center; gap: 16px;
  }
  .vision-eyebrow::before, .vision-eyebrow::after {
    content: ''; width: 40px; height: 1px; background: var(--gold);
  }

  .vision-headline {
    font-family: 'Instrument Serif', serif;
    font-size: clamp(32px, 4vw, 56px);
    font-weight: 400; color: var(--cream);
    line-height: 1.15; margin-bottom: 28px;
  }
  .vision-headline em { font-style: italic; color: var(--rust-light); }

  .vision-words {
    display: flex; justify-content: center; gap: 0; flex-wrap: wrap;
    margin: 48px 0;
  }
  .vision-word {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(48px, 7vw, 96px);
    color: rgba(245,240,232,0.08);
    padding: 0 20px; line-height: 1;
    transition: color 0.3s;
    cursor: none;
  }
  .vision-word:hover { color: rgba(245,240,232,0.25); }
  .vision-word.accent { color: rgba(196,75,43,0.4); }

  /* CONNECT */
  .connect-section { background: var(--cream); }

  .connect-grid {
    display: grid; grid-template-columns: 1fr 1fr; gap: 60px;
    margin-top: 20px; align-items: start;
  }

  .connect-text .big-email {
    font-family: 'Instrument Serif', serif;
    font-size: clamp(22px, 2.5vw, 36px);
    color: var(--ink); margin-bottom: 24px;
    line-height: 1.4; font-style: italic;
  }

  .connect-links {
    display: flex; flex-direction: column; gap: 0;
    border: 1.5px solid rgba(26,18,9,0.12);
  }
  .connect-link-item {
    display: flex; align-items: center; justify-content: space-between;
    padding: 24px 28px;
    border-bottom: 1.5px solid rgba(26,18,9,0.08);
    text-decoration: none;
    transition: background 0.2s;
    cursor: none;
  }
  .connect-link-item:last-child { border-bottom: none; }
  .connect-link-item:hover { background: rgba(196,75,43,0.05); }
  .connect-link-left {
    display: flex; align-items: center; gap: 16px;
  }
  .connect-link-icon { font-size: 20px; }
  .connect-link-name {
    font-family: 'Instrument Serif', serif;
    font-size: 20px; color: var(--ink);
  }
  .connect-link-sub {
    font-family: 'DM Mono', monospace;
    font-size: 10px; text-transform: uppercase;
    letter-spacing: 0.1em; color: var(--ink-light);
  }
  .connect-link-arrow {
    font-family: 'DM Mono', monospace;
    font-size: 18px; color: var(--rust);
    transition: transform 0.2s;
  }
  .connect-link-item:hover .connect-link-arrow { transform: translateX(6px); }

  .connect-handwritten {
    padding: 40px 36px;
    background: var(--paper);
    border: 2px solid var(--ink);
    box-shadow: 6px 6px 0 rgba(26,18,9,0.1);
    position: relative;
  }
  .connect-handwritten::before {
    content: '';
    position: absolute; left: 0; right: 0; top: 0; bottom: 0;
    background-image: repeating-linear-gradient(
      transparent, transparent 31px,
      rgba(26,18,9,0.06) 31px, rgba(26,18,9,0.06) 32px
    );
    pointer-events: none;
  }
  .connect-handwritten-text {
    font-family: 'Caveat', cursive;
    font-size: 19px; line-height: 2.12;
    color: var(--ink); position: relative; z-index: 1;
  }
  .connect-handwritten-sig {
    font-family: 'Caveat', cursive;
    font-size: 32px; font-weight: 700;
    color: var(--ink); margin-top: 24px;
    position: relative; z-index: 1;
    padding-top: 16px;
    border-top: 1.5px solid rgba(26,18,9,0.12);
  }

  /* FOOTER / SIGNATURE LINE */
  footer {
    background: var(--ink);
    padding: 40px 48px;
    display: flex; align-items: center; justify-content: space-between;
    flex-wrap: wrap; gap: 20px;
  }
  .footer-sig {
    font-family: 'Instrument Serif', serif;
    font-size: 20px; font-style: italic;
    color: var(--cream);
  }
  .footer-sig strong { font-style: normal; color: var(--rust-light); }

  .footer-copy {
    font-family: 'DM Mono', monospace;
    font-size: 10px; letter-spacing: 0.12em; text-transform: uppercase;
    color: rgba(245,240,232,0.3);
  }

  /* DIVIDER */
  .section-divider {
    text-align: center; padding: 20px 0;
    position: relative;
  }
  .section-divider span {
    font-family: 'Caveat', cursive;
    font-size: 15px; color: rgba(26,18,9,0.25);
    position: relative; z-index: 1;
    background: inherit; padding: 0 20px;
  }
  .section-divider::before {
    content: '';
    position: absolute; left: 48px; right: 48px;
    top: 50%; height: 1px;
    background: rgba(26,18,9,0.1);
  }

  /* SCROLL INDICATOR */
  .scroll-indicator {
    position: absolute; bottom: 40px; left: 50%; transform: translateX(-50%);
    display: flex; flex-direction: column; align-items: center; gap: 8px;
    opacity: 0; animation: fadeIn 0.8s 1.2s forwards;
  }
  .scroll-indicator span {
    font-family: 'DM Mono', monospace;
    font-size: 9px; letter-spacing: 0.2em; text-transform: uppercase;
    color: rgba(26,18,9,0.35);
  }
  .scroll-line {
    width: 1px; height: 40px;
    background: linear-gradient(to bottom, var(--rust), transparent);
    animation: scroll-pulse 2s infinite;
  }
  @keyframes scroll-pulse { 0%,100%{opacity:1;transform:scaleY(1)} 50%{opacity:0.3;transform:scaleY(0.6)} }

  /* ANIMATIONS */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }

  .reveal {
    opacity: 0; transform: translateY(32px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  /* ═══════ RUNNING MAN CANVAS ═══════ */
  #runnerCanvas {
    position: fixed;
    bottom: 0; left: 0;
    width: 100vw; height: 130px;
    pointer-events: none;
    z-index: 600;
  }

  /* Mobile */
  @media (max-width: 900px) {
    nav { padding: 16px 24px; }
    .nav-links { display: none; }
    .hero { grid-template-columns: 1fr; padding: 100px 24px 60px; gap: 40px; }
    .hero::after { left: 20px; }
    .hero-illustration { display: none; }
    section { padding: 72px 24px; }
    .skills-grid { grid-template-columns: repeat(2, 1fr); }
    .lab-grid { grid-template-columns: repeat(2, 1fr); }
    .writing-grid { grid-template-columns: 1fr; }
    .about-grid { grid-template-columns: 1fr; }
    .connect-grid { grid-template-columns: 1fr; }
    .about-pillars { grid-template-columns: repeat(2, 1fr); }
    footer { flex-direction: column; gap: 8px; padding: 24px; }
    .vision-words { gap: 0; }
    .project-featured { padding: 32px 28px; }
  }
</style>
</head>
<body>

<!-- CURSOR -->
<div class="cursor" id="cursor"></div>
<div class="cursor-trail" id="cursorTrail"></div>

<!-- NAV -->
<nav id="mainNav">
  <a href="#" class="nav-logo">AHS<span>.</span></a>
  <ul class="nav-links">
    <li><a href="#projects">Projects</a></li>
    <li><a href="#lab">Lab</a></li>
    <li><a href="#writing">Writing</a></li>
    <li><a href="#about">About</a></li>
    <li><a href="#connect">Connect</a></li>
  </ul>
</nav>

<!-- ═══════════ HERO ═══════════ -->
<section class="hero" id="home">
  <div class="hero-text">
    <div class="hero-label">Est. 202 · Digital Systems Builder</div>
    <h1 class="hero-headline">
      Building <em>smart</em><br>
      digital systems,<br>
      not just websites.
    </h1>
    <p class="hero-sub">
      <strong>Ahsanul Habib Safin</strong><br>
      Developer · Creator · AI Builder
    </p>
    <div class="hero-btns">
      <a href="#projects" class="btn btn-primary">View Work</a>
      <a href="#lab" class="btn btn-secondary">Explore Projects</a>
    </div>
  </div>

  <div class="hero-illustration" style="animation-delay:0.6s">
    <div class="notebook-card">
      <div class="notebook-holes">
        <div class="hole"></div>
        <div class="hole"></div>
        <div class="hole"></div>
        <div class="hole"></div>
      </div>
      <div class="nc-label">Current Build Log</div>
      <div class="nc-title">Systems<br>in motion.</div>
      <ul class="nc-list">
        <li>AI Plant Platform</li>
        <li>UI/UX Experiments</li>
        <li>Digital Strategy</li>
        <li>Scalable Products</li>
      </ul>
      <div class="nc-stamp"><span>In<br>Progress</span></div>
    </div>

    <!-- Floating doodle elements -->
    <svg style="position:absolute;top:-30px;right:10px;opacity:0.4;animation:fadeIn 1s 1s forwards;" width="60" height="60" viewBox="0 0 60 60" fill="none" xmlns="http://www.w3.org/2000/svg">
      <path d="M10 30 Q30 5 50 30 Q30 55 10 30Z" stroke="#C44B2B" stroke-width="1.5" fill="none" stroke-dasharray="4 2"/>
    </svg>
    <svg style="position:absolute;bottom:20px;left:-20px;opacity:0.35;animation:fadeIn 1s 1.3s forwards;" width="50" height="50" viewBox="0 0 50 50" fill="none">
      <circle cx="25" cy="25" r="20" stroke="#2B4A8C" stroke-width="1.5" stroke-dasharray="3 3"/>
      <circle cx="25" cy="25" r="10" stroke="#2B4A8C" stroke-width="1" fill="none"/>
    </svg>
    <svg style="position:absolute;top:60px;left:-40px;opacity:0.3;animation:fadeIn 1s 1.5s forwards;" width="80" height="30" viewBox="0 0 80 30" fill="none">
      <path d="M0 15 Q20 5 40 15 Q60 25 80 15" stroke="#C44B2B" stroke-width="1.5" fill="none"/>
    </svg>
  </div>

  <!-- Scroll -->
  <div class="scroll-indicator">
    <div class="scroll-line"></div>
    <span>Scroll</span>
  </div>
</section>

<!-- ═══════════ PROJECTS ═══════════ -->
<section class="projects-section" id="projects">
  <div class="section-inner">
    <div class="section-label reveal">02 / Projects</div>
    <h2 class="section-title reveal" style="color:var(--cream)">
      Executed <em>ideas.</em>
    </h2>
    <p class="section-desc reveal">
      These are not experiments — these are executed ideas. Each project reflects my approach to solving problems through design, logic, and scalable systems.
    </p>

    <div class="project-featured reveal">
      <div class="project-number">01</div>
      <div class="project-tag">🌱 AI · Marketplace · Plant Tech</div>
      <h3 class="project-name"><em>AI-Powered</em> Plant Platform</h3>
      <p class="project-desc">
        A system designed to scan plant health, provide intelligent solutions, and enable a global plant marketplace. Built at the intersection of computer vision, intelligent diagnostics, and community commerce.
      </p>
      <div class="project-features">
        <span class="project-feature">Plant Health Scanner</span>
        <span class="project-feature">AI Diagnostics Engine</span>
        <span class="project-feature">Global Marketplace</span>
        <span class="project-feature">Community Layer</span>
      </div>
      <a href="#" class="project-link">View Case Study →</a>
    </div>

    <div class="projects-wip reveal">
      <div class="wip-dot"></div>
      <span>More builds in progress — the lab is running 24/7.</span>
    </div>
  </div>
</section>

<!-- ═══════════ LAB ═══════════ -->
<section class="lab-section" id="lab">
  <div class="section-inner">
    <div class="section-label reveal">03 / Lab</div>
    <h2 class="section-title reveal">Where ideas <em>get tested.</em></h2>
    <p class="section-desc reveal">
      This space contains experiments, prototypes, and concepts. Some stay here. Some evolve into products.
    </p>

    <div class="lab-grid reveal">
      <div class="lab-item">
        <span class="lab-icon">🤖</span>
        <div class="lab-item-title">AI Integrations</div>
        <div class="lab-item-desc">Connecting intelligence to real-world workflows and interfaces.</div>
      </div>
      <div class="lab-item">
        <span class="lab-icon">⬡</span>
        <div class="lab-item-title">UI/UX Systems</div>
        <div class="lab-item-desc">Design systems that are functional, scalable, and human-first.</div>
      </div>
      <div class="lab-item">
        <span class="lab-icon">✦</span>
        <div class="lab-item-title">Interaction Design</div>
        <div class="lab-item-desc">Moments that feel inevitable, surprising, and right.</div>
      </div>
      <div class="lab-item" style="border-right:none">
        <span class="lab-icon">⚡</span>
        <div class="lab-item-title">Future-Ready Tools</div>
        <div class="lab-item-desc">Building infrastructure that outlasts the current wave.</div>
      </div>
    </div>

    <div class="lab-philosophy reveal">
      <div>
        <div class="lab-philosophy-text">
          "Some ideas belong in the lab forever.<br>Others are just waiting for the right moment."
        </div>
        <div class="lab-philosophy-note">— Lab Philosophy</div>
      </div>
    </div>
  </div>
</section>

<!-- ═══════════ WRITING ═══════════ -->
<section class="writing-section" id="writing">
  <div class="section-inner">
    <div class="section-label reveal">04 / Writing</div>
    <h2 class="section-title reveal">Clear thoughts. <em>Practical insights.</em></h2>
    <p class="section-desc reveal">
      I document ideas, systems, and perspectives. Not noise — signal.
    </p>

    <div class="writing-grid">
      <div class="writing-card reveal">
        <div class="writing-topic">Development</div>
        <div class="writing-title">The System Thinker's Approach to Building Products</div>
        <div class="writing-excerpt">Why the best developers think in flows, not features — and how that changes everything.</div>
        <div class="writing-card-num">01</div>
      </div>
      <div class="writing-card reveal" style="transition-delay:0.1s">
        <div class="writing-topic">AI Thinking</div>
        <div class="writing-title">When AI Stops Being a Tool and Becomes Infrastructure</div>
        <div class="writing-excerpt">A perspective on integrating intelligence into the foundation of digital products.</div>
        <div class="writing-card-num">02</div>
      </div>
      <div class="writing-card reveal" style="transition-delay:0.2s">
        <div class="writing-topic">Digital Strategy</div>
        <div class="writing-title">Building Less. Shipping Better. Thinking Longer.</div>
        <div class="writing-excerpt">The case against output-maximalism and for intentional, durable digital work.</div>
        <div class="writing-card-num">03</div>
      </div>
    </div>
  </div>
</section>

<!-- ═══════════ ABOUT ═══════════ -->
<section class="about-section" id="about">
  <div class="section-inner">
    <div class="section-label reveal">05 / About</div>
    <h2 class="section-title reveal">The person <em>behind the work.</em></h2>

    <div class="about-grid">
      <div class="about-portrait reveal">
        <div class="portrait-frame">
          <!-- Hand-drawn style portrait SVG -->
          <svg viewBox="0 0 300 375" fill="none" xmlns="http://www.w3.org/2000/svg">
            <!-- Background ruled lines -->
            <g opacity="0.08">
              <line x1="0" y1="40" x2="300" y2="40" stroke="#1A1209" stroke-width="1"/>
              <line x1="0" y1="72" x2="300" y2="72" stroke="#1A1209" stroke-width="1"/>
              <line x1="0" y1="104" x2="300" y2="104" stroke="#1A1209" stroke-width="1"/>
              <line x1="0" y1="136" x2="300" y2="136" stroke="#1A1209" stroke-width="1"/>
              <line x1="0" y1="168" x2="300" y2="168" stroke="#1A1209" stroke-width="1"/>
              <line x1="0" y1="200" x2="300" y2="200" stroke="#1A1209" stroke-width="1"/>
              <line x1="0" y1="232" x2="300" y2="232" stroke="#1A1209" stroke-width="1"/>
              <line x1="0" y1="264" x2="300" y2="264" stroke="#1A1209" stroke-width="1"/>
              <line x1="0" y1="296" x2="300" y2="296" stroke="#1A1209" stroke-width="1"/>
              <line x1="0" y1="328" x2="300" y2="328" stroke="#1A1209" stroke-width="1"/>
              <line x1="0" y1="360" x2="300" y2="360" stroke="#1A1209" stroke-width="1"/>
            </g>
            <!-- Body/shirt -->
            <path d="M80 290 Q80 270 90 260 Q110 245 150 242 Q190 245 210 260 Q220 270 220 290 L220 375 L80 375 Z" fill="#3D2F1A" opacity="0.9"/>
            <!-- Collar -->
            <path d="M130 258 L150 275 L170 258" stroke="#F5F0E8" stroke-width="2" fill="none"/>
            <!-- Neck -->
            <path d="M135 240 Q135 258 150 258 Q165 258 165 240" fill="#D4A882"/>
            <!-- Head -->
            <ellipse cx="150" cy="185" rx="52" ry="62" fill="#D4A882"/>
            <!-- Hair - curly/natural -->
            <path d="M98 175 Q95 145 105 130 Q115 110 130 105 Q140 100 150 100 Q160 100 170 105 Q185 110 195 130 Q205 145 202 175 Q198 155 185 148 Q175 142 165 148 Q158 152 150 152 Q142 152 135 148 Q125 142 115 148 Q102 155 98 175Z" fill="#2A1A0A"/>
            <!-- Hair texture lines -->
            <path d="M110 130 Q120 118 135 115" stroke="#1A1209" stroke-width="1.5" fill="none" opacity="0.4"/>
            <path d="M165 115 Q180 118 190 130" stroke="#1A1209" stroke-width="1.5" fill="none" opacity="0.4"/>
            <!-- Ear -->
            <ellipse cx="98" cy="190" rx="8" ry="11" fill="#C9956A"/>
            <ellipse cx="202" cy="190" rx="8" ry="11" fill="#C9956A"/>
            <!-- Eyes -->
            <ellipse cx="132" cy="185" rx="9" ry="7" fill="white"/>
            <ellipse cx="168" cy="185" rx="9" ry="7" fill="white"/>
            <circle cx="134" cy="185" r="5" fill="#2A1A0A"/>
            <circle cx="170" cy="185" r="5" fill="#2A1A0A"/>
            <circle cx="136" cy="183" r="1.5" fill="white"/>
            <circle cx="172" cy="183" r="1.5" fill="white"/>
            <!-- Eyebrows -->
            <path d="M122 175 Q132 170 142 173" stroke="#2A1A0A" stroke-width="2.5" fill="none" stroke-linecap="round"/>
            <path d="M158 173 Q168 170 178 175" stroke="#2A1A0A" stroke-width="2.5" fill="none" stroke-linecap="round"/>
            <!-- Nose -->
            <path d="M147 193 Q144 205 140 208 Q150 211 160 208 Q156 205 153 193" stroke="#B88260" stroke-width="1.5" fill="none"/>
            <!-- Smile -->
            <path d="M136 222 Q150 232 164 222" stroke="#2A1A0A" stroke-width="2" fill="none" stroke-linecap="round"/>
            <!-- Laptop/device hint -->
            <rect x="85" y="300" width="130" height="2" rx="1" fill="#F5F0E8" opacity="0.3"/>
            <!-- Decorative doodles around figure -->
            <text x="30" y="80" font-family="serif" font-size="11" fill="#C44B2B" opacity="0.5" transform="rotate(-15, 30, 80)">✦ builder</text>
            <text x="220" y="100" font-family="serif" font-size="10" fill="#2B4A8C" opacity="0.5" transform="rotate(12, 220, 100)">creator ✦</text>
            <path d="M240 150 Q255 140 260 155 Q255 170 240 160" stroke="#D4A017" stroke-width="1.5" fill="none" opacity="0.4" stroke-dasharray="3 2"/>
            <path d="M30 200 Q20 190 25 210 Q30 220 40 210" stroke="#4A6741" stroke-width="1.5" fill="none" opacity="0.4"/>
          </svg>
        </div>
        <div class="portrait-sticker">AI<br>Builder</div>
        <p class="portrait-caption">Ahsanul Habib Safin — somewhere between a debugger and a dreamer.</p>
      </div>

      <div class="about-content reveal" style="transition-delay:0.15s">
        <p class="bio-text">
          I'm Ahsanul Habib Safin — a developer focused on building systems that <em>go beyond basic execution.</em> I work at the intersection of technology, creativity, and real-world application.
        </p>
        <p class="bio-text">
          Currently developing an <em>AI-driven plant ecosystem</em> designed for global use. I don't focus on doing more. I focus on building <em>better.</em>
        </p>

        <div class="about-pillars">
          <div class="pillar">
            <div class="pillar-icon">💡</div>
            <div class="pillar-name">Technology</div>
          </div>
          <div class="pillar">
            <div class="pillar-icon">🎨</div>
            <div class="pillar-name">Creativity</div>
          </div>
          <div class="pillar">
            <div class="pillar-icon">🌍</div>
            <div class="pillar-name">Real-World Application</div>
          </div>
        </div>

        <div class="about-quote">
          "I don't focus on doing more.<br>I focus on building better."
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ═══════════ SKILLS ═══════════ -->
<section class="skills-section" id="skills">
  <div class="section-inner">
    <div class="section-label reveal">06 / Skills</div>
    <h2 class="section-title reveal">The toolkit <em>behind the work.</em></h2>
  </div>

  <div class="skills-track-wrapper" style="margin-top:40px">
    <div class="skills-track">
      <span class="skill-pill">Web Development</span>
      <span class="skill-pill">UI/UX Design</span>
      <span class="skill-pill">AI-based Systems</span>
      <span class="skill-pill">Graphic Design</span>
      <span class="skill-pill">Content Creation</span>
      <span class="skill-pill">Web Development</span>
      <span class="skill-pill">UI/UX Design</span>
      <span class="skill-pill">AI-based Systems</span>
      <span class="skill-pill">Graphic Design</span>
      <span class="skill-pill">Content Creation</span>
    </div>
  </div>

  <div class="section-inner">
    <div class="skills-grid reveal">
      <div class="skill-card">
        <div class="skill-card-icon">🌐</div>
        <div class="skill-card-name">Web Dev</div>
      </div>
      <div class="skill-card">
        <div class="skill-card-icon">⬡</div>
        <div class="skill-card-name">UI/UX Design</div>
      </div>
      <div class="skill-card">
        <div class="skill-card-icon">🤖</div>
        <div class="skill-card-name">AI Systems</div>
      </div>
      <div class="skill-card">
        <div class="skill-card-icon">🎨</div>
        <div class="skill-card-name">Graphic Design</div>
      </div>
      <div class="skill-card">
        <div class="skill-card-icon">✍️</div>
        <div class="skill-card-name">Content Creation</div>
      </div>
    </div>
  </div>
</section>

<!-- ═══════════ VISION ═══════════ -->
<section class="vision-section">
  <div class="section-inner" style="position:relative;z-index:2">
    <div class="vision-eyebrow reveal">Vision</div>
    <h2 class="vision-headline reveal">
      To create digital platforms<br>
      that <em>scale, solve,</em> and sustain.
    </h2>

    <div class="vision-words">
      <div class="vision-word">SCALE</div>
      <div class="vision-word accent">·</div>
      <div class="vision-word">SOLVE</div>
      <div class="vision-word accent">·</div>
      <div class="vision-word">SUSTAIN</div>
    </div>
  </div>
</section>

<!-- ═══════════ CONNECT ═══════════ -->
<section class="connect-section" id="connect">
  <div class="section-inner">
    <div class="section-label reveal">08 / Connect</div>
    <h2 class="section-title reveal">Let's <em>connect.</em></h2>
    <p class="section-desc reveal">Not "hire me." Just — let's talk about building something that matters.</p>

    <div class="connect-grid">
      <div>
        <a href="mailto:ahsanul@example.com" class="connect-link-item" style="border:1.5px solid rgba(26,18,9,0.12);margin-bottom:-1px;display:flex;" >
          <div class="connect-link-left">
            <span class="connect-link-icon">✉️</span>
            <div>
              <div class="connect-link-name">Email</div>
              <div class="connect-link-sub">Direct Line</div>
            </div>
          </div>
          <div class="connect-link-arrow">→</div>
        </a>
        <div class="connect-links">
          <a href="#" class="connect-link-item">
            <div class="connect-link-left">
              <span class="connect-link-icon">🛍</span>
              <div>
                <div class="connect-link-name">Fiverr</div>
                <div class="connect-link-sub">Freelance Work</div>
              </div>
            </div>
            <div class="connect-link-arrow">→</div>
          </a>
          <a href="#" class="connect-link-item">
            <div class="connect-link-left">
              <span class="connect-link-icon">𝕏</span>
              <div>
                <div class="connect-link-name">Twitter / X</div>
                <div class="connect-link-sub">Thoughts & Updates</div>
              </div>
            </div>
            <div class="connect-link-arrow">→</div>
          </a>
          <a href="#" class="connect-link-item">
            <div class="connect-link-left">
              <span class="connect-link-icon">💼</span>
              <div>
                <div class="connect-link-name">LinkedIn</div>
                <div class="connect-link-sub">Professional Profile</div>
              </div>
            </div>
            <div class="connect-link-arrow">→</div>
          </a>
          <a href="#" class="connect-link-item" style="border-bottom:none">
            <div class="connect-link-left">
              <span class="connect-link-icon">📦</span>
              <div>
                <div class="connect-link-name">GitHub</div>
                <div class="connect-link-sub">Open Source Work</div>
              </div>
            </div>
            <div class="connect-link-arrow">→</div>
          </a>
        </div>
      </div>

      <div class="connect-handwritten reveal" style="transition-delay:0.2s">
        <div class="connect-handwritten-text">
          If you've made it this far,<br>
          you're probably the kind of person<br>
          I'd want to build with.<br><br>
          Let's not make this complicated —<br>
          just reach out.
        </div>
        <div class="connect-handwritten-sig">— Safin</div>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-sig">
    I build with <strong>intention</strong>, not attention.
  </div>
  <div class="footer-copy">© 2025 Ahsanul Habib Safin — All systems running.</div>
</footer>

<!-- ═══════════ RUNNING MAN CANVAS ═══════════ -->
<canvas id="runnerCanvas"></canvas>

<script>
// CURSOR
const cursor = document.getElementById('cursor');
const trail = document.getElementById('cursorTrail');
let mx = 0, my = 0, tx = 0, ty = 0;

document.addEventListener('mousemove', e => {
  mx = e.clientX; my = e.clientY;
  cursor.style.transform = `translate(${mx - 6}px, ${my - 6}px)`;
});

function animateTrail() {
  tx += (mx - tx) * 0.18;
  ty += (my - ty) * 0.18;
  trail.style.transform = `translate(${tx - 16}px, ${ty - 16}px)`;
  requestAnimationFrame(animateTrail);
}
animateTrail();

document.querySelectorAll('a, button, .skill-card, .lab-item, .writing-card').forEach(el => {
  el.addEventListener('mouseenter', () => {
    cursor.style.transform += ' scale(2)';
    trail.style.transform += ' scale(1.5)';
  });
  el.addEventListener('mouseleave', () => {});
});

// NAV SCROLL
const nav = document.getElementById('mainNav');
window.addEventListener('scroll', () => {
  nav.classList.toggle('scrolled', window.scrollY > 60);
});

// REVEAL ON SCROLL
const reveals = document.querySelectorAll('.reveal');
const observer = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) { e.target.classList.add('visible'); }
  });
}, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' });
reveals.forEach(r => observer.observe(r));

// SECTION LABEL auto-number via CSS counter removed; using manual labels

// Subtle parallax on hero notebook
const notebook = document.querySelector('.notebook-card');
if (notebook) {
  document.addEventListener('mousemove', e => {
    const x = (e.clientX / window.innerWidth - 0.5) * 10;
    const y = (e.clientY / window.innerHeight - 0.5) * 8;
    notebook.style.transform = `rotate(2deg) translate(${x}px, ${y}px)`;
  });
}

// Running man speech bubble cycle
const bubbleMessages = [
  '⚡ building the future →',
  '🤖 training AI models →',
  '🌱 growing the platform →',
  '💡 shipping ideas →',
  '🔥 no days off →',
  '→ just one more feature',
  '☕ fueled by caffeine →',
  '🚀 deploying in 3.. 2.. →',
];
let bubbleIdx = 0;
const bubble = document.querySelector('.runner-bubble');
const runnerEl = document.getElementById('runnerEl');

// Each time runner completes a lap, change the message
if (runnerEl && bubble) {
  runnerEl.addEventListener('animationiteration', () => {
    bubbleIdx = (bubbleIdx + 1) % bubbleMessages.length;
    bubble.textContent = bubbleMessages[bubbleIdx];
  });
}
</script>
</body>
</html>
