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
    <p style="font-size: 25px;"><strong>نظریه NP-کامل بودن (NP-Completeness)</strong></p>
    <p style="font-size: 20px;"><strong>دکتر حامد فهیمی</strong></p>
  </div>

  <div class="logo-block">
    <img src="MathmaticaFacultyLogo.jpg" alt="لوگوی دانشکده علوم ریاضی" class="logo-img">
    <div><p><strong>دانشکده علوم ریاضی</strong></p></div>
  </div>

</div>

<br>

این فصل به معرفی تکنیک‌هایی می‌پردازد که با استفاده از آن‌ها می‌توان ثابت کرد که برای یک مسئله‌ی مشخص، **الگوریتم کارآمدی (Efficient Algorithm) وجود ندارد**. اگرچه این نظریه نتایجی منفی ارائه می‌دهد، اما یک ابزار فوق‌العاده مفید برای طراح الگوریتم است. نظریه NP-کامل بودن به ما امکان می‌دهد تا تلاش‌هایمان را پربارتر متمرکز کنیم و مشخص سازد که چه زمانی جستجو برای یک الگوریتم کارآمد، محکوم به شکست است.

-----

### ۱. مسائل و مفهوم کاهش (Problems and Reductions)

ما در بسیاری از مسائل، الگوریتم کارآمدی پیدا نکرده‌ایم. نظریه NP-کامل بودن ابزارهایی را فراهم می‌کند تا نشان دهیم که این مسائل، در سطح بنیادین، **واقعاً یک مسئله واحد هستند**.

#### تعریف مسئله و نمونه (Problem and Instance)

1.  **مسئله‌ی الگوریتمی (Algorithmic Problem):** یک سؤال کلی است که دارای پارامترهای ورودی و شرایطی برای پاسخ یا راه‌حل رضایت‌بخش است.
2.  **نمونه (Instance):** یک مسئله الگوریتمی است که پارامترهای ورودی آن مشخص شده باشند.

**مثال: مسئله فروشنده دوره‌گرد (Traveling Salesman Problem - TSP)**

  * **مسئله:** کدام تور (<span class="math_normal">$v_1, v_2, ..., v_n$</span>) هزینه‌ی <span class="math_normal">$\sum_{i=1}^{n-1}d[v_i, v_{i+1}] + d[v_n, v_1]$</span> را به حداقل می‌رساند؟
  * **ورودی (Input):** یک گراف وزن‌دار (<span class="math_normal">$G$</span>).
  * هر گراف وزن‌دار یک **نمونه** از مسئله TSP را تعریف می‌کند. مسئله‌ی کلی TSP به دنبال یافتن الگوریتمی برای یافتن تور بهینه برای هر نمونه ممکن است.

#### ایده‌ی اصلی: کاهش (The Key Idea: Reduction)

**کاهش (Reduction)** یا **تبدیل (Translation)**، الگوریتمی است که یک مسئله را به مسئله‌ای دیگر تبدیل می‌کند.

دو مسئله‌ی الگوریتمی (Bandersnatch) و (Bo-billy) را در نظر بگیرید. فرض کنید الگوریتم زیر برای حل مسئله Bandersnatch وجود داشته باشد:

<div style="background-color: #f6f8fa; border: 1px solid #d1d5da; border-radius: 6px; padding: 16px; font-family: Consolas, 'Courier New', monospace; direction: rtl; text-align: right; line-height: 1.6; color: #24292e;">
    <strong>الگوریتم Bandersnatch(G):</strong><br>
    1. ورودی G را به یک نمونه Y از مسئله Bo-billy تبدیل کن.<br>
    2. زیرروال Bo-billy را برای حل نمونه Y فراخوانی کن.<br>
    3. پاسخ Bo-billy(Y) را به عنوان پاسخ Bandersnatch(G) بازگردان.
</div>

این الگوریتم زمانی مسئله Bandersnatch را به درستی حل می‌کند که تبدیل به Bo-billy همواره **صحت پاسخ** را حفظ کند.

**کاهش** یعنی یک تبدیل نمونه‌ها از یک نوع مسئله به نمونه‌های نوع دیگر، به طوری که پاسخ‌ها حفظ شوند:
$$\text{پاسخ Bandersnatch}(G) = \text{پاسخ Bo-billy}(Y)$$

-----

### ۲. مفهوم کاهش و کران پایین (Lower Bounds)

اگر تبدیل نمونه <span class="math_normal">$G$</span> به <span class="math_normal">$Y$</span> در زمان <span class="math_normal">$O(P(n))$</span> انجام شود، دو نتیجه ممکن است وجود داشته باشد:

1.  **اگر الگوریتم Bo-billy در زمان <span class="math_normal">$O(P'(n))$</span> اجرا شود:**
    این امر منجر به یک الگوریتم برای حل Bandersnatch در زمان <span class="math_normal">$O(P(n) + P'(n))$</span> می‌شود. ( با تبدیل مسئله و سپس اجرای زیرروال Bo-billy برای حل آن.)

2.  **اگر کران پایین <span class="math_normal">$\Omega(P''(n))$</span> برای حل Bandersnatch مشخص باشد:**
    در این صورت، <span class="math_normal">$\Omega(P''(n) - P(n))$</span> باید کران پایین برای محاسبه Bo-billy باشد.

      * **دلیل:** اگر می‌توانستیم Bo-billy را سریع‌تر از این زمان حل کنیم، کاهش فوق، کران پایین مشخص شده برای Bandersnatch را نقض می‌کرد. از آنجا که این امر غیرممکن است، راهی برای حل سریع‌تر Bo-billy وجود ندارد.

**نتیجه‌گیری مهم:** این کاهش نشان می‌دهد که **Bo-billy از Bandersnatch آسان‌تر نیست**. بنابراین، **اگر Bandersnatch سخت باشد، Bo-billy نیز باید سخت باشد.**

**درس کلیدی:** کاهش‌ها راهی برای نشان دادن این است که دو مسئله اساساً **یکسان** هستند. یک الگوریتم سریع (یا فقدان آن) برای یکی از مسائل، وجود یک الگوریتم سریع (یا فقدان آن) را برای دیگری نتیجه می‌دهد.

-----

### ۳. مسائل تصمیم‌گیری (Decision Problems)

کاهش‌ها تبدیل‌هایی بین مسائل هستند به طوری که پاسخ‌های آن‌ها در هر نمونه‌ی مسئله یکسان باشد.

**مسائل تصمیم‌گیری** ساده‌ترین و جالب‌ترین دسته از مسائل هستند که پاسخ‌های آن‌ها محدود به **درست (True)** و **نادرست (False)** است.

**مزیت:** کار کردن با تبدیل بین مسائل تصمیم‌گیری راحت‌تر است، زیرا هر دو تنها پاسخ‌های درست و غلط را مجاز می‌دانند. خوشبختانه، بسیاری از مسائل بهینه‌سازی (Optimization Problems) جالب را می‌توان به صورت مسائل تصمیم‌گیری بیان کرد که جوهر محاسباتی مسئله اصلی را حفظ می‌کنند.

**مثال: تبدیل مسئله TSP به مسئله تصمیم‌گیری TSP (TSDP)**

  * **مسئله فروشنده دوره‌گرد تصمیم‌گیری (TSDP):**
      * **ورودی:** یک گراف وزن‌دار $G$ و یک عدد صحیح $k$.
      * **خروجی:** آیا توری برای TSP با هزینه $\le k$ وجود دارد؟

این نسخه‌ی تصمیم‌گیری جوهره‌ی مسئله فروشنده دوره‌گرد را در بر می‌گیرد:

  * اگر یک الگوریتم سریع برای مسئله تصمیم‌گیری داشته باشید، می‌توانید با جستجوی دودویی بر روی مقادیر مختلف $k$، به سرعت به هزینه‌ی راه‌حل بهینه‌ی TSP دست یابید.
  * با کمی هوشمندی بیشتر، می‌توانید **ترتیب واقعی تور** را با استفاده از یک راه‌حل سریع برای مسئله تصمیم‌گیری بازسازی کنید.

از این به بعد، به طور کلی در مورد مسائل تصمیم‌گیری صحبت می‌کنیم، زیرا کار با آن‌ها آسان‌تر است و همچنان قدرت نظریه NP-کامل بودن را حفظ می‌کنند.

-----

### ۴. حل تمرین: کاهش برای الگوریتم‌های کارآمد (Closest Pair)

کاهش‌ها راهی محترمانه برای ایجاد الگوریتم‌های جدید از الگوریتم‌های قدیمی هستند. در این قسمت به مثالی از یک کاهش می‌پردازیم که منجر به یک الگوریتم کارآمد می‌شود.

#### مسئله جفت نزدیک‌ترین (Closest Pair)

  * **مسئله:** یافتن جفتی از اعداد در یک مجموعه‌ی <span class="math_normal">$S$</span> که کوچکترین اختلاف بین آن‌ها را دارند.
      * *مثال:* نزدیک‌ترین جفت در <span class="math_normal">$S = \{10, 4, 8, 3, 12\}$</span>، جفت <span class="math_normal">$(3, 4)$</span> است.

ما می‌توانیم آن را به یک مسئله تصمیم‌گیری تبدیل کنیم (آیا کوچکترین اختلاف کمتر یا مساوی یک آستانه <span class="math_normal">$t$</span> است؟).

  * **مسئله تصمیم‌گیری جفت نزدیک به اندازه کافی (Close Enough Pair):**
      * **ورودی:** یک مجموعه‌ی <span class="math_normal">$S$</span> از <span class="math_normal">$n$</span> عدد و آستانه‌ی <span class="math_normal">$t$</span>.
      * **خروجی:** آیا جفتی <span class="math_normal">$s_i, s_j \in S$</span> وجود دارد به طوری که <span class="math_normal">$|s_i - s_j| \le t$</span>؟

#### الگوریتم مبتنی بر کاهش به مرتب‌سازی (Reduction to Sorting)

یافتن نزدیک‌ترین جفت، یک کاربرد ساده‌ی **مرتب‌سازی (Sorting)** است، زیرا نزدیک‌ترین جفت **باید** بعد از مرتب‌سازی، همسایه‌ی یکدیگر باشند.

**الگوریتم CloseEnoughPair(S, t):**
    1. S را مرتب کن.
    2. آیا <span class="math_normal">$min_{1 <= i < n} |s_{i+1} - s_{i}| <= t$</span> است؟ 
       (یعنی کوچکترین اختلاف بین عناصر متوالی در لیست مرتب شده، کمتر یا مساوی t است؟)

**تحلیل کارایی:**

  * **کاهش:** این مسئله به **مرتب‌سازی** کاهش داده شده است.
  * **پیچیدگی زمانی:** اگر از الگوریتم مرتب‌سازی <span class="math_normal">$O(n \log n)$</span> استفاده کنیم، زمان اجرای کل الگوریتم برای یافتن نزدیک‌ترین جفت <span class="math_normal">$O(n \log n + n)$</span> خواهد بود که در نهایت <span class="math_normal">$O(n \log n)$</span> است.

-----

### ۵. حل تمرین: اثبات کران پایین مرتب‌سازی با استفاده از کاهش

این کاهش (جفت نزدیک‌ترین به مرتب‌سازی) می‌تواند برای اثبات کران‌های پایین نیز استفاده شود.

**سؤال:** فرض کنید ما بدانیم که مسئله **جفت نزدیک‌ترین به اندازه کافی** (Close Enough Pair) در بدترین حالت به <span class="math_normal">$\Omega(n \log n)$</span> زمان نیاز دارد. با استفاده از کاهش فوق، چگونه می‌توان ثابت کرد که مرتب‌سازی نمی‌تواند سریع‌تر از <span class="math_normal">$\Omega(n \log n)$</span> حل شود؟

**حل:**

ما یک کاهش از **جفت نزدیک‌ترین به اندازه کافی (A)** به **مرتب‌سازی (B)** داریم.

1.  **فرض (Premise):** کران پایین برای حل مسئله A برابر با <span class="math_normal">$\Omega(n \log n)$</span> است.
2.  **فرضیه‌ی نقض:** فرض کنید یک الگوریتم سریع‌تر برای **مرتب‌سازی (B)** وجود دارد، مثلاً یک الگوریتم <span class="math_normal">$O(P'(n))$</span> که <span class="math_normal">$P'(n)$</span> سریع‌تر از <span class="math_normal">$O(n \log n)$</span> است.
3.  **ترکیب (Composition):** طبق کاهش، ما می‌توانیم مسئله A را در زمان <span class="math_normal">$O(\text{زمان کاهش} + \text{زمان حل B})$</span> حل کنیم. زمان کاهش برای این مسئله <span class="math_normal">$O(n)$</span> (برای بررسی اختلافات همسایه‌ها) است. پس زمان کل برای حل A می‌شود <span class="math_normal">$O(n + P'(n))$</span>.
4.  **تناقض:** اگر <span class="math_normal">$P'(n)$</span> سریع‌تر از <span class="math_normal">$O(n \log n)$</span> باشد، کل زمان حل A یعنی <span class="math_normal">$O(n + P'(n))$</span> نیز سریع‌تر از <span class="math_normal">$\Omega(n \log n)$</span> خواهد بود. این نتیجه، فرض اولیه (کران پایین A برابر با <span class="math_normal">$\Omega(n \log n)$</span> است) را نقض می‌کند.
5.  **نتیجه‌گیری:** چون نقض کران پایین امکان‌پذیر نیست، فرضیه‌ی نقض ما (وجود الگوریتمی سریع‌تر از <span class="math_normal">$O(n \log n)$</span> برای مرتب‌سازی) باید غلط باشد.

**اثبات:** این کاهش کفایت می‌کند تا ثابت کند که **مرتب‌سازی** در بدترین حالت نمی‌تواند سریع‌تر از <span class="math_normal">$\Omega(n \log n)$</span> حل شود.

</div>