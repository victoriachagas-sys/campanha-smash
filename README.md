<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Campanha Smash - Time N1</title>
<link href="https://fonts.googleapis.com/css2?family=Bangers&family=Bebas+Neue&family=Outfit:wght@300;400;600;700;800&display=swap" rel="stylesheet">
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }

  :root {
    --bg-dark: #0a0a12;
    --neon-yellow: #f5e642;
    --neon-orange: #ff6b35;
    --neon-red: #ff2d55;
    --neon-cyan: #00e5ff;
    --neon-purple: #b14aed;
    --neon-green: #39ff14;
    --white: #ffffff;
    --card-bg: rgba(255,255,255,0.04);
    --silver: #c0c0c0;
    --gold: #ffd700;
    --diamond: #b9f2ff;
  }

  body {
    background: var(--bg-dark);
    font-family: 'Outfit', sans-serif;
    color: var(--white);
    min-height: 100vh;
    overflow-x: hidden;
  }

  .poster { max-width: 840px; margin: 0 auto; padding: 40px 24px; position: relative; }

  .bg-grid {
    position: fixed; top: 0; left: 0; right: 0; bottom: 0;
    background-image:
      linear-gradient(rgba(255,255,255,0.02) 1px, transparent 1px),
      linear-gradient(90deg, rgba(255,255,255,0.02) 1px, transparent 1px);
    background-size: 60px 60px; pointer-events: none; z-index: 0;
  }

  .bg-glow { position: fixed; width: 500px; height: 500px; border-radius: 50%; filter: blur(120px); opacity: 0.3; pointer-events: none; z-index: 0; }
  .bg-glow.one { top: -100px; left: -100px; background: var(--neon-purple); }
  .bg-glow.two { bottom: -150px; right: -100px; background: var(--neon-orange); }
  .bg-glow.three { top: 50%; left: 50%; transform: translate(-50%,-50%); background: var(--neon-red); opacity: 0.1; }

  .content { position: relative; z-index: 1; }

  .badge {
    display: inline-flex; align-items: center; gap: 8px;
    background: linear-gradient(135deg, var(--neon-red), var(--neon-orange));
    padding: 8px 20px; border-radius: 50px;
    font-weight: 700; font-size: 13px; letter-spacing: 2px; text-transform: uppercase;
    margin-bottom: 24px; animation: fadeSlideDown 0.6s ease-out;
  }
  .badge::before { content: "🔥"; }

  .title-block { margin-bottom: 40px; animation: fadeSlideDown 0.8s ease-out; }

  .title-main {
    font-family: 'Bangers', cursive;
    font-size: clamp(56px, 10vw, 96px); line-height: 0.9; letter-spacing: 3px;
    background: linear-gradient(135deg, var(--neon-yellow) 0%, var(--neon-orange) 40%, var(--neon-red) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
    filter: drop-shadow(0 0 30px rgba(255,107,53,0.4)); margin-bottom: 8px;
  }

  .title-sub {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(24px, 4.5vw, 40px); letter-spacing: 6px;
    color: var(--neon-cyan); text-shadow: 0 0 20px rgba(0,229,255,0.4);
  }

  /* ── TIERS ── */
  .tiers-container { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin: 40px 0; }
  @media (max-width: 640px) { .tiers-container { grid-template-columns: 1fr; } }

  .tier-card {
    border-radius: 20px; padding: 32px 24px; text-align: center;
    position: relative; overflow: hidden; transition: transform 0.3s ease;
  }
  .tier-card:hover { transform: translateY(-6px); }
  .tier-card::before {
    content: ''; position: absolute; top: -50%; left: -50%; width: 200%; height: 200%;
    background: conic-gradient(from 0deg, transparent, rgba(255,255,255,0.08), transparent, rgba(255,255,255,0.05), transparent);
    animation: shimmer 4s linear infinite;
  }

  .tier-gold {
    background: linear-gradient(160deg, rgba(255,215,0,0.12), rgba(255,140,0,0.08));
    border: 2px solid rgba(255,215,0,0.35); box-shadow: 0 0 40px rgba(255,215,0,0.15);
    animation: fadeSlideUp 1s ease-out 0.3s both;
  }
  .tier-silver {
    background: linear-gradient(160deg, rgba(192,192,192,0.1), rgba(160,160,180,0.06));
    border: 2px solid rgba(192,192,192,0.25); box-shadow: 0 0 30px rgba(192,192,192,0.1);
    animation: fadeSlideUp 1s ease-out 0.5s both;
  }

  .tier-emoji { font-size: 48px; position: relative; z-index: 1; margin-bottom: 8px; }
  .tier-label { font-family: 'Bebas Neue', sans-serif; font-size: 18px; letter-spacing: 4px; position: relative; z-index: 1; margin-bottom: 12px; }
  .tier-gold .tier-label { color: var(--gold); }
  .tier-silver .tier-label { color: var(--silver); }

  .tier-tickets { font-family: 'Bangers', cursive; font-size: 52px; line-height: 1; position: relative; z-index: 1; margin-bottom: 4px; }
  .tier-gold .tier-tickets { background: linear-gradient(135deg, var(--neon-yellow), var(--neon-orange)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
  .tier-silver .tier-tickets { background: linear-gradient(135deg, #e0e0e0, #a0a0b0); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }

  .tier-tickets-sub { font-size: 14px; color: rgba(255,255,255,0.45); font-weight: 300; position: relative; z-index: 1; margin-bottom: 20px; }
  .tier-divider { height: 1px; background: rgba(255,255,255,0.08); margin: 16px 0; position: relative; z-index: 1; }
  .tier-prize { position: relative; z-index: 1; margin-top: 16px; }
  .tier-prize-label { font-size: 12px; letter-spacing: 2px; text-transform: uppercase; color: rgba(255,255,255,0.4); margin-bottom: 8px; font-weight: 600; }
  .tier-prize-value { font-family: 'Bangers', cursive; font-size: 40px; line-height: 1.1; }
  .tier-gold .tier-prize-value { background: linear-gradient(135deg, var(--neon-yellow), var(--neon-orange)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; filter: drop-shadow(0 0 12px rgba(255,215,0,0.3)); }
  .tier-silver .tier-prize-value { background: linear-gradient(135deg, #e0e0e0, #a8a8b8); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
  .tier-prize-desc { font-size: 13px; color: rgba(255,255,255,0.4); margin-top: 4px; position: relative; z-index: 1; }

  /* ── BONUS CSAT CARD ── */
  .bonus-section { margin: 44px 0 36px; animation: fadeSlideUp 1s ease-out 0.6s both; }
  .bonus-section-label {
    font-family: 'Bebas Neue', sans-serif; font-size: 20px; letter-spacing: 5px;
    color: rgba(255,255,255,0.4); text-align: center; margin-bottom: 20px;
    display: flex; align-items: center; gap: 16px; justify-content: center;
  }
  .bonus-section-label::before,
  .bonus-section-label::after {
    content: ''; flex: 1; max-width: 100px; height: 1px;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
  }

  .bonus-card {
    border-radius: 24px; padding: 36px 32px; text-align: center;
    position: relative; overflow: hidden;
    background: linear-gradient(160deg, rgba(185,242,255,0.08), rgba(0,229,255,0.04), rgba(177,74,237,0.06));
    border: 2px solid rgba(185,242,255,0.25);
    box-shadow: 0 0 50px rgba(0,229,255,0.12), 0 0 100px rgba(177,74,237,0.06);
    transition: transform 0.3s ease;
  }
  .bonus-card:hover { transform: translateY(-6px); }
  .bonus-card::before {
    content: ''; position: absolute; top: -50%; left: -50%; width: 200%; height: 200%;
    background: conic-gradient(from 0deg, transparent, rgba(185,242,255,0.1), transparent, rgba(177,74,237,0.06), transparent);
    animation: shimmer 5s linear infinite;
  }

  .bonus-top-row {
    display: flex; align-items: center; justify-content: center; gap: 20px;
    position: relative; z-index: 1; margin-bottom: 16px; flex-wrap: wrap;
  }

  .bonus-emoji { font-size: 52px; }

  .bonus-tag {
    background: linear-gradient(135deg, var(--neon-cyan), var(--neon-purple));
    padding: 6px 18px; border-radius: 50px;
    font-weight: 700; font-size: 12px; letter-spacing: 2px; text-transform: uppercase;
  }

  .bonus-title {
    font-family: 'Bangers', cursive; font-size: 36px; letter-spacing: 2px;
    position: relative; z-index: 1; margin-bottom: 6px;
    background: linear-gradient(135deg, var(--diamond), var(--neon-cyan), var(--neon-purple));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
    filter: drop-shadow(0 0 16px rgba(0,229,255,0.3));
  }

  .bonus-desc {
    font-size: 15px; color: rgba(255,255,255,0.55); line-height: 1.6; font-weight: 300;
    position: relative; z-index: 1; max-width: 520px; margin: 0 auto 24px;
  }
  .bonus-desc strong { color: var(--neon-cyan); font-weight: 600; }

  .bonus-rewards {
    display: grid; grid-template-columns: 1fr 1fr; gap: 14px;
    position: relative; z-index: 1; max-width: 440px; margin: 0 auto;
  }
  @media (max-width: 480px) { .bonus-rewards { grid-template-columns: 1fr; } }

  .bonus-reward-item {
    background: rgba(255,255,255,0.04); border: 1px solid rgba(255,255,255,0.08);
    border-radius: 14px; padding: 18px 16px; text-align: center;
  }

  .bonus-reward-csat {
    font-family: 'Bebas Neue', sans-serif; font-size: 15px; letter-spacing: 3px;
    color: rgba(255,255,255,0.45); margin-bottom: 6px;
  }
  .bonus-reward-csat-val {
    font-family: 'Bangers', cursive; font-size: 38px; line-height: 1;
    margin-bottom: 4px;
  }
  .bonus-reward-item:first-child .bonus-reward-csat-val {
    background: linear-gradient(135deg, var(--neon-cyan), var(--neon-purple));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
  }
  .bonus-reward-item:last-child .bonus-reward-csat-val {
    background: linear-gradient(135deg, var(--diamond), var(--neon-cyan));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
  }
  .bonus-reward-amount {
    font-family: 'Bangers', cursive; font-size: 28px; line-height: 1;
    color: var(--neon-green); filter: drop-shadow(0 0 8px rgba(57,255,20,0.3));
  }

  .bonus-conditions {
    position: relative; z-index: 1;
    margin-top: 20px; padding-top: 18px;
    border-top: 1px solid rgba(255,255,255,0.06);
    font-size: 13px; color: rgba(255,255,255,0.35); line-height: 1.7;
  }
  .bonus-conditions strong { color: rgba(255,255,255,0.55); }

  /* ── MAX COMBO ── */
  .combo-box {
    background: linear-gradient(135deg, rgba(57,255,20,0.06), rgba(0,229,255,0.04));
    border: 1px dashed rgba(57,255,20,0.25); border-radius: 16px;
    padding: 24px 28px; margin: 28px 0; text-align: center;
    animation: fadeSlideUp 1s ease-out 0.8s both;
  }
  .combo-title {
    font-family: 'Bangers', cursive; font-size: 22px; letter-spacing: 2px;
    color: var(--neon-green); margin-bottom: 8px;
    filter: drop-shadow(0 0 8px rgba(57,255,20,0.3));
  }
  .combo-value {
    font-family: 'Bangers', cursive; font-size: 56px; line-height: 1;
    background: linear-gradient(135deg, var(--neon-green), var(--neon-cyan), var(--neon-yellow));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;
    filter: drop-shadow(0 0 20px rgba(57,255,20,0.3));
    margin-bottom: 6px;
  }
  .combo-desc { font-size: 14px; color: rgba(255,255,255,0.45); font-weight: 300; }
  .combo-formula {
    display: inline-flex; align-items: center; gap: 8px; flex-wrap: wrap; justify-content: center;
    margin-top: 14px; font-size: 14px; font-weight: 600; color: rgba(255,255,255,0.5);
  }
  .combo-chip {
    padding: 4px 12px; border-radius: 6px; font-size: 13px; font-weight: 700;
  }
  .combo-chip.gold-c { background: rgba(255,215,0,0.15); color: var(--gold); }
  .combo-chip.bonus-c { background: rgba(0,229,255,0.12); color: var(--neon-cyan); }
  .combo-plus { font-family: 'Bangers', cursive; font-size: 20px; color: rgba(255,255,255,0.3); }
  .combo-equals { font-family: 'Bangers', cursive; font-size: 20px; color: var(--neon-green); }

  /* ── CONDITIONS ── */
  .conditions-section {
    background: var(--card-bg); border: 1px solid rgba(255,255,255,0.06);
    border-radius: 20px; padding: 36px; margin: 36px 0;
    backdrop-filter: blur(10px); animation: fadeSlideUp 1s ease-out 0.9s both;
  }
  .conditions-header { font-family: 'Bebas Neue', sans-serif; font-size: 22px; letter-spacing: 4px; color: rgba(255,255,255,0.5); margin-bottom: 24px; }

  .condition-item { display: flex; align-items: flex-start; gap: 16px; margin-bottom: 20px; }
  .condition-item:last-child { margin-bottom: 0; }
  .condition-icon { width: 40px; height: 40px; border-radius: 12px; display: flex; align-items: center; justify-content: center; font-size: 20px; flex-shrink: 0; }
  .condition-icon.green { background: rgba(57,255,20,0.1); border: 1px solid rgba(57,255,20,0.2); }
  .condition-icon.red { background: rgba(255,45,85,0.1); border: 1px solid rgba(255,45,85,0.2); }
  .condition-icon.cyan { background: rgba(0,229,255,0.1); border: 1px solid rgba(0,229,255,0.2); }
  .condition-icon.yellow { background: rgba(245,230,66,0.1); border: 1px solid rgba(245,230,66,0.2); }
  .condition-icon.purple { background: rgba(177,74,237,0.1); border: 1px solid rgba(177,74,237,0.2); }

  .ct-title { font-weight: 700; font-size: 15px; margin-bottom: 4px; }
  .ct-desc { font-size: 14px; color: rgba(255,255,255,0.5); line-height: 1.5; font-weight: 300; }
  .ct-desc strong { color: var(--neon-red); font-weight: 600; }
  .ct-desc em { color: var(--neon-cyan); font-style: normal; font-weight: 600; }

  /* ── RULES GRID ── */
  .rules-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin: 32px 0; }
  @media (max-width: 640px) { .rules-grid { grid-template-columns: 1fr; } }

  .rule-card {
    background: var(--card-bg); border: 1px solid rgba(255,255,255,0.06);
    border-radius: 16px; padding: 24px;
    transition: transform 0.3s ease, border-color 0.3s ease;
    animation: fadeSlideUp 1s ease-out both;
  }
  .rule-card:nth-child(1) { animation-delay: 1s; }
  .rule-card:nth-child(2) { animation-delay: 1.1s; }
  .rule-card:nth-child(3) { animation-delay: 1.2s; }
  .rule-card:nth-child(4) { animation-delay: 1.3s; }
  .rule-card:hover { transform: translateY(-4px); border-color: rgba(255,255,255,0.12); }
  .rule-icon { font-size: 32px; margin-bottom: 12px; }
  .rule-title { font-weight: 700; font-size: 16px; margin-bottom: 6px; }
  .rule-desc { font-size: 14px; color: rgba(255,255,255,0.5); line-height: 1.5; font-weight: 300; }

  .alert-box {
    background: linear-gradient(135deg, rgba(255,45,85,0.08), rgba(255,45,85,0.04));
    border-left: 3px solid var(--neon-red); border-radius: 0 14px 14px 0;
    padding: 22px 24px; margin: 28px 0; animation: fadeSlideUp 1s ease-out 1.35s both;
  }
  .alert-title { font-weight: 700; font-size: 15px; color: var(--neon-red); margin-bottom: 6px; display: flex; align-items: center; gap: 8px; }
  .alert-desc { font-size: 14px; color: rgba(255,255,255,0.55); line-height: 1.6; font-weight: 300; }

  .highlight-box {
    background: linear-gradient(135deg, rgba(245,230,66,0.08), rgba(255,107,53,0.08));
    border-left: 3px solid var(--neon-orange); border-radius: 0 12px 12px 0;
    padding: 20px 24px; margin: 24px 0; font-size: 15px; line-height: 1.7;
    color: rgba(255,255,255,0.7); animation: fadeSlideUp 1s ease-out 1.4s both;
  }
  .highlight-box strong { color: var(--neon-yellow); }

  .cta-section { text-align: center; margin-top: 48px; animation: fadeSlideUp 1s ease-out 1.5s both; }
  .cta-text { font-family: 'Bebas Neue', sans-serif; font-size: 28px; letter-spacing: 4px; color: rgba(255,255,255,0.7); margin-bottom: 20px; }
  .cta-button {
    display: inline-flex; align-items: center; gap: 10px;
    background: linear-gradient(135deg, var(--neon-orange), var(--neon-red));
    color: white; border: none; padding: 16px 40px; border-radius: 60px;
    font-family: 'Outfit', sans-serif; font-size: 18px; font-weight: 700; letter-spacing: 1px;
    cursor: pointer; box-shadow: 0 0 30px rgba(255,45,85,0.4);
    transition: transform 0.2s ease, box-shadow 0.2s ease; text-transform: uppercase;
  }
  .cta-button:hover { transform: scale(1.05); box-shadow: 0 0 50px rgba(255,45,85,0.6); }

  .footer-note {
    text-align: center; margin-top: 40px; padding-top: 32px;
    border-top: 1px solid rgba(255,255,255,0.06);
    font-size: 13px; color: rgba(255,255,255,0.3); line-height: 1.8;
    animation: fadeSlideUp 1s ease-out 1.6s both;
  }

  @keyframes fadeSlideDown { from { opacity: 0; transform: translateY(-20px); } to { opacity: 1; transform: translateY(0); } }
  @keyframes fadeSlideUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
  @keyframes shimmer { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }

  .sparkles { position: absolute; width: 100%; height: 100%; top: 0; left: 0; pointer-events: none; overflow: hidden; }
  .sparkle { position: absolute; width: 4px; height: 4px; background: var(--neon-yellow); border-radius: 50%; animation: twinkle 2s ease-in-out infinite; }
  .sparkle:nth-child(1) { top: 8%; left: 12%; animation-delay: 0s; }
  .sparkle:nth-child(2) { top: 20%; right: 8%; animation-delay: 0.5s; }
  .sparkle:nth-child(3) { top: 45%; left: 6%; animation-delay: 1s; }
  .sparkle:nth-child(4) { bottom: 25%; right: 15%; animation-delay: 1.5s; }
  .sparkle:nth-child(5) { top: 35%; left: 88%; animation-delay: 0.7s; }
  .sparkle:nth-child(6) { top: 65%; left: 25%; animation-delay: 1.2s; }
  .sparkle:nth-child(7) { top: 55%; right: 5%; animation-delay: 0.3s; background: var(--neon-cyan); }
  .sparkle:nth-child(8) { bottom: 10%; left: 50%; animation-delay: 0.9s; background: var(--neon-cyan); }
  @keyframes twinkle { 0%, 100% { opacity: 0; transform: scale(0); } 50% { opacity: 1; transform: scale(1); } }
</style>
</head>
<body>

<div class="bg-grid"></div>
<div class="bg-glow one"></div>
<div class="bg-glow two"></div>
<div class="bg-glow three"></div>

<div class="poster">
  <div class="sparkles">
    <div class="sparkle"></div><div class="sparkle"></div><div class="sparkle"></div>
    <div class="sparkle"></div><div class="sparkle"></div><div class="sparkle"></div>
    <div class="sparkle"></div><div class="sparkle"></div>
  </div>

  <div class="content">

    <div class="badge">CAMPANHA MENSAL — TIME N1</div>

    <div class="title-block">
      <div class="title-main">SMASH<br>CHALLENGE</div>
      <div class="title-sub">Quebre a meta. Ganhe o cartão.</div>
    </div>

    <!-- ── PRODUCTION TIERS ── -->
    <div class="tiers-container">
      <div class="tier-card tier-gold">
        <div class="tier-emoji">🥇</div>
        <div class="tier-label">TIER OURO</div>
        <div class="tier-tickets">65+</div>
        <div class="tier-tickets-sub">média de tickets/dia no mês</div>
        <div class="tier-divider"></div>
        <div class="tier-prize">
          <div class="tier-prize-label">Premiação</div>
          <div class="tier-prize-value">R$ 100</div>
          <div class="tier-prize-desc">Cartão Smash + Bônus máximo</div>
        </div>
      </div>
      <div class="tier-card tier-silver">
        <div class="tier-emoji">🥈</div>
        <div class="tier-label">TIER PRATA</div>
        <div class="tier-tickets">50+</div>
        <div class="tier-tickets-sub">média de tickets/dia no mês</div>
        <div class="tier-divider"></div>
        <div class="tier-prize">
          <div class="tier-prize-label">Premiação</div>
          <div class="tier-prize-value">R$ 50</div>
          <div class="tier-prize-desc">Cartão Smash</div>
        </div>
      </div>
    </div>

    <!-- ── BONUS CSAT ── -->
    <div class="bonus-section">
      <div class="bonus-section-label">⭐ BÔNUS QUALIDADE ⭐</div>
      <div class="bonus-card">
        <div class="bonus-top-row">
          <div class="bonus-emoji">💎</div>
          <div class="bonus-tag">BÔNUS CSAT</div>
        </div>
        <div class="bonus-title">+ R$ 100 EXTRA</div>
        <div class="bonus-desc">
          Além da premiação por produtividade, quem mantiver um <strong>CSAT acima de 75% ou 80%</strong> no mês leva um bônus adicional de <strong>R$ 100</strong>. Qualidade + Volume = Recompensa máxima!
        </div>
        <div class="bonus-rewards">
          <div class="bonus-reward-item">
            <div class="bonus-reward-csat">CSAT MÍNIMO</div>
            <div class="bonus-reward-csat-val">75%</div>
            <div class="bonus-reward-amount">+ R$ 100</div>
          </div>
          <div class="bonus-reward-item">
            <div class="bonus-reward-csat">CSAT IDEAL</div>
            <div class="bonus-reward-csat-val">80%+</div>
            <div class="bonus-reward-amount">+ R$ 100</div>
          </div>
        </div>
        <div class="bonus-conditions">
          <strong>Pré-requisitos do bônus:</strong> Bater a meta de produtividade (Tier Ouro ou Prata) + Zero faltas/ABS no mês.<br>
          O bônus CSAT é cumulativo com a premiação de produtividade.
        </div>
      </div>
    </div>

    <!-- ── MAX COMBO ── -->
    <div class="combo-box">
      <div class="combo-title">🔥 COMBO MÁXIMO POSSÍVEL</div>
      <div class="combo-value">R$ 200</div>
      <div class="combo-desc">Tier Ouro + Bônus CSAT no mesmo mês</div>
      <div class="combo-formula">
        <span class="combo-chip gold-c">R$100 Ouro</span>
        <span class="combo-plus">+</span>
        <span class="combo-chip bonus-c">R$100 CSAT</span>
        <span class="combo-equals">=</span>
        <span class="combo-chip" style="background:rgba(57,255,20,0.15);color:var(--neon-green);">R$200</span>
      </div>
    </div>

    <!-- ── CONDITIONS ── -->
    <div class="conditions-section">
      <div class="conditions-header">📋 CONDIÇÕES OBRIGATÓRIAS</div>

      <div class="condition-item">
        <div class="condition-icon green">✅</div>
        <div class="condition-text">
          <div class="ct-title">Frequência Impecável</div>
          <div class="ct-desc">O colaborador <strong>não pode ter nenhuma falta, ABS ou ausência injustificada</strong> durante o mês. Presença total é pré-requisito para qualquer premiação.</div>
        </div>
      </div>

      <div class="condition-item">
        <div class="condition-icon cyan">📊</div>
        <div class="condition-text">
          <div class="ct-title">Média Mensal de Tickets</div>
          <div class="ct-desc">A contagem é baseada na <em>média diária de tickets tratados ao longo de todo o mês</em>, incluindo backlogs resolvidos.</div>
        </div>
      </div>

      <div class="condition-item">
        <div class="condition-icon yellow">📁</div>
        <div class="condition-text">
          <div class="ct-title">Backlogs Contam</div>
          <div class="ct-desc">Tickets de backlog resolvidos <em>são somados à contagem diária</em>. Aproveite para limpar a fila e turbinar sua média!</div>
        </div>
      </div>

      <div class="condition-item">
        <div class="condition-icon purple">⭐</div>
        <div class="condition-text">
          <div class="ct-title">Bônus CSAT é Cumulativo</div>
          <div class="ct-desc">O bônus de R$100 por CSAT <em>soma com a premiação de produtividade</em>, mas exige que o colaborador já tenha batido a meta de tickets e tenha zero faltas.</div>
        </div>
      </div>

      <div class="condition-item">
        <div class="condition-icon red">⚡</div>
        <div class="condition-text">
          <div class="ct-title">Qualidade Sempre</div>
          <div class="ct-desc">Apenas tickets <strong>corretamente resolvidos</strong> serão contabilizados. Fechamentos indevidos não entram na contagem.</div>
        </div>
      </div>
    </div>

    <!-- ── RULES GRID ── -->
    <div class="rules-grid">
      <div class="rule-card">
        <div class="rule-icon">🗓️</div>
        <div class="rule-title">Período</div>
        <div class="rule-desc">Válido durante todo o mês. A média é calculada considerando todos os dias úteis trabalhados.</div>
      </div>
      <div class="rule-card">
        <div class="rule-icon">🚫</div>
        <div class="rule-title">Zero Faltas</div>
        <div class="rule-desc">Qualquer ABS, falta ou ausência no mês elimina a participação de todas as premiações automaticamente.</div>
      </div>
      <div class="rule-card">
        <div class="rule-icon">🎯</div>
        <div class="rule-title">Três Premiações</div>
        <div class="rule-desc">Tier Ouro (R$100), Tier Prata (R$50) e Bônus CSAT (+R$100). Acumule para o máximo!</div>
      </div>
      <div class="rule-card">
        <div class="rule-icon">🏆</div>
        <div class="rule-title">Entrega</div>
        <div class="rule-desc">Cartão Smash + premiação entregues ao final do mês para quem bater as metas com presença total.</div>
      </div>
    </div>

    <!-- ── ALERT ── -->
    <div class="alert-box">
      <div class="alert-title">🚨 ATENÇÃO</div>
      <div class="alert-desc">
        Faltas, ABS ou ausências injustificadas durante o mês <strong style="color: var(--neon-red);">desclassificam automaticamente</strong> o colaborador de todas as premiações (produtividade + CSAT), independente das médias atingidas.
      </div>
    </div>

    <!-- ── TIP ── -->
    <div class="highlight-box">
      💡 <strong>Dica:</strong> Mire no combo máximo! Mantenha a produtividade alta, cuide da qualidade no atendimento para garantir o CSAT, e não falte nenhum dia. R$200 no final do mês é possível!
    </div>

    <!-- ── CTA ── -->
    <div class="cta-section">
      <div class="cta-text">Está pronto para o desafio?</div>
      <button class="cta-button">🚀 BORA SMASH!</button>
    </div>

    <div class="footer-note">
      Campanha válida para todos os integrantes do Time N1.<br>
      Contabilização baseada nos relatórios diários de tickets + CSAT mensal.<br>
      Backlogs resolvidos são somados à contagem geral do dia.<br>
      Bônus CSAT exige meta de produtividade batida + zero faltas/ABS.<br>
      Colaboradores com qualquer tipo de falta são automaticamente desclassificados de todas as premiações.<br>
      © 2026 — Smash Challenge N1
    </div>

  </div>
</div>

</body>
</html>
