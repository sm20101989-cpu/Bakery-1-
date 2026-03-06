<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
<title>Grammar Catcher 🥐</title>
<link href="https://fonts.googleapis.com/css2?family=Fredoka+One&family=Nunito:wght@800&display=swap" rel="stylesheet">
<style>
  * { margin:0; padding:0; box-sizing:border-box; }
  body {
    background: linear-gradient(135deg, #2b1a0e 0%, #1a0f08 100%);
    display:flex; align-items:center; justify-content:center;
    height:100vh; overflow:hidden;
    font-family:'Nunito',sans-serif;
    user-select:none;
    touch-action: none;
  }
  #gameCanvas {
    display:block;
    border-radius:18px;
    box-shadow:0 10px 60px rgba(0,0,0,0.6), 0 0 0 8px rgba(200,130,60,0.15);
    touch-action:none;
    cursor:none;
    max-width: 100vw;
    max-height: 100vh;
  }
</style>
</head>
<body>
<canvas id="gameCanvas"></canvas>
<script>
/**
 * GRAMMAR BAKERY - Образовательная игра
 * Улучшенная версия с оптимизацией и комментариями
 */

const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');
const W = 480, H = 640;
canvas.width = W; canvas.height = H;

// ========== НАСТРОЙКИ ИГРЫ ==========
const CONFIG = {
  basketWidth: 90,
  basketHeight: 38,
  basketY: H - 100,
  maxWords: 5,
  spawnInterval: 1050,
  baseSpeed: 1.7,
  levelTime: 60,
  targetScore: 10
};

// ========== УРОВНИ ==========
const LEVELS = [
  {
    label: '🥐  She  ___',
    color: '#e07b39',
    name: 'Level 1 — Catch verbs with -s / -es',
    hint: 'Catch croissants with -s / -es !',
    correct: ['likes','plays','watches','goes','studies','reads','runs','dances','sings','teaches','fixes','tries'],
    wrong: ['like', 'play', 'watch', 'go', 'study', 'read', 'run', 'dance', 'sing', 'teach', 'fix', 'try']
  },
  {
    label: "🥐  She doesn't  ___",
    color: '#c0392b',
    name: "Level 2 — Catch base form verbs",
    hint: "Catch croissants WITHOUT -s !",
    correct: ['like', 'play', 'watch', 'go', 'study', 'read', 'run', 'dance', 'sing', 'teach', 'fix', 'try'],
    wrong: ['likes','plays','watches','goes','studies','reads','runs','dances','sings','teaches','fixes','tries']
  }
];

// ========== СОСТОЯНИЕ ИГРЫ ==========
let state = 'START';
let currentLevel = 0;
let lives = 3;
let score = 0;
let caught = 0;
let streak = 0;
let bestStreak = 0;
let totalOk = 0;
let totalBad = 0;
let timer = 60;
let basketX = W/2 - CONFIG.basketWidth/2;
let mouseX = W/2;
let keyLeft = false;
let keyRight = false;
let words = [];
let pool = [];
let poolIndex = 0;
let timerInterval = null;
let spawnInterval = null;
let rafId = null;
let flashTimer = 0;
let shakeTimer = 0;
let particles = [];
let floats = [];
let countdownNum = 3;
let savedStats = {};
let buttons = {};
let lastTime = 0;

// ========== ЗАМЕНИТЕ ПЕРСОНАЖА ЗДЕСЬ ==========
const PLAYER_CHARACTER = '🧒'; // ← Измените на нужного персонажа (например: '👨‍🍳', '', '', '🤖')

// ========== УТИЛИТЫ ==========
function shuffle(array) {
  const arr = [...array];
  for (let i = arr.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [arr[i], arr[j]] = [arr[j], arr[i]];
  }
  return arr;
}

function roundRect(ctx, x, y, w, h, r) {
  ctx.beginPath();
  ctx.moveTo(x + r, y);
  ctx.lineTo(x + w - r, y);
  ctx.arcTo(x + w, y, x + w, y + r, r);
  ctx.lineTo(x + w, y + h - r);
  ctx.arcTo(x + w, y + h, x + w - r, y + h, r);
  ctx.lineTo(x + r, y + h);
  ctx.arcTo(x, y + h, x, y + h - r, r);
  ctx.lineTo(x, y + r);
  ctx.arcTo(x, y, x + r, y, r);
  ctx.closePath();
}

function resize() {
  const scale = Math.min(window.innerWidth / W, window.innerHeight / H, 1);
  canvas.style.width = (W * scale) + 'px';
  canvas.style.height = (H * scale) + 'px';
}

// ========== ПУЛ СЛОВ ==========
function buildWordPool() {
  const level = LEVELS[currentLevel];
  const correct = shuffle([...level.correct]);
  const wrong = shuffle([...level.wrong]);
  const pool = [];
  
  for (let i = 0; i < 9; i++) {
    pool.push({ text: correct[i % correct.length], ok: true });
  }
  for (let i = 0; i < 6; i++) {
    pool.push({ text: wrong[i % wrong.length], ok: false });
  }
  
  return shuffle(pool);
}

function getNextWord() {
  if (poolIndex >= pool.length) {
    pool = buildWordPool();
    poolIndex = 0;
  }
  return pool[poolIndex++];
}

// ========== СПАВН СЛОВ ==========
function measureTextWidth(text) {
  ctx.font = 'bold 15px Nunito,sans-serif';
  return ctx.measureText(text).width + 36;
}

function spawnWord() {
  if (words.length >= CONFIG.maxWords) return;
  
  const item = getNextWord();
  const width = measureTextWidth(item.text);
  const x = 12 + Math.random() * (W - width - 24);
  const speed = CONFIG.baseSpeed + (currentLevel * 0.5) + Math.random() * 0.8;
  
  words.push({
    text: item.text,
    ok: item.ok,
    x: x,
    y: -50,
    w: width,
    h: 42,
    speed: speed,
    angle: 0,
    spin: (Math.random() - 0.5) * 0.03
  });
}

// ========== ОТРИСОВКА ФОНА ==========
function drawBackground() {
  // Стена с градиентом
  const wallGradient = ctx.createLinearGradient(0, 0, 0, H);
  wallGradient.addColorStop(0, '#3b2010');
  wallGradient.addColorStop(0.55, '#4a2a14');
  wallGradient.addColorStop(1, '#2d1a0a');
  ctx.fillStyle = wallGradient;
  ctx.fillRect(0, 0, W, H);

  // Кирпичная кладка
  ctx.save();
  ctx.globalAlpha = 0.18;
  const brickW = 52, brickH = 22;
  for (let row = 0; row < Math.ceil(H / brickH) + 1; row++) {
    const offset = row % 2 === 0 ? 0 : brickW / 2;
    ctx.fillStyle = '#c87941';
    for (let col = -1; col < Math.ceil(W / brickW) + 1; col++) {
      const bx = col * brickW + offset;
      const by = row * brickH;
      ctx.fillRect(bx + 1, by + 1, brickW - 2, brickH - 2);
    }
  }
  ctx.globalAlpha = 1;
  ctx.restore();

  // Окно-печь с подсветкой
  drawOvenWindow();
  
  // Полки
  drawShelf(10, 220, 120);
  drawShelf(350, 220, 120);
  
  // Еда на полках
  drawBreadItem(22, 207, '🍞');
  drawBreadItem(64, 207, '🥖');
  drawBreadItem(362, 207, '🧁');
  drawBreadItem(404, 207, '🍰');

  // Стойка и пол
  drawCounter();
  
  // Подвесные светильники
  drawLight(80, 0, 160);
  drawLight(W/2, 0, 155);
  drawLight(W-80, 0, 162);

  // Вывеска
  drawSign();
}

function drawOvenWindow() {
  ctx.save();
  ctx.shadowColor = '#f59a23';
  ctx.shadowBlur = 40;
  
  const archX = W/2 - 70, archW = 140, archH = 120;
  const archY = 80;
  
  ctx.fillStyle = '#ffeaa0';
  ctx.beginPath();
  ctx.arc(W/2, archY + archH/2, archW/2, Math.PI, 0);
  ctx.rect(archX, archY + archH/2, archW, archH/2);
  ctx.fill();
  ctx.shadowBlur = 0;
  
  // Шторы
  ctx.fillStyle = '#c0392b';
  ctx.fillRect(archX - 5, archY, 18, archH + 5);
  ctx.fillRect(archX + archW - 13, archY, 18, archH + 5);
  ctx.restore();

  // Свечение от окна
  const glow = ctx.createRadialGradient(W/2, archY + archH, 5, W/2, archY + archH, 200);
  glow.addColorStop(0, 'rgba(255,200,80,0.22)');
  glow.addColorStop(1, 'rgba(255,200,80,0)');
  ctx.fillStyle = glow;
  ctx.fillRect(0, 0, W, H);
}

function drawShelf(x, y, w) {
  ctx.fillStyle = '#5a2d0c';
  ctx.fillRect(x, y, w, 12);
  ctx.fillStyle = 'rgba(255,200,100,.13)';
  ctx.fillRect(x, y, w, 3);
  
  ctx.fillStyle = '#4a2408';
  ctx.fillRect(x + 6, y, 8, 22);
  ctx.fillRect(x + w - 14, y, 8, 22);
}

function drawBreadItem(x, y, emoji) {
  ctx.font = '26px serif';
  ctx.textAlign = 'center';
  ctx.shadowColor = 'rgba(0,0,0,.3)';
  ctx.shadowBlur = 4;
  ctx.fillText(emoji, x, y);
  ctx.shadowBlur = 0;
}

function drawLight(x, y, len) {
  ctx.strokeStyle = '#4a2408';
  ctx.lineWidth = 2;
  ctx.beginPath();
  ctx.moveTo(x, y);
  ctx.lineTo(x, len);
  ctx.stroke();
  
  ctx.save();
  ctx.shadowColor = '#fff3a0';
  ctx.shadowBlur = 22;
  ctx.fillStyle = '#fff9c4';
  ctx.beginPath();
  ctx.arc(x, len, 7, 0, Math.PI * 2);
  ctx.fill();
  ctx.shadowBlur = 0;
  
  const coneH = 60;
  const cone = ctx.createRadialGradient(x, len, 2, x, len, coneH);
  cone.addColorStop(0, 'rgba(255,240,160,0.28)');
  cone.addColorStop(1, 'rgba(255,240,160,0)');
  ctx.fillStyle = cone;
  ctx.beginPath();
  ctx.moveTo(x, len);
  ctx.arc(x, len, coneH, 0.45 * Math.PI, 0.55 * Math.PI);
  ctx.fill();
  ctx.restore();
}

function drawCounter() {
  ctx.fillStyle = '#6b3a1f';
  ctx.fillRect(0, H - 90, W, 90);
  
  const cTop = ctx.createLinearGradient(0, H - 90, 0, H - 74);
  cTop.addColorStop(0, '#a0531e');
  cTop.addColorStop(1, '#6b3a1f');
  ctx.fillStyle = cTop;
  ctx.fillRect(0, H - 90, W, 16);
  
  ctx.fillStyle = 'rgba(255,200,100,.18)';
  ctx.fillRect(0, H - 91, W, 3);
  
  ctx.save();
  ctx.globalAlpha = 0.12;
  ctx.fillStyle = '#f5c57a';
  for (let c = 0; c < W; c += 40) {
    for (let r = H - 88; r < H; r += 38) {
      ctx.fillRect(c + 1, r + 1, 38, 36);
    }
  }
  ctx.globalAlpha = 1;
  ctx.restore();
}

function drawSign() {
  ctx.save();
  ctx.fillStyle = 'rgba(60,20,0,0.7)';
  roundRect(ctx, W/2 - 90, 16, 180, 32, 8);
  ctx.fill();
  
  ctx.strokeStyle = '#f5a623';
  ctx.lineWidth = 2;
  roundRect(ctx, W/2 - 90, 16, 180, 32, 8);
  ctx.stroke();
  
  ctx.font = 'bold 15px "Fredoka One",cursive';
  ctx.fillStyle = '#ffd700';
  ctx.textAlign = 'center';
  ctx.shadowColor = '#f59a23';
  ctx.shadowBlur = 8;
  ctx.fillText('🥐  Grammar Bakery  🥐', W/2, 37);
  ctx.shadowBlur = 0;
  ctx.textAlign = 'left';
  ctx.restore();
}

// ========== КРУАССАН СЛОВА ==========
function drawCroissantWord(word) {
  ctx.save();
  const cx = word.x + word.w / 2;
  const cy = word.y + word.h / 2;
  ctx.translate(cx, cy);
  ctx.rotate(word.angle);

  // Тень
  ctx.shadowColor = 'rgba(0,0,0,.35)';
  ctx.shadowBlur = 8;

  // Тело круассана
  const cg = ctx.createLinearGradient(-word.w/2, -word.h/2, word.w/2, word.h/2);
  cg.addColorStop(0, '#f5c842');
  cg.addColorStop(0.4, '#e8a020');
  cg.addColorStop(1, '#c47a15');
  ctx.fillStyle = cg;
  ctx.beginPath();
  ctx.ellipse(0, 0, word.w/2, word.h/2, 0, 0, Math.PI * 2);
  ctx.fill();
  ctx.shadowBlur = 0;

  // Рога круассана
  ctx.fillStyle = '#d4860e';
  ctx.beginPath();
  ctx.ellipse(-word.w/2 + 8, 0, 10, word.h/2 - 4, 0.3, 0, Math.PI * 2);
  ctx.fill();
  ctx.beginPath();
  ctx.ellipse(word.w/2 - 8, 0, 10, word.h/2 - 4, -0.3, 0, Math.PI * 2);
  ctx.fill();

  // Блеск глазури
  ctx.fillStyle = 'rgba(255,230,100,.35)';
  ctx.beginPath();
  ctx.ellipse(-word.w/8, -word.h/5, word.w/5, word.h/6, -0.3, 0, Math.PI * 2);
  ctx.fill();

  // Насечки
  ctx.strokeStyle = 'rgba(150,70,0,.4)';
  ctx.lineWidth = 1;
  for (let i = -1; i <= 1; i++) {
    ctx.beginPath();
    ctx.moveTo(i * word.w/6 - 6, -word.h/3);
    ctx.lineTo(i * word.w/6 + 6, word.h/3);
    ctx.stroke();
  }

  // Текст
  ctx.font = 'bold 15px Nunito,sans-serif';
  ctx.fillStyle = '#3b1a00';
  ctx.shadowColor = 'rgba(255,200,80,.6)';
  ctx.shadowBlur = 4;
  ctx.textAlign = 'center';
  ctx.fillText(word.text, 0, 5);
  ctx.shadowBlur = 0;

  ctx.restore();
}

// ========== КОРЗИНА С ПЕРСОНАЖЕМ ==========
function drawBasket() {
  const x = basketX;
  const y = CONFIG.basketY;
  const bob = Math.sin(Date.now() * 0.005) * 3;

  // === ПЕРСОНАЖ (ЗАМЕНИТЕ ЗДЕСЬ) ===
  ctx.font = '34px serif';
  ctx.textAlign = 'center';
  ctx.shadowColor = 'rgba(0,0,0,.4)';
  ctx.shadowBlur = 6;
  ctx.fillText(PLAYER_CHARACTER, x + CONFIG.basketWidth/2, y - 14 + bob);
  ctx.shadowBlur = 0;

  // Корзина
  ctx.save();
  ctx.beginPath();
  ctx.moveTo(x + 6, y + 2);
  ctx.lineTo(x + CONFIG.basketWidth - 6, y + 2);
  ctx.lineTo(x + CONFIG.basketWidth - 14, y + CONFIG.basketHeight + 8);
  ctx.lineTo(x + 14, y + CONFIG.basketHeight + 8);
  ctx.closePath();
  
  const bg = ctx.createLinearGradient(0, y, 0, y + CONFIG.basketHeight + 8);
  bg.addColorStop(0, '#c87941');
  bg.addColorStop(1, '#8b4513');
  ctx.fillStyle = bg;
  ctx.shadowColor = 'rgba(0,0,0,.3)';
  ctx.shadowBlur = 8;
  ctx.fill();
  ctx.shadowBlur = 0;
  
  // Плетение
  ctx.strokeStyle = 'rgba(0,0,0,.18)';
  ctx.lineWidth = 1;
  for (let i = 8; i < CONFIG.basketWidth - 8; i += 10) {
    ctx.beginPath();
    ctx.moveTo(x + i, y + 2);
    ctx.lineTo(x + i, y + CONFIG.basketHeight + 8);
    ctx.stroke();
  }
  for (let j = 8; j < CONFIG.basketHeight + 6; j += 8) {
    ctx.beginPath();
    ctx.moveTo(x + 6, y + j);
    ctx.lineTo(x + CONFIG.basketWidth - 6, y + j);
    ctx.stroke();
  }
  ctx.restore();

  // Ободок
  const rimG = ctx.createLinearGradient(0, y, 0, y + 12);
  rimG.addColorStop(0, '#e8a020');
  rimG.addColorStop(1, '#c87941');
  ctx.fillStyle = rimG;
  ctx.shadowColor = 'rgba(0,0,0,.25)';
  ctx.shadowBlur = 5;
  roundRect(ctx, x, y, CONFIG.basketWidth, 12, 6);
  ctx.fill();
  ctx.shadowBlur = 0;

  // Эффект вспышки
  if (flashTimer > 0) {
    ctx.globalAlpha = Math.min(flashTimer / 10, 0.5);
    ctx.fillStyle = '#00e676';
    roundRect(ctx, x, y, CONFIG.basketWidth, CONFIG.basketHeight + 12, 6);
    ctx.fill();
    ctx.globalAlpha = 1;
  }
  if (flashTimer < 0) {
    ctx.globalAlpha = Math.min(-flashTimer / 10, 0.5);
    ctx.fillStyle = '#ff1744';
    roundRect(ctx, x, y, CONFIG.basketWidth, CONFIG.basketHeight + 12, 6);
    ctx.fill();
    ctx.globalAlpha = 1;
  }

  // Подсказка уровня
  const level = LEVELS[currentLevel];
  ctx.font = 'bold 13px "Fredoka One",cursive';
  const lw = ctx.measureText(level.label).width + 20;
  const lx = Math.max(4, Math.min(W - lw - 4, x + CONFIG.basketWidth/2 - lw/2));
  const ly = y - 46;
  
  ctx.shadowColor = 'rgba(0,0,0,.3)';
  ctx.shadowBlur = 6;
  ctx.fillStyle = 'rgba(255,240,200,.95)';
  roundRect(ctx, lx, ly, lw, 24, 12);
  ctx.fill();
  ctx.shadowBlur = 0;
  
  ctx.fillStyle = '#4a1800';
  ctx.textAlign = 'center';
  ctx.fillText(level.label, lx + lw/2, ly + 16);
  ctx.textAlign = 'left';
}

// ========== HUD ==========
function drawHUD() {
  // Верхняя панель
  ctx.fillStyle = 'rgba(30,10,0,.65)';
  ctx.fillRect(0, 0, W, 48);
  ctx.strokeStyle = 'rgba(200,120,40,.4)';
  ctx.lineWidth = 1;
  ctx.beginPath();
  ctx.moveTo(0, 48);
  ctx.lineTo(W, 48);
  ctx.stroke();

  // Жизни
  ctx.font = '20px serif';
  for (let i = 0; i < 3; i++) {
    ctx.globalAlpha = i < lives ? 1 : 0.22;
    ctx.fillText('❤️', 8 + i * 26, 32);
  }
  ctx.globalAlpha = 1;

  // Счет и время
  ctx.font = 'bold 16px "Fredoka One",cursive';
  ctx.shadowColor = 'rgba(0,0,0,.6)';
  ctx.shadowBlur = 4;
  ctx.fillStyle = '#ffd700';
  ctx.textAlign = 'center';
  ctx.fillText('⭐ ' + score, W/2, 30);
  
  ctx.textAlign = 'right';
  ctx.fillStyle = timer <= 10 ? '#ff6b6b' : '#ffd700';
  ctx.fillText('⏱ ' + timer, W - 56, 30);
  ctx.fillStyle = '#ffd700';
  ctx.fillText('🥐 ' + caught + '/10', W - 1, 30);
  ctx.textAlign = 'left';
  ctx.shadowBlur = 0;

  // Название уровня
  const level = LEVELS[currentLevel];
  ctx.font = 'bold 12px Nunito,sans-serif';
  const nw = ctx.measureText(level.name).width + 22;
  const nx = (W - nw) / 2;
  ctx.fillStyle = level.color + 'cc';
  roundRect(ctx, nx, 50, nw, 20, 10);
  ctx.fill();
  
  ctx.fillStyle = '#fff';
  ctx.textAlign = 'center';
  ctx.shadowColor = 'rgba(0,0,0,.4)';
  ctx.shadowBlur = 3;
  ctx.fillText(level.name, W/2, 64);
  ctx.textAlign = 'left';
  ctx.shadowBlur = 0;

  // Прогресс бар
  ctx.fillStyle = 'rgba(255,255,255,.15)';
  roundRect(ctx, 14, 73, W - 28, 7, 4);
  ctx.fill();
  
  if (caught > 0) {
    const pg = ctx.createLinearGradient(14, 0, 14 + (W - 28) * (caught/10), 0);
    pg.addColorStop(0, '#ffd700');
    pg.addColorStop(1, '#e07b39');
    roundRect(ctx, 14, 73, Math.max(8, (W - 28) * caught/10), 7, 4);
    ctx.fillStyle = pg;
    ctx.fill();
  }

  // Серия
  if (streak >= 2) {
    ctx.font = 'bold 13px "Fredoka One",cursive';
    const sw = ctx.measureText('🔥 x' + streak).width + 18;
    ctx.fillStyle = '#e07b39';
    roundRect(ctx, W - sw - 8, 82, sw, 20, 10);
    ctx.fill();
    ctx.fillStyle = '#fff';
    ctx.textAlign = 'right';
    ctx.fillText('🔥 x' + streak, W - 10, 96);
    ctx.textAlign = 'left';
  }
}

// ========== ЭФФЕКТЫ ==========
function burst(x, y, color) {
  for (let i = 0; i < 18; i++) {
    const angle = Math.random() * Math.PI * 2;
    const speed = 2.5 + Math.random() * 5;
    particles.push({
      x: x,
      y: y,
      vx: Math.cos(angle) * speed,
      vy: Math.sin(angle) * speed - 2,
      r: 3 + Math.random() * 5,
      alpha: 1,
      color: color
    });
  }
}

function addFloat(text, color, x, y) {
  floats.push({ text, color, x, y, vy: -1.8, alpha: 1 });
}

function updateParticles() {
  particles.forEach(p => {
    p.x += p.vx;
    p.y += p.vy;
    p.vy += 0.18;
    p.alpha -= 0.028;
    p.r *= 0.97;
  });
  particles = particles.filter(p => p.alpha > 0);
}

function drawParticles() {
  particles.forEach(p => {
    ctx.globalAlpha = Math.max(0, p.alpha);
    ctx.fillStyle = p.color;
    ctx.beginPath();
    ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
    ctx.fill();
  });
  ctx.globalAlpha = 1;
}

function updateFloats() {
  floats.forEach(f => {
    f.y += f.vy;
    f.alpha -= 0.024;
  });
  floats = floats.filter(f => f.alpha > 0);
}

function drawFloats() {
  floats.forEach(f => {
    ctx.globalAlpha = f.alpha;
    ctx.font = 'bold 22px "Fredoka One",cursive';
    ctx.shadowColor = 'rgba(0,0,0,.4)';
    ctx.shadowBlur = 4;
    ctx.fillStyle = f.color;
    ctx.textAlign = 'center';
    ctx.fillText(f.text, f.x, f.y);
  });
  ctx.globalAlpha = 1;
  ctx.shadowBlur = 0;
  ctx.textAlign = 'left';
}

// ========== ЭКРАНЫ ==========
function drawButton(x, y, w, h, label, c1, c2, textColor, id) {
  const g = ctx.createLinearGradient(x, y, x + w, y + h);
  g.addColorStop(0, c1);
  g.addColorStop(1, c2);
  
  ctx.shadowColor = 'rgba(0,0,0,.4)';
  ctx.shadowBlur = 10;
  roundRect(ctx, x, y, w, h, h/2);
  ctx.fillStyle = g;
  ctx.fill();
  ctx.shadowBlur = 0;
  
  ctx.font = 'bold 18px "Fredoka One",cursive';
  ctx.fillStyle = textColor;
  ctx.textAlign = 'center';
  ctx.fillText(label, x + w/2, y + h/2 + 6);
  ctx.textAlign = 'left';
  
  if (id) buttons[id] = { x, y, w, h };
}

function drawStatBox(stats) {
  const sx = 44, sy = 218, sw = W - 88;
  const rows = Object.entries(stats).filter(([,v]) => v !== '');
  const sh = rows.length * 46 + 16;
  
  ctx.fillStyle = 'rgba(255,230,180,.12)';
  roundRect(ctx, sx, sy, sw, sh, 16);
  ctx.fill();
  
  ctx.strokeStyle = 'rgba(200,140,40,.3)';
  ctx.lineWidth = 1.5;
  roundRect(ctx, sx, sy, sw, sh, 16);
  ctx.stroke();
  
  let iy = sy + 40;
  rows.forEach(([k, v]) => {
    ctx.font = 'bold 14px Nunito,sans-serif';
    ctx.fillStyle = 'rgba(255,220,160,.8)';
    ctx.textAlign = 'left';
    ctx.fillText(k, sx + 18, iy);
    
    ctx.font = 'bold 20px "Fredoka One",cursive';
    ctx.fillStyle = '#ffd700';
    ctx.textAlign = 'right';
    ctx.fillText(v, sx + sw - 18, iy);
    
    ctx.strokeStyle = 'rgba(200,140,40,.15)';
    ctx.lineWidth = 1;
    ctx.beginPath();
    ctx.moveTo(sx + 14, iy + 8);
    ctx.lineTo(sx + sw - 14, iy + 8);
    ctx.stroke();
    
    iy += 46;
  });
  ctx.textAlign = 'left';
}

function drawStartScreen() {
  ctx.save();
  ctx.fillStyle = 'rgba(20,8,2,.82)';
  ctx.fillRect(0, 0, W, H);
  
  const vg = ctx.createRadialGradient(W/2, H/2, 80, W/2, H/2, 320);
  vg.addColorStop(0, 'rgba(180,80,10,.18)');
  vg.addColorStop(1, 'rgba(0,0,0,0)');
  ctx.fillStyle = vg;
  ctx.fillRect(0, 0, W, H);
  ctx.restore();

  ctx.font = '52px serif';
  ctx.textAlign = 'center';
  ctx.shadowColor = '#f59a23';
  ctx.shadowBlur = 20;
  ctx.fillText('🥐', W/2, 100);
  ctx.shadowBlur = 0;

  ctx.font = 'bold 46px "Fredoka One",cursive';
  ctx.fillStyle = '#ffd700';
  ctx.shadowColor = 'rgba(0,0,0,.7)';
  ctx.shadowBlur = 12;
  ctx.fillText('Grammar', W/2, 160);
  ctx.fillText('Bakery!', W/2, 212);
  ctx.shadowBlur = 0;

  ctx.font = 'bold 14px Nunito,sans-serif';
  ctx.fillStyle = 'rgba(255,220,160,.9)';
  ctx.fillText('Catch the right croissants 🥐', W/2, 248);
  ctx.fillText('and become a Grammar Master! 🌟', W/2, 268);

  const cards = [
    ['🟢', 'Level 1 — She ___', 'Catch verbs with -s / -es'],
    ['🟡', "Level 2 — She doesn't ___", 'Catch base form verbs (no -s)']
  ];
  
  cards.forEach(([icon, title, desc], i) => {
    const cy = 295 + i * 80;
    ctx.fillStyle = 'rgba(200,130,40,.18)';
    roundRect(ctx, 36, cy, W - 72, 66, 14);
    ctx.fill();
    
    ctx.strokeStyle = 'rgba(200,140,40,.35)';
    ctx.lineWidth = 1.5;
    roundRect(ctx, 36, cy, W - 72, 66, 14);
    ctx.stroke();
    
    ctx.font = '26px serif';
    ctx.fillText(icon, 66, cy + 38);
    
    ctx.font = 'bold 15px Nunito,sans-serif';
    ctx.fillStyle = '#ffd700';
    ctx.fillText(title, 100, cy + 28);
    
    ctx.font = '13px Nunito,sans-serif';
    ctx.fillStyle = 'rgba(255,200,120,.8)';
    ctx.fillText(desc, 100, cy + 50);
  });

  drawButton(W/2 - 100, 482, 200, 54, '▶  Play Now!', '#e07b39', '#c0392b', '#fff', 'PLAY');
  ctx.textAlign = 'left';
}

function drawCountdownScreen() {
  ctx.fillStyle = 'rgba(20,8,2,.78)';
  ctx.fillRect(0, 0, W, H);
  
  ctx.font = '110px "Fredoka One",cursive';
  ctx.textAlign = 'center';
  ctx.shadowColor = '#f5a623';
  ctx.shadowBlur = 40;
  ctx.fillStyle = '#ffd700';
  ctx.fillText(countdownNum === 0 ? 'GO!' : countdownNum, W/2, H/2 + 20);
  ctx.shadowBlur = 0;
  
  ctx.font = 'bold 19px "Fredoka One",cursive';
  ctx.fillStyle = 'rgba(255,200,120,.9)';
  ctx.fillText(LEVELS[currentLevel].hint, W/2, H/2 + 75);
  ctx.textAlign = 'left';
}

function drawLevelClearScreen() {
  ctx.fillStyle = 'rgba(10,30,10,.86)';
  ctx.fillRect(0, 0, W, H);
  
  ctx.font = '62px serif';
  ctx.textAlign = 'center';
  ctx.fillText('🎉', W/2, 110);
  
  ctx.font = 'bold 48px "Fredoka One",cursive';
  ctx.fillStyle = '#ffd700';
  ctx.shadowColor = '#0008';
  ctx.shadowBlur = 10;
  ctx.fillText('Level Clear!', W/2, 170);
  ctx.shadowBlur = 0;
  
  drawStatBox(savedStats);
  
  const nextText = currentLevel + 1 >= LEVELS.length ? '🏆  Finish!' : 'Next Level  ➡';
  drawButton(W/2 - 100, 500, 200, 52, nextText, '#e07b39', '#c0392b', '#fff', 'NEXT');
  ctx.textAlign = 'left';
}

function drawGameOverScreen() {
  ctx.fillStyle = 'rgba(30,5,5,.88)';
  ctx.fillRect(0, 0, W, H);
  
  ctx.font = '62px serif';
  ctx.textAlign = 'center';
  ctx.fillText('😢', W/2, 110);
  
  ctx.font = 'bold 48px "Fredoka One",cursive';
  ctx.fillStyle = '#ff6b6b';
  ctx.shadowColor = '#0008';
  ctx.shadowBlur = 10;
  ctx.fillText('Game Over', W/2, 170);
  ctx.shadowBlur = 0;
  
  drawStatBox(savedStats);
  drawButton(W/2 - 110, 490, 220, 50, '🔄  Try Again', '#e07b39', '#c0392b', '#fff', 'RETRY');
  drawButton(W/2 - 65, 552, 130, 44, '🏠  Menu', 'rgba(255,200,100,.2)', 'rgba(255,200,100,.2)', '#ffd700', 'MENU');
  ctx.textAlign = 'left';
}

function drawWinScreen() {
  ctx.fillStyle = 'rgba(5,20,5,.88)';
  ctx.fillRect(0, 0, W, H);
  
  ctx.font = '62px serif';
  ctx.textAlign = 'center';
  ctx.fillText('🏆', W/2, 100);
  
  ctx.font = 'bold 40px "Fredoka One",cursive';
  ctx.fillStyle = '#ffd700';
  ctx.shadowColor = '#0008';
  ctx.shadowBlur = 10;
  ctx.fillText('You are a', W/2, 158);
  ctx.fillText('Grammar Master!', W/2, 204);
  ctx.shadowBlur = 0;
  
  ctx.font = '28px serif';
  ctx.fillText('🥐 🥐 🥐', W/2, 235);
  
  drawStatBox(savedStats);
  drawButton(W/2 - 110, 495, 220, 50, '🎮  Play Again', '#e07b39', '#c0392b', '#fff', 'RETRY');
  drawButton(W/2 - 60, 555, 120, 42, '🏠 Menu', 'rgba(255,200,100,.2)', 'rgba(255,200,100,.2)', '#ffd700', 'MENU');
  ctx.textAlign = 'left';
}

// ========== ИГРОВАЯ ЛОГИКА ==========
function onCatch(word) {
  const fx = basketX + CONFIG.basketWidth/2;
  const fy = CONFIG.basketY - 30;
  
  if (word.ok) {
    score += 10;
    caught++;
    streak++;
    totalOk++;
    
    if (streak > bestStreak) bestStreak = streak;
    
    let msg = '+10 🥐';
    if (streak >= 5) {
      score += 20;
      msg = '🔥 +30!';
    }
    
    addFloat(msg, '#ffd700', fx, fy);
    burst(fx, CONFIG.basketY, '#ffd700');
    flashTimer = 12;
    
    if (caught >= CONFIG.targetScore) {
      clearIntervals();
      setTimeout(doLevelClear, 250);
      return;
    }
  } else {
    score = Math.max(0, score - 5);
    streak = 0;
    lives--;
    totalBad++;
    
    addFloat('-5 ✗', '#ff6b6b', fx, fy);
    burst(fx, CONFIG.basketY, '#ff1744');
    flashTimer = -12;
    shakeTimer = 16;
    
    if (lives <= 0) {
      clearIntervals();
      setTimeout(() => doEnd('lives'), 250);
      return;
    }
  }
}

function clearIntervals() {
  if (timerInterval) clearInterval(timerInterval);
  if (spawnInterval) clearInterval(spawnInterval);
  timerInterval = null;
  spawnInterval = null;
}

function startGame() {
  currentLevel = 0;
  score = 0;
  bestStreak = 0;
  totalOk = 0;
  totalBad = 0;
  beginLevel();
}

function beginLevel() {
  lives = 3;
  caught = 0;
  streak = 0;
  timer = CONFIG.levelTime;
  basketX = W/2 - CONFIG.basketWidth/2;
  mouseX = W/2;
  words = [];
  particles = [];
  floats = [];
  flashTimer = 0;
  shakeTimer = 0;
  pool = buildWordPool();
  poolIndex = 0;
  
  clearIntervals();
  state = 'COUNTDOWN';
  countdownNum = 3;
  
  let n = 3;
  const iv = setInterval(() => {
    n--;
    countdownNum = n;
    if (n < 0) {
      clearInterval(iv);
      state = 'PLAY';
      
      timerInterval = setInterval(() => {
        if (state !== 'PLAY') return;
        timer--;
        if (timer <= 0) {
          clearIntervals();
          doEnd('time');
        }
      }, 1000);
      
      spawnInterval = setInterval(() => {
        if (state === 'PLAY') spawnWord();
      }, CONFIG.spawnInterval);
    }
  }, 850);
}

function getAccuracyPercent() {
  const total = totalOk + totalBad;
  return total ? Math.round(totalOk / total * 100) : 0;
}

function doLevelClear() {
  state = 'LEVELCLEAR';
  savedStats = {
    'Score': '⭐ ' + score,
    'Accuracy': getAccuracyPercent() + '%',
    'Best Streak': '🔥 ' + bestStreak,
    'Time Left': '⏱ ' + timer + 's'
  };
}

function doNextLevel() {
  currentLevel++;
  if (currentLevel >= LEVELS.length) {
    doWin();
    return;
  }
  beginLevel();
}

function doEnd(reason) {
  state = 'GAMEOVER';
  const reasonText = reason === 'time' ? '⏰ Time\'s up!' : '💔 No lives!';
  savedStats = {
    [reasonText]: '',
    'Score': '⭐ ' + score,
    'Accuracy': getAccuracyPercent() + '%',
    'Best Streak': '🔥 ' + bestStreak
  };
}

function doWin() {
  state = 'WIN';
  savedStats = {
    'Total Score': '⭐ ' + score,
    'Accuracy': getAccuracyPercent() + '%',
    'Best Streak': '🔥 ' + bestStreak,
    'Correct Catches': '✅ ' + totalOk
  };
}

function showStart() {
  clearIntervals();
  state = 'START';
  words = [];
}

// ========== ОБРАБОТКА ВВОДА ==========
function hitTest(cx, cy, button) {
  return button && cx >= button.x && cx <= button.x + button.w && 
         cy >= button.y && cy <= button.y + button.h;
}

function handleClick(cx, cy) {
  if (state === 'START' && hitTest(cx, cy, buttons['PLAY'])) {
    startGame();
    return;
  }
  if (state === 'LEVELCLEAR' && hitTest(cx, cy, buttons['NEXT'])) {
    doNextLevel();
    return;
  }
  if (state === 'GAMEOVER') {
    if (hitTest(cx, cy, buttons['RETRY'])) {
      startGame();
      return;
    }
    if (hitTest(cx, cy, buttons['MENU'])) {
      showStart();
      return;
    }
  }
  if (state === 'WIN') {
    if (hitTest(cx, cy, buttons['RETRY'])) {
      startGame();
      return;
    }
    if (hitTest(cx, cy, buttons['MENU'])) {
      showStart();
      return;
    }
  }
}

// ========== ГЛАВНЫЙ ЦИКЛ ==========
function loop(timestamp) {
  rafId = requestAnimationFrame(loop);
  const dt = Math.min((timestamp - lastTime) / 16.67, 3);
  lastTime = timestamp;
  
  ctx.clearRect(0, 0, W, H);

  if (state === 'START') {
    drawBackground();
    drawStartScreen();
    return;
  }
  if (state === 'COUNTDOWN') {
    drawBackground();
    drawCountdownScreen();
    return;
  }
  if (state === 'LEVELCLEAR') {
    drawBackground();
    drawLevelClearScreen();
    return;
  }
  if (state === 'GAMEOVER') {
    drawBackground();
    drawGameOverScreen();
    return;
  }
  if (state === 'WIN') {
    drawBackground();
    drawWinScreen();
    return;
  }

  // PLAY STATE
  ctx.save();
  if (shakeTimer > 0) {
    ctx.translate((Math.random() - 0.5) * 10, (Math.random() - 0.5) * 10);
    shakeTimer--;
  }

  drawBackground();

  // Движение корзины
  if (keyLeft) basketX = Math.max(0, basketX - 5 * dt);
  if (keyRight) basketX = Math.min(W - CONFIG.basketWidth - 2, basketX + 5 * dt);
  
  const targetX = Math.max(0, Math.min(W - CONFIG.basketWidth - 2, mouseX - CONFIG.basketWidth/2));
  basketX += (targetX - basketX) * 0.18 * dt;

  // Зона ловли
  const cy1 = CONFIG.basketY + 2;
  const cy2 = CONFIG.basketY + 22;
  const cx1 = basketX + 6;
  const cx2 = basketX + CONFIG.basketWidth - 6;

  // Обновление слов
  for (let i = words.length - 1; i >= 0; i--) {
    const w = words[i];
    w.y += w.speed * dt;
    w.angle += w.spin;
    
    const bottom = w.y + w.h;
    const mid = w.x + w.w / 2;
    
    if (bottom >= cy1 && w.y <= cy2 && mid >= cx1 && mid <= cx2) {
      words.splice(i, 1);
      onCatch(w);
    } else if (w.y > H + 20) {
      words.splice(i, 1);
    }
  }

  if (flashTimer > 0) flashTimer = Math.max(0, flashTimer - 0.6);
  if (flashTimer < 0) flashTimer = Math.min(0, flashTimer + 0.6);
  
  updateParticles();
  updateFloats();

  words.forEach(w => drawCroissantWord(w));
  drawParticles();
  drawBasket();
  drawFloats();
  drawHUD();

  ctx.restore();
}

// ========== СОБЫТИЯ ==========
canvas.addEventListener('click', e => {
  const rect = canvas.getBoundingClientRect();
  handleClick(
    (e.clientX - rect.left) * (W / rect.width),
    (e.clientY - rect.top) * (H / rect.height)
  );
});

canvas.addEventListener('touchend', e => {
  const rect = canvas.getBoundingClientRect();
  const t = e.changedTouches[0];
  handleClick(
    (t.clientX - rect.left) * (W / rect.width),
    (t.clientY - rect.top) * (H / rect.height)
  );
});

window.addEventListener('keydown', e => {
  if (e.code === 'ArrowLeft' || e.code === 'KeyA') keyLeft = true;
  if (e.code === 'ArrowRight' || e.code === 'KeyD') keyRight = true;
  if (['ArrowLeft', 'ArrowRight', 'ArrowUp', 'ArrowDown', 'Space'].includes(e.code)) {
    e.preventDefault();
  }
});

window.addEventListener('keyup', e => {
  if (e.code === 'ArrowLeft' || e.code === 'KeyA') keyLeft = false;
  if (e.code === 'ArrowRight' || e.code === 'KeyD') keyRight = false;
});

canvas.addEventListener('mousemove', e => {
  const rect = canvas.getBoundingClientRect();
  mouseX = (e.clientX - rect.left) * (W / rect.width);
});

canvas.addEventListener('touchmove', e => {
  e.preventDefault();
  const rect = canvas.getBoundingClientRect();
  mouseX = (e.touches[0].clientX - rect.left) * (W / rect.width);
}, { passive: false });

canvas.addEventListener('touchstart', e => {
  const rect = canvas.getBoundingClientRect();
  mouseX = (e.touches[0].clientX - rect.left) * (W / rect.width);
}, { passive: true });

// ========== ИНИЦИАЛИЗАЦИЯ ==========
resize();
window.addEventListener('resize', resize);
requestAnimationFrame(loop);
</script>
</body>
</html>
