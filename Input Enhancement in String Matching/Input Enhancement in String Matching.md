<head>
  <link href="https://cdn.fontcdn.ir/Font/Persian/Vazir/Vazir.css" rel="stylesheet" type="text/css">
  <style>
  * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body, div, p, h1, h2, h3, h4, h5, h6 {
      font-family: 'Vazir', sans-serif;
    }
    .math {
  direction: ltr;
  unicode-bidi: isolate;
  display: block;     /* باعث می‌شه مثل بلوک رفتار کنه */
  text-align: center; /* وسط‌چین محتوا */
  margin: 12px auto;  /* فاصله و وسط‌چینی */
  font-size: 1.2em;   /* اختیاری: قشنگ‌تر */
}
.math_normal {
  direction: ltr;
  unicode-bidi: isolate;
  display: inline-block;
}
    .header-container {
      width: 100%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 18px 60px;
      border-bottom: 3px solid #003c8f;
      background: #f5f8ff;
    }
    .logo-block {
      text-align: center;
      min-width: 120px;
    }
    .logo-img {
      width: 80px;
      height: auto;
      margin-bottom: 6px;
    }
    .info-block {
      flex-grow: 1;
      text-align: center;
      color: #222;
      line-height: 1.8;
      font-size: 17px;
    }
    .info-block strong {
      color: #003c8f;
      font-weight: bold;
    }
    hr {
      border: none;
      height: 1px;
      background: #ccc;
      margin: 0;
    }

  </style>
</head>

<div dir="rtl" align="right" style="padding: 0 60px;">

<p align="center" dir="rtl" style="font-weight: bold; font-size: 24px;">

<div class="header-container">

  <div class="logo-block">
    <img src="FUM_Logo.png" alt="لوگوی دانشگاه فردوسی مشهد" class="logo-img">
    <div><p><strong>دانشگاه فردوسی مشهد</strong></p></div>
  </div>

  <div class="info-block">
    <p style="font-size: 30px;"><strong>الگوریتم پیشرفته</strong></p>
    <p style="font-size: 25px;"><strong>بهبود ورودی در تطبیق رشته (Input Enhancement in String Matching)</strong></p>
    <p style="font-size: 20px;"><strong>دکتر حامد فهیمی</strong></p>
  </div>

  <div class="logo-block">
    <img src="MathmaticaFacultyLogo.jpg" alt="لوگوی دانشکده علوم ریاضی" class="logo-img">
    <div><p><strong>دانشکده علوم ریاضی</strong></p></div>
  </div>

</div>

### الگوریتم‌های Horspool و Boyer-Moore

---

### ۱. مقدمه

مسئله تطبیق رشته (String Matching) شامل یافتن الگوی $P$ (به طول $m$) در متن $T$ (به طول $n$) است.
* **روش Brute-Force:** در بدترین حالت دارای پیچیدگی $O(nm)$ است، زیرا برای هر موقعیت ممکن است $m$ مقایسه انجام دهد.
* **ایده بهبود ورودی (Input Enhancement):** به جای پردازش مستقیم، ابتدا الگوی $P$ را پیش‌پردازش می‌کنیم تا اطلاعاتی به دست آوریم که در حین جستجو به ما اجازه دهد "پرش‌های" بلندتری روی متن انجام دهیم.

دو الگوریتم مشهور که از این ایده استفاده می‌کنند عبارتند از:
1.  الگوریتم **Knuth-Morris-Pratt (KMP)** (چپ به راست مقایسه می‌کند).
2.  الگوریتم **Boyer-Moore** (راست به چپ مقایسه می‌کند).

در این جلسه روی خانواده الگوریتم‌های Boyer-Moore (شامل نسخه ساده‌شده آن، الگوریتم Horspool) تمرکز می‌کنیم.

---

### ۲. الگوریتم Horspool (نسخه ساده‌شده Boyer-Moore)

این الگوریتم توسط R. Horspool ارائه شد و اغلب برای متون تصادفی (مانند متن‌های زبان طبیعی) به اندازه Boyer-Moore کارآمد است، اما پیاده‌سازی ساده‌تری دارد.

#### نحوه عملکرد
1.  **جهت مقایسه:** الگو را با متن تراز کرده و مقایسه‌ها را از **راست به چپ** (از آخرین کاراکتر الگو) انجام می‌دهیم.
2.  **ایده پرش (Shift):** اگر عدم تطبیق رخ داد یا حتی اگر تطبیق کامل شد، باید الگو را به سمت راست حرکت دهیم. اندازه این پرش بر اساس کاراکتری از متن تعیین می‌شود که **هم‌راستا با آخرین کاراکتر الگو** است. بیایید این کاراکتر را $c$ بنامیم.


#### محاسبه جدول پرش (Shift Table)
برای تعیین اندازه پرش، یک جدول بر اساس تمام کاراکترهای ممکن الفبا می‌سازیم. فرض کنید طول الگو $m$ است. اندازه پرش $t(c)$ به صورت زیر محاسبه می‌شود :

$$
t(c) =
\begin{cases}
m & \text{اگر } c \text{ در } m-1 \text{ کاراکتر اول الگو نباشد} \\
\text{فاصله آخرین رخداد } c \text{ تا انتهای الگو} & \text{اگر } c \text{ در } m-1 \text{ کاراکتر اول موجود باشد}
\end{cases}
$$

**نکته مهم:** ما فقط <span class="math_normal">$m-1$</span> کاراکتر اول الگو را برای محاسبه فاصله بررسی می‌کنیم. آخرین کاراکتر الگو در محاسبه فاصله لحاظ نمی‌شود (مگر اینکه در جای دیگری از الگو تکرار شده باشد).

#### مثال: ساخت جدول برای الگوی `BARBER`
طول الگو <span class="math_normal">$m=6$</span>.
کاراکترهای موجود در <span class="math_normal">$m-1$</span> بخش اول (`BARBE`): B, A, R, E.

* **B:** در اندیس ۰ و ۳ است. آخرین رخداد (اندیس ۳) فاصله تا انتها (<span class="math_normal">$m-1-3 = 2$</span>) است. پس <span class="math_normal">$t(B)=2$</span>.
* **A:** در اندیس ۱ است. فاصله (<span class="math_normal">$6-1-1=4$</span>). پس <span class="math_normal">$t(A)=4$</span>.
* **R:** در اندیس ۲ است. فاصله (<span class="math_normal">$6-1-2=3$</span>). پس <span class="math_normal">$t(R)=3$</span>.
* **E:** در اندیس ۴ است. فاصله (<span class="math_normal">$6-1-4=1$</span>). پس <span class="math_normal">$t(E)=1$</span>.
* **سایر کاراکترها:** در الگو نیستند، پس <span class="math_normal">$t(c)=6$</span>.

| کاراکتر | A | B | E | R | سایر |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **Shift** | 4 | 2 | 1 | 3 | 6 |


#### شبه‌کد الگوریتم Horspool

<div style="direction: rtl; text-align: left; font-family: 'Courier New', monospace; font-size: 0.9em; background-color: #f6f8fa; border: 1px solid #d1d5da; border-radius: 6px; padding: 16px; line-height: 1.6; color: #24292e;">
    <span style="font-weight: bold;">ALGORITHM HorspoolMatching(P[0..m-1], T[0..n-1])</span><br>
    <span style="color: #6a737d;">// 1. Preprocessing: Generate Shift Table</span><br>
    <span style="margin-left: 20px; display: inline-block;">ShiftTable(P) -> Table</span><br>
    <br>
    <span style="color: #6a737d;">// 2. Searching</span><br>
    <span style="margin-left: 20px; display: inline-block;">i <- m - 1</span><br>
    <span style="margin-left: 20px; display: inline-block;">while i <= n - 1 do</span><br>
    <span style="margin-left: 40px; display: inline-block;">k <- 0</span><br>
    <span style="margin-left: 40px; display: inline-block;">while k <= m - 1 and P[m - 1 - k] == T[i - k] do</span><br>
    <span style="margin-left: 60px; display: inline-block;">k <- k + 1</span><br>
    <span style="margin-left: 40px; display: inline-block;">if k == m</span><br>
    <span style="margin-left: 60px; display: inline-block;">return i - m + 1 </span><span style="color: #6a737d;">// Match found</span><br>
    <span style="margin-left: 40px; display: inline-block;">else</span><br>
    <span style="margin-left: 60px; display: inline-block;">i <- i + Table[T[i]] </span><span style="color: #6a737d;">// Shift based on text char aligned with pattern end</span><br>
    <span style="margin-left: 20px; display: inline-block;">return -1</span>
</div>

#### تحلیل پیچیدگی
* **بدترین حالت:** $O(nm)$ (مشابه Brute-force).
* **حالت میانگین:** $O(n)$ (اغلب بسیار سریع‌تر از Brute-force برای متون بزرگ و الفبای بزرگ).

---

### ۳. الگوریتم Boyer-Moore (نسخه کامل)

این الگوریتم پیچیده‌تر است و از **دو** قانون برای تعیین بیشترین پرش ممکن استفاده می‌کند و ماکسیمم آن دو را انتخاب می‌کند:
<span class="math">$$d = \max \{d_1, d_2\}$$</span>

#### ۱. قانون نماد بد (Bad-Symbol Shift) - <span class="math_normal">$d_1$</span>
این قانون مشابه الگوریتم Horspool عمل می‌کند اما تعداد کاراکترهای تطبیق‌یافته (<span class="math_normal">$k$</span>) را نیز در نظر می‌گیرد.
فرمول:
<span class="math">$$d_1 = \max \{t_1(c) - k, 1\}$$</span>
که در آن <span class="math_normal">$t_1(c)$</span> همان مقدار جدول Horspool برای کاراکتر ناسازگار در متن است و <span class="math_normal">$k$</span> تعداد کاراکترهایی است که از راست با موفقیت تطبیق داده‌ایم.

#### ۲. قانون پسوند خوب (Good-Suffix Shift) - <span class="math_normal">$d_2$</span>
این قانون بر اساس کاراکترهایی که با موفقیت تطبیق یافته‌اند (پسوند به طول <span class="math_normal">$k$</span>) عمل می‌کند.
* الگوریتم بررسی می‌کند آیا این پسوند (<span class="math_normal">$suff(k)$</span>) جای دیگری در الگو تکرار شده است؟
* اگر تکرار شده باشد، الگو را طوری جابجا می‌کند که رخداد قبلی با متن تراز شود.
* اگر تکرار نشده باشد، کل الگو را به اندازه <span class="math_normal">$m$</span> جابجا می‌کند (با در نظر گرفتن استثناهایی برای پیشوندها) .


#### مثال اجرایی: الگوی `BAOBAB`
متن: `B E S S _ K N E W _ A B O U T _ B A O B A B S`
1.  تطبیق `BAOBAB` با ابتدای متن.
2.  آخرین حرف الگو `B` است، حرف متناظر در متن `_` (فاصله) است. تطبیق شکست می‌خورد (<span class="math_normal">$k=0$</span>).
3.  جدول Bad-Symbol برای `_` مقدار ۶ می‌دهد. پرش <span class="math_normal">$d_1=6$</span>.
4.  ... (الگوریتم ادامه می‌یابد تا جایی که تطبیق بخشی صورت گیرد).
5.  در یک مرحله، `BAB` (پسوند) تطبیق می‌یابد اما کاراکتر قبل از آن شکست می‌خورد. در اینجا از قانون Good-Suffix استفاده می‌شود تا الگوی `BAB` بعدی در کلمه `BAOBAB` زیر بخش تطبیق یافته قرار گیرد .

---

### ۴. حل تمرین‌های منتخب

#### تمرین ۱: جستجو با Horspool
**سوال:** الگوریتم Horspool را برای جستجوی الگوی `SORTING` در متن زیر اعمال کنید:
`SORTING_ALGORITHM_CAN_USE_BRUTE_FORCE_METHOD`

**حل:**
**گام ۱: ساخت جدول پرش (Shift Table)**
طول الگو <span class="math_normal">$m=7$</span>. الفبا شامل حروف و `_` است.
بررسی حروف `SORTIN` (بدون G آخر):
* S (اندیس 0): <span class="math_normal">$7 - 1 - 0 = 6$</span>
* O (اندیس 1): <span class="math_normal">$7 - 1 - 1 = 5$</span>
* R (اندیس 2): <span class="math_normal">$7 - 1 - 2 = 4$</span>
* T (اندیس 3): <span class="math_normal">$7 - 1 - 3 = 3$</span>
* I (اندیس 4): <span class="math_normal">$7 - 1 - 4 = 2$</span>
* N (اندیس 5): <span class="math_normal">$7 - 1 - 5 = 1$</span>
* G (آخرین): پیش‌فرض <span class="math_normal">$m=7$</span>.
* سایر (_ و ...): ۷.

**جدول:** `{S:6, O:5, R:4, T:3, I:2, N:1, G:7, Others:7}`

**گام ۲: جستجو**
1.  الگو زیر `SORTING` قرار می‌گیرد.
    * مقایسه آخر: `G` با `_` (در متن). عدم تطبیق.
    * کاراکتر متن `_` است. مقدار پرش از جدول: ۷.
2.  الگو ۷ خانه به راست می‌رود. زیر `ALGORITHM` قرار می‌گیرد.
    * مقایسه `G` با `M`. عدم تطبیق.
    * کاراکتر متن `M` است. در جدول نیست (Others). پرش: ۷.
3.  الگو ۷ خانه جلو می‌رود... (و به همین ترتیب ادامه می‌یابد).

#### تمرین ۲: توالی یابی DNA
**سوال:** جدول پرش را برای قطعه ژنی `TCCTATTCTT` بسازید.

**حل:**
طول الگو <span class="math_normal">$m=10$</span>. الفبا: <span class="math_normal">$\{A, C, G, T\}$</span>.
باید ۹ کاراکتر اول `TCCTATTCT` را بررسی کنیم:
* T (اندیس 0): <span class="math_normal">$9$</span>
* C (اندیس 1): <span class="math_normal">$8$</span>
* C (اندیس 2): <span class="math_normal">$7$</span>
* T (اندیس 3): <span class="math_normal">$6$</span>
* A (اندیس 4): <span class="math_normal">$5$</span>
* T (اندیس 5): <span class="math_normal">$4$</span>
* T (اندیس 6): <span class="math_normal">$3$</span>
* C (اندیس 7): <span class="math_normal">$2$</span>
* T (اندیس 8): <span class="math_normal">$1$</span>

**نکته:** وقتی یک حرف تکرار می‌شود (مثل T یا C)، **آخرین** رخداد (راست‌ترین در ۹ کاراکتر اول) مقدار نهایی جدول را تعیین می‌کند.

**جدول نهایی:**
* **A:** مقدار ۵ (از اندیس 4).
* **C:** مقدار ۲ (از اندیس 7).
* **G:** در الگو نیست <span class="math_normal">$\to 10$</span>.
* **T:** مقدار ۱ (از اندیس 8).

</div>