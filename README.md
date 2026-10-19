# nova-pay
NOVA Pay App
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#063f35">
<title>NOVA Pay</title>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f2f6f5;
  color: #183a32;
}

header {
  background: linear-gradient(135deg, #063f35, #087d61);
  color: white;
  padding: 26px 22px 32px;
  border-radius: 0 0 28px 28px;
}

.top {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  font-size: 27px;
  font-weight: bold;
}

.logo span {
  color: #65f0b8;
}

.avatar {
  background: #ffffff22;
  border: 1px solid #ffffff55;
  padding: 11px;
  border-radius: 50%;
}

.welcome {
  margin-top: 28px;
  color: #d2eee4;
}

.balance-label {
  margin-top: 22px;
  font-size: 14px;
  color: #d2eee4;
}

.balance {
  font-size: 32px;
  font-weight: bold;
  margin-top: 9px;
}

.currency {
  font-size: 15px;
}

.container {
  padding: 20px;
  max-width: 550px;
  margin: auto;
}

.section-title {
  font-size: 19px;
  margin: 8px 0 16px;
}

.card {
  background: white;
  padding: 19px;
  border-radius: 20px;
  margin-bottom: 20px;
  box-shadow: 0 5px 22px #163c300a;
}

.actions {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}

.action {
  background: #eff8f4;
  padding: 15px 5px;
  border-radius: 15px;
  text-align: center;
  cursor: pointer;
  border: none;
  color: #087d61;
  font-size: 13px;
}

.action .icon {
  font-size: 25px;
  display: block;
  margin-bottom: 9px;
}

button {
  font-family: inherit;
}

input {
  display: block;
  width: 100%;
  padding: 14px;
  margin: 9px 0 16px;
  border: 1px solid #dce8e2;
  border-radius: 12px;
  font-size: 16px;
  background: #fbfdfc;
}

.primary {
  width: 100%;
  padding: 15px;
  border: none;
  border-radius: 12px;
  background: #087d61;
  color: white;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
}

.secondary {
  width: 100%;
  padding: 13px;
  border: none;
  border-radius: 12px;
  background: #e8f5ef;
  color: #087d61;
  font-weight: bold;
  cursor: pointer;
}

.transaction {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 10px;
  padding: 15px 0;
  border-bottom: 1px solid #edf1ef;
}

.transaction:last-child {
  border-bottom: none;
}

.tx-icon {
  background: #e8f5ef;
  padding: 12px;
  border-radius: 13px;
}

.tx-info {
  flex: 1;
  min-width: 0;
}

.tx-info strong {
  display: block;
  font-size: 14px;
}

.tx-info small {
  display: block;
  color: #819089;
  margin-top: 5px;
}

.tx-amount {
  font-weight: bold;
  color: #b64c4c;
  white-space: nowrap;
}

.note {
  color: #7a8982;
  font-size: 12px;
  line-height: 1.8;
}

footer {
  text-align: center;
  padding: 20px;
  color: #7a8982;
  font-size: 12px;
}

.hidden {
  display: none;
}
</style>
</head>

<body>

<header>
  <div class="top">
    <div class="logo">NOVA <span>Pay</span></div>
    <div class="avatar">👤</div>
  </div>

  <div class="welcome">أهلاً بيك في محفظتك الرقمية 👋</div>

  <div class="balance-label">رصيد تجريبي</div>

  <div class="balance">
    <span id="balance">5,000.00</span>
    <span class="currency">ج.م</span>
  </div>
</header>

<main class="container">

  <h2 class="section-title">خدماتك المالية</h2>

  <div class="card">
    <div class="actions">
      <button class="action" onclick="openTransfer()">
        <span class="icon">💸</span>
        تحويل
      </button>

      <button class="action" onclick="showHistory()">
        <span class="icon">📋</span>
        العمليات
      </button>

      <button class="action" onclick="showInfo()">
        <span class="icon">👤</span>
        حسابي
      </button>
    </div>
  </div>

  <div class="card hidden" id="transferCard">
    <h3>💸 تحويل تجريبي</h3>

    <label for="recipient">اسم المستلم التجريبي</label>
    <input id="recipient" maxlength="40"
      placeholder="اكتب اسمًا تجريبيًا">

    <label for="amount">المبلغ بالجنيه المصري</label>
    <input id="amount" type="number"
      min="1" step="0.01" placeholder="مثال: 100">

    <button class="primary" onclick="transfer()">
      تأكيد التحويل التجريبي
    </button>

    <p class="note">
      هذه محاكاة فقط. لا تستخدم بيانات بنكية حقيقية.
      لا يتم إرسال أي أموال.
    </p>
  </div>

  <div class="card hidden" id="accountCard">
    <h3>👤 حسابي</h3>
    <p>اسم التطبيق: NOVA Pay</p>
    <p>نوع الحساب: نسخة تجريبية</p>
    <p class="note">
      لا يوجد حساب بنكي مرتبط بهذا النموذج.
    </p>
  </div>

  <h2 class="section-title" id="historyTitle">
    آخر العمليات
  </h2>

  <div class="card" id="historyCard">
    <div id="history">
      <p class="note">لسه مفيش عمليات تجريبية.</p>
    </div>
  </div>

  <div class="card">
    <h3>🛡️ أمانك مهم</h3>
    <p class="note">
      NOVA Pay نموذج أولي للتجربة والتطوير.
      الرصيد والعمليات غير حقيقية، ولا يتصل التطبيق
      بالبنوك أو بشبكات الدفع.
    </p>
  </div>

</main>

<footer>
  NOVA Pay © 2026<br>
  نموذج تجريبي غير مخصص للمعاملات المالية الحقيقية
</footer>

<script>
let balance = 5000;
let transactions = [];

function openTransfer() {
  const card = document.getElementById("transferCard");
  card.classList.remove("hidden");
  document.getElementById("accountCard").classList.add("hidden");
  card.scrollIntoView({behavior: "smooth", block: "start"});
}

function showHistory() {
  document.getElementById("historyCard")
    .scrollIntoView({behavior: "smooth", block: "start"});
}

function showInfo() {
  const card = document.getElementById("accountCard");
  card.classList.toggle("hidden");
  card.scrollIntoView({behavior: "smooth", block: "start"});
}

function transfer() {
  const recipient = document.getElementById("recipient")
    .value.trim();

  const amount = Number(
    document.getElementById("amount").value
  );

  if (!recipient) {
    alert("اكتب اسم المستلم التجريبي.");
    return;
  }

  if (!Number.isFinite(amount) || amount <= 0) {
    alert("اكتب مبلغًا صحيحًا.");
    return;
  }

  if (amount > balance) {
    alert("الرصيد التجريبي غير كافٍ.");
    return;
  }

  balance -= amount;

  transactions.unshift({
    recipient: recipient,
    amount: amount,
    date: new Date().toLocaleString("ar-EG")
  });

  document.getElementById("balance").textContent =
    balance.toLocaleString("en-US", {
      minimumFractionDigits: 2,
      maximumFractionDigits: 2
    });

  renderHistory();

  document.getElementById("recipient").value = "";
  document.getElementById("amount").value = "";

  alert("تم تسجيل التحويل التجريبي بنجاح.");
}

function escapeHTML(value) {
  return value.replace(/[&<>"']/g, function(char) {
    return {
      "&": "&amp;",
      "<": "&lt;",
      ">": "&gt;",
      '"': "&quot;",
      "'": "&#39;"
    }[char];
  });
}

function renderHistory() {
  const history = document.getElementById("history");

  if (transactions.length === 0) {
    history.innerHTML =
      '<p class="note">لسه مفيش عمليات تجريبية.</p>';
    return;
  }

  history.innerHTML = transactions.map(function(tx) {
    return `
      <div class="transaction">
        <div class="tx-icon">💸</div>
        <div class="tx-info">
          <strong>تحويل تجريبي</strong>
          <small>إلى: ${escapeHTML(tx.recipient)}</small>
          <small>${escapeHTML(tx.date)}</small>
        </div>
        <div class="tx-amount">
          -${tx.amount.toFixed(2)} ج.م
        </div>
      </div>
    `;
  }).join("");
}
</script>

</body>
</html>
