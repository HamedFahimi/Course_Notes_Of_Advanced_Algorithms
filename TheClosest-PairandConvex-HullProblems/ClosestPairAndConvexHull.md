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
    <p style="font-size: 20px;"><strong>حل مسائل هندسی با روش تقسیم و غلبه (D&C)</strong></p>
    <p style="font-size: 20px;"><strong>دکتر حامد فهیمی</strong></p>
  </div>

  <div class="logo-block">
    <img src="MathmaticaFacultyLogo.jpg" alt="لوگوی دانشکده علوم ریاضی" class="logo-img">
    <div><p><strong>دانشکده علوم ریاضی</strong></p></div>
  </div>

</div>

### مسئله نزدیک‌ترین زوج نقاط و مسئله پوسته محدب

-----

### مقدمه

در مباحث قبلی دیدیم که روش‌های "الگوریتم‌های brute-force" برای مسائل هندسی معمولاً کارایی پایینی دارند. برای مثال، پیدا کردن نزدیک‌ترین زوج نقاط در صفحه با روش brute-force نیاز به زمان $\Theta(n^2)$ دارد. در این جلسه، با استفاده از تکنیک **تقسیم و غلبه**، الگوریتم‌هایی با کارایی مجانبی بسیار بهتر برای دو مسئله کلاسیک هندسه محاسباتی ارائه می‌دهیم:

1. **مسئله نزدیک‌ترین زوج (The Closest-Pair Problem)**
2. **مسئله پوسته محدب (The Convex-Hull Problem)**

-----

### ۱. مسئله نزدیک‌ترین زوج (The Closest-Pair Problem)

#### تعریف مسئله

مجموعه‌ای از $n$ نقطه ($n>1$) در صفحه مختصات دکارتی داریم. هدف پیدا کردن دو نقطه‌ای است که کمترین فاصله اقلیدسی را نسبت به یکدیگر دارند.

#### پیش‌پردازش (Preprocessing)

برای ساده‌سازی، فرض می‌کنیم نقاط متمایز هستند. قبل از شروع الگوریتم اصلی، نقاط را مرتب می‌کنیم:

  * آرایه $P$: نقاط مرتب شده بر اساس مختصات $x$.
  * آرایه $Q$: نقاط مرتب شده بر اساس مختصات $y$.

#### مراحل الگوریتم تقسیم و غلبه

اگر تعداد نقاط کم باشد (<span class="math_normal">$2 \le n \le 3$</span>)، مسئله به سادگی با روش brute-force حل می‌شود. اما برای <span class="math_normal">$n>3$</span>:

1.  **تقسیم (Divide):** نقاط را با یک خط عمودی <span class="math_normal">$x=m$</span> (که <span class="math_normal">$m$</span> میانه مختصات <span class="math_normal">$x$</span> نقاط است) به دو زیرمجموعه <span class="math_normal">$P_l$</span> (چپ) و <span class="math_normal">$P_r$</span> (راست) تقسیم می‌کنیم. هر بخش تقریباً <span class="math_normal">$n/2$</span> نقطه دارد.

2.  **غلبه (Conquer):** الگوریتم را به صورت بازگشتی برای <span class="math_normal">$P_l$</span> و <span class="math_normal">$P_r$</span> فراخوانی می‌کنیم تا کمترین فاصله‌ها در سمت چپ (<span class="math_normal">$d_l$</span>) و سمت راست (<span class="math_normal">$d_r$</span>) به دست آیند.

      * فرض کنید <span class="math_normal">$d = \min\{d_l, d_r\}$</span> باشد.

3.  **ترکیب (Combine):**

      * آیا <span class="math_normal">$d$</span> پاسخ نهایی است؟ خیر. ممکن است نزدیک‌ترین زوج شامل یک نقطه در چپ و یک نقطه در راست باشد که فاصله آن‌ها کمتر از <span class="math_normal">$d$</span> است.
      * **ناحیه نواری (The Strip):** ما فقط نیاز داریم نقاطی را بررسی کنیم که در فاصله <span class="math_normal">$d$</span> از خط جداکننده <span class="math_normal">$x=m$</span> قرار دارند (یک نوار عمودی با عرض <span class="math_normal">$2d$</span>).

#### بررسی نقاط داخل نوار (The Strip Analysis)

  * لیست $S$ را از نقاطی درون $Q$ که در نوار قرار دارند تشکیل می‌دهیم (این نقاط قبلاً بر اساس $y$ مرتب شده‌اند).
  * برای هر نقطه $p$ در $S$، تنها نیاز است نقاطی را بررسی کنیم که مختصات $y$ آن‌ها حداکثر به اندازه $d$ با $p$ فاصله دارد.
  * **نکته کلیدی:** از نظر هندسی می‌توان ثابت کرد که در مستطیل مورد نظر ($d \times 2d$)، تعداد نقاطی که کاندیدای بررسی هستند بسیار محدود است.
  * بنابراین، حلقه داخلی الگوریتم به جای چک کردن تمام نقاط، برای هر نقطه فقط تعداد محدودی (مثلاً ۵ تا ۷ نقطه بعدی) را چک می‌کند که این عمل زمان خطی $O(n)$ می‌برد.

#### شبه‌کد (خلاصه)

<div style="background-color: #f6f8fa; border: 1px solid #d1d5da; border-radius: 6px; padding: 16px; font-family: Consolas, 'Courier New', monospace; direction: rtl; text-align: right; line-height: 1.6; color: #24292e;">
    <strong>Algorithm EfficientClosestPair(P, Q):</strong><br>
    1. اگر n <= 3: حل با brute-force.<br>
    2. P_l, Q_l = نیمه چپ نقاط؛ P_r, Q_r = نیمه راست نقاط.<br>
    3. d_l = EfficientClosestPair(P_l, Q_l)<br>
    4. d_r = EfficientClosestPair(P_r, Q_r)<br>
    5. d = min(d_l, d_r)<br>
    6. m = خط جداکننده<br>
    7. S = نقاطی از Q که <span class="math_normal">|x - m| < d</span> هستند.<br>
    8. برای هر نقطه i در S:<br>
    <span style="margin-right: 25px; display: inline-block;">برای k از i+1 تا i+7:</span><br>
    <span style="margin-right: 50px; display: inline-block;">اگر فاصله عمودی < d:</span><br>
    <span style="margin-right: 75px; display: inline-block;">فاصله اقلیدسی را محاسبه و d را در صورت لزوم آپدیت کن.</span><br>
    9. بازگرداندن d.
</div>

#### تحلیل پیچیدگی زمانی

از آنجا که مرحله تقسیم و مرحله ترکیب هر دو در زمان خطی <span class="math_normal">$O(n)$</span> انجام می‌شوند، رابطه بازگشتی به صورت زیر است:
<span class="math">$$T(n) = 2T(n/2) + \Theta(n)$$</span>
طبق قضیه اصلی (Master Theorem)، پیچیدگی زمانی برابر است با:
<span class="math">$$T(n) \in \Theta(n \log n)$$</span>

-----

# مطالعه پوسته محدب اختیاری
### ۲. مسئله پوسته محدب (Convex-Hull Problem) - الگوریتم Quickhull

#### تعریف مسئله

یافتن کوچکترین چندضلعی محدب که شامل تمام <span class="math_normal">$n$</span> نقطه داده شده باشد.

#### ایده کلی (Quickhull)

این الگوریتم شباهت زیادی به Quicksort دارد.

1.  نقطه‌ای با کمترین <span class="math_normal">$x$</span> (<span class="math_normal">$p_1$</span>) و بیشترین <span class="math_normal">$x$</span> (<span class="math_normal">$p_n$</span>) قطعاً رئوس پوسته محدب هستند.
2.  خط واصل <span class="math_normal">$p_1$</span> به <span class="math_normal">$p_n$</span> مجموعه نقاط را به دو بخش "پوسته بالایی" (Upper Hull) و "پوسته پایینی" (Lower Hull) تقسیم می‌کند.

#### مراحل ساخت پوسته بالایی

1.  نقطه‌ای مانند <span class="math_normal">$p_{max}$</span> را پیدا کنید که بیشترین فاصله را از خط <span class="math_normal">$p_1p_n$</span> دارد. این نقطه حتماً یک رأس پوسته است.
2.  نقاطی که درون مثلث <span class="math_normal">$p_1 p_{max} p_n$</span> قرار دارند، نمی‌توانند جزو پوسته باشند و حذف می‌شوند.
3.  سپس الگوریتم به صورت بازگشتی برای دو ناحیه باقیمانده (سمت چپ خط <span class="math_normal">$p_1p_{max}$</span> و سمت چپ خط <span class="math_normal">$p_{max}p_n$</span>) اجرا می‌شود.

#### نکات پیاده‌سازی هندسی

برای تشخیص اینکه یک نقطه سمت چپ یک خط است یا برای محاسبه مساحت مثلث (جهت یافتن دورترین نقطه)، از دترمینان استفاده می‌کنیم. مساحت مثلث با رئوس <span class="math_normal">$(x_1, y_1), (x_2, y_2), (x_3, y_3)$</span> برابر است با نصف مقدار دترمینان زیر:
<span class="math">$$\text{Area} = \frac{1}{2} (x_1y_2 + x_3y_1 + x_2y_3 - x_3y_2 - x_2y_1 - x_1y_3)$$</span>
علامت این عبارت مشخص می‌کند نقطه <span class="math_normal">$q_3$</span> در کدام سمت خط جهت‌دار <span class="math_normal">$q_1q_2$</span> قرار دارد.

#### تحلیل پیچیدگی زمانی

  * **بدترین حالت:** مشابه Quicksort، اگر تقسیم‌بندی نامتوازن باشد (مثلاً هر بار فقط یک نقطه حذف شود)، زمان اجرا <span class="math_normal">$\Theta(n^2)$</span> خواهد بود.
  * **حالت میانگین:** اگر نقاط به صورت تصادفی توزیع شده باشند، بسیاری از نقاط در هر مرحله حذف می‌شوند و زمان اجرا خطی <span class="math_normal">$O(n)$</span> خواهد بود.

-----

### ۳. حل تمرین‌های منتخب

#### تمرین ۱: مسئله نزدیک‌ترین زوج در حالت یک‌بعدی

**سوال:** الگوریتمی بر اساس تقسیم و غلبه برای یافتن نزدیک‌ترین دو عدد در یک مجموعه <span class="math_normal">$n$</span> تایی از اعداد حقیقی طراحی کنید.

**پاسخ:**
در حالت یک‌بعدی، نقاط روی محور اعداد (<span class="math_normal">$x$</span>) هستند.

1.  **راه حل ساده:**
      * ابتدا اعداد را مرتب می‌کنیم (Sort). این کار <span class="math_normal">$O(n \log n)$</span> زمان می‌برد.
      * پس از مرتب‌سازی، نزدیک‌ترین زوج الزاماً دو عدد مجاور در آرایه مرتب شده هستند.
      * با یک پیمایش خطی <span class="math_normal">$O(n)$</span> روی آرایه مرتب شده، تفاضل هر دو عنصر همسایه را محاسبه و کمترین را پیدا می‌کنیم.
2.  **راه حل بازگشتی (مشابه ساختار دوبعدی):**
      * میانه <span class="math_normal">$m$</span> را پیدا می‌کنیم. مجموعه را به <span class="math_normal">$S_L$</span> (اعداد کوچکتر از <span class="math_normal">$m$</span>) و <span class="math_normal">$S_R$</span> (اعداد بزرگتر از <span class="math_normal">$m$</span>) تقسیم می‌کنیم.
      * به صورت بازگشتی کمترین فاصله در چپ (<span class="math_normal">$d_L$</span>) و راست (<span class="math_normal">$d_R$</span>) را می‌یابیم.
      * <span class="math_normal">$d = \min(d_L, d_R)$</span>.
      * در مرحله ترکیب، باید فاصله بین "بزرگترین عدد در <span class="math_normal">$S_L$</span>" و "کوچکترین عدد در <span class="math_normal">$S_R$</span>" را چک کنیم. اگر فاصله آن‌ها کمتر از <span class="math_normal">$d$</span> بود، جواب جدید ما آن فاصله است.

#### تمرین ۸: بدترین حالت الگوریتم Quickhull

**سوال:** بدترین کارایی زمانی Quickhull چقدر است؟

**پاسخ:**
بدترین حالت زمانی رخ می‌دهد که در هر مرحله از بازگشت، افراز نقاط بسیار نامتوازن باشد.

  * این اتفاق زمانی می‌افتد که تمام نقاط داده شده واقعاً روی محیط پوسته محدب باشند (مثلاً نقاط روی محیط یک دایره قرار داشته باشند).
  * در این حالت، هیچ نقطه‌ای در داخل مثلث حذف نمی‌شود (مرحله حذفی وجود ندارد).
  * در هر مرحله بازگشتی، ما یک نقطه (<span class="math_normal">$p_{max}$</span>) را به عنوان رأس پیدا می‌کنیم و مسئله به دو زیرمسئله تقسیم می‌شود که یکی از آن‌ها ممکن است تهی و دیگری شامل <span class="math_normal">$n-1$</span> نقطه باشد.
  * رابطه بازگشتی مشابه بدترین حالت Quicksort می‌شود:
    <span class="math">$$T(n) = T(n-1) + O(n) \rightarrow T(n) \in \Theta(n^2)$$</span>
    بنابراین در بدترین حالت، کارایی آن مربعی است.

-----

</div>
