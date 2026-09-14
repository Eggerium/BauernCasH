index.html
#BauernCasH
<!doctype html>
<html lang="de">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<meta name="theme-color" content="#0a7a45" media="(prefers-color-scheme: light)">
<meta name="theme-color" content="#064a2a" media="(prefers-color-scheme: dark)">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<meta name="description" content="EGGERIUM — QR scannen, BCH bezahlen, fertig. Keine Formulare.">
<link rel="manifest" href='data:application/manifest+json,{"name":"EGGERIUM","short_name":"EGGERIUM","start_url":".","scope":".","display":"standalone","orientation":"portrait","background_color":"%23f3f7f4","theme_color":"%230a7a45","lang":"de","icons":[]}'>
<title>EGGERIUM — SCAN → PAY → FERTIG</title>
<style>
:root{
  --g:#087a43;--g2:#10a65d;--bg:#f3f7f4;--card:#fff;--ink:#10251b;
  --muted:#5a6b62;--line:#dce7e0;--gold:#e8b949;--danger:#b3261e;--ok:#087a43;
  --radius:22px;--radius-sm:14px;
}
@media (prefers-color-scheme:dark){
  :root{
    --bg:#0a130e;--card:#12211a;--ink:#e8f2ec;--muted:#9aaca2;
    --line:#1e332a;--g:#0e8f50;--g2:#13b968;
  }
}
*{box-sizing:border-box}
html{-webkit-text-size-adjust:100%}
body{
  margin:0;background:var(--bg);color:var(--ink);
  font-family:system-ui,-apple-system,"Segoe UI",Roboto,sans-serif;
  min-height:100dvh;line-height:1.4;
}
header{
  color:#fff;background:linear-gradient(145deg,var(--g),var(--g2));
  padding:28px 18px 24px;border-radius:0 0 30px 30px;
}
h1{margin:0;font-size:32px;letter-spacing:-.04em;font-weight:950}
header p{margin:5px 0 0;opacity:.92}
main{max-width:620px;margin:auto;padding:14px 14px 34px}
.card{
  background:var(--card);border:1px solid var(--line);border-radius:var(--radius);
  padding:18px;margin:12px 0;box-shadow:0 8px 28px rgba(16,37,27,.06);
}
@media (prefers-color-scheme:dark){
  .card{box-shadow:0 8px 28px rgba(0,0,0,.35)}
}
.anchor{text-align:center;border:2px solid var(--g);padding:22px}
.label{font-size:11px;text-transform:uppercase;letter-spacing:.11em;color:var(--muted);font-weight:900}
.anchor .big{font-size:48px;line-height:1;font-weight:950;letter-spacing:-.06em;margin:8px 0 4px}
.anchor strong{font-size:18px}
.small{font-size:13px;line-height:1.45;color:var(--muted);margin:8px 0 0}
button{font:inherit}
.scan{
  width:100%;border:0;border-radius:18px;padding:20px;
  background:var(--g);color:#fff;font-size:21px;font-weight:950;cursor:pointer;
  transition:transform .08s ease,background .2s ease;
}
.scan:hover:not(:disabled){background:var(--g2)}
.scan:active:not(:disabled){transform:scale(.99)}
.scan:disabled{opacity:.6;cursor:not-allowed}
.scan:focus-visible,select:focus-visible,button:focus-visible{
  outline:3px solid var(--gold);outline-offset:2px;
}
video{
  width:100%;border-radius:18px;background:#08120d;display:none;
  margin-top:12px;aspect-ratio:4/3;object-fit:cover;
}
.stop{
  width:100%;margin-top:10px;padding:13px;border:1px solid var(--line);
  background:transparent;color:var(--ink);border-radius:var(--radius-sm);
  font-weight:800;display:none;cursor:pointer;
}
.result{display:none}
.result .amount{font-size:38px;font-weight:950;letter-spacing:-.02em}
.grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-top:12px}
.stat{border:1px solid var(--line);border-radius:17px;padding:14px}
.stat b{display:block;font-size:25px;margin-top:3px}
.ok{color:var(--ok);font-weight:900}
.warn{background:color-mix(in srgb,var(--gold) 18%,var(--card));border-color:var(--gold)}
.select{
  width:100%;padding:13px;border:1px solid var(--line);border-radius:var(--radius-sm);
  background:var(--card);color:var(--ink);
}
.money{font-size:29px;font-weight:950;margin:8px 0;letter-spacing:-.01em}
.row{
  display:flex;justify-content:space-between;gap:12px;
  border-bottom:1px solid var(--line);padding:10px 0;
}
.row:last-child{border-bottom:0}
.value{font-weight:900}
.paid{background:var(--g2)!important;cursor:default!important}
footer{text-align:center;color:var(--muted);font-size:12px;padding:14px 10px 24px}
.sr-only{
  position:absolute;width:1px;height:1px;padding:0;margin:-1px;overflow:hidden;
  clip:rect(0,0,0,0);white-space:nowrap;border:0;
}
/* Adress-Box */
.addr-box{
  display:flex;align-items:center;gap:10px;
  background:color-mix(in srgb,var(--g) 8%,var(--card));
  border:1px solid var(--line);border-radius:var(--radius-sm);
  padding:12px 14px;margin-top:10px;
}
.addr-box code{
  flex:1;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;
  font-size:12px;word-break:break-all;line-height:1.4;color:var(--ink);
}
.copy-btn{
  flex:0 0 auto;padding:9px 12px;border:1px solid var(--line);
  background:var(--card);color:var(--ink);border-radius:10px;
  font-weight:800;font-size:12px;cursor:pointer;white-space:nowrap;
}
.copy-btn:hover{background:color-mix(in srgb,var(--g) 12%,var(--card))}
.copy-btn:active{transform:scale(.97)}
.qr-link{
  display:inline-block;margin-top:8px;font-size:12px;
  color:var(--g);font-weight:800;text-decoration:none;
}
.qr-link:hover{text-decoration:underline}
</style>
</head>
<body>
<header>
  <h1>🌱 EGGERIUM</h1>
  <p>Einfach produzieren. Die Technik macht den Rest.</p>
</header>
<main>

  <section class="card anchor" aria-label="Fester Rechenanker">
    <div class="label">Fester EGGERIUM-Rechenanker</div>
    <div class="big">0,01 BCH</div>
    <strong>= 1 kg interner Rechenwert</strong>
    <p class="small">Das ist die interne EGGERIUM-Regel. Der Marktpreis von BCH verändert sich; 1 kg bleibt 1 kg.</p>
  </section>

  <section class="card" aria-label="Empfängeradresse">
    <div class="label">Empfänger-Adresse (BCH)</div>
    <div class="addr-box">
      <code id="addrText">bitcoincash:qz86fmmckzjqw7kasj5jeju7jgthexdzsck98pvdge</code>
      <button class="copy-btn" id="copyAddr" type="button">Kopieren</button>
    </div>
    <a class="qr-link" id="qrLink" href="#" target="_blank" rel="noopener">Adresse als QR anzeigen →</a>
    <p class="small">Jede Zahlung geht direkt an diese Adresse. Kein Mittelsmann, keine Registrierung.</p>
  </section>

  <section class="card">
    <div class="label" id="scanLabel">Der ganze Vorgang</div>
    <button class="scan" id="start" aria-describedby="scanText">📷 SCAN → PAY → FERTIG</button>
    <video id="video" playsinline muted aria-label="Kameravorschau zum QR-Scan"></video>
    <button class="stop" id="stop">Kamera schließen</button>
    <p class="small" id="scanText" aria-live="polite">
      Ein QR-Code trägt die Aktion. Keine Namen. Keine Telefonnummer. Kein Formular.
    </p>
  </section>

  <section class="card result" id="result" aria-live="polite">
    <div class="label">Automatisch erkannt</div>
    <div class="amount" id="amount">—</div>
    <div id="areaLine" class="ok">—</div>
    <div class="grid">
      <div class="stat"><span class="label">Pflanzen</span><b id="plants">—</b></div>
      <div class="stat"><span class="label">100-Tage-Zyklus</span><b id="day">Tag 1</b></div>
    </div>
    <button class="scan" id="pay" style="margin-top:14px">💚 ZAHLUNG AUSFÜHREN</button>
    <p class="small" id="payState" aria-live="polite"></p>
  </section>

  <section class="card">
    <div class="label">Mein Bitcoin-Penny — jetzt in anderen Währungen</div>
    <div class="money" id="selected">Lade …</div>
    <label for="currency" class="sr-only">Zielwährung wählen</label>
    <select class="select" id="currency">
      <option value="eur">Euro (EUR)</option>
      <option value="usd">US-Dollar (USD)</option>
      <option value="gmd">Dalasi (GMD)</option>
      <option value="rub">Rubel (RUB)</option>
      <option value="jpy">Yen (JPY)</option>
    </select>
    <p class="small" id="status" aria-live="polite">Aktuelle Marktdaten werden geladen.</p>
    <div id="rates"></div>
  </section>

  <section class="card warn">
    <b>So läuft es im echten Betrieb:</b>
    <p class="small">
      QR scannen → Betrag kommt aus dem QR → BCH bezahlen → die App prüft die
      Blockchain bis zur Bestätigung → Fläche, 100 Pflanzen/m², Zyklus und
      Abrechnung entstehen automatisch im Hintergrund.
    </p>
  </section>

  <footer>EGGERIUM • SCAN → PAY → FERTIG</footer>
</main>

<script>
"use strict";
(function () {

  /* ------------------------------------------------------------------ *
   *  Konfiguration — mit deiner Empfängeradresse
   * ------------------------------------------------------------------ */
  const CONFIG = Object.freeze({
    // Deine BCH-Adresse (CashAddr, mit Prefix)
    ADDRESS: "bitcoincash:qz86fmmckzjqw7kasj5jeju7jgthexdzsck98pvdge",
    // Ohne Prefix für die Anzeige
    ADDRESS_BARE: "qz86fmmckzjqw7kasj5jeju7jgthexdzsck98pvdge",
    BCH_PER_UNIT: 0.01,
    MIN_UNITS: 0.01,           // 0,01 m² — kleinste sinnvolle Fläche
    MAX_UNITS: 10000,          // 1 ha Obergrenze pro Vorgang
    MAX_BCH: 100,              // harte Obergrenze BCH pro Vorgang
    PLANTS_PER_M2: 100,
    CYCLE_DAYS: 100,
    PRICE_API: "https://api.coingecko.com/api/v3/simple/price?ids=bitcoin-cash&vs_currencies=eur,usd,gmd,rub,jpy",
    BALANCE_API: "https://api.whatsonchain.com/v1/bch/mainnet/address/",
    PRICE_REFRESH_MS: 90_000,
    PRICE_BACKOFF_BASE_MS: 5 * 60_000,
    PRICE_BACKOFF_MAX_MS: 30 * 60_000,
    PAYMENT_POLL_MS: 15_000,
    PAYMENT_TIMEOUT_MS: 30 * 60_000,
    TOLERANCE: 0.99,           // 1 % Toleranz (Rundung Wallet)
    JSQR_CDN: "https://cdn.jsdelivr.net/npm/jsqr@1.4.0/dist/jsQR.js"
  });

  const SYMBOLS = { eur: "€", usd: "$", gmd: "D", rub: "₽", jpy: "¥" };

  /* ------------------------------------------------------------------ *
   *  DOM-Referenzen
   * ------------------------------------------------------------------ */
  const $ = (id) => document.getElementById(id);
  const els = {
    startBtn: $("start"), stopBtn: $("stop"), video: $("video"),
    scanText: $("scanText"), result: $("result"), amount: $("amount"),
    areaLine: $("areaLine"), plants: $("plants"), day: $("day"),
    payBtn: $("pay"), payState: $("payState"), selected: $("selected"),
    currency: $("currency"), status: $("status"), rates: $("rates"),
    addrText: $("addrText"), copyAddr: $("copyAddr"), qrLink: $("qrLink")
  };

  /* ------------------------------------------------------------------ *
   *  Zustand
   * ------------------------------------------------------------------ */
  const state = {
    tx: { area: 1, amount: 0.01, scanStart: Date.now(), paidAt: null },
    rates: {},
    currency: "eur",
    // Scanner
    stream: null,
    detector: null,
    detectorMode: null,     // 'native' | 'jsqr' | null
    detectTimer: null,
    detecting: false,
    canvas: null,
    // Preise
    priceFailures: 0,
    priceBackoffUntil: 0,
    priceTimer: null,
    // Zahlung
    paying: false,
    balanceAtStart: null,
    paymentTimer: null,
    paymentStartedAt: 0
  };

  /* ------------------------------------------------------------------ *
   *  Hilfsfunktionen
   * ------------------------------------------------------------------ */
  const fmt = (n, currency) =>
    new Intl.NumberFormat("de-DE", {
      maximumFractionDigits: currency === "jpy" ? 0 : 2
    }).format(n);

  const fmtBCH = (n) =>
    new Intl.NumberFormat("de-DE", {
      minimumFractionDigits: 2, maximumFractionDigits: 8
    }).format(n) + " BCH";

  const fmtArea = (n) =>
    new Intl.NumberFormat("de-DE", { maximumFractionDigits: 4 }).format(n);

  const shortAddr = (a) => a.replace(/^bitcoincash:/i, "").slice(0, 8) + "…";

  const setText = (el, txt) => { if (el && el.textContent !== txt) el.textContent = txt; };

  /* ------------------------------------------------------------------ *
   *  QR-Parsing mit strenger Validierung
   * ------------------------------------------------------------------ */
  function validUnits(u) {
    return Number.isFinite(u) && u >= CONFIG.MIN_UNITS && u <= CONFIG.MAX_UNITS;
  }
  function validBCH(amt) {
    return Number.isFinite(amt) && amt > 0 && amt <= CONFIG.MAX_BCH;
  }

  /**
   * Akzeptiert:
   *   eggerium:?area=5
   *   web+eggerium:?area=5
   *   eggerium:5
   *   bitcoincash:<addr>?amount=0.05
   *   bitcoincash:<addr>?amount=0.05&...
   *   <reine CashAddr>   (wird als Zahlung ohne Betrag behandelt → Demo-Betrag)
   * Gibt {area, amount} zurück oder null.
   */
  function parseQR(raw) {
    if (typeof raw !== "string") return null;
    const s = raw.trim();
    if (!s || s.length > 2048) return null;

    // EGGERIUM-Schema
    if (/^(web\+)?eggerium:/i.test(s)) {
      const q = s.match(/[?&]area=([0-9]*\.?[0-9]+)/i);
      let units;
      if (q) units = Number(q[1]);
      else units = Number(s.replace(/^(web\+)?eggerium:/i, "").replace(/^\/+/, ""));
      if (!validUnits(units)) return null;
      return { area: units, amount: units * CONFIG.BCH_PER_UNIT };
    }

    // BCH-Schema mit optionalem Betrag
    if (/^bitcoincash:/i.test(s)) {
      const m = s.match(/[?&]amount=([0-9]*\.?[0-9]+)/i);
      if (!m) {
        // Adresse ohne Betrag: wir nehmen 1 m² als Standard.
        return { area: 1, amount: 1 * CONFIG.BCH_PER_UNIT };
      }
      const amt = Number(m[1]);
      if (!validBCH(amt)) return null;
      const units = amt / CONFIG.BCH_PER_UNIT;
      if (!validUnits(units)) return null;
      return { area: units, amount: amt };
    }

    // Reine CashAddr (ohne Prefix) — verbreitetes QR-Format
    if (/^[qpzry9x8gf2tvdw0s3jn54khce6mua7l]{42}$/i.test(s)) {
      return { area: 1, amount: 1 * CONFIG.BCH_PER_UNIT };
    }

    return null;
  }

  /* ------------------------------------------------------------------ *
   *  Transaktion anwenden / anzeigen
   * ------------------------------------------------------------------ */
  function applyTransaction(parsed) {
    state.tx = {
      area: parsed.area,
      amount: parsed.amount,
      scanStart: Date.now(),
      paidAt: null
    };
    state.paying = false;
    state.balanceAtStart = null;
    stopPaymentPoll();
    els.payBtn.disabled = false;
    els.payBtn.classList.remove("paid");
    els.payBtn.textContent = "💚 ZAHLUNG AUSFÜHREN";
    els.payState.textContent = "";
    showTx();
  }

  function showTx() {
    const { area, amount, scanStart } = state.tx;
    els.result.style.display = "block";
    els.amount.textContent = fmtBCH(amount);
    els.areaLine.textContent =
      fmtArea(area) + " m² → " +
      (area * CONFIG.PLANTS_PER_M2).toLocaleString("de-DE") + " Pflanzen";
    els.plants.textContent = (area * CONFIG.PLANTS_PER_M2).toLocaleString("de-DE");

    const days = Math.max(1, Math.min(CONFIG.CYCLE_DAYS,
      Math.floor((Date.now() - scanStart) / 86_400_000) + 1));
    els.day.textContent = "Tag " + days;
  }

  /* ------------------------------------------------------------------ *
   *  Kamera + QR-Scan
   * ------------------------------------------------------------------ */
  function loadJsQR() {
    return new Promise((resolve, reject) => {
      if (typeof window.jsQR === "function") return resolve(window.jsQR);
      const script = document.createElement("script");
      script.src = CONFIG.JSQR_CDN;
      script.async = true;
      script.crossOrigin = "anonymous";
      script.onload = () => {
        if (typeof window.jsQR === "function") resolve(window.jsQR);
        else reject(new Error("jsQR global nicht gefunden"));
      };
      script.onerror = () => reject(new Error("jsQR Download fehlgeschlagen"));
      document.head.appendChild(script);
    });
  }

  function pickBestCode(codes) {
    for (const c of codes) {
      const v = c && c.rawValue;
      if (typeof v === "string" && /^(web\+)?eggerium:|^bitcoincash:/i.test(v.trim())) return c;
    }
    return codes[0];
  }

  function detectWithJsQR() {
    if (!state.canvas) state.canvas = document.createElement("canvas");
    const v = els.video;
    const w = v.videoWidth, h = v.videoHeight;
    if (!w || !h) return null;
    const scale = Math.min(1, 480 / Math.max(w, h));
    state.canvas.width  = Math.round(w * scale);
    state.canvas.height = Math.round(h * scale);
    const ctx = state.canvas.getContext("2d", { willReadFrequently: true });
    ctx.drawImage(v, 0, 0, state.canvas.width, state.canvas.height);
    const img = ctx.getImageData(0, 0, state.canvas.width, state.canvas.height);
    const res = window.jsQR(img.data, img.width, img.height, { inversionAttempts: "dontInvert" });
    return res ? res.data : null;
  }

  async function scanTick() {
    if (!state.stream || state.detecting) return;
    const v = els.video;
    if (!v || v.readyState < 2) return;
    state.detecting = true;
    let raw = null;
    try {
      if (state.detectorMode === "native") {
        const codes = await state.detector.detect(v);
        if (codes && codes.length) raw = pickBestCode(codes).rawValue;
      } else if (state.detectorMode === "jsqr") {
        raw = detectWithJsQR();
      }
    } catch (_) {
      /* stiller Fehler, nächster Tick versucht es erneut */
    } finally {
      state.detecting = false;
    }
    if (!raw) return;

    const parsed = parseQR(raw);
    if (parsed) {
      stopScan();
      applyTransaction(parsed);
      setText(els.scanText, "QR erkannt. Alles Weitere ist automatisch.");
    } else {
      setText(els.scanText,
        "QR erkannt, aber nicht gültig. Bitte einen EGGERIUM- oder BCH-Code verwenden.");
    }
  }

  async function startScan() {
    stopScan();

    if (!navigator.mediaDevices || !navigator.mediaDevices.getUserMedia) {
      setText(els.scanText, "Kamera-API nicht verfügbar. Demo-Aktion wird verwendet.");
      demo();
      return;
    }

    try {
      state.stream = await navigator.mediaDevices.getUserMedia({
        video: {
          facingMode: { ideal: "environment" },
          width:  { ideal: 1280 },
          height: { ideal: 720 }
        },
        audio: false
      });
      els.video.srcObject = state.stream;
      els.video.style.display = "block";
      els.stopBtn.style.display = "block";
      await els.video.play();

      state.detectorMode = null;
      if ("BarcodeDetector" in window) {
        try {
          state.detector = new BarcodeDetector({ formats: ["qr_code"] });
          state.detectorMode = "native";
        } catch (_) { state.detectorMode = null; }
      }
      if (!state.detectorMode) {
        setText(els.scanText, "QR-Decoder wird geladen …");
        try {
          await loadJsQR();
          state.detectorMode = "jsqr";
        } catch (err) {
          stopScan();
          setText(els.scanText,
            "QR-Decoder konnte nicht geladen werden. Demo-Aktion wird verwendet.");
          demo();
          return;
        }
      }

      setText(els.scanText, "QR-Code vor die Kamera halten …");
      state.detectTimer = window.setInterval(scanTick, 250);
    } catch (err) {
      stopScan();
      setText(els.scanText,
        "Kamera nicht verfügbar (" + (err && err.name ? err.name : "Fehler") +
        "). Demo-Aktion wird verwendet.");
      demo();
    }
  }

  function stopScan() {
    if (state.detectTimer) {
      clearInterval(state.detectTimer);
      state.detectTimer = null;
    }
    if (state.stream) {
      try { state.stream.getTracks().forEach((t) => t.stop()); } catch (_) {}
      state.stream = null;
    }
    if (els.video) {
      try { els.video.pause(); } catch (_) {}
      els.video.srcObject = null;
      els.video.style.display = "none";
    }
    if (els.stopBtn) els.stopBtn.style.display = "none";
    state.detector = null;
    state.detectorMode = null;
    state.detecting = false;
  }

  function demo() {
    applyTransaction({ area: 1, amount: 1 * CONFIG.BCH_PER_UNIT });
    setText(els.scanText, "Demo-Aktion: 1 m². In der Produktion kommt der Wert aus dem QR.");
  }

  /* ------------------------------------------------------------------ *
   *  Zahlung
   * ------------------------------------------------------------------ */
  function buildPaymentURI(tx) {
    const amountStr = tx.amount.toFixed(8).replace(/0+$/, "").replace(/\.$/, "");
    const params = new URLSearchParams({
      amount: amountStr,
      message: "EGGERIUM " + fmtArea(tx.area) + "m2"
    });
    return CONFIG.ADDRESS + "?" + params.toString();
  }

  async function fetchBalance() {
    const addr = CONFIG.ADDRESS_BARE;
    const res = await fetch(CONFIG.BALANCE_API + addr + "/balance", { cache: "no-store" });
    if (!res.ok) throw new Error("HTTP " + res.status);
    const json = await res.json();
    const confirmed = Number(json && json.confirmed) || 0;
    const unconfirmed = Number(json && json.unconfirmed) || 0;
    return confirmed + unconfirmed; // Satoshi
  }

  function stopPaymentPoll() {
    if (state.paymentTimer) {
      clearInterval(state.paymentTimer);
      state.paymentTimer = null;
    }
  }

  function startPaymentPoll() {
    stopPaymentPoll();
    state.paymentStartedAt = Date.now();
    const expectedSats = Math.round(state.tx.amount * 1e8);

    state.paymentTimer = window.setInterval(async () => {
      if (Date.now() - state.paymentStartedAt > CONFIG.PAYMENT_TIMEOUT_MS) {
        stopPaymentPoll();
        state.paying = false;
        els.payBtn.disabled = false;
        els.payState.textContent =
          "Zeitüberschreitung. Bitte Zahlung prüfen und Scan erneut starten.";
        return;
      }
      try {
        const balance = await fetchBalance();
        if (state.balanceAtStart == null) {
          state.balanceAtStart = balance;
          return;
        }
        const diff = balance - state.balanceAtStart;
        if (diff >= expectedSats * CONFIG.TOLERANCE) {
          stopPaymentPoll();
          onPaymentConfirmed();
        } else if (diff > 0) {
          els.payState.textContent =
            "Eingegangen: " + (diff / 1e8).toFixed(8).replace(".", ",") +
            " BCH von " + fmtBCH(state.tx.amount) + " …";
        }
      } catch (_) {
        /* Netzwerkfehler — nächster Tick versucht es erneut. */
      }
    }, CONFIG.PAYMENT_POLL_MS);
  }

  function onPaymentConfirmed() {
    state.paying = false;
    state.tx.paidAt = Date.now();
    els.payBtn.disabled = true;
    els.payBtn.classList.add("paid");
    els.payBtn.textContent = "✓ BEZAHLT";
    els.payState.textContent =
      "✓ Zahlung in der Blockchain bestätigt. Vorgang abgeschlossen.";
  }

  async function handlePay() {
    if (state.paying) return;
    const { area, amount } = state.tx;

    const ok = window.confirm(
      "EGGERIUM-Zahlung bestätigen\n\n" +
      "Betrag:   " + fmtBCH(amount) + "\n" +
      "Fläche:   " + fmtArea(area) + " m²\n" +
      "Pflanzen: " + (area * CONFIG.PLANTS_PER_M2).toLocaleString("de-DE") + "\n" +
      "Empfänger: " + shortAddr(CONFIG.ADDRESS) + "\n\n" +
      "Jetzt Wallet öffnen?"
    );
    if (!ok) return;

    state.paying = true;
    els.payBtn.disabled = true;
    els.payState.textContent = "Zahlung wird vorbereitet …";

    try {
      state.balanceAtStart = await fetchBalance();
    } catch (_) {
      state.balanceAtStart = null;
    }

    try {
      window.location.href = buildPaymentURI(state.tx);
    } catch (_) {
      els.payState.textContent =
        "Wallet konnte nicht geöffnet werden. Bitte Adresse manuell verwenden: " +
        CONFIG.ADDRESS;
      state.paying = false;
      els.payBtn.disabled = false;
      return;
    }

    els.payState.textContent = "Wallet geöffnet. Warte auf Blockchain-Bestätigung …";
    startPaymentPoll();
  }

  /* ------------------------------------------------------------------ *
   *  Preise (CoinGecko) mit Backoff
   * ------------------------------------------------------------------ */
  async function loadRates() {
    if (state.priceBackoffUntil && Date.now() < state.priceBackoffUntil) return;
    try {
      const res = await fetch(CONFIG.PRICE_API, { cache: "no-store" });
      if (!res.ok) throw new Error("HTTP " + res.status);
      const json = await res.json();
      const rates = json && json["bitcoin-cash"];
      if (!rates || typeof rates !== "object") throw new Error("Keine Kursdaten");
      state.rates = rates;
      state.priceFailures = 0;
      state.priceBackoffUntil = 0;
      els.status.textContent =
        "Live-Marktdaten • CoinGecko • " + new Date().toLocaleTimeString("de-DE");
      updateRate();
    } catch (_) {
      state.priceFailures += 1;
      if (state.priceFailures >= 2) {
        const wait = Math.min(
          CONFIG.PRICE_BACKOFF_BASE_MS * state.priceFailures,
          CONFIG.PRICE_BACKOFF_MAX_MS
        );
        state.priceBackoffUntil = Date.now() + wait;
        els.status.textContent =
          "Marktdaten momentan nicht erreichbar. Nächster Versuch in " +
          Math.round(wait / 60_000) + " min.";
      } else {
        els.status.textContent = "Marktdaten momentan nicht erreichbar.";
      }
    }
  }

  function updateRate() {
    const c = state.currency;
    const r = state.rates;
    const perUnit = r && typeof r[c] === "number" ? r[c] * CONFIG.BCH_PER_UNIT : null;
    els.selected.textContent =
      perUnit == null
        ? "—"
        : "0,01 BCH = " + SYMBOLS[c] + " " + fmt(perUnit, c);

    els.rates.innerHTML = Object.keys(SYMBOLS).map((x) => {
      const v = r && typeof r[x] === "number" ? r[x] * CONFIG.BCH_PER_UNIT : null;
      return (
        '<div class="row"><span>0,01 BCH → ' + x.toUpperCase() + "</span>" +
        '<span class="value">' +
        (v == null ? "—" : SYMBOLS[x] + " " + fmt(v, x)) +
        "</span></div>"
      );
    }).join("");
  }

  /* ------------------------------------------------------------------ *
   *  Adress-Box: Kopieren + QR-Link
   * ------------------------------------------------------------------ */
  async function copyAddress() {
    const txt = CONFIG.ADDRESS;
    try {
      if (navigator.clipboard && navigator.clipboard.writeText) {
        await navigator.clipboard.writeText(txt);
      } else {
        const ta = document.createElement("textarea");
        ta.value = txt;
        ta.setAttribute("readonly", "");
        ta.style.position = "absolute";
        ta.style.left = "-9999px";
        document.body.appendChild(ta);
        ta.select();
        document.execCommand("copy");
        document.body.removeChild(ta);
      }
      els.copyAddr.textContent = "Kopiert ✓";
      setTimeout(() => { els.copyAddr.textContent = "Kopieren"; }, 1600);
    } catch (_) {
      els.copyAddr.textContent = "Fehler";
      setTimeout(() => { els.copyAddr.textContent = "Kopieren"; }, 1600);
    }
  }

  function wireAddressUI() {
    // Adresse anzeigen
    if (els.addrText) els.addrText.textContent = CONFIG.ADDRESS;
    // Copy-Button
    if (els.copyAddr) els.copyAddr.addEventListener("click", copyAddress);
    // Externer QR-Link (öffentlicher QR-Generator, öffnet neuen Tab)
    if (els.qrLink) {
      const qrTarget = encodeURIComponent(CONFIG.ADDRESS);
      els.qrLink.href = "https://api.qrserver.com/v1/create-qr-code/?size=320x320&data=" + qrTarget;
    }
  }

  /* ------------------------------------------------------------------ *
   *  Protocol-Handler (web+eggerium:)
   * ------------------------------------------------------------------ */
  function registerProtocol() {
    if (!navigator.registerProtocolHandler) return;
    try {
      const base = location.href.split(/[?#]/)[0];
      navigator.registerProtocolHandler("web+eggerium", base + "?qr=%s");
    } catch (_) { /* still ok */ }
  }

  /* ------------------------------------------------------------------ *
   *  Init
   * ------------------------------------------------------------------ */
  function handleInitialQRFromURL() {
    const params = new URLSearchParams(location.search);
    const qr = params.get("qr");
    if (!qr) return;
    const parsed = parseQR(qr);
    if (parsed) {
      applyTransaction(parsed);
      setText(els.scanText, "QR aus Link geladen.");
    }
  }

  function bindEvents() {
    els.startBtn.addEventListener("click", startScan);
    els.stopBtn.addEventListener("click", () => {
      stopScan();
      setText(els.scanText, "Kamera geschlossen.");
    });
    els.payBtn.addEventListener("click", handlePay);
    els.currency.addEventListener("change", () => {
      state.currency = els.currency.value;
      updateRate();
    });

    document.addEventListener("visibilitychange", () => {
      if (document.hidden) {
        stopScan();
        stopPaymentPoll();
      } else if (state.paying) {
        startPaymentPoll();
      }
    });

    window.addEventListener("pagehide", () => {
      stopScan();
      stopPaymentPoll();
      if (state.priceTimer) clearInterval(state.priceTimer);
    });
  }

  function init() {
    state.currency = els.currency.value;
    bindEvents();
    wireAddressUI();
    registerProtocol();
    handleInitialQRFromURL();
    showTx();
    loadRates();
    state.priceTimer = window.setInterval(loadRates, CONFIG.PRICE_REFRESH_MS);

    // Zyklustag regelmäßig aktualisieren
    window.setInterval(showTx, 60_000);
  }

  if (document.readyState === "loading") {
    document.addEventListener("DOMContentLoaded", init);
  } else {
    init();
  }
})();
</script>
</body>
</html><!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="./style.css">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pen</title>
  </head>
  <body>

    <script src="./script.js"></script>
  </body>
</html>
