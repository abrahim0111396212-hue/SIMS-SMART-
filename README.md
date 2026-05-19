لقد قمت بإعداد ملف index.html كامل ومتكامل، يحتوي على جميع الميزات التي 
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes, viewport-fit=cover">
    <title>SIM-ERP | نظام تخطيط موارد المؤسسات</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.1.1/crypto-js.min.js"></script>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', -apple-system, BlinkMacSystemFont, Roboto, sans-serif; }
        body { background: #f0f4f8; display: flex; justify-content: center; align-items: center; padding: 12px; min-height: 100vh; }
        .app-container { width: 100%; max-width: 550px; background: #fff; border-radius: 32px; box-shadow: 0 20px 40px rgba(0,0,0,0.05); overflow: hidden; height: 85vh; max-height: 800px; display: flex; flex-direction: column; }
        .screen { flex: 1; overflow-y: auto; padding: 20px 16px; display: none; background: #fff; }
        .screen.active { display: block; }
        .header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; gap: 8px; flex-wrap: wrap; position: sticky; top: 0; background: #fff; z-index: 10; padding-bottom: 5px; }
        .logo-circle { width: 44px; height: 44px; border-radius: 28px; background: #1e3a5f; display: flex; align-items: center; justify-content: center; color: white; font-weight: 600; font-size: 12px; }
        .page-title { font-size: 22px; font-weight: 700; color: #1e293b; }
        .lang-btn, .logout-btn { background: #eef2ff; border: none; border-radius: 30px; padding: 5px 12px; cursor: pointer; font-size: 12px; font-weight: 500; }
        .logout-btn { background: #fee2e2; color: #b91c1c; }
        .digital-cards { display: flex; gap: 10px; margin-bottom: 20px; }
        .digital-card { flex: 1; background: #f8fafc; border-radius: 24px; padding: 12px 6px; text-align: center; border: 1px solid #e2e8f0; }
        .digital-card .label { font-size: 11px; color: #64748b; }
        .digital-card .value { font-size: 18px; font-weight: 700; }
        .stats-bar { display: flex; gap: 10px; background: #f8fafc; border-radius: 24px; padding: 10px; margin-bottom: 20px; }
        .stat-card { flex: 1; text-align: center; }
        .stat-value { font-size: 20px; font-weight: 700; color: #1e3a5f; }
        .input-group { margin-bottom: 14px; }
        .input-group label { display: block; margin-bottom: 5px; font-size: 12px; font-weight: 500; color: #334155; }
        .input-group input, .input-group select, .input-group textarea { width: 100%; padding: 10px 12px; background: #fff; border: 1px solid #e2e8f0; border-radius: 20px; font-size: 13px; }
        .btn { width: 100%; padding: 12px; border: none; border-radius: 28px; font-size: 14px; font-weight: 600; cursor: pointer; margin-bottom: 10px; transition: all 0.2s; }
        .btn-primary { background: #1e3a5f; color: white; }
        .btn-secondary { background: #f1f5f9; color: #1e3a5f; border: 1px solid #e2e8f0; }
        .btn-success { background: #10b981; color: white; }
        .icons-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 12px; margin: 20px 0; }
        .icon-item { display: flex; flex-direction: column; align-items: center; cursor: pointer; gap: 5px; }
        .icon-circle { width: 48px; height: 48px; border-radius: 28px; background: #eef2ff; display: flex; align-items: center; justify-content: center; font-size: 22px; transition: 0.2s; }
        .icon-item:hover .icon-circle { background: #1e3a5f; color: white; }
        .icon-label { font-size: 10px; color: #475569; text-align: center; }
        .table-container { overflow-x: auto; margin: 12px 0; background: #fff; border-radius: 20px; border: 1px solid #e2e8f0; }
        table { width: 100%; border-collapse: collapse; font-size: 12px; min-width: 480px; }
        th { background: #1e3a5f; color: white; padding: 10px 8px; font-weight: 600; text-align: center; }
        td { padding: 8px 6px; border-bottom: 1px solid #e2e8f0; text-align: center; }
        .action-btn { background: none; border: none; cursor: pointer; font-size: 16px; padding: 4px 6px; border-radius: 8px; }
        .status-good { background: #dcfce7; color: #15803d; padding: 3px 8px; border-radius: 40px; display: inline-block; font-size: 10px; }
        .status-medium { background: #fef9c3; color: #854d0e; padding: 3px 8px; border-radius: 40px; display: inline-block; font-size: 10px; }
        .status-critical { background: #fee2e2; color: #b91c1c; padding: 3px 8px; border-radius: 40px; display: inline-block; font-size: 10px; }
        .tabs { display: flex; gap: 6px; margin: 16px 0; flex-wrap: wrap; }
        .tab { flex: 1; padding: 8px; background: #f1f5f9; border: none; border-radius: 30px; cursor: pointer; font-weight: 500; font-size: 12px; text-align: center; }
        .tab.active { background: #1e3a5f; color: white; }
        .legend-colors { display: flex; justify-content: center; gap: 20px; margin-bottom: 16px; background: #f8fafc; padding: 6px 12px; border-radius: 60px; width: fit-content; margin: 0 auto 16px; }
        .legend-color { width: 10px; height: 10px; border-radius: 50%; display: inline-block; margin-left: 4px; }
        .legend-green { background: #22c55e; }
        .legend-yellow { background: #eab308; }
        .legend-red { background: #ef4444; }
        .welcome-message { background: #eef2ff; padding: 14px; border-radius: 28px; margin-bottom: 20px; text-align: center; font-size: 14px; }
        .forecast-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px; }
        .forecast-item { background: #fff; padding: 10px; border-radius: 20px; text-align: center; border: 1px solid #e2e8f0; }
        .forecast-item .label { font-size: 10px; color: #64748b; }
        .forecast-item .value { font-size: 14px; font-weight: 700; }
        .recommendation { margin-top: 14px; padding: 12px; border-radius: 28px; text-align: center; font-weight: 600; font-size: 13px; }
        .rec-buy { background: #dcfce7; color: #15803d; }
        .rec-sell { background: #fee2e2; color: #b91c1c; }
        .modal-fullscreen { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.7); backdrop-filter: blur(8px); z-index: 2000; display: none; justify-content: center; align-items: center; padding: 20px; }
        .modal-fullscreen .modal-content { background: #fff; border-radius: 32px; max-width: 440px; width: 100%; max-height: 85%; overflow-y: auto; padding: 20px; }
        .close-modal { background: #eef2ff; border: none; border-radius: 40px; padding: 10px; width: 100%; font-weight: 600; cursor: pointer; margin-bottom: 16px; }
        .profit-positive { color: #10b981; font-weight: bold; }
        hr { margin: 16px 0; border-top: 1px solid #e2e8f0; }
        .search-box { width: 100%; padding: 10px 14px; border: 1px solid #e2e8f0; border-radius: 40px; margin-bottom: 14px; font-size: 13px; }
        .otp-group { display: flex; gap: 8px; align-items: center; margin-top: 8px; }
        .otp-group input { flex: 2; }
        .otp-group button { flex: 1; padding: 8px; font-size: 12px; margin: 0; }
        .timer { font-size: 11px; color: #1e3a5f; margin-top: 5px; }
        .link-btn { background: none; color: #1e3a5f; border: none; font-size: 12px; cursor: pointer; width: 100%; margin-top: 6px; }
        @media (max-width: 450px) {
            .digital-card .value { font-size: 16px; }
            .stat-value { font-size: 18px; }
            .icon-circle { width: 44px; height: 44px; font-size: 20px; }
            .icon-label { font-size: 9px; }
            .btn { padding: 10px; font-size: 13px; }
        }
    </style>
</head>
<body>
<div class="app-container">
    <!-- شاشة تسجيل الدخول -->
    <div class="screen active" id="loginScreen">
        <div class="header">
            <div class="page-title" data-i18n="loginTitle">تسجيل الدخول</div>
            <button class="lang-btn" onclick="toggleLanguage()">🌐 English</button>
            <div class="logo-circle">ERP</div>
        </div>
        <div class="input-group"><label data-i18n="usernameLabel">البريد أو الهاتف</label><input type="text" id="username" placeholder="admin@sims.com"></div>
        <div class="input-group"><label data-i18n="passwordLabel">كلمة المرور</label><input type="password" id="password" placeholder="admin123"></div>
        <button class="btn btn-primary" onclick="login()" data-i18n="loginBtn">دخول</button>
        <button class="btn btn-secondary" onclick="showRegister()" data-i18n="registerBtn">حساب جديد</button>
        <button class="link-btn" onclick="showForgotPassword()" data-i18n="forgotBtn">نسيت كلمة المرور؟</button>
    </div>

    <!-- شاشة التسجيل مع OTP -->
    <div class="screen" id="registerScreen">
        <div class="header"><div class="page-title" data-i18n="registerTitle">حساب جديد</div><div class="logo-circle">ERP</div></div>
        <div class="input-group"><label data-i18n="nameLabel">الاسم</label><input type="text" id="regName"></div>
        <div class="input-group"><label data-i18n="emailLabel">البريد الإلكتروني</label><input type="email" id="regEmail"></div>
        <div class="input-group"><label data-i18n="phoneLabel">رقم الهاتف (يبدأ 249)</label><input type="tel" id="regPhone" placeholder="249XXXXXXXXX"></div>
        <div class="input-group"><label data-i18n="regPassLabel">كلمة المرور</label><input type="password" id="regPassword"></div>
        <div class="input-group"><label data-i18n="sectorLabel">القطاع</label>
            <select id="regSector">
                <option value="صناعي">صناعي</option><option value="تجاري">تجاري</option><option value="صيدليات">صيدليات</option>
                <option value="مصانع">مصانع</option><option value="بقالات">بقالات</option><option value="سوبرماركت">سوبرماركت</option>
                <option value="فني (ورش/صيانة)">فني (ورش/صيانة)</option><option value="مغالق (تفصيل/خياطة)">مغالق (تفصيل/خياطة)</option>
                <option value="الكترونيات">الكترونيات</option><option value="مواد بناء">مواد بناء</option><option value="أخرى">أخرى</option>
            </select>
        </div>
        <div class="input-group"><label data-i18n="branchLabel">اسم الفرع</label><input type="text" id="regBranch"></div>
        <div class="input-group">
            <label>📱 التحقق عبر رقم الهاتف (OTP)</label>
            <div class="otp-group">
                <input type="text" id="otpCode" placeholder="رمز التحقق" maxlength="6">
                <button class="btn btn-secondary" id="sendOtpBtn" onclick="sendOTP()">إرسال الرمز</button>
            </div>
            <div class="timer" id="otpTimer"></div>
        </div>
        <button class="btn btn-primary" onclick="registerWithOTP()" data-i18n="createBtn">إنشاء حساب</button>
        <button class="btn btn-secondary" onclick="showLogin()" data-i18n="backBtn">رجوع</button>
    </div>

    <!-- شاشة استعادة كلمة المرور -->
    <div class="screen" id="forgotPasswordScreen">
        <div class="header"><div class="page-title" data-i18n="forgotTitle">استعادة كلمة المرور</div><div class="logo-circle">ERP</div></div>
        <div class="input-group"><label data-i18n="forgotUserLabel">رقم الهاتف (249xxxxxxxxx)</label><input type="text" id="forgotPhone"></div>
        <div class="otp-group"><input type="text" id="forgotOtp" placeholder="رمز التحقق"><button onclick="sendForgotOTP()">إرسال الرمز</button></div>
        <div class="input-group"><label>كلمة المرور الجديدة</label><input type="password" id="newPassReset"></div>
        <button class="btn btn-primary" onclick="resetPassword()">إعادة تعيين</button>
        <button class="btn btn-secondary" onclick="showLogin()" data-i18n="backBtn">رجوع</button>
    </div>

    <!-- اللوحة الرئيسية -->
    <div class="screen" id="mainScreen">
        <div class="header">
            <div class="page-title" data-i18n="dashboardTitle">لوحة التحكم</div>
            <div style="display: flex; gap: 6px;"><button class="lang-btn" onclick="toggleLanguage()">🌐</button><button class="logout-btn" onclick="logout()" data-i18n="logoutBtn">خروج</button></div>
            <div class="logo-circle">ERP</div>
        </div>
        <div class="welcome-message" id="welcomeMessage"></div>
        <div class="digital-cards">
            <div class="digital-card"><div class="label" data-i18n="capitalLabel">رأس المال</div><div class="value" id="capitalValue">0</div></div>
            <div class="digital-card"><div class="label" data-i18n="profitLabel">صافي الأرباح</div><div class="value" id="profitValue">0</div></div>
            <div class="digital-card"><div class="label" data-i18n="totalSalesLabel">إجمالي المبيعات</div><div class="value" id="totalSalesValue">0</div></div>
        </div>
        <div class="stats-bar">
            <div class="stat-card"><div class="stat-value" id="totalProductsStat">0</div><div data-i18n="productsLabel">المنتجات</div></div>
            <div class="stat-card"><div class="stat-value" id="totalSalesCountStat">0</div><div data-i18n="salesCountLabel">عمليات البيع</div></div>
            <div class="stat-card"><div class="stat-value" id="totalPurchasesStat">0</div><div data-i18n="purchasesLabel">المشتريات</div></div>
        </div>
        <div class="icons-grid">
            <div class="icon-item" onclick="showAllProducts()"><div class="icon-circle">📊</div><span data-i18n="productsIcon">المنتجات</span></div>
            <div class="icon-item" onclick="showAddProduct()"><div class="icon-circle">➕</div><span data-i18n="addIcon">إضافة</span></div>
            <div class="icon-item" onclick="showSellProduct()"><div class="icon-circle">💰</div><span data-i18n="sellIcon">بيع</span></div>
            <div class="icon-item" onclick="showReturnProduct()"><div class="icon-circle">🔄</div><span data-i18n="returnIcon">إرجاع</span></div>
            <div class="icon-item" onclick="showInvoices()"><div class="icon-circle">📄</div><span data-i18n="invoicesIcon">الفواتير</span></div>
            <div class="icon-item" onclick="showInventoryAudit()"><div class="icon-circle">📋</div><span data-i18n="auditIcon">جرد</span></div>
            <div class="icon-item" onclick="showInspectProducts()"><div class="icon-circle">🔍</div><span data-i18n="inspectIcon">فحص</span></div>
            <div class="icon-item" onclick="showEconomicOrder()"><div class="icon-circle">📈</div><span data-i18n="eoqIcon">الكمية الاقتصادية</span></div>
            <div class="icon-item" onclick="showForecast()"><div class="icon-circle">🔮</div><span data-i18n="forecastIcon">تنبؤ</span></div>
            <div class="icon-item" onclick="showSettings()"><div class="icon-circle">⚙️</div><span data-i18n="settingsIcon">ضبط</span></div>
            <div class="icon-item" onclick="showBankStatement()"><div class="icon-circle">🏦</div><span data-i18n="statementIcon">كشف حساب</span></div>
            <div class="icon-item" onclick="showFinancialReports()"><div class="icon-circle">📑</div><span data-i18n="reportsIcon">تقارير مالية</span></div>
        </div>
    </div>

    <!-- شاشة جميع المنتجات -->
    <div class="screen" id="allProductsScreen">
        <div class="header"><div class="page-title" data-i18n="allProductsTitle">جميع المنتجات</div><div class="logo-circle">ERP</div></div>
        <div class="legend-colors"><span><span class="legend-color legend-green"></span> <span data-i18n="goodStatus">جيد</span></span><span><span class="legend-color legend-yellow"></span> <span data-i18n="mediumStatus">متوسط</span></span><span><span class="legend-color legend-red"></span> <span data-i18n="criticalStatus">حرج</span></span></div>
        <input type="text" class="search-box" id="searchProducts" placeholder="بحث..." onkeyup="renderProductsTable()">
        <div id="productsTableContainer"></div>
        <button class="btn btn-secondary" onclick="backToMain()" data-i18n="backBtn">رجوع</button>
    </div>

    <!-- شاشة إضافة منتج -->
    <div class="screen" id="addProductScreen">
        <div class="header"><div class="page-title" data-i18n="addTitle">إضافة منتج</div><div class="logo-circle">ERP</div></div>
        <div class="input-group"><label data-i18n="productNameLabel">اسم المنتج</label><input type="text" id="productName"></div>
        <div class="input-group"><label data-i18n="productQtyLabel">الكمية</label><input type="number" id="productQuantity" value="0"></div>
        <div class="input-group"><label data-i18n="productPurchaseLabel">سعر الشراء</label><input type="number" id="purchasePrice" value="0"></div>
        <div class="input-group"><label data-i18n="productSellingLabel">سعر البيع</label><input type="number" id="sellingPrice" value="0"></div>
        <div class="input-group"><label data-i18n="productMinLabel">الحد الأدنى</label><input type="number" id="minLimit"></div>
        <div class="input-group"><label data-i18n="productProdDateLabel">تاريخ الإنتاج</label><input type="date" id="productionDate"></div>
        <div class="input-group"><label data-i18n="productExpDateLabel">تاريخ الانتهاء</label><input type="date" id="expiryDate"></div>
        <button class="btn btn-primary" onclick="addProduct()" data-i18n="confirmAddBtn">إضافة منتج</button>
        <button class="btn btn-secondary" onclick="backToMain()" data-i18n="backBtn">رجوع</button>
    </div>

    <!-- شاشة بيع -->
    <div class="screen" id="sellProductScreen">
        <div class="header"><div class="page-title" data-i18n="sellTitle">بيع منتج</div><div class="logo-circle">ERP</div></div>
        <div class="input-group"><label data-i18n="productSelectLabel">المنتج</label><select id="sellProductSelect" onchange="updateTotalPrice()"></select></div>
        <div class="input-group"><label data-i18n="sellQtyLabel">الكمية</label><input type="number" id="sellQuantity" oninput="updateTotalPrice()"></div>
        <div class="input-group"><label data-i18n="totalLabel">الإجمالي</label><input type="text" id="totalPrice" readonly></div>
        <div class="input-group"><label data-i18n="buyerPhoneLabel">رقم المشتري</label><input type="text" id="buyerPhone"></div>
        <div class="input-group"><label data-i18n="buyerNameLabel">اسم المشتري</label><input type="text" id="buyerName"></div>
        <button class="btn btn-primary" onclick="sellProduct()" data-i18n="confirmSellBtn">تأكيد البيع</button>
        <button class="btn btn-secondary" onclick="backToMain()" data-i18n="backBtn">رجوع</button>
    </div>

    <!-- شاشة إرجاع -->
    <div class="screen" id="returnProductScreen">
        <div class="header"><div class="page-title" data-i18n="returnTitle">إرجاع مبيعات</div><div class="logo-circle">ERP</div></div>
        <div class="input-group"><label data-i18n="selectSaleLabel">اختر عملية بيع</label><select id="returnSaleSelect"></select></div>
        <div class="input-group"><label data-i18n="returnReasonLabel">سبب الإرجاع</label><select id="returnReason"><option>خطأ في البيع</option><option>إرجاع من العميل</option></select></div>
        <button class="btn btn-primary" onclick="returnSale()" data-i18n="confirmReturnBtn">تأكيد الإرجاع</button>
        <button class="btn btn-secondary" onclick="backToMain()" data-i18n="backBtn">رجوع</button>
    </div>

    <!-- الفواتير -->
    <div class="screen" id="invoicesScreen">
        <div class="header"><div class="page-title" data-i18n="invoicesTitle">الفواتير</div><div class="logo-circle">ERP</div></div>
        <div class="tabs"><button class="tab active" onclick="showInvoicesList('all')" data-i18n="allTab">الكل</button><button class="tab" onclick="showInvoicesList('purchase')" data-i18n="purchasesTab">مشتريات</button><button class="tab" onclick="showInvoicesList('sale')" data-i18n="salesTab">مبيعات</button></div>
        <div id="invoicesList"></div>
        <button class="btn btn-secondary" onclick="backToMain()" data-i18n="backBtn">رجوع</button>
    </div>

    <!-- كشف الحساب -->
    <div class="screen" id="statementScreen">
        <div class="header"><div class="page-title" data-i18n="statementTitle">كشف الحساب</div><div class="logo-circle">ERP</div></div>
        <div class="tabs"><button class="tab active" onclick="showPurchaseStatement()" data-i18n="purchasesStmtTab">المشتريات</button><button class="tab" onclick="showSalesStatement()" data-i18n="salesStmtTab">المبيعات</button></div>
        <div id="statementContent"></div>
        <button class="btn btn-secondary" onclick="backToMain()" data-i18n="backBtn">رجوع</button>
    </div>

    <!-- الكمية الاقتصادية -->
    <div class="screen" id="economicOrderScreen">
        <div class="header"><div class="page-title" data-i18n="eoqTitle">الكمية الاقتصادية</div><div class="logo-circle">ERP</div></div>
        <div id="economicContent"></div>
        <button class="btn btn-secondary" onclick="backToMain()" data-i18n="backBtn">رجوع</button>
    </div>

    <!-- التنبؤ -->
    <div class="screen" id="forecastScreen">
        <div class="header"><div class="page-title" data-i18n="forecastTitle">التنبؤ الذكي</div><div class="logo-circle">ERP</div></div>
        <div id="forecastContent"></div>
        <button class="btn btn-secondary" onclick="backToMain()" data-i18n="backBtn">رجوع</button>
    </div>

    <!-- التقارير المالية -->
    <div class="screen" id="financialReportsScreen">
        <div class="header"><div class="page-title" data-i18n="financialTitle">التقارير المالية</div><div class="logo-circle">ERP</div></div>
        <div class="tabs"><button class="tab active" onclick="showIncomeStatement()" data-i18n="incomeTab">قائمة الدخل</button><button class="tab" onclick="showBalanceSheet()" data-i18n="balanceTab">الميزانية</button><button class="tab" onclick="showCashFlow()" data-i18n="cashflowTab">التدفقات</button></div>
        <div id="financialReportContent"></div>
        <button class="btn btn-secondary" onclick="backToMain()" data-i18n="backBtn">رجوع</button>
    </div>

    <!-- الضبط -->
    <div class="screen" id="settingsScreen">
        <div class="header"><div class="page-title" data-i18n="settingsTitle">الضبط</div><div class="logo-circle">ERP</div></div>
        <div class="input-group"><label data-i18n="oldPassLabel">كلمة المرور القديمة</label><input type="password" id="oldPass"></div>
        <div class="input-group"><label data-i18n="newPassLabel">كلمة المرور الجديدة</label><input type="password" id="newPass"></div>
        <button class="btn btn-primary" onclick="changePassword()" data-i18n="changePassBtn">تغيير كلمة المرور</button>
        <hr><h4 data-i18n="securityTitle">أسئلة الأمان</h4>
        <div class="security-question"><label data-i18n="secQ1Label">اسم والدتك؟</label><input type="text" id="secQ1"></div>
        <div class="security-question"><label data-i18n="secQ2Label">أول مدرسة؟</label><input type="text" id="secQ2"></div>
        <button class="btn btn-primary" onclick="saveSecurityQuestions()" data-i18n="saveSecurityBtn">حفظ</button>
        <button class="btn btn-secondary" onclick="backToMain()" data-i18n="backBtn">رجوع</button>
    </div>

    <!-- فحص ذكي -->
    <div class="screen" id="inspectScreen">
        <div class="header"><div class="page-title" data-i18n="inspectTitle">فحص ذكي</div><div class="logo-circle">ERP</div></div>
        <div class="input-group"><label data-i18n="barcodeLabel">باركود المنتج</label><input type="text" id="inspectBarcode"></div>
        <button class="btn btn-primary" onclick="inspectByBarcode()" data-i18n="inspectBtn">فحص</button>
        <div id="inspectDetails"></div>
        <button class="btn btn-secondary" onclick="backToMain()" data-i18n="backBtn">رجوع</button>
    </div>

    <!-- شاشة الجرد -->
    <div class="screen" id="auditScreen">
        <div class="header"><div class="page-title" data-i18n="auditTitle">جرد المخزون</div><div class="logo-circle">ERP</div></div>
        <div class="input-group"><label data-i18n="auditTypeLabel">نوع الجرد</label><select id="auditType"><option value="all" data-i18n="auditAll">جميع المنتجات</option><option value="single" data-i18n="auditSingle">منتج محدد</option></select></div>
        <div class="input-group" id="auditSingleDiv" style="display:none;"><label data-i18n="selectProductLabel">اختر منتج</label><select id="auditProductSelect"></select></div>
        <button class="btn btn-primary" onclick="prepareAudit()" data-i18n="startAuditBtn">بدء الجرد</button>
        <div id="auditProductsList"></div>
        <div id="auditForm" style="display: none; margin-top: 16px;">
            <div class="input-group"><label data-i18n="auditActualQty">الكمية الفعلية بعد الجرد</label><input type="number" id="auditActualQty" step="1" value="0"></div>
            <div class="input-group"><label data-i18n="auditNewPrice">سعر الجرد الجديد</label><input type="number" id="auditNewPrice" step="0.01" value="0"></div>
            <div class="input-group"><label data-i18n="auditNotes">ملاحظات الجرد</label><textarea id="auditNotes" rows="2"></textarea></div>
            <button class="btn btn-success" onclick="executeAudit()" data-i18n="executeAuditBtn">جرد الآن ✅</button>
        </div>
        <div id="auditResults"></div>
        <button class="btn btn-secondary" onclick="backToMain()" data-i18n="backBtn">رجوع</button>
    </div>

    <div id="notificationModal" class="modal-fullscreen">
        <div class="modal-content">
            <button class="close-modal" onclick="closeNotificationModal()" data-i18n="closeModalBtn">إغلاق</button>
            <div id="modalNotificationContent"></div>
        </div>
    </div>
</div>

<script>
    // -------------------- الترجمة --------------------
    let currentLang = 'ar';
    const translations = {
        ar: {
            loginTitle: 'تسجيل الدخول', usernameLabel: 'البريد أو الهاتف', passwordLabel: 'كلمة المرور', loginBtn: 'دخول', registerBtn: 'حساب جديد', forgotBtn: 'نسيت كلمة المرور؟',
            registerTitle: 'حساب جديد', nameLabel: 'الاسم', emailLabel: 'البريد الإلكتروني', phoneLabel: 'رقم الهاتف (يبدأ 249)', regPassLabel: 'كلمة المرور', sectorLabel: 'القطاع', branchLabel: 'اسم الفرع', createBtn: 'إنشاء حساب', backBtn: 'رجوع',
            dashboardTitle: 'لوحة التحكم', logoutBtn: 'خروج', capitalLabel: 'رأس المال', profitLabel: 'صافي الأرباح', totalSalesLabel: 'إجمالي المبيعات',
            productsLabel: 'المنتجات', salesCountLabel: 'عمليات البيع', purchasesLabel: 'المشتريات', productsIcon: 'المنتجات', addIcon: 'إضافة', sellIcon: 'بيع', returnIcon: 'إرجاع',
            invoicesIcon: 'الفواتير', auditIcon: 'جرد', inspectIcon: 'فحص', eoqIcon: 'الكمية الاقتصادية', forecastIcon: 'تنبؤ', settingsIcon: 'ضبط', statementIcon: 'كشف حساب', reportsIcon: 'تقارير مالية',
            allProductsTitle: 'جميع المنتجات', goodStatus: 'جيد', mediumStatus: 'متوسط', criticalStatus: 'حرج',
            addTitle: 'إضافة منتج', productNameLabel: 'اسم المنتج', productQtyLabel: 'الكمية', productPurchaseLabel: 'سعر الشراء', productSellingLabel: 'سعر البيع', productMinLabel: 'الحد الأدنى',
            productProdDateLabel: 'تاريخ الإنتاج', productExpDateLabel: 'تاريخ الانتهاء', confirmAddBtn: 'إضافة منتج',
            sellTitle: 'بيع منتج', productSelectLabel: 'المنتج', sellQtyLabel: 'الكمية', totalLabel: 'الإجمالي', buyerPhoneLabel: 'رقم المشتري', buyerNameLabel: 'اسم المشتري', confirmSellBtn: 'تأكيد البيع',
            returnTitle: 'إرجاع مبيعات', selectSaleLabel: 'اختر عملية بيع', returnReasonLabel: 'سبب الإرجاع', confirmReturnBtn: 'تأكيد الإرجاع',
            invoicesTitle: 'الفواتير', allTab: 'الكل', purchasesTab: 'مشتريات', salesTab: 'مبيعات',
            statementTitle: 'كشف الحساب', purchasesStmtTab: 'المشتريات', salesStmtTab: 'المبيعات',
            eoqTitle: 'الكمية الاقتصادية', forecastTitle: 'التنبؤ الذكي',
            financialTitle: 'التقارير المالية', incomeTab: 'قائمة الدخل', balanceTab: 'الميزانية', cashflowTab: 'التدفقات',
            settingsTitle: 'الضبط', oldPassLabel: 'كلمة المرور القديمة', newPassLabel: 'كلمة المرور الجديدة', changePassBtn: 'تغيير كلمة المرور',
            securityTitle: 'أسئلة الأمان', secQ1Label: 'اسم والدتك؟', secQ2Label: 'أول مدرسة؟', saveSecurityBtn: 'حفظ',
            inspectTitle: 'فحص ذكي', barcodeLabel: 'باركود المنتج', inspectBtn: 'فحص',
            auditTitle: 'جرد المخزون', auditTypeLabel: 'نوع الجرد', auditAll: 'جميع المنتجات', auditSingle: 'منتج محدد', selectProductLabel: 'اختر منتج',
            startAuditBtn: 'بدء الجرد', auditActualQty: 'الكمية الفعلية بعد الجرد', auditNewPrice: 'سعر الجرد الجديد', auditNotes: 'ملاحظات الجرد', executeAuditBtn: 'جرد الآن ✅',
            forgotTitle: 'استعادة كلمة المرور', forgotUserLabel: 'رقم الهاتف (249xxxxxxxxx)', verifyBtn: 'تحقق',
            closeModalBtn: 'إغلاق'
        },
        en: {
            loginTitle: 'Login', usernameLabel: 'Email or Phone', passwordLabel: 'Password', loginBtn: 'Login', registerBtn: 'Sign Up', forgotBtn: 'Forgot Password?',
            registerTitle: 'Sign Up', nameLabel: 'Name', emailLabel: 'Email', phoneLabel: 'Phone (starting 249)', regPassLabel: 'Password', sectorLabel: 'Sector', branchLabel: 'Branch Name', createBtn: 'Create Account', backBtn: 'Back',
            dashboardTitle: 'Dashboard', logoutBtn: 'Logout', capitalLabel: 'Capital', profitLabel: 'Net Profit', totalSalesLabel: 'Total Sales',
            productsLabel: 'Products', salesCountLabel: 'Sales Count', purchasesLabel: 'Purchases', productsIcon: 'Products', addIcon: 'Add', sellIcon: 'Sell', returnIcon: 'Return',
            invoicesIcon: 'Invoices', auditIcon: 'Audit', inspectIcon: 'Check', eoqIcon: 'EOQ', forecastIcon: 'Forecast', settingsIcon: 'Settings', statementIcon: 'Statement', reportsIcon: 'Financial Reports',
            allProductsTitle: 'All Products', goodStatus: 'Good', mediumStatus: 'Medium', criticalStatus: 'Critical',
            addTitle: 'Add Product', productNameLabel: 'Product Name', productQtyLabel: 'Quantity', productPurchaseLabel: 'Purchase Price', productSellingLabel: 'Selling Price', productMinLabel: 'Min Limit',
            productProdDateLabel: 'Production Date', productExpDateLabel: 'Expiry Date', confirmAddBtn: 'Add Product',
            sellTitle: 'Sell Product', productSelectLabel: 'Product', sellQtyLabel: 'Quantity', totalLabel: 'Total', buyerPhoneLabel: 'Buyer Phone', buyerNameLabel: 'Buyer Name', confirmSellBtn: 'Confirm Sale',
            returnTitle: 'Return Sales', selectSaleLabel: 'Select Sale', returnReasonLabel: 'Return Reason', confirmReturnBtn: 'Confirm Return',
            invoicesTitle: 'Invoices', allTab: 'All', purchasesTab: 'Purchases', salesTab: 'Sales',
            statementTitle: 'Statement', purchasesStmtTab: 'Purchases', salesStmtTab: 'Sales',
            eoqTitle: 'Economic Order Quantity', forecastTitle: 'Smart Forecast',
            financialTitle: 'Financial Reports', incomeTab: 'Income Statement', balanceTab: 'Balance Sheet', cashflowTab: 'Cash Flow',
            settingsTitle: 'Settings', oldPassLabel: 'Old Password', newPassLabel: 'New Password', changePassBtn: 'Change Password',
            securityTitle: 'Security Questions', secQ1Label: "Mother's Name?", secQ2Label: 'First School?', saveSecurityBtn: 'Save',
            inspectTitle: 'Smart Check', barcodeLabel: 'Barcode', inspectBtn: 'Check',
            auditTitle: 'Inventory Audit', auditTypeLabel: 'Audit Type', auditAll: 'All Products', auditSingle: 'Single Product', selectProductLabel: 'Select Product',
            startAuditBtn: 'Start Audit', auditActualQty: 'Actual Quantity After Audit', auditNewPrice: 'New Audit Price', auditNotes: 'Audit Notes', executeAuditBtn: 'Audit Now ✅',
            forgotTitle: 'Forgot Password', forgotUserLabel: 'Phone (249xxxxxxxxx)', verifyBtn: 'Verify',
            closeModalBtn: 'Close'
        }
    };
    function applyLanguage() {
        document.querySelectorAll('[data-i18n]').forEach(el => {
            const key = el.getAttribute('data-i18n');
            if(translations[currentLang] && translations[currentLang][key]) {
                if(el.tagName === 'INPUT' && el.hasAttribute('placeholder')) el.placeholder = translations[currentLang][key];
                else el.innerText = translations[currentLang][key];
            }
        });
        document.documentElement.lang = currentLang === 'ar' ? 'ar' : 'en';
        document.documentElement.dir = currentLang === 'ar' ? 'rtl' : 'ltr';
        updateWelcomeMessage();
        refreshCurrentScreen();
    }
    function toggleLanguage() { currentLang = currentLang === 'ar' ? 'en' : 'ar'; applyLanguage(); }

    // -------------------- البيانات الأساسية --------------------
    let currentUser = null;
    let products = [], purchases = [], sales = [], audits = [], users = [];
    let currentAuditProduct = null;
    let pendingOTP = null, otpTimerInterval = null, pendingForgotPhone = null;
    const SECRET = "SIMS2025";
    function encrypt(data) { return CryptoJS.AES.encrypt(JSON.stringify(data), SECRET).toString(); }
    function decrypt(enc) { try { return JSON.parse(CryptoJS.AES.decrypt(enc, SECRET).toString(CryptoJS.enc.Utf8)); } catch(e) { return null; } }

    function loadData() {
        users = decrypt(localStorage.getItem('sims_users')) || [];
        if(users.length === 0) {
            users = [{ id: 1, name: 'أحمد محمد', email: 'admin@sims.com', phone: '249123456789', password: 'admin123', sector: 'تجاري', branchName: 'الفرع الرئيسي', securityAnswers: {}, isVerified: true }];
            products = [
                { id: 101, name: 'هاتف ذكي', barcode: 'SIM1001', quantity: 50, purchasePrice: 500, sellingPrice: 800, minLimit: 10, productionDate: '2024-01-01', expiryDate: '2025-12-31', sector: 'تجاري' },
                { id: 102, name: 'حاسوب محمول', barcode: 'SIM1002', quantity: 20, purchasePrice: 2000, sellingPrice: 3000, minLimit: 5, productionDate: '2024-01-01', expiryDate: '2025-12-31', sector: 'تجاري' }
            ];
            purchases = []; sales = []; audits = [];
        }
        currentUser = decrypt(localStorage.getItem('sims_currentUser'));
        products = decrypt(localStorage.getItem('sims_products')) || products;
        purchases = decrypt(localStorage.getItem('sims_purchases')) || purchases;
        sales = decrypt(localStorage.getItem('sims_sales')) || sales;
        audits = decrypt(localStorage.getItem('sims_audits')) || audits;
    }
    function saveData() {
        localStorage.setItem('sims_users', encrypt(users));
        localStorage.setItem('sims_currentUser', encrypt(currentUser));
        localStorage.setItem('sims_products', encrypt(products));
        localStorage.setItem('sims_purchases', encrypt(purchases));
        localStorage.setItem('sims_sales', encrypt(sales));
        localStorage.setItem('sims_audits', encrypt(audits));
    }

    function getUserSector() { return currentUser ? currentUser.sector : null; }
    function getProductsByUserSector() { let s = getUserSector(); if(!s) return products; return products.filter(p => p.sector === s); }
    function calculateTotalCapital() { return getProductsByUserSector().reduce((s,p) => s + p.quantity * (p.purchasePrice||0), 0); }
    function calculateTotalSalesAmount() { return sales.filter(s => s.sector === getUserSector()).reduce((s,sl) => s + (sl.total||0), 0); }
    function calculateTotalCostOfGoodsSold() { let cost=0; sales.filter(s=>s.sector===getUserSector()).forEach(sale=>{ let prod=products.find(p=>p.id===sale.productId); if(prod) cost+=sale.quantity*(prod.purchasePrice||0); }); return cost; }
    function calculateNetProfit() { return calculateTotalSalesAmount() - calculateTotalCostOfGoodsSold(); }
    function getDaysRemaining(expiry) { if(!expiry) return 365; let d = (new Date(expiry)-new Date())/(86400000); return Math.max(0, Math.ceil(d)); }
    function getProductStatus(expiry) { let d=getDaysRemaining(expiry); if(d<90) return {class:'status-critical', text: currentLang==='ar'?'حرج':'Critical'}; if(d<180) return {class:'status-medium', text: currentLang==='ar'?'متوسط':'Medium'}; return {class:'status-good', text: currentLang==='ar'?'جيد':'Good'}; }
    function updateFinancialCards() {
        document.getElementById('capitalValue').innerText = calculateTotalCapital().toFixed(2);
        document.getElementById('profitValue').innerText = calculateNetProfit().toFixed(2);
        document.getElementById('totalSalesValue').innerText = calculateTotalSalesAmount().toFixed(2);
        document.getElementById('totalProductsStat').innerText = getProductsByUserSector().length;
        document.getElementById('totalSalesCountStat').innerText = sales.filter(s=>s.sector===getUserSector()).length;
        document.getElementById('totalPurchasesStat').innerText = purchases.filter(p=>p.sector===getUserSector()).length;
    }
    function showNotification(title, content) { document.getElementById('modalNotificationContent').innerHTML = `<h3>${title}</h3><div>${content}</div>`; document.getElementById('notificationModal').style.display = 'flex'; }
    function closeNotificationModal() { document.getElementById('notificationModal').style.display = 'none'; }
    function hideAllScreens() { document.querySelectorAll('.screen').forEach(s => s.classList.remove('active')); }
    function backToMain() { hideAllScreens(); document.getElementById('mainScreen').classList.add('active'); updateFinancialCards(); updateWelcomeMessage(); refreshCurrentScreen(); }
    function showLogin() { hideAllScreens(); document.getElementById('loginScreen').classList.add('active'); }
    function showRegister() { hideAllScreens(); document.getElementById('registerScreen').classList.add('active'); }
    function showForgotPassword() { hideAllScreens(); document.getElementById('forgotPasswordScreen').classList.add('active'); }
    function updateWelcomeMessage() { let hour=new Date().getHours(); let g = hour<12?(currentLang==='ar'?'صباح الخير':'Good Morning'):(currentLang==='ar'?'مساء الخير':'Good Evening'); document.getElementById('welcomeMessage').innerText = `${g} ${currentUser?.name||''}`; }
    function refreshCurrentScreen() {
        if(document.getElementById('allProductsScreen').classList.contains('active')) renderProductsTable();
        if(document.getElementById('forecastScreen').classList.contains('active')) showForecast();
        if(document.getElementById('economicOrderScreen').classList.contains('active')) showEconomicOrder();
        if(document.getElementById('statementScreen').classList.contains('active')) {
            let t = document.querySelector('#statementScreen .tab.active')?.innerText||'';
            if(t.includes('المشتريات')||t.includes('Purchases')) showPurchaseStatement(); else showSalesStatement();
        }
        if(document.getElementById('invoicesScreen').classList.contains('active')) {
            let t = document.querySelector('#invoicesScreen .tab.active')?.innerText||'';
            if(t.includes('الكل')||t.includes('All')) showInvoicesList('all');
            else if(t.includes('مشتريات')||t.includes('Purchases')) showInvoicesList('purchase');
            else showInvoicesList('sale');
        }
        if(document.getElementById('financialReportsScreen').classList.contains('active')) {
            let t = document.querySelector('#financialReportsScreen .tab.active')?.innerText||'';
            if(t.includes('قائمة الدخل')||t.includes('Income')) showIncomeStatement();
            else if(t.includes('الميزانية')||t.includes('Balance')) showBalanceSheet();
            else showCashFlow();
        }
    }

    // -------------------- OTP --------------------
    function sendOTP() {
        const phone = document.getElementById('regPhone').value.trim();
        if(!phone.match(/^249[0-9]{9}$/)) { showNotification('خطأ','رقم غير صحيح (249XXXXXXXXX)'); return; }
        const otp = Math.floor(100000+Math.random()*900000).toString();
        pendingOTP = otp;
        console.log(`OTP for ${phone}: ${otp}`);
        showNotification('تم الإرسال',`تم إرسال الرمز إلى ${phone} (محاكاة: ${otp})`);
        let timeLeft=60;
        const timerEl=document.getElementById('otpTimer');
        if(otpTimerInterval) clearInterval(otpTimerInterval);
        otpTimerInterval=setInterval(()=>{ if(timeLeft<=0){ clearInterval(otpTimerInterval); timerEl.innerText=''; pendingOTP=null; } else { timerEl.innerText=`إعادة الإرسال بعد ${timeLeft} ثانية`; timeLeft--; } },1000);
    }
    function registerWithOTP() {
        if(!pendingOTP) { showNotification('تنبيه','اطلب الرمز أولاً'); return; }
        if(document.getElementById('otpCode').value.trim() !== pendingOTP) { showNotification('خطأ','رمز غير صحيح'); return; }
        const name=document.getElementById('regName').value.trim(), email=document.getElementById('regEmail').value.trim(), phone=document.getElementById('regPhone').value.trim(), password=document.getElementById('regPassword').value.trim(), sector=document.getElementById('regSector').value, branch=document.getElementById('regBranch').value.trim();
        if(!name||!email||!phone||!password||!branch) { showNotification('تنبيه','املأ الحقول'); return; }
        if(users.find(u=>u.email===email||u.phone===phone)) { showNotification('خطأ','مسجل مسبقاً'); return; }
        const newUser={ id:Date.now(), name, email, phone, password, sector, branchName:branch, securityAnswers:{}, isVerified:true };
        users.push(newUser); currentUser=newUser; saveData(); clearInterval(otpTimerInterval);
        showNotification('مرحباً',`تم إنشاء حساب ${name}`); backToMain();
    }
    function sendForgotOTP() {
        const phone=document.getElementById('forgotPhone').value.trim();
        if(!phone.match(/^249[0-9]{9}$/)) { showNotification('خطأ','رقم غير صحيح'); return; }
        const user=users.find(u=>u.phone===phone);
        if(!user) { showNotification('خطأ','لا يوجد حساب'); return; }
        const otp=Math.floor(100000+Math.random()*900000).toString();
        pendingForgotPhone={phone,otp};
        showNotification('تم الإرسال',`رمز التحقق: ${otp}`);
    }
    function resetPassword() {
        const phone=document.getElementById('forgotPhone').value.trim();
        const otp=document.getElementById('forgotOtp').value.trim();
        const newPass=document.getElementById('newPassReset').value.trim();
        if(!pendingForgotPhone || pendingForgotPhone.phone!==phone || pendingForgotPhone.otp!==otp) { showNotification('خطأ','رمز غير صحيح'); return; }
        const user=users.find(u=>u.phone===phone); if(!user) return;
        user.password=newPass; saveData(); showNotification('تم','تم تغيير كلمة المرور'); showLogin();
    }

    // -------------------- المنتجات --------------------
    function showAllProducts() { hideAllScreens(); document.getElementById('allProductsScreen').classList.add('active'); renderProductsTable(); }
    function renderProductsTable() {
        let userProducts=getProductsByUserSector();
        let search=document.getElementById('searchProducts')?.value.toLowerCase()||'';
        let filtered=search? userProducts.filter(p=>p.name.toLowerCase().includes(search)) : userProducts;
        let html='<div class="table-container"><table><thead><tr>';
        html+=(currentLang==='ar'?'<th>المنتج</th><th>الكمية</th><th>سعر الشراء</th><th>سعر البيع</th><th>الحد الأدنى</th><th>تاريخ الانتهاء</th><th>الأيام</th><th>الحالة</th><th>حذف</th>':'<th>Product</th><th>Qty</th><th>Purchase</th><th>Selling</th><th>Min</th><th>Expiry</th><th>Days</th><th>Status</th><th>Delete</th>');
        html+='</tr></thead><tbody>';
        filtered.forEach(p=>{ let days=getDaysRemaining(p.expiryDate); let status=getProductStatus(p.expiryDate); html+=`<tr><td>${p.name}</td><td>${p.quantity}</td><td>${p.purchasePrice}</td><td>${p.sellingPrice}</td><td>${p.minLimit}</td><td>${p.expiryDate}</td><td>${days}</td><td><span class="${status.class}">${status.text}</span></td><td><button class="action-btn" onclick="deleteProduct(${p.id})">🗑️</button></td></tr>`; });
        html+='</tbody></table></div>';
        document.getElementById('productsTableContainer').innerHTML = html;
    }
    function deleteProduct(id) { if(confirm('هل أنت متأكد؟')){ products=products.filter(p=>p.id!==id); saveData(); renderProductsTable(); updateFinancialCards(); showNotification('تم','تم حذف المنتج'); } }
    function showAddProduct() { hideAllScreens(); document.getElementById('addProductScreen').classList.add('active'); }
    function addProduct() {
        let name=document.getElementById('productName').value.trim(), qty=parseInt(document.getElementById('productQuantity').value)||0, pur=parseFloat(document.getElementById('purchasePrice').value)||0, sell=parseFloat(document.getElementById('sellingPrice').value)||0, min=parseInt(document.getElementById('minLimit').value), prodDate=document.getElementById('productionDate').value, expDate=document.getElementById('expiryDate').value;
        if(!name||!min||!prodDate||!expDate) { showNotification('تنبيه','املأ الحقول'); return; }
        let barcode='SIM'+Date.now()+Math.floor(Math.random()*10000);
        products.push({ id:Date.now(), name, barcode, quantity:qty, purchasePrice:pur, sellingPrice:sell, minLimit:min, productionDate:prodDate, expiryDate:expDate, sector:getUserSector() });
        purchases.push({ id:Date.now(), productName:name, quantity:qty, price:pur, total:pur*qty, timestamp:new Date().toLocaleString(), sector:getUserSector() });
        saveData(); backToMain(); showNotification('تم','تمت الإضافة');
    }

    // -------------------- بيع --------------------
    function showSellProduct() { hideAllScreens(); document.getElementById('sellProductScreen').classList.add('active'); let sel=document.getElementById('sellProductSelect'); let prods=getProductsByUserSector().filter(p=>p.quantity>0); sel.innerHTML='<option value="">اختر</option>'; prods.forEach(p=>sel.innerHTML+=`<option value="${p.id}" data-price="${p.sellingPrice}">${p.name} (${p.quantity}) - ${p.sellingPrice}</option>`); document.getElementById('sellQuantity').value=''; document.getElementById('totalPrice').value=''; }
    function updateTotalPrice() { let sel=document.getElementById('sellProductSelect'); let price=parseFloat(sel.options[sel.selectedIndex]?.getAttribute('data-price')||0); let qty=parseFloat(document.getElementById('sellQuantity').value)||0; document.getElementById('totalPrice').value=(price*qty).toFixed(2); }
    function sellProduct() {
        let pid=parseInt(document.getElementById('sellProductSelect').value), qty=parseInt(document.getElementById('sellQuantity').value), buyerPhone=document.getElementById('buyerPhone').value, buyerName=document.getElementById('buyerName').value, prod=products.find(p=>p.id===pid);
        if(!prod||prod.quantity<qty) { showNotification('خطأ','كمية غير كافية'); return; }
        let total=prod.sellingPrice*qty, cost=prod.purchasePrice*qty;
        prod.quantity-=qty; if(prod.quantity===0) products=products.filter(p=>p.id!==pid);
        sales.push({ id:Date.now(), productId:pid, productName:prod.name, quantity:qty, price:prod.sellingPrice, total, cost, buyerName, buyerPhone, timestamp:new Date().toLocaleString(), sector:getUserSector() });
        saveData(); backToMain(); showNotification('تم البيع',`${qty} من ${prod.name} بـ ${total}`);
    }

    // -------------------- إرجاع --------------------
    function showReturnProduct() { hideAllScreens(); document.getElementById('returnProductScreen').classList.add('active'); let sel=document.getElementById('returnSaleSelect'); let sls=sales.filter(s=>s.sector===getUserSector()); sel.innerHTML='<option value="">اختر</option>'; sls.forEach(s=>sel.innerHTML+=`<option value="${s.id}">${s.productName} - ${s.quantity} - ${s.timestamp}</option>`); }
    function returnSale() {
        let sid=parseInt(document.getElementById('returnSaleSelect').value), reason=document.getElementById('returnReason').value, idx=sales.findIndex(s=>s.id===sid);
        if(idx===-1) return; let sale=sales[idx]; let prod=products.find(p=>p.id===sale.productId);
        if(prod) prod.quantity+=sale.quantity; else products.push({ id:sale.productId, name:sale.productName, quantity:sale.quantity, purchasePrice:sale.cost/sale.quantity, sellingPrice:sale.price, minLimit:1, productionDate:new Date().toISOString().slice(0,10), expiryDate:new Date(Date.now()+365*86400000).toISOString().slice(0,10), sector:getUserSector() });
        purchases.push({ id:Date.now(), productName:sale.productName, quantity:sale.quantity, price:sale.cost/sale.quantity, total:sale.cost, reason, type:'RETURN', timestamp:new Date().toLocaleString(), sector:getUserSector() });
        sales.splice(idx,1); saveData(); backToMain(); showNotification('تم الإرجاع',`تم إرجاع ${sale.quantity} من ${sale.productName}`);
    }

    // -------------------- فواتير --------------------
    function showInvoices() { hideAllScreens(); document.getElementById('invoicesScreen').classList.add('active'); showInvoicesList('all'); }
    function showInvoicesList(type) { let list=[]; if(type==='all'||type==='purchase') list.push(...purchases.filter(p=>p.sector===getUserSector()).map(p=>({...p, type:currentLang==='ar'?'شراء':'Purchase'}))); if(type==='all'||type==='sale') list.push(...sales.filter(s=>s.sector===getUserSector()).map(s=>({...s, type:currentLang==='ar'?'بيع':'Sale'}))); list.sort((a,b)=>new Date(b.timestamp)-new Date(a.timestamp)); let html=''; list.forEach(inv=>{ html+=`<div class="invoice-item" onclick='showInvoiceDetails(${JSON.stringify(inv).replace(/'/g,"&#39;")})'><h4>${inv.type} - ${inv.productName}</h4><p>${inv.timestamp} | ${currentLang==='ar'?'الكمية':'Qty'}: ${inv.quantity}</p></div>`; }); document.getElementById('invoicesList').innerHTML = html||(currentLang==='ar'?'<p>لا توجد فواتير</p>':'<p>No invoices</p>'); }
    function showInvoiceDetails(inv) { let profit=(inv.type===(currentLang==='ar'?'بيع':'Sale'))?((inv.total||0)-(inv.cost||0)).toFixed(2):'-'; let html=`<table><tr><th colspan="2">${currentLang==='ar'?'تفاصيل الفاتورة':'Invoice Details'}</th></tr><tr><td>${currentLang==='ar'?'المنتج':'Product'}</td><td>${inv.productName}</td></tr><tr><td>${currentLang==='ar'?'الكمية':'Qty'}</td><td>${inv.quantity}</td></tr><tr><td>${currentLang==='ar'?'الإجمالي':'Total'}</td><td>${inv.total||inv.quantity*inv.price}</td></tr>${inv.type===(currentLang==='ar'?'بيع':'Sale')?`<tr><td>${currentLang==='ar'?'الربح':'Profit'}</td><td class="profit-positive">${profit}</td></tr>`:''}<tr><td>${currentLang==='ar'?'التاريخ':'Date'}</td><td>${inv.timestamp}</td></tr></table>`; showNotification(currentLang==='ar'?'تفاصيل':'Details',html); }

    // -------------------- كشف حساب --------------------
    function showBankStatement() { hideAllScreens(); document.getElementById('statementScreen').classList.add('active'); showPurchaseStatement(); }
    function showPurchaseStatement() { let data=purchases.filter(p=>p.sector===getUserSector()).sort((a,b)=>new Date(b.timestamp)-new Date(a.timestamp)); let html='<div class="table-container"><table><thead><tr><th>'+ (currentLang==='ar'?'التاريخ':'Date')+'</th><th>'+ (currentLang==='ar'?'المنتج':'Product')+'</th><th>'+ (currentLang==='ar'?'الكمية':'Qty')+'</th><th>'+ (currentLang==='ar'?'سعر الشراء':'Price')+'</th><th>'+ (currentLang==='ar'?'الإجمالي':'Total')+'</th></tr></thead><tbody>'; data.forEach(d=>{html+=`<tr><td>${d.timestamp}</td><td>${d.productName}</td><td>${d.quantity}</td><td>${d.price||0}</td><td>${d.total||d.quantity*d.price}</td></tr>`;}); html+='</tbody></table></div>'; document.getElementById('statementContent').innerHTML=html; let tabs=document.querySelectorAll('#statementScreen .tab'); tabs.forEach((t,i)=>{if(i===0) t.classList.add('active'); else t.classList.remove('active');}); }
    function showSalesStatement() { let data=sales.filter(s=>s.sector===getUserSector()).sort((a,b)=>new Date(b.timestamp)-new Date(a.timestamp)); let html='<div class="table-container"><table><thead><tr><th>'+ (currentLang==='ar'?'التاريخ':'Date')+'</th><th>'+ (currentLang==='ar'?'المنتج':'Product')+'</th><th>'+ (currentLang==='ar'?'الكمية':'Qty')+'</th><th>'+ (currentLang==='ar'?'سعر البيع':'Price')+'</th><th>'+ (currentLang==='ar'?'الإجمالي':'Total')+'</th><th>'+ (currentLang==='ar'?'الربح':'Profit')+'</th><th>'+ (currentLang==='ar'?'المشتري':'Buyer')+'</th></tr></thead><tbody>'; data.forEach(s=>{let profit=(s.total||0)-(s.cost||0); html+=`<tr><td>${s.timestamp}</td><td>${s.productName}</td><td>${s.quantity}</td><td>${s.price||0}</td><td>${s.total||0}</td><td class="profit-positive">${profit.toFixed(2)}</td><td>${s.buyerName||'-'}</td></tr>`;}); html+='</tbody></table></div>'; document.getElementById('statementContent').innerHTML=html; let tabs=document.querySelectorAll('#statementScreen .tab'); tabs.forEach((t,i)=>{if(i===1) t.classList.add('active'); else t.classList.remove('active');}); }

    // -------------------- EOQ, Forecast, Financial --------------------
    function showEconomicOrder() { hideAllScreens(); document.getElementById('economicOrderScreen').classList.add('active'); let prods=getProductsByUserSector(); let salesData=sales.filter(s=>s.sector===getUserSector()); let html='<div class="table-container"><table><thead><tr><th>'+ (currentLang==='ar'?'المنتج':'Product')+'</th><th>'+ (currentLang==='ar'?'الطلب السنوي':'Annual Demand')+'</th><th>EOQ</th><th>ROP</th></tr></thead><tbody>'; prods.forEach(p=>{ let productSales=salesData.filter(s=>s.productId===p.id); let totalSold=productSales.reduce((a,b)=>a+b.quantity,0); let days=30; if(productSales.length){ let first=new Date(Math.min(...productSales.map(s=>new Date(s.timestamp)))); let daysRange=Math.max(1,Math.ceil((new Date()-first)/86400000)); days=daysRange; } let annual=(totalSold/days)*365; if(annual<1) annual=100; let eoq=Math.sqrt((2*annual*50)/10); html+=`<tr><td>${p.name}</td><td>${Math.round(annual)}</td><td>${Math.round(eoq)}</td><td>${p.minLimit}</td></tr>`; }); html+='</tbody></table></div>'; document.getElementById('economicContent').innerHTML=html; }
    function showForecast() { hideAllScreens(); document.getElementById('forecastScreen').classList.add('active'); let prods=getProductsByUserSector(); let salesData=sales.filter(s=>s.sector===getUserSector()); let html=''; prods.forEach(p=>{ let productSales=salesData.filter(s=>s.productId===p.id); let totalSold=productSales.reduce((a,b)=>a+b.quantity,0); let days=30; if(productSales.length){ let first=new Date(Math.min(...productSales.map(s=>new Date(s.timestamp)))); let daysRange=Math.max(1,Math.ceil((new Date()-first)/86400000)); days=daysRange; } let avg=totalSold/days; let monthly=avg*30; let daysLeft=avg>0? Math.floor(p.quantity/avg):999; let rec=Math.max(0, Math.ceil(monthly - p.quantity + (avg*14))); html+=`<div class="product-card"><strong>${p.name}</strong><div class="forecast-grid"><div class="forecast-item"><div class="label">${currentLang==='ar'?'متوسط يومي':'Avg Daily'}</div><div class="value">${avg.toFixed(2)}</div></div><div class="forecast-item"><div class="label">${currentLang==='ar'?'توقع شهري':'Monthly'}</div><div class="value">${Math.round(monthly)}</div></div><div class="forecast-item"><div class="label">${currentLang==='ar'?'أيام حتى النفاد':'Days left'}</div><div class="value">${daysLeft}</div></div><div class="forecast-item"><div class="label">${currentLang==='ar'?'موصى به':'Recommend'}</div><div class="value">${rec}</div></div></div></div>`; }); let margin=calculateTotalSalesAmount()>0? (calculateNetProfit()/calculateTotalSalesAmount())*100:0; let recClass=margin>30? 'rec-sell': (margin<10?'rec-buy':'rec-hold'); let recText=margin>30? (currentLang==='ar'?'يوصى بالبيع':'Sell'): (margin<10?(currentLang==='ar'?'يوصى بالشراء':'Buy'):(currentLang==='ar'?'يوصى بالاحتفاظ':'Hold')); html+=`<div class="forecast-section"><h4>🎯 ${currentLang==='ar'?'توصيات':'Recommendations'}</h4><div class="recommendation ${recClass}"><strong>${recText}</strong></div><div class="forecast-grid"><div class="forecast-item"><div class="label">${currentLang==='ar'?'هامش الربح':'Margin'}</div><div class="value">${margin.toFixed(2)}%</div></div></div></div>`; document.getElementById('forecastContent').innerHTML=html; }
    function showFinancialReports() { hideAllScreens(); document.getElementById('financialReportsScreen').classList.add('active'); showIncomeStatement(); }
    function showIncomeStatement() { let salesTotal=calculateTotalSalesAmount(), cogs=calculateTotalCostOfGoodsSold(), gross=salesTotal-cogs; let html=`<div class="table-container"><table><thead><tr><th colspan="2">${currentLang==='ar'?'قائمة الدخل':'Income Statement'}</th></tr></thead><tbody><tr><td>${currentLang==='ar'?'إجمالي المبيعات':'Total Sales'}</td><td>${salesTotal.toFixed(2)}</td></tr><tr><td>${currentLang==='ar'?'تكلفة البضاعة المباعة':'COGS'}</td><td>${cogs.toFixed(2)}</td></tr><tr><td><strong>${currentLang==='ar'?'صافي الربح':'Net Profit'}</strong></td><td><strong>${gross.toFixed(2)}</strong></td></tr></tbody></table></div>`; document.getElementById('financialReportContent').innerHTML=html; let tabs=document.querySelectorAll('#financialReportsScreen .tab'); tabs.forEach((t,i)=>{if(i===0) t.classList.add('active'); else t.classList.remove('active');}); }
    function showBalanceSheet() { let assets=calculateTotalCapital(), cash=calculateTotalSalesAmount()-calculateTotalCostOfGoodsSold(), totalAssets=assets+Math.max(0,cash), equity=calculateNetProfit(); let html=`<div class="table-container"><table><thead><tr><th colspan="2">${currentLang==='ar'?'الميزانية':'Balance Sheet'}</th></tr></thead><tbody><tr><td>${currentLang==='ar'?'المخزون':'Inventory'}</td><td>${assets.toFixed(2)}</td></tr><tr><td>${currentLang==='ar'?'النقدية':'Cash'}</td><td>${Math.max(0,cash).toFixed(2)}</td></tr><tr><td><strong>${currentLang==='ar'?'إجمالي الأصول':'Total Assets'}</strong></td><td><strong>${totalAssets.toFixed(2)}</strong></td></tr><tr><td>${currentLang==='ar'?'حقوق الملكية':'Equity'}</td><td>${equity.toFixed(2)}</td></tr></tbody></table></div>`; document.getElementById('financialReportContent').innerHTML=html; let tabs=document.querySelectorAll('#financialReportsScreen .tab'); tabs.forEach((t,i)=>{if(i===1) t.classList.add('active'); else t.classList.remove('active');}); }
    function showCashFlow() { let inflow=calculateTotalSalesAmount(), outflow=calculateTotalCostOfGoodsSold(), net=inflow-outflow; let html=`<div class="table-container"><table><thead><tr><th colspan="2">${currentLang==='ar'?'التدفقات النقدية':'Cash Flow'}</th></tr></thead><tbody><tr><td>${currentLang==='ar'?'التدفقات الداخلة':'Inflows'}</td><td>${inflow.toFixed(2)}</td></tr><tr><td>${currentLang==='ar'?'التدفقات الخارجة':'Outflows'}</td><td>${outflow.toFixed(2)}</td></tr><tr><td><strong>${currentLang==='ar'?'صافي التدفق':'Net'}</strong></td><td><strong>${net.toFixed(2)}</strong></td></tr></tbody></table></div>`; document.getElementById('financialReportContent').innerHTML=html; let tabs=document.querySelectorAll('#financialReportsScreen .tab'); tabs.forEach((t,i)=>{if(i===2) t.classList.add('active'); else t.classList.remove('active');}); }

    // -------------------- الإعدادات --------------------
    function showSettings() { hideAllScreens(); document.getElementById('settingsScreen').classList.add('active'); }
    function changePassword() { let old=document.getElementById('oldPass').value, newp=document.getElementById('newPass').value; if(!old||!newp){ showNotification('تنبيه','أدخل القديمة والجديدة'); return; } if(old!==currentUser.password){ showNotification('خطأ','كلمة المرور القديمة خاطئة'); return; } currentUser.password=newp; saveData(); showNotification('تم','تم تغيير كلمة المرور'); }
    function saveSecurityQuestions() { if(!currentUser) return; currentUser.securityAnswers={ q1:document.getElementById('secQ1').value, q2:document.getElementById('secQ2').value }; saveData(); showNotification('حفظ','تم حفظ أسئلة الأمان'); }

    // -------------------- الفحص الذكي --------------------
    function showInspectProducts() { hideAllScreens(); document.getElementById('inspectScreen').classList.add('active'); document.getElementById('inspectDetails').innerHTML=''; }
    function inspectByBarcode() { let barcode=document.getElementById('inspectBarcode').value.trim(); let prod=products.find(p=>p.barcode===barcode); if(!prod){ document.getElementById('inspectDetails').innerHTML='<p style="color:red;">منتج غير موجود</p>'; return; } let days=getDaysRemaining(prod.expiryDate); let status=getProductStatus(prod.expiryDate); let profit=(prod.sellingPrice||0)-(prod.purchasePrice||0); document.getElementById('inspectDetails').innerHTML=`<div style="padding:16px; background:#f8fafc; border-radius:20px;"><h4>${prod.name}</h4><p>${currentLang==='ar'?'الكمية':'Qty'}: ${prod.quantity}</p><p>${currentLang==='ar'?'سعر الشراء':'Purchase'}: ${prod.purchasePrice}</p><p>${currentLang==='ar'?'سعر البيع':'Selling'}: ${prod.sellingPrice}</p><p>${currentLang==='ar'?'الربح':'Profit'}: ${profit}</p><p>${currentLang==='ar'?'تاريخ الانتهاء':'Expiry'}: ${prod.expiryDate} (${days} ${currentLang==='ar'?'يوم':'days'})</p><p>${currentLang==='ar'?'الحالة':'Status'}: <span class="${status.class}">${status.text}</span></p></div>`; }

    // -------------------- جرد المخزون --------------------
    function showInventoryAudit() { hideAllScreens(); document.getElementById('auditScreen').classList.add('active'); document.getElementById('auditForm').style.display='none'; document.getElementById('auditProductsList').innerHTML=''; document.getElementById('auditResults').innerHTML=''; currentAuditProduct=null; let select=document.getElementById('auditProductSelect'); let prods=getProductsByUserSector(); select.innerHTML='<option value="">'+(currentLang==='ar'?'اختر':'Select')+'</option>'; prods.forEach(p=>select.innerHTML+=`<option value="${p.id}">${p.name}</option>`); document.getElementById('auditType').onchange=function(){ document.getElementById('auditSingleDiv').style.display=this.value==='single'?'block':'none'; document.getElementById('auditForm').style.display='none'; document.getElementById('auditProductsList').innerHTML=''; }; document.getElementById('auditType').dispatchEvent(new Event('change')); }
    function prepareAudit() { let type=document.getElementById('auditType').value; let productsList=[]; if(type==='all') productsList=[...getProductsByUserSector()]; else { let pid=parseInt(document.getElementById('auditProductSelect').value); if(!pid){ showNotification('تنبيه','اختر منتجاً'); return; } let prod=products.find(p=>p.id===pid); if(prod) productsList=[prod]; } if(productsList.length===0){ showNotification('تنبيه','لا توجد منتجات'); return; } let html='<div class="table-container"><table><thead><tr><th>'+ (currentLang==='ar'?'المنتج':'Product')+'</th><th>'+ (currentLang==='ar'?'الكمية الحالية':'Current Qty')+'</th><th>'+ (currentLang==='ar'?'السعر الحالي':'Current Price')+'</th><th>'+ (currentLang==='ar'?'إجراء':'Action')+'</th></tr></thead><tbody>'; productsList.forEach(p=>{ html+=`<tr><td>${p.name}</td><td>${p.quantity}</td><td>${p.purchasePrice}</td><td><button class="btn btn-secondary" style="padding:4px 8px;" onclick="showAuditFormForProduct(${p.id})">${currentLang==='ar'?'جرد هذا المنتج':'Audit'}</button></td></tr>`; }); html+='</tbody></table></div>'; document.getElementById('auditProductsList').innerHTML=html; document.getElementById('auditForm').style.display='none'; document.getElementById('auditResults').innerHTML=''; }
    function showAuditFormForProduct(productId) { currentAuditProduct=products.find(p=>p.id===productId); if(!currentAuditProduct) return; document.getElementById('auditActualQty').value=currentAuditProduct.quantity; document.getElementById('auditNewPrice').value=currentAuditProduct.purchasePrice; document.getElementById('auditNotes').value=''; document.getElementById('auditForm').style.display='block'; let infoHtml=`<div class="table-container"><table><thead><tr><th colspan="2">${currentLang==='ar'?'بيانات المنتج قبل الجرد':'Product Data'}</th></tr></thead><tbody><tr><td>${currentLang==='ar'?'المنتج':'Product'}</td><td>${currentAuditProduct.name}</td></tr><tr><td>${currentLang==='ar'?'الكمية الحالية':'Current Qty'}</td><td>${currentAuditProduct.quantity}</td></tr><tr><td>${currentLang==='ar'?'سعر التكلفة الحالي':'Current Cost'}</td><td>${currentAuditProduct.purchasePrice}</td></tr></tbody></table></div>`; document.getElementById('auditResults').innerHTML=infoHtml; }
    function executeAudit() { if(!currentAuditProduct){ showNotification('خطأ','اختر منتجاً أولاً'); return; } let actualQty=parseInt(document.getElementById('auditActualQty').value), newPrice=parseFloat(document.getElementById('auditNewPrice').value), notes=document.getElementById('auditNotes').value; if(isNaN(actualQty)||actualQty<0){ showNotification('خطأ','كمية غير صالحة'); return; } if(isNaN(newPrice)||newPrice<0) newPrice=currentAuditProduct.purchasePrice; let oldQty=currentAuditProduct.quantity, oldPrice=currentAuditProduct.purchasePrice, qtyDiff=actualQty-oldQty, priceDiff=newPrice-oldPrice; currentAuditProduct.quantity=actualQty; currentAuditProduct.purchasePrice=newPrice; audits.push({ id:Date.now(), productId:currentAuditProduct.id, productName:currentAuditProduct.name, oldQuantity:oldQty, newQuantity:actualQty, oldPrice, newPrice, quantityDifference:qtyDiff, priceDifference:priceDiff, notes, timestamp:new Date().toLocaleString(), sector:getUserSector() }); saveData(); let valuationDiff=(actualQty*newPrice)-(oldQty*oldPrice); let diffHtml=''; if(qtyDiff!==0) diffHtml+=`<p>${currentLang==='ar'?'تغير الكمية':'Qty change'}: ${oldQty} → ${actualQty} (${qtyDiff>0?'+':''}${qtyDiff})</p>`; if(priceDiff!==0) diffHtml+=`<p>${currentLang==='ar'?'تغير السعر':'Price change'}: ${oldPrice} → ${newPrice} (${priceDiff>0?'+':''}${priceDiff.toFixed(2)})</p>`; diffHtml+=`<p><strong>${currentLang==='ar'?'تغير قيمة المخزون':'Inventory value change'}: ${valuationDiff>0?'+':''}${valuationDiff.toFixed(2)}</strong></p>`; showNotification(currentLang==='ar'?'نتيجة الجرد':'Audit Result', `<h4>${currentAuditProduct.name}</h4>${diffHtml}<p>${currentLang==='ar'?'ملاحظات':'Notes'}: ${notes||'-'}</p>`); document.getElementById('auditForm').style.display='none'; currentAuditProduct=null; document.getElementById('auditProductsList').innerHTML=''; document.getElementById('auditResults').innerHTML=''; updateFinancialCards(); if(document.getElementById('allProductsScreen').classList.contains('active')) renderProductsTable(); }

    // -------------------- المصادقة --------------------
    function login() { let u=document.getElementById('username').value, p=document.getElementById('password').value; let user=users.find(uu=>(uu.email===u||uu.phone===u)&&uu.password===p); if(user){ currentUser=user; saveData(); backToMain(); showNotification('مرحباً',`مرحباً ${user.name}`); } else showNotification('خطأ','بيانات غير صحيحة'); }
    function logout() { currentUser=null; saveData(); showLogin(); showNotification('خروج','تم تسجيل الخروج'); }

    window.onload = () => { loadData(); if(currentUser) backToMain(); else showLogin(); applyLanguage(); };
</script>
</body>
</html>
```
