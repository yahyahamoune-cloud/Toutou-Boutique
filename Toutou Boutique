<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no, viewport-fit=cover" />
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
  <meta name="apple-mobile-web-app-title" content="الخزينة الذكية" />
  <title>الخزينة الذكية - الإدارة الشاملة</title>
  <link rel="apple-touch-icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><rect width='100' height='100' rx='22' fill='%23059669'/><text x='50' y='66' font-size='52' text-anchor='middle' fill='white' font-family='sans-serif' font-weight='bold'>خ</text></svg>" />
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;500;700;800&display=swap" rel="stylesheet">
  <style>
    body { font-family: 'Tajawal', sans-serif; background-color: #f8fafc; padding-top: env(safe-area-inset-top); padding-bottom: calc(80px + env(safe-area-inset-bottom)); }
    .safe-bottom { padding-bottom: env(safe-area-inset-bottom); }
  </style>
</head>
<body class="text-slate-800 antialiased select-none">

  <header class="sticky top-0 z-30 bg-slate-900 text-white px-4 py-3 shadow-md flex items-center justify-between">
    <div class="flex items-center gap-2.5">
      <div class="w-9 h-9 rounded-xl bg-emerald-500 flex items-center justify-center font-extrabold text-lg">خ</div>
      <div>
        <h1 class="font-bold text-base leading-tight">الخزينة الذكية</h1>
        <div class="flex items-center gap-1.5 text-xs text-slate-300">
          <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse" id="status-dot"></span>
          <span id="status-text">متصل ومزامن</span>
        </div>
      </div>
    </div>
    <div class="flex items-center gap-2">
      <button onclick="toggleSimulatedOffline()" class="p-2 rounded-lg bg-slate-800 text-xs border border-slate-700">📶</button>
      <button onclick="openUserModal()" class="bg-slate-800 px-2.5 py-1.5 rounded-lg border border-slate-700 text-xs font-medium">
        👤 <span id="current-user-name">أحمد</span>
      </button>
    </div>
  </header>

  <div id="offline-banner" class="hidden bg-amber-500 text-slate-950 text-xs font-bold px-4 py-2 flex items-center justify-between">
    <span>وضع عدم الاتصال: يتم الحفظ محلياً للمزامنة لاحقاً.</span>
    <span id="pending-count" class="bg-slate-900 text-white px-2 py-0.5 rounded-full">0</span>
  </div>

  <main class="max-w-lg mx-auto p-4 space-y-4">
    <!-- 1. نقطة البيع -->
    <section id="tab-pos" class="space-y-4">
      <div class="bg-white rounded-2xl p-4 shadow-sm border border-slate-200 space-y-3">
        <div class="flex items-center justify-between">
          <h2 class="font-bold text-slate-800 text-base">نقطة البيع</h2>
          <span class="text-xs text-slate-500 bg-slate-100 px-2 py-1 rounded-md">MRU</span>
        </div>
        <div>
          <label class="block text-xs font-bold text-slate-600 mb-1">المنتج</label>
          <select id="pos-product-select" onchange="updatePosPrice()" class="w-full bg-slate-50 border border-slate-300 rounded-xl px-3 py-2.5 text-sm font-medium"></select>
        </div>
        <div class="grid grid-cols-2 gap-3">
          <div>
            <label class="block text-xs font-bold text-slate-600 mb-1">الكمية</label>
            <input type="number" id="pos-qty" value="1" min="1" oninput="updatePosPrice()" class="w-full bg-slate-50 border border-slate-300 rounded-xl px-3 py-2 text-sm font-bold text-center" />
          </div>
          <div>
            <label class="block text-xs font-bold text-slate-600 mb-1">السعر (MRU)</label>
            <input type="number" id="pos-unit-price" oninput="updatePosTotalOnly()" class="w-full bg-slate-50 border border-slate-300 rounded-xl px-3 py-2 text-sm font-bold text-center" />
          </div>
        </div>
        <div>
          <label class="block text-xs font-bold text-slate-600 mb-1.5">وسيلة استلام المبلغ</label>
          <div class="grid grid-cols-4 gap-2">
            <button type="button" onclick="selectPayment('كاش', this)" class="pay-btn bg-emerald-600 text-white border border-emerald-600 rounded-xl py-2.5 text-xs font-bold">كاش</button>
            <button type="button" onclick="selectPayment('بنكيلي', this)" class="pay-btn bg-slate-50 text-slate-700 border border-slate-300 rounded-xl py-2.5 text-xs font-bold">بنكيلي</button>
            <button type="button" onclick="selectPayment('مصرفي', this)" class="pay-btn bg-slate-50 text-slate-700 border border-slate-300 rounded-xl py-2.5 text-xs font-bold">مصرفي</button>
            <button type="button" onclick="selectPayment('سداد', this)" class="pay-btn bg-slate-50 text-slate-700 border border-slate-300 rounded-xl py-2.5 text-xs font-bold">سداد</button>
          </div>
        </div>
        <div class="pt-2 border-t border-slate-100 flex items-center justify-between">
          <div>
            <span class="text-xs text-slate-500 block">الإجمالي</span>
            <span id="pos-total-display" class="text-xl font-extrabold text-emerald-600">0 MRU</span>
          </div>
          <button onclick="executeSale()" class="bg-emerald-600 text-white font-bold px-6 py-3 rounded-xl shadow text-sm">إتمام البيع ✓</button>
        </div>
      </div>

      <div class="grid grid-cols-2 gap-3">
        <div class="bg-white p-3.5 rounded-2xl border border-slate-200">
          <span class="text-xs text-slate-500 block">النقد المتوفر</span>
          <span id="summary-total-cash" class="text-lg font-extrabold text-slate-800 mt-1 block">0 MRU</span>
        </div>
        <div class="bg-white p-3.5 rounded-2xl border border-slate-200">
          <span class="text-xs text-slate-500 block">قيمة المخزون</span>
          <span id="summary-stock-value" class="text-lg font-extrabold text-sky-600 mt-1 block">0 MRU</span>
        </div>
      </div>
    </section>

    <!-- 2. المخزون (قابل للتعديل والإضافة) -->
    <section id="tab-inventory" class="hidden space-y-4">
      <div class="bg-white rounded-2xl p-4 shadow-sm border border-slate-200 space-y-3">
        <h2 class="font-bold text-slate-800 text-base">إضافة منتج جديد للمخزون</h2>
        <input type="text" id="inv-name" placeholder="اسم المنتج" class="w-full bg-slate-50 border border-slate-300 rounded-xl px-3 py-2 text-sm" />
        <div class="grid grid-cols-3 gap-2">
          <input type="number" id="inv-qty" placeholder="الكمية" class="bg-slate-50 border border-slate-300 rounded-xl px-3 py-2 text-sm text-center" />
          <input type="number" id="inv-cost" placeholder="الشراء" class="bg-slate-50 border border-slate-300 rounded-xl px-3 py-2 text-sm text-center" />
          <input type="number" id="inv-price" placeholder="البيع" class="bg-slate-50 border border-slate-300 rounded-xl px-3 py-2 text-sm text-center" />
        </div>
        <div class="flex items-center gap-2">
          <select id="inv-pay-method" class="flex-1 bg-slate-50 border border-slate-300 rounded-xl px-3 py-2 text-xs font-bold">
            <option value="كاش">خصم من: كاش</option>
            <option value="بنكيلي">خصم من: بنكيلي</option>
            <option value="مصرفي">خصم من: مصرفي</option>
            <option value="سداد">خصم من: سداد</option>
          </select>
          <button onclick="addStockPurchase()" class="bg-slate-900 text-white font-bold px-4 py-2 rounded-xl text-xs">+ إضافة</button>
        </div>
      </div>
      <div class="bg-white rounded-2xl p-4 shadow-sm border border-slate-200">
        <h3 class="font-bold text-slate-800 text-sm mb-3">تعديل وإدارة المخزون الحالي</h3>
        <div id="inventory-list" class="space-y-2.5"></div>
      </div>
    </section>

    <!-- 3. الخزينة (قابلة للتعديل والتغيير المباشر) -->
    <section id="tab-treasury" class="hidden space-y-4">
      <div class="bg-white rounded-2xl p-4 shadow-sm border border-slate-200">
        <div class="flex items-center justify-between mb-3">
          <h2 class="font-bold text-slate-800 text-base">النقد والأرصدة (قابلة للتعديل)</h2>
          <span id="audit-badge" class="text-[11px] font-bold bg-emerald-100 text-emerald-800 px-2 py-0.5 rounded-full">✓ مطابق</span>
        </div>
        <div class="grid grid-cols-2 gap-2.5" id="wallet-cards"></div>
      </div>
      <div class="bg-white rounded-2xl p-4 shadow-sm border border-slate-200 space-y-3">
        <h3 class="font-bold text-slate-800 text-sm">مصروفات أو إيداع</h3>
        <div class="grid grid-cols-2 gap-2">
          <select id="tx-type" class="bg-slate-50 border border-slate-300 rounded-xl px-3 py-2 text-xs font-bold">
            <option value="expense">مصروف (خارج)</option>
            <option value="deposit">إيداع (داخل)</option>
          </select>
          <select id="tx-wallet" class="bg-slate-50 border border-slate-300 rounded-xl px-3 py-2 text-xs font-bold">
            <option value="كاش">كاش</option>
            <option value="بنكيلي">بنكيلي</option>
            <option value="مصرفي">مصرفي</option>
            <option value="سداد">سداد</option>
          </select>
        </div>
        <div class="grid grid-cols-3 gap-2">
          <input type="number" id="tx-amount" placeholder="المبلغ" class="col-span-1 bg-slate-50 border border-slate-300 rounded-xl px-3 py-2 text-sm font-bold" />
          <input type="text" id="tx-note" placeholder="البيان" class="col-span-2 bg-slate-50 border border-slate-300 rounded-xl px-3 py-2 text-sm" />
        </div>
        <button onclick="recordFinancialTx()" class="w-full bg-slate-900 text-white font-bold py-2.5 rounded-xl text-xs">حفظ الحركة</button>
      </div>
    </section>

    <!-- 4. السجل (مع إمكانية تعديل وإرجاع المبيعات) -->
    <section id="tab-logs" class="hidden space-y-3">
      <div class="bg-white rounded-2xl p-4 shadow-sm border border-slate-200">
        <div class="flex items-center justify-between mb-3">
          <h2 class="font-bold text-slate-800 text-base">سجل العمليات (تعديل أو إرجاع)</h2>
          <button onclick="resetDemoData()" class="text-[11px] text-rose-600 underline">إعادة ضبط</button>
        </div>
        <div id="logs-list" class="space-y-2.5"></div>
      </div>
    </section>
  </main>

  <nav class="fixed bottom-0 inset-x-0 bg-white border-t border-slate-200 safe-bottom z-30">
    <div class="max-w-lg mx-auto grid grid-cols-4 h-16">
      <button onclick="switchTab('pos', this)" class="nav-btn text-emerald-600 flex flex-col items-center justify-center font-bold text-xs">🛒<span>البيع</span></button>
      <button onclick="switchTab('inventory', this)" class="nav-btn text-slate-400 flex flex-col items-center justify-center font-medium text-xs">📦<span>المخزون</span></button>
      <button onclick="switchTab('treasury', this)" class="nav-btn text-slate-400 flex flex-col items-center justify-center font-medium text-xs">💰<span>الخزينة</span></button>
      <button onclick="switchTab('logs', this)" class="nav-btn text-slate-400 flex flex-col items-center justify-center font-medium text-xs">📋<span>السجل</span></button>
    </div>
  </nav>

  <!-- نافذة تعديل منتج في المخزون -->
  <div id="edit-product-modal" class="hidden fixed inset-0 bg-slate-900/70 z-50 flex items-center justify-center p-4">
    <div class="bg-white rounded-3xl max-w-sm w-full p-5 space-y-3">
      <h3 class="font-extrabold text-base">تعديل بيانات المنتج</h3>
      <input type="hidden" id="edit-prod-id" />
      <div>
        <label class="text-xs font-bold text-slate-600">اسم المنتج</label>
        <input type="text" id="edit-prod-name" class="w-full border rounded-xl px-3 py-2 text-sm font-bold" />
      </div>
      <div class="grid grid-cols-3 gap-2">
        <div>
          <label class="text-xs font-bold text-slate-600">الكمية</label>
          <input type="number" id="edit-prod-qty" class="w-full border rounded-xl px-2 py-2 text-sm text-center font-bold" />
        </div>
        <div>
          <label class="text-xs font-bold text-slate-600">الشراء</label>
          <input type="number" id="edit-prod-cost" class="w-full border rounded-xl px-2 py-2 text-sm text-center font-bold" />
        </div>
        <div>
          <label class="text-xs font-bold text-slate-600">البيع</label>
          <input type="number" id="edit-prod-price" class="w-full border rounded-xl px-2 py-2 text-sm text-center font-bold" />
        </div>
      </div>
      <div class="flex gap-2 pt-2">
        <button onclick="saveEditedProduct()" class="flex-1 bg-emerald-600 text-white font-bold py-2.5 rounded-xl text-xs">حفظ التعديل</button>
        <button onclick="document.getElementById('edit-product-modal').classList.add('hidden')" class="px-4 bg-slate-100 rounded-xl text-xs font-bold">إلغاء</button>
      </div>
    </div>
  </div>

  <!-- نافذة تعديل رصيد وسيلة دفع -->
  <div id="edit-wallet-modal" class="hidden fixed inset-0 bg-slate-900/70 z-50 flex items-center justify-center p-4">
    <div class="bg-white rounded-3xl max-w-sm w-full p-5 space-y-3">
      <h3 class="font-extrabold text-base">تعديل رصيد: <span id="edit-wallet-title"></span></h3>
      <input type="hidden" id="edit-wallet-name" />
      <div>
        <label class="text-xs font-bold text-slate-600">الرصيد الجديد (MRU)</label>
        <input type="number" id="edit-wallet-amount" class="w-full border rounded-xl px-3 py-2 text-base font-bold text-center" />
      </div>
      <div class="flex gap-2 pt-2">
        <button onclick="saveEditedWallet()" class="flex-1 bg-emerald-600 text-white font-bold py-2.5 rounded-xl text-xs">تحديث الرصيد</button>
        <button onclick="document.getElementById('edit-wallet-modal').classList.add('hidden')" class="px-4 bg-slate-100 rounded-xl text-xs font-bold">إلغاء</button>
      </div>
    </div>
  </div>

  <!-- نافذة المستخدم -->
  <div id="user-modal" class="hidden fixed inset-0 bg-slate-900/70 z-50 flex items-center justify-center p-4">
    <div class="bg-white rounded-3xl max-w-sm w-full p-5 space-y-4">
      <h3 class="font-extrabold text-base">اسم المستخدم الحالي</h3>
      <input type="text" id="input-user-name" class="w-full border border-slate-300 rounded-xl px-3 py-2.5 text-sm font-bold" />
      <div class="flex gap-2">
        <button onclick="saveUserName()" class="flex-1 bg-emerald-600 text-white font-bold py-2.5 rounded-xl text-xs">حفظ</button>
        <button onclick="document.getElementById('user-modal').classList.add('hidden')" class="px-4 bg-slate-100 rounded-xl text-xs font-bold">إلغاء</button>
      </div>
    </div>
  </div>

  <div id="toast" class="fixed top-16 inset-x-4 max-w-md mx-auto bg-slate-900 text-white text-xs font-bold px-4 py-3 rounded-xl shadow-lg hidden z-50 text-center"></div>

  <script>
    const WALLETS = ['كاش', 'بنكيلي', 'مصرفي', 'سداد'];
    let selectedPayment = 'كاش';
    let isSimulatedOffline = false;

    const defaultState = {
      userName: 'أحمد',
      products: [
        { id: 'p1', name: 'شاحن آيفون 20W', qty: 15, cost: 600, price: 900 },
        { id: 'p2', name: 'سماعات بلوتوث', qty: 8, cost: 1500, price: 2200 }
      ],
      wallets: { 'كاش': 15000, 'بنكيلي': 8500, 'مصرفي': 4000, 'سداد': 2500 },
      logs: [
        { id: 'l1', type: 'deposit', wallet: 'كاش', amount: 15000, note: 'رصيد افتتاحي', user: 'أحمد', time: '09:00', synced: true },
        { id: 'l2', type: 'deposit', wallet: 'بنكيلي', amount: 8500, note: 'رصيد افتتاحي', user: 'أحمد', time: '09:00', synced: true },
        { id: 'l3', type: 'deposit', wallet: 'مصرفي', amount: 4000, note: 'رصيد افتتاحي', user: 'أحمد', time: '09:00', synced: true },
        { id: 'l4', type: 'deposit', wallet: 'سداد', amount: 2500, note: 'رصيد افتتاحي', user: 'أحمد', time: '09:00', synced: true }
      ]
    };

    let state = JSON.parse(localStorage.getItem('smart_treasury_v3')) || defaultState;
    function saveState() { localStorage.setItem('smart_treasury_v3', JSON.stringify(state)); renderAll(); }
    function showToast(msg, isError = false) {
      const t = document.getElementById('toast');
      t.textContent = msg;
      t.className = `fixed top-16 inset-x-4 max-w-md mx-auto text-white text-xs font-bold px-4 py-3 rounded-xl shadow-lg z-50 text-center ${isError ? 'bg-rose-600' : 'bg-slate-900'}`;
      t.classList.remove('hidden');
      setTimeout(() => t.classList.add('hidden'), 3000);
    }
    function switchTab(tabId, btn) {
      ['pos', 'inventory', 'treasury', 'logs'].forEach(id => document.getElementById('tab-' + id).classList.add('hidden'));
      document.getElementById('tab-' + tabId).classList.remove('hidden');
      document.querySelectorAll('.nav-btn').forEach(b => { b.classList.remove('text-emerald-600', 'font-bold'); b.classList.add('text-slate-400'); });
      btn.classList.remove('text-slate-400'); btn.classList.add('text-emerald-600', 'font-bold');
    }
    function selectPayment(method, btn) {
      selectedPayment = method;
      document.querySelectorAll('.pay-btn').forEach(b => b.className = 'pay-btn bg-slate-50 text-slate-700 border border-slate-300 rounded-xl py-2.5 text-xs font-bold');
      btn.className = 'pay-btn bg-emerald-600 text-white border border-emerald-600 rounded-xl py-2.5 text-xs font-bold';
    }
    function updatePosPrice() {
      const prod = state.products.find(p => p.id === document.getElementById('pos-product-select').value);
      if (prod) document.getElementById('pos-unit-price').value = prod.price;
      updatePosTotalOnly();
    }
    function updatePosTotalOnly() {
      const qty = Number(document.getElementById('pos-qty').value) || 0;
      const price = Number(document.getElementById('pos-unit-price').value) || 0;
      document.getElementById('pos-total-display').textContent = (qty * price).toLocaleString() + ' MRU';
    }

    // إتمام البيع
    function executeSale() {
      const prodId = document.getElementById('pos-product-select').value;
      const qty = Number(document.getElementById('pos-qty').value);
      const unitPrice = Number(document.getElementById('pos-unit-price').value);
      const idx = state.products.findIndex(p => p.id === prodId);
      if (idx === -1 || qty <= 0) return showToast('تحقق من البيانات', true);
      if (state.products[idx].qty < qty) return showToast(`الكمية المتوفرة ${state.products[idx].qty} فقط`, true);
      
      const total = qty * unitPrice;
      state.products[idx].qty -= qty;
      state.wallets[selectedPayment] = (state.wallets[selectedPayment] || 0) + total;
      
      state.logs.unshift({
        id: 'tx_' + Date.now(),
        type: 'sale',
        wallet: selectedPayment,
        amount: total,
        prodId: state.products[idx].id,
        qty: qty,
        note: `بيع ${qty} × ${state.products[idx].name}`,
        user: state.userName,
        time: new Date().toLocaleTimeString('ar-EG', { hour: '2-digit', minute: '2-digit' }),
        synced: !isSimulatedOffline
      });
      saveState();
      document.getElementById('pos-qty').value = 1; updatePosPrice();
      showToast(`تم البيع وإضافة ${total} MRU إلى ${selectedPayment}`);
    }

    // إرجاع مبيعات وعكس أثرها تلقائياً
    function returnSale(logId) {
      const logIdx = state.logs.findIndex(l => l.id === logId);
      if (logIdx === -1) return;
      const log = state.logs[logIdx];
      if (log.type !== 'sale') return;

      // خصم المبلغ من وسيلة الدفع
      if ((state.wallets[log.wallet] || 0) < log.amount) {
        return showToast(`رصيد وسيلة الدفع (${log.wallet}) لا يكفي لإتمام الإرجاع`, true);
      }
      state.wallets[log.wallet] -= log.amount;

      // إرجاع الكمية للمخزون
      const prod = state.products.find(p => p.id === log.prodId);
      if (prod) {
        prod.qty += log.qty;
      } else if (log.prodId) {
        // لو المنتج تم حذفه سابقاً، نعيد إنشاؤه
        state.products.push({ id: log.prodId, name: log.note.replace('بيع ', ''), qty: log.qty, cost: 0, price: 0 });
      }

      // تحديث حالة السجل إلى مُرتجع
      log.type = 'returned';
      log.note = `[مُرتجع] ${log.note}`;
      saveState();
      showToast('تم إرجاع العملية وعكس أثرها على المخزون والخزينة بنجاح');
    }

    // إضافة بضاعة جديدة
    function addStockPurchase() {
      const name = document.getElementById('inv-name').value.trim();
      const qty = Number(document.getElementById('inv-qty').value);
      const cost = Number(document.getElementById('inv-cost').value);
      const price = Number(document.getElementById('inv-price').value);
      const wallet = document.getElementById('inv-pay-method').value;
      if (!name || qty <= 0 || price <= 0) return showToast('أكمل البيانات', true);
      const totalCost = qty * cost;
      if ((state.wallets[wallet] || 0) < totalCost) return showToast(`رصيد ${wallet} غير كافٍ`, true);
      
      state.products.push({ id: 'p_' + Date.now(), name, qty, cost, price });
      state.wallets[wallet] -= totalCost;
      state.logs.unshift({ id: 'tx_' + Date.now(), type: 'purchase', wallet, amount: totalCost, note: `شراء مخزون: ${qty} × ${name}`, user: state.userName, time: new Date().toLocaleTimeString('ar-EG', { hour: '2-digit', minute: '2-digit' }), synced: !isSimulatedOffline });
      ['inv-name', 'inv-qty', 'inv-cost', 'inv-price'].forEach(id => document.getElementById(id).value = '');
      saveState(); showToast('تمت الإضافة للمخزون');
    }

    // تعديل المخزون
    function openEditProduct(id) {
      const p = state.products.find(item => item.id === id);
      if (!p) return;
      document.getElementById('edit-prod-id').value = p.id;
      document.getElementById('edit-prod-name').value = p.name;
      document.getElementById('edit-prod-qty').value = p.qty;
      document.getElementById('edit-prod-cost').value = p.cost;
      document.getElementById('edit-prod-price').value = p.price;
      document.getElementById('edit-product-modal').classList.remove('hidden');
    }
    function saveEditedProduct() {
      const id = document.getElementById('edit-prod-id').value;
      const p = state.products.find(item => item.id === id);
      if (!p) return;
      p.name = document.getElementById('edit-prod-name').value.trim();
      p.qty = Number(document.getElementById('edit-prod-qty').value);
      p.cost = Number(document.getElementById('edit-prod-cost').value);
      p.price = Number(document.getElementById('edit-prod-price').value);
      saveState();
      document.getElementById('edit-product-modal').classList.add('hidden');
      showToast('تم تحديث المنتج بنجاح');
    }

    // تعديل رصيد الخزينة مباشرة
    function openEditWallet(walletName) {
      document.getElementById('edit-wallet-name').value = walletName;
      document.getElementById('edit-wallet-title').textContent = walletName;
      document.getElementById('edit-wallet-amount').value = state.wallets[walletName] || 0;
      document.getElementById('edit-wallet-modal').classList.remove('hidden');
    }
    function saveEditedWallet() {
      const wName = document.getElementById('edit-wallet-name').value;
      const newAmt = Number(document.getElementById('edit-wallet-amount').value);
      const oldAmt = state.wallets[wName] || 0;
      const diff = newAmt - oldAmt;
      
      state.wallets[wName] = newAmt;
      state.logs.unshift({
        id: 'tx_' + Date.now(),
        type: diff >= 0 ? 'deposit' : 'expense',
        wallet: wName,
        amount: Math.abs(diff),
        note: `تعديل يدوي لرصيد ${wName} (${oldAmt} ➔ ${newAmt})`,
        user: state.userName,
        time: new Date().toLocaleTimeString('ar-EG', { hour: '2-digit', minute: '2-digit' }),
        synced: !isSimulatedOffline
      });
      saveState();
      document.getElementById('edit-wallet-modal').classList.add('hidden');
      showToast('تم تحديث رصيد الخزينة وتعديل السجل');
    }

    function recordFinancialTx() {
      const type = document.getElementById('tx-type').value;
      const wallet = document.getElementById('tx-wallet').value;
      const amount = Number(document.getElementById('tx-amount').value);
      const note = document.getElementById('tx-note').value.trim() || (type === 'expense' ? 'مصروف' : 'إيداع');
      if (amount <= 0) return showToast('أدخل مبلغاً صحيحاً', true);
      if (type === 'expense' && (state.wallets[wallet] || 0) < amount) return showToast(`رصيد ${wallet} لا يكفي`, true);
      
      state.wallets[wallet] = type === 'expense' ? state.wallets[wallet] - amount : (state.wallets[wallet] || 0) + amount;
      state.logs.unshift({ id: 'tx_' + Date.now(), type, wallet, amount, note, user: state.userName, time: new Date().toLocaleTimeString('ar-EG', { hour: '2-digit', minute: '2-digit' }), synced: !isSimulatedOffline });
      document.getElementById('tx-amount').value = ''; document.getElementById('tx-note').value = '';
      saveState(); showToast('تم حفظ الحركة');
    }

    function toggleSimulatedOffline() {
      isSimulatedOffline = !isSimulatedOffline;
      document.getElementById('status-text').textContent = isSimulatedOffline ? 'غير متصل' : 'متصل ومزامن';
      document.getElementById('offline-banner').classList.toggle('hidden', !isSimulatedOffline);
      if (!isSimulatedOffline) { state.logs.forEach(l => l.synced = true); saveState(); showToast('تمت المزامنة ✓'); }
    }
    function openUserModal() { document.getElementById('input-user-name').value = state.userName; document.getElementById('user-modal').classList.remove('hidden'); }
    function saveUserName() {
      const n = document.getElementById('input-user-name').value.trim();
      if (n) { state.userName = n; saveState(); document.getElementById('user-modal').classList.add('hidden'); }
    }
    function resetDemoData() { localStorage.removeItem('smart_treasury_v3'); state = JSON.parse(JSON.stringify(defaultState)); saveState(); }

    function renderAll() {
      document.getElementById('current-user-name').textContent = state.userName;
      const select = document.getElementById('pos-product-select');
      const prev = select.value;
      select.innerHTML = state.products.map(p => `<option value="${p.id}" ${p.qty === 0 ? 'disabled' : ''}>${p.name} (${p.qty}) — ${p.price} MRU</option>`).join('');
      if (prev && state.products.some(p => p.id === prev)) select.value = prev;
      updatePosPrice();

      // قائمة المخزون مع زر تعديل لكل منتج
      document.getElementById('inventory-list').innerHTML = state.products.map(p => `
        <div class="flex items-center justify-between p-3 rounded-xl bg-slate-50 border">
          <div>
            <div class="font-bold text-sm">${p.name}</div>
            <div class="text-xs text-slate-500">شراء: ${p.cost} | بيع: ${p.price} | كمية: <span class="font-extrabold text-slate-800">${p.qty}</span></div>
          </div>
          <button onclick="openEditProduct('${p.id}')" class="bg-sky-50 text-sky-600 px-3 py-1.5 rounded-lg text-xs font-bold border border-sky-200">تعديل</button>
        </div>
      `).join('');

      let totalCash = 0, matched = true;
      document.getElementById('wallet-cards').innerHTML = WALLETS.map(w => {
        const bal = state.wallets[w] || 0; totalCash += bal;
        return `
          <div class="p-3 rounded-xl bg-slate-50 border flex items-center justify-between">
            <div>
              <div class="text-xs font-bold text-slate-600">${w}</div>
              <div class="text-base font-extrabold mt-1">${bal.toLocaleString()} MRU</div>
            </div>
            <button onclick="openEditWallet('${w}')" class="bg-slate-200 hover:bg-slate-300 text-slate-700 px-2.5 py-1.5 rounded-lg text-xs font-bold">تغيير</button>
          </div>
        `;
      }).join('');

      document.getElementById('summary-total-cash').textContent = totalCash.toLocaleString() + ' MRU';
      document.getElementById('summary-stock-value').textContent = state.products.reduce((a, p) => a + p.qty * p.cost, 0).toLocaleString() + ' MRU';
      document.getElementById('audit-badge').textContent = '✓ محدث';
      document.getElementById('pending-count').textContent = state.logs.filter(l => !l.synced).length;

      // السجل مع زر إرجاع لعمليات البيع
      document.getElementById('logs-list').innerHTML = state.logs.map(l => {
        const isIn = l.type === 'sale' || l.type === 'deposit';
        const isSale = l.type === 'sale';
        return `
          <div class="p-3 rounded-xl bg-slate-50 border flex items-center justify-between">
            <div class="space-y-0.5">
              <div class="font-bold text-xs">${l.note}</div>
              <div class="text-[11px] text-slate-500">👤 ${l.user} • ${l.wallet} • ${l.time} ${!l.synced ? '⏳' : '✓'}</div>
            </div>
            <div class="flex items-center gap-2">
              <div class="font-extrabold text-xs ${isIn ? 'text-emerald-600' : 'text-rose-600'}">${isIn ? '+' : '-'}${l.amount.toLocaleString()}</div>
              ${isSale ? `<button onclick="returnSale('${l.id}')" class="bg-rose-50 text-rose-600 px-2 py-1 rounded-lg text-[10px] font-bold border border-rose-200">إرجاع</button>` : ''}
            </div>
          </div>
        `;
      }).join('');
    }
    renderAll();
  </script>
</body>
</html>
