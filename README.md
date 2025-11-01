<!doctype html>
<html lang="ar">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <meta name="description" content="محول التاريخ بين التقويم الهجري (أم القرى) والميلادي مع حساب المدة بالسنوات والشهور والأيام">
  <meta name="keywords" content="محول التاريخ, تقويم أم القرى, هجري, ميلادي, حساب العمر">
  <meta name="author" content="Your Name">
  <title>محول التاريخ - تقويم أم القرى</title>
  <style>
    body {
      font-family: "Segoe UI", Tahoma, Arial, sans-serif;
      background: #f7f9fc;
      display: flex;
      justify-content: center;
      align-items: flex-start;
      min-height: 100vh;
      margin: 0;
      direction: rtl;
      padding-top: 100px;
    }
    .container {
      display: flex;
      gap: 20px;
      padding: 20px;
      max-width: 1000px;
      width: 100%;
    }
    .container.rtl {
      flex-direction: row-reverse;
    }
    .container.ltr {
      flex-direction: row;
    }
    .card {
      background: white;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 6px 20px rgba(0,0,0,0.1);
      width: 400px;
      text-align: center;
      flex: 1;
    }
    .hijri-months, .gregorian-months {
      background: white;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 6px 20px rgba(0,0,0,0.1);
      width: 200px;
      text-align: right;
    }
    .hijri-months h2, .gregorian-months h2 {
      font-size: 18px;
      margin-top: 0;
      margin-bottom: 10px;
      color: #333;
    }
    .hijri-months ol, .gregorian-months ol {
      padding-right: 20px;
      margin: 0;
      color: #333;
      font-size: 14px;
    }
    .hijri-months li, .gregorian-months li {
      margin-bottom: 8px;
    }
    h1 {
      margin-top: 0;
      font-size: 20px;
      margin-bottom: 15px;
      color: #333;
    }
    select, input, button {
      padding: 10px;
      border-radius: 8px;
      border: 1px solid #ddd;
      font-size: 14px;
      width: 100%;
      box-sizing: border-box;
    }
    input[type="number"] {
      -moz-appearance: textfield;
      appearance: textfield;
      text-align: center;
      width: 100px;
      font-family: monospace;
      direction: ltr;
    }
    input[type="number"]::-webkit-outer-spin-button,
    input[type="number"]::-webkit-inner-spin-button {
      -webkit-appearance: inner-spin-button !important;
      opacity: 1;
      margin: 0;
      width: 20px;
    }
    .row {
      display: flex;
      gap: 8px;
      margin-top: 15px;
      justify-content: center;
    }
    .btn {
      margin-top: 15px;
      background: #0b5ed7;
      color: white;
      border: none;
      cursor: pointer;
      font-weight: bold;
      transition: background 0.2s;
    }
    .btn:hover {
      background: #084298;
    }
    .reset-btn {
      background: #6c757d;
      margin-left: 10px;
    }
    .reset-btn:hover {
      background: #5c636a;
    }
    .result {
      margin-top: 15px;
      padding: 15px;
      border-radius: 8px;
      background: #f1f5ff;
      border: 1px solid rgba(11,94,215,0.1);
      display: none;
      font-weight: bold;
      color: #333;
      text-align: right;
      position: relative;
      min-height: 40px;
    }
    .error {
      background: #ffe5e5;
      border: 1px solid #ff0000;
      color: #d32f2f;
    }
    .copy-btn {
      position: absolute;
      top: 8px;
      left: 8px;
      background: #0b5ed7;
      color: white;
      border: none;
      padding: 4px 8px;
      font-size: 12px;
      border-radius: 4px;
      cursor: pointer;
      opacity: 0;
      transition: opacity 0.2s;
    }
    .result:hover .copy-btn {
      opacity: 1;
    }
    .copy-notif {
      position: fixed;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      background: #28a745;
      color: white;
      padding: 10px 20px;
      border-radius: 6px;
      font-size: 14px;
      z-index: 1000;
      opacity: 0;
      transition: opacity 0.3s;
    }
    .age-section {
      margin-top: 15px;
      padding: 10px;
      border-top: 1px solid #ddd;
    }
    .age-section h3 {
      font-size: 16px;
      margin: 0 0 5px;
      color: #0b5ed7;
    }
    .age-calculation ul {
      list-style: none;
      padding: 0;
      margin: 0;
      font-size: 14px;
    }
    .age-calculation li {
      margin-bottom: 5px;
    }
    .lang-select {
      margin-bottom: 10px;
    }
    .year-tooltip {
      position: absolute;
      background: #333;
      color: white;
      padding: 8px;
      border-radius: 4px;
      font-size: 12px;
      z-index: 10;
      display: none;
      max-width: 200px;
      text-align: center;
      box-shadow: 0 2px 8px rgba(0,0,0,0.2);
    }
    @media (max-width: 800px) {
      .container {
        flex-direction: column;
        align-items: center;
      }
      .card, .hijri-months, .gregorian-months {
        width: 100%;
        max-width: 400px;
      }
      .copy-btn {
        opacity: 1;
        position: static;
        margin-top: 10px;
        width: auto;
      }
    }
  </style>
</head>
<body>
  <div class="container rtl">
    <aside class="hijri-months">
      <h2 id="hijri-months-title">الشهور الهجرية</h2>
      <ol id="hijri-months-list"></ol>
    </aside>
    <div class="card">
      <h1 id="title">محول التاريخ - تقويم أم القرى</h1>
      <select id="language" class="lang-select">
        <option value="ar">العربية</option>
        <option value="en">English</option>
      </select>
      <label id="direction-label">تحويل من:</label><br>
      <select id="direction">
        <option value="h2g" data-en="Hijri to Gregorian">من هجري إلى ميلادي</option>
        <option value="g2h" data-en="Gregorian to Hijri">من ميلادي إلى هجري</option>
      </select>
      <div class="row">
        <input type="number" id="day" placeholder="اليوم" min="1" max="31" inputmode="numeric">
        <input type="number" id="month" placeholder="الشهر" min="1" max="12" inputmode="numeric">
        <input type="number" id="year" placeholder="السنة" min="1" inputmode="numeric">
      </div>
      <div class="row">
        <button class="btn" id="convert">تحويل</button>
        <button class="btn reset-btn" id="reset">إعادة تعيين</button>
      </div>
      <div class="result" id="result">
        <button class="copy-btn" id="copy-btn" style="display:none;">نسخ</button>
      </div>
      <div class="year-tooltip" id="year-tooltip"></div>
    </div>
    <aside class="gregorian-months">
      <h2 id="gregorian-months-title">الشهور الميلادية</h2>
      <ol id="gregorian-months-list"></ol>
    </aside>
  </div>

  <script>
    // إعداد العناصر
    const directionEl = document.getElementById("direction");
    const languageEl = document.getElementById("language");
    const dayEl = document.getElementById("day");
    const monthEl = document.getElementById("month");
    const yearEl = document.getElementById("year");
    const resultEl = document.getElementById("result");
    const convertBtn = document.getElementById("convert");
    const resetBtn = document.getElementById("reset");
    const copyBtn = document.getElementById("copy-btn");
    const titleEl = document.getElementById("title");
    const directionLabelEl = document.getElementById("direction-label");
    const yearTooltipEl = document.getElementById("year-tooltip");
    const hijriMonthsTitleEl = document.getElementById("hijri-months-title");
    const hijriMonthsListEl = document.getElementById("hijri-months-list");
    const gregorianMonthsTitleEl = document.getElementById("gregorian-months-title");
    const gregorianMonthsListEl = document.getElementById("gregorian-months-list");
    const containerEl = document.querySelector(".container");

    // كائن الترجمات
    const translations = {
      ar: {
        title: "محول التاريخ - تقويم أم القرى",
        directionLabel: "تحويل من:",
        dayPlaceholder: "اليوم",
        monthPlaceholder: "الشهر",
        yearPlaceholder: "السنة",
        convert: "تحويل",
        reset: "إعادة تعيين",
        invalidInput: "الرجاء إدخال اليوم والشهر والسنة كاملة.",
        invalidRange: "الرجاء إدخال قيم صحيحة (اليوم: 1-31، الشهر: 1-12، السنة: أكبر من 0).",
        error: "التاريخ غير صالح أو خطأ في الاتصال بالخدمة.",
        hijriMonthsTitle: "الشهور الهجرية",
        gregorianMonthsTitle: "الشهور الميلادية",
        hijriMonths: ['محرم', 'صفر', 'ربيع الأول', 'ربيع الثاني', 'جمادى الأولى', 'جمادى الآخرة', 'رجب', 'شعبان', 'رمضان', 'شوال', 'ذو القعدة', 'ذو الحجة'],
        gregorianMonths: ['يناير', 'فبراير', 'مارس', 'أبريل', 'مايو', 'يونيو', 'يوليو', 'أغسطس', 'سبتمبر', 'أكتوبر', 'نوفمبر', 'ديسمبر'],
        yearTooltip: "السنوات المتاحة: من 1318 هـ إلى 1638 هـ (1900 م إلى 2200 م تقريبًا). خارج 1356-1500 هـ، قد تكون التحويلات تقريبية.",
        gregAgeTitle: "حساب المدة بالتاريخ الميلادي",
        hijriAgeTitle: "حساب المدة بالتاريخ الهجري",
        ageYearsMonthsDays: "السنوات: {years}، الشهور: {months}، الأيام: {days}",
        ageMonthsDays: "الشهور: {months}، الأيام: {days}",
        ageDays: "الأيام: {days}",
        pastPrefix: "الماضي: ",
        futurePrefix: "المتبقي: ",
        copyText: "نسخ"
      },
      en: {
        title: "Date Converter - Umm Al-Qura Calendar",
        directionLabel: "Convert from:",
        dayPlaceholder: "Day",
        monthPlaceholder: "Month",
        yearPlaceholder: "Year",
        convert: "Convert",
        reset: "Reset",
        invalidInput: "Please enter day, month, and year completely.",
        invalidRange: "Please enter valid values (Day: 1-31, Month: 1-12, Year: > 0).",
        error: "Invalid date or connection error with the service.",
        hijriMonthsTitle: "Hijri Months",
        gregorianMonthsTitle: "Gregorian Months",
        hijriMonths: ['Muharram', 'Safar', 'Rabi Al-Awwal', 'Rabi Al-Thani', 'Jumada Al-Awwal', 'Jumada Al-Akhirah', 'Rajab', 'Shaban', 'Ramadan', 'Shawwal', 'Dhu Al-Qadah', 'Dhu Al-Hijjah'],
        gregorianMonths: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'],
        yearTooltip: "Available years: from 1318 AH to 1638 AH (approximately 1900 CE to 2200 CE). Outside 1356-1500 AH, conversions may be approximate.",
        gregAgeTitle: "Duration Calculation in Gregorian Calendar",
        hijriAgeTitle: "Duration Calculation in Hijri Calendar",
        ageYearsMonthsDays: "Years: {years}, Months: {months}, Days: {days}",
        ageMonthsDays: "Months: {months}, Days: {days}",
        ageDays: "Days: {days}",
        pastPrefix: "Past: ",
        futurePrefix: "Remaining: ",
        copyText: "Copy"
      }
    };

    // دالة تحويل الأرقام العربية إلى إنجليزية
    function toEnglishNumber(str) {
      const arabic = ['٠', '١', '٢', '٣', '٤', '٥', '٦', '٧', '٨', '٩'];
      const english = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9'];
      return str.replace(/[٠-٩]/g, w => english[arabic.indexOf(w)]);
    }

    // === ميزة: تعديل الأرقام بعجلة الماوس ===
    function addMouseWheelSupport(inputEl, min, max) {
      inputEl.addEventListener('wheel', (e) => {
        if (document.activeElement !== inputEl) return;
        e.preventDefault();
        let value = parseInt(toEnglishNumber(inputEl.value)) || 0;
        const step = e.deltaY > 0 ? -1 : 1;
        value += step;
        if (value < min) value = min;
        if (value > max) value = max;
        inputEl.value = value;
        autoConvert();
      });
    }
    addMouseWheelSupport(dayEl, 1, 31);
    addMouseWheelSupport(monthEl, 1, 12);
    addMouseWheelSupport(yearEl, 1, 9999);

    // === ميزة: نسخ التاريخ ===
    function showCopyNotification() {
      let notif = document.getElementById("copy-notif");
      if (!notif) {
        notif = document.createElement("div");
        notif.id = "copy-notif";
        notif.className = "copy-notif";
        notif.textContent = languageEl.value === 'ar' ? 'تم النسخ!' : 'Copied!';
        document.body.appendChild(notif);
      }
      notif.style.opacity = "1";
      setTimeout(() => notif.style.opacity = "0", 2000);
    }

    function copyResult() {
      const resultText = resultEl.querySelector("span[style*='direction: ltr']")?.textContent || resultEl.textContent.replace(/نسخ/g, '').trim();
      navigator.clipboard.writeText(resultText).then(showCopyNotification).catch(() => {
        const textarea = document.createElement("textarea");
        textarea.value = resultText;
        document.body.appendChild(textarea);
        textarea.select();
        document.execCommand("copy");
        document.body.removeChild(textarea);
        showCopyNotification();
      });
    }

    // دالة تحديث الواجهة
    function updateLanguage(lang) {
      const t = translations[lang];
      titleEl.textContent = t.title;
      directionLabelEl.textContent = t.directionLabel;
      dayEl.placeholder = t.dayPlaceholder;
      monthEl.placeholder = t.monthPlaceholder;
      yearEl.placeholder = t.yearPlaceholder;
      convertBtn.textContent = t.convert;
      resetBtn.textContent = t.reset;
      copyBtn.textContent = t.copyText;
      directionEl.options[0].text = lang === 'ar' ? 'من هجري إلى ميلادي' : 'Hijri to Gregorian';
      directionEl.options[1].text = lang === 'ar' ? 'من ميلادي إلى هجري' : 'Gregorian to Hijri';
      hijriMonthsTitleEl.textContent = t.hijriMonthsTitle;
      hijriMonthsListEl.innerHTML = t.hijriMonths.map(m => `<li>${m}</li>`).join('');
      gregorianMonthsTitleEl.textContent = t.gregorianMonthsTitle;
      gregorianMonthsListEl.innerHTML = t.gregorianMonths.map(m => `<li>${m}</li>`).join('');
      document.body.style.direction = lang === 'ar' ? 'rtl' : 'ltr';
      containerEl.className = `container ${lang === 'ar' ? 'rtl' : 'ltr'}`;
      resultEl.style.textAlign = lang === 'ar' ? 'right' : 'left';
      yearTooltipEl.textContent = t.yearTooltip;
    }

    // دالة إظهار/إخفاء أيقونة السنوات
    let tooltipTimeout;
    function showYearTooltip() {
      const rect = yearEl.getBoundingClientRect();
      yearTooltipEl.style.top = `${rect.bottom + window.scrollY + 5}px`;
      yearTooltipEl.style.left = `${rect.left + window.scrollX}px`;
      yearTooltipEl.style.display = 'block';
      clearTimeout(tooltipTimeout);
      tooltipTimeout = setTimeout(() => yearTooltipEl.style.display = 'none', 10000);
    }

    // دالة التحقق من الإدخال
    function validateInput(day, month, year, lang) {
      const t = translations[lang];
      if (!day || !month || !year) return t.invalidInput;
      if (day < 1 || day > 31 || month < 1 || month > 12 || year < 1) return t.invalidRange;
      if (directionEl.value === 'h2g' && (year < 1318 || year > 1638)) {
        return lang === 'ar' ? 'السنة يجب أن تكون بين 1318 هـ و1638 هـ' : 'Year must be between 1318 AH and 1638 AH';
      }
      if (directionEl.value === 'g2h' && (year < 1900 || year > 2200)) {
        return lang === 'ar' ? 'السنة يجب أن تكون بين 1900 م و2200 م' : 'Year must be between 1900 CE and 2200 CE';
      }
      return null;
    }

    // دالة التحويل
    async function convertDate(d, m, y, direction, lang) {
      const t = translations[lang];
      let apiUrl = direction === 'h2g'
        ? `https://api.aladhan.com/v1/hToG?date=${d.toString().padStart(2,'0')}-${m.toString().padStart(2,'0')}-${y}`
        : `https://api.aladhan.com/v1/gToH?date=${d.toString().padStart(2,'0')}-${m.toString().padStart(2,'0')}-${y}`;
      const response = await fetch(apiUrl);
      const data = await response.json();
      if (data.code !== 200) throw new Error(t.error);
      const g = data.data.gregorian;
      const h = data.data.hijri;
      const gMonthName = t.gregorianMonths[parseInt(g.month.number) - 1];
      const hMonthName = t.hijriMonths[parseInt(h.month.number) - 1];
      const text = direction === 'h2g'
        ? `${lang === 'ar' ? 'الميلادي' : 'Gregorian'}: <span style="direction: ltr; font-family: monospace">${g.day} ${gMonthName} ${g.year}</span>${lang === 'ar' ? ' م' : ''}`
        : `${lang === 'ar' ? 'الهجري' : 'Hijri'}: <span style="direction: ltr; font-family: monospace">${h.day} ${hMonthName} ${h.year}</span>${lang === 'ar' ? ' هـ' : ' AH'}`;
      return {
        text,
        gregDate: new Date(g.year, parseInt(g.month.number) - 1, g.day),
        hijriDate: { day: parseInt(h.day), month: parseInt(h.month.number), year: parseInt(h.year) }
      };
    }

    // حساب المدة
    function calculateDuration(diffDays, yearLength, monthLength, t) {
      const isFuture = diffDays < 0;
      const absDiffDays = Math.abs(diffDays);
      const years = Math.floor(absDiffDays / yearLength);
      const months = Math.floor((absDiffDays % yearLength) / monthLength);
      const days = Math.floor((absDiffDays % yearLength) % monthLength);
      const totalMonths = Math.floor(absDiffDays / monthLength);
      const totalDays = absDiffDays;
      const prefix = isFuture ? t.futurePrefix : t.pastPrefix;
      return `
        <div class="age-calculation">
          <ul>
            <li>${prefix}${t.ageYearsMonthsDays.replace('{years}', years).replace('{months}', months).replace('{days}', days)}</li>
            <li>${prefix}${t.ageMonthsDays.replace('{months}', totalMonths).replace('{days}', totalDays % monthLength)}</li>
            <li>${prefix}${t.ageDays.replace('{days}', totalDays)}</li>
          </ul>
        </div>
      `;
    }

    // التحويل التلقائي
    async function autoConvert() {
      const d = parseInt(toEnglishNumber(dayEl.value.trim())) || 0;
      const m = parseInt(toEnglishNumber(monthEl.value.trim())) || 0;
      const y = parseInt(toEnglishNumber(yearEl.value.trim())) || 0;
      const lang = languageEl.value;
      const t = translations[lang];
      const error = validateInput(d, m, y, lang);
      if (error) {
        resultEl.innerHTML = `<button class="copy-btn" id="copy-btn" style="display:none;">${t.copyText}</button>${error}`;
        resultEl.className = "result error";
        resultEl.style.display = "block";
        copyBtn.style.display = "none";
        return;
      }

      resultEl.classList.remove("error");
      try {
        const result = await convertDate(d, m, y, directionEl.value, lang);
        let out = result.text;

        const currentDate = new Date(); currentDate.setHours(0,0,0,0);
        const inputDate = directionEl.value === 'g2h' ? new Date(y, m - 1, d) : result.gregDate;
        const diffDays = Math.floor((currentDate - inputDate) / (1000*60*60*24));

        const gregAge = calculateDuration(diffDays, 365.25, 365.25/12, t);
        const hijriAge = calculateDuration(diffDays, 354.367, 354.367/12, t);

        out += `
          <div class="age-section"><h3>${t.gregAgeTitle}</h3>${gregAge}</div>
          <div class="age-section"><h3>${t.hijriAgeTitle}</h3>${hijriAge}</div>
        `;

        resultEl.innerHTML = `<button class="copy-btn" id="copy-btn">${t.copyText}</button>${out}`;
        resultEl.style.display = "block";

        // تفعيل زر النسخ
        document.getElementById("copy-btn").onclick = copyResult;

      } catch (e) {
        resultEl.innerHTML = `<button class="copy-btn" id="copy-btn" style="display:none;">${t.copyText}</button>${e.message || t.error}`;
        resultEl.className = "result error";
        resultEl.style.display = "block";
      }
    }

    // تعبئة التاريخ الحالي
    async function setCurrentDate() {
      const now = new Date();
      dayEl.value = now.getDate();
      monthEl.value = now.getMonth() + 1;
      yearEl.value = now.getFullYear();
      directionEl.value = "g2h";
      await autoConvert();
    }

    // مستمعات الأحداث
    [dayEl, monthEl, yearEl, directionEl].forEach(el => el.addEventListener('input', autoConvert));
    yearEl.addEventListener('focus', showYearTooltip);
    yearEl.addEventListener('blur', () => { clearTimeout(tooltipTimeout); yearTooltipEl.style.display = 'none'; });
    languageEl.addEventListener('change', () => { updateLanguage(languageEl.value); if (dayEl.value && monthEl.value && yearEl.value) autoConvert(); });
    convertBtn.addEventListener("click", autoConvert);
    resetBtn.addEventListener("click", async () => { await setCurrentDate(); resultEl.style.display = "none"; });

    // تحميل
    updateLanguage(languageEl.value);
    setCurrentDate();
  </script>
</body>
</html>
