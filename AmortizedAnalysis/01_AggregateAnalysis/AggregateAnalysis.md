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
    <p style="font-size: 25px;"><strong>تحلیل سرشکن</strong></p>
    <p style="font-size: 20px;"><strong>دکتر حامد فهیمی</strong></p>
  </div>

  <div class="logo-block">
    <img src="MathmaticaFacultyLogo.jpg" alt="لوگوی دانشکده علوم ریاضی" class="logo-img">
    <div><p><strong>دانشکده علوم ریاضی</strong></p></div>
  </div>

</div>

## تحلیل سرشکن‌شده (Amortized Analysis)

**مقدمه:**

در ادامه می‌خواهیم مفهومی مهم در تحلیل الگوریتم‌ها به نام **«تحلیل سرشکن‌شده» (Amortized Analysis)** را بررسی کنیم.

در تحلیل سرشکن‌شده، ما زمان مورد نیاز برای انجام دنباله‌ای از عملیات روی یک ساختمان داده را بر کل عملیات انجام شده، میانگین می‌گیریم. هدف این است که نشان دهیم، اگرچه ممکن است یک عملیات واحد در یک دنباله بسیار گران باشد، اما میانگین هزینه هر عملیات در آن دنباله، کوچک است.

### تفاوت تحلیل سرشکن‌شده و تحلیل حالت میانگین (Average-Case)

ممکن است این تحلیل شبیه به تحلیل حالت میانگین (Average-Case Analysis) به نظر برسد، اما یک تفاوت اساسی وجود دارد:

* **تحلیل سرشکن‌شده** هیچ احتمالی را در بر نمی‌گیرد.
* این تحلیل، **عملکرد میانگین هر عملیات را در بدترین حالت (worst-case) تضمین می‌کند**. یعنی ما یک مرز بالای قطعی (Deterministic) برای هزینه کل یک دنباله از عملیات به دست می‌آوریم.

### سه تکنیک اصلی تحلیل سرشکن‌شده

در این فصل، ما سه تکنیک رایج برای تحلیل سرشکن‌شده را پوشش خواهیم داد:

1.  **تحلیل تجمعی (Aggregate Analysis):** که امروز به تفصیل به آن خواهیم پرداخت. در این روش، ما یک کران بالای <span class="math_normal">$T(n)$</span> را برای هزینه کل یک دنباله از <span class="math_normal">$n$</span> عملیات تعیین می‌کنیم. سپس هزینه سرشکن‌شده (Amortized Cost) هر عملیات <span class="math_normal">$T(n)/n$</span> خواهد بود. در این روش، همه عملیات هزینه سرشکن‌شده یکسانی دریافت می‌کنند.
2.  **روش حسابداری (Accounting Method):** در این روش، ما به عملیات‌های مختلف، هزینه‌های سرشکن‌شده متفاوتی اختصاص می‌دهیم. ما برخی عملیات‌ها را بیش از هزینه واقعی‌شان شارژ می‌کنیم (overcharge)  و این اضافه پرداخت را به عنوان "اعتبار پیش‌پرداخت" (prepaid credit) در ساختمان داده ذخیره می‌کنیم تا بعداً هزینه عملیاتی را که کمتر از هزینه واقعی‌شان شارژ می‌شوند، پرداخت کنیم.
3.  **روش پتانسیل (Potential Method):** این روش شبیه به روش حسابداری است، با این تفاوت که اعتبار پیش‌پرداخت را به عنوان "انرژی پتانسیل" کل ساختمان داده در نظر می‌گیرد، نه اینکه اعتبار را به اشیاء خاصی در داخل آن مرتبط کند.

**مثال‌هایی که بررسی خواهیم کرد:**
برای بررسی این سه روش، از دو مثال کلاسیک استفاده خواهیم کرد:
1.  پشته (Stack) با عملیات اضافی `MULTIPOP` (خالی کردن چند عنصر با هم).
2.  شمارنده دودویی (Binary Counter) با عملیات `INCREMENT` (یکی افزودن).

<div style="border-right: 4px solid #ccc; padding-right: 15px; margin-right: 0; padding-left: 0; text-align: right; direction: rtl;">
    <p><strong>نکته مهم:</strong> هزینه‌هایی که در طول تحلیل سرشکن‌شده تخصیص داده می‌شوند، <strong>فقط برای اهداف تحلیلی</strong> هستند و نباید در کد واقعی پیاده‌سازی شوند.</p>
</div>

---

## بخش ۱۷.۱: تحلیل تجمعی (Aggregate Analysis) 

در تحلیل تجمعی، ما نشان می‌دهیم که برای هر <span class="math_normal">$n$</span> دلخواه، یک دنباله از <span class="math_normal">$n$</span> عملیات در **کل**، زمان <span class="math_normal">$T(n)$</span> (در بدترین حالت) طول می‌کشد.

بنابراین، هزینه میانگین یا **هزینه سرشکن‌شده** (Amortized Cost) برای هر عملیات <span class="math_normal">$T(n)/n$</span> است.

توجه داشته باشید که این هزینه سرشکن‌شده به *هر* عملیات اعمال می‌شود، حتی اگر انواع مختلفی از عملیات‌ها در دنباله وجود داشته باشند. (این برخلاف دو روش دیگر است که می‌توانند هزینه‌های سرشکن‌شده متفاوتی به عملیات‌های مختلف اختصاص دهند ).

---

### مثال ۱: عملیات پشته (Stack Operations) 

بیایید تحلیل تجمعی را با یک پشته که عملیات جدیدی به آن اضافه شده، بررسی کنیم.

**عملیات استاندارد پشته:**
ما دو عملیات اساسی پشته را می‌شناسیم که هر دو در زمان <span class="math_normal">$O(1)$</span> اجرا می‌شوند:
* `PUSH(S, x)`: شیء <span class="math_normal">$x$</span> را به پشته <span class="math_normal">$S$</span> اضافه می‌کند.
* `POP(S)`: عنصر بالای پشته <span class="math_normal">$S$</span> را برمی‌گرداند.

فرض کنید هزینه واقعی هر یک از این عملیات‌ها 1 باشد. هزینه کل یک دنباله از <span class="math_normal">$n$</span> عملیات `PUSH` و `POP` برابر <span class="math_normal">$n$</span> و زمان اجرای کل <span class="math_normal">$\Theta(n)$</span> است.

**عملیات جدید: `MULTIPOP`**
حالا عملیات `MULTIPOP(S, k)` را اضافه می‌کنیم که <span class="math_normal">$k$</span> عنصر بالای پشته <span class="math_normal">$S$</span> را حذف می‌کند (یا اگر پشته کمتر از <span class="math_normal">$k$</span> عنصر داشت، کل پشته را خالی می‌کند).

<pre style="direction:ltr; text-align:left;">
MULTIPOP(S, k)
    while not STACK-EMPTY(S) and k > 0
        POP(S)
        k = k - 1
</pre>

**هزینه `MULTIPOP`:**
هزینه واقعی `MULTIPOP` برابر است با <span class="math_normal">$min(s, k)$</span>  که <span class="math_normal">$s$</span> تعداد عناصر پشته و <span class="math_normal">$k$</span> آرگومان تابع است.

**تحلیل ساده‌لوحانه (Naive Analysis):**
بیایید یک دنباله از <span class="math_normal">$n$</span> عملیات `PUSH`، `POP` و `MULTIPOP` را روی یک پشته خالی تحلیل کنیم.

  * هزینه بدترین حالت (Worst-case) یک عملیات `MULTIPOP` چقدر است؟ <span class="math_normal">$O(n)$</span>. (مثلاً پشته <span class="math_normal">$n$</span> عنصر داشته باشد و ما `MULTIPOP(S, n)` را صدا بزنیم ).
  * چون بدترین حالت *یک* عملیات <span class="math_normal">$O(n)$</span> است ، اگر <span class="math_normal">$n$</span> عملیات داشته باشیم (که <span class="math_normal">$O(n)$</span> تای آن‌ها می‌توانند `MULTIPOP` باشند)، هزینه کل <span class="math_normal">$O(n^2)$</span> خواهد بود.
  * این تحلیل <span class="math_normal">$O(n^2)$</span> اگرچه **صحیح** است، اما **دقیق (tight) نیست**.

**تحلیل تجمعی (Aggregate Analysis):**
بیایید با استفاده از تحلیل تجمعی، مرز بهتری پیدا کنیم.

  * **بینش کلیدی:** اگرچه یک `MULTIPOP` می‌تواند گران باشد، اما هر دنباله از <span class="math_normal">$n$</span> عملیات `PUSH`، `POP` و `MULTIPOP` روی یک پشته خالی، حداکثر <span class="math_normal">$O(n)$</span> هزینه دارد.
  * **چرا؟** یک شیء تنها زمانی می‌تواند از پشته `POP` شود (چه توسط `POP` عادی و چه درون `MULTIPOP`) که قبلاً `PUSH` شده باشد.
  * تعداد کل فراخوانی‌های `POP` (شامل فراخوانی‌های درون `MULTIPOP`) حداکثر برابر با تعداد کل عملیات‌های `PUSH` است.
  * در یک دنباله <span class="math_normal">$n$</span> عملیاتی، ما حداکثر <span class="math_normal">$n$</span> عملیات `PUSH` می‌توانیم داشته باشیم.
  * بنابراین، تعداد کل `POP`ها (شامل `MULTIPOP`) حداکثر <span class="math_normal">$n$</span> است. هزینه کل `PUSH`ها نیز حداکثر <span class="math_normal">$n$</span> است.
  * **نتیجه:** هزینه کل (<span class="math_normal">$T(n)$</span>) برای هر دنباله <span class="math_normal">$n$</span> عملیاتی، <span class="math_normal">$O(n)$</span> است.
  * **هزینه سرشکن‌شده:** <span class="math_normal">$T(n)/n = O(n)/n = O(1)$</span>.

**تأکید مجدد:** ما از استدلال احتمالی استفاده نکردیم. ما یک مرز بدترین حالت <span class="math_normal">$O(n)$</span> را برای *کل دنباله* <span class="math_normal">$n$</span> عملیاتی نشان دادیم  و سپس این هزینه کل را بر <span class="math_normal">$n$</span> تقسیم کردیم تا هزینه سرشکن‌شده به دست آید.

-----

### مثال ۲: افزایش‌دهنده شمارنده دودویی (Incrementing a Binary Counter) 

به عنوان مثال دوم تحلیل تجمعی، پیاده‌سازی یک شمارنده دودویی (binary counter) <span class="math_normal">$k$</span>-بیتی را در نظر بگیرید که از 0 به بالا می‌شمارد. ما از یک آرایه <span class="math_normal">$A[0..k-1]$</span> استفاده می‌کنیم.

<pre style="direction:ltr; text-align:left;">
INCREMENT(A)
    i = 0
    while i < A.length and A[i] == 1
        A[i] = 0
        i = i + 1
    if i < A.length
        A[i] = 1
</pre>

**هزینه `INCREMENT`:**
هزینه این عملیات، خطی با تعداد بیت‌هایی است که فلیپ (Flip) می‌شوند (از 0 به 1 یا 1 به 0).

**تحلیل ساده‌لوحانه:**

  * بدترین حالت (Worst-case) برای یک `INCREMENT` چه زمانی است؟ زمانی که تمام آرایه <span class="math_normal">$A$</span> پر از 1 باشد. (مثلاً 1111...1). در این حالت، هزینه <span class="math_normal">$\Theta(k)$</span> است.
  * بنابراین، یک دنباله از <span class="math_normal">$n$</span> عملیات `INCREMENT` در بدترین حالت <span class="math_normal">$O(nk)$</span> هزینه خواهد داشت.
  * باز هم، این تحلیل صحیح است، اما دقیق (tight) نیست.

**تحلیل تجمعی:**
ما می‌توانیم تحلیل خود را دقیق‌تر کنیم و نشان دهیم هزینه <span class="math_normal">$n$</span> عملیات `INCREMENT` (با شروع از صفر) <span class="math_normal">$O(n)$</span> است.

  * **مشاهده کلیدی:** همه بیت‌ها در هر بار `INCREMENT` فلیپ نمی‌شوند. (به جدول شکل 17.2 در PDF مراجعه کنید ).
  * بیت <span class="math_normal">$A[0]$</span> هر بار `INCREMENT` فلیپ می‌شود  (در <span class="math_normal">$n$</span> عملیات، <span class="math_normal">$n$</span> بار فلیپ می‌شود).
  * بیت <span class="math_normal">$A[1]$</span> یک در میان فلیپ می‌شود (در <span class="math_normal">$n$</span> عملیات، <span class="math_normal">$\lfloor n/2 \rfloor$</span> بار فلیپ می‌شود).
  * بیت <span class="math_normal">$A[2]$</span> هر چهار بار یکبار فلیپ می‌شود (در <span class="math_normal">$n$</span> عملیات، <span class="math_normal">$\lfloor n/4 \rfloor$</span> بار فلیپ می‌شود).
  * به طور کلی، بیت <span class="math_normal">$A[i]$</span> در یک دنباله <span class="math_normal">$n$</span> عملیاتی، <span class="math_normal">$\lfloor n/2^i \rfloor$</span> بار فلیپ می‌شود.

**محاسبه کل فلیپ‌ها (T(n)):**
تعداد کل فلیپ‌ها در <span class="math_normal">$n$</span> عملیات برابر است با:
<span class="math">$$T(n) = \sum_{i=0}^{k-1} \lfloor \frac{n}{2^i} \rfloor$$</span>
ما می‌توانیم این مجموع را با یک سری هندسی بی‌نهایت کران‌دار کنیم:
<span class="math">$$T(n) = \sum_{i=0}^{k-1} \lfloor \frac{n}{2^i} \rfloor \sum_{i=0}^{\infty} \frac{n}{2^i} = n \sum_{i=0}^{\infty} (\frac{1}{2})^i = n \cdot 2 = 2n$$</span>


  * **نتیجه:** هزینه کل بدترین حالت برای <span class="math_normal">$n$</span> عملیات `INCREMENT` (با شروع از صفر) <span class="math_normal">$O(n)$</span> است.
  * **هزینه سرشکن‌شده:** <span class="math_normal">$T(n)/n = O(n)/n = O(1)$</span>.
-----

## حل تمرین‌های بخش ۱۷.۱

### تمرین ۱-۱۷.۱ (MULTIPUSH) 

<div style="border-right: 4px solid #ccc; padding-right: 15px; margin-right: 0; padding-left: 0; text-align: right; direction: rtl;">
    <p><strong>سوال:</strong> اگر مجموعه عملیات پشته شامل عملیات <code>MULTIPUSH</code> نیز باشد که <strong>k</strong> آیتم را روی پشته PUSH می‌کند، آیا مرز <strong>O(1)</strong> برای هزینه سرشکن‌شده عملیات پشته همچنان پابرجا خواهد بود؟</p>
</div>

**پاسخ:** خیر، مرز <span class="math_normal">$O(1)$</span> لزوماً پابرجا نخواهد بود. هزینه سرشکن‌شده می‌تواند <span class="math_normal">$O(n)$</span> باشد.

**تحلیل تجمعی:**

1.  بیایید هزینه عملیات `MULTIPUSH(S, k)` را برابر <span class="math_normal">$k$</span> در نظر بگیریم (زیرا <span class="math_normal">$k$</span> آیتم را PUSH می‌کند).
2.  تحلیل تجمعی قبلی ما (برای `MULTIPOP`) متکی بر این واقعیت بود که تعداد کل `POP`ها نمی‌تواند از تعداد کل `PUSH`ها بیشتر باشد  و تعداد کل `PUSH`ها توسط <span class="math_normal">$n$</span> (تعداد کل عملیات) محدود می‌شد.
3.  با `MULTIPUSH`، این فرض دوم دیگر برقرار نیست.
4.  **بدترین حالت:** دنباله‌ای از <span class="math_normal">$n$</span> عملیات را در نظر بگیرید که همگی `MULTIPUSH(S, n)` باشند.
      * عملیات اول: `MULTIPUSH(S, n)`. هزینه = <span class="math_normal">$n$</span>.
      * عملیات دوم: `MULTIPUSH(S, n)`. هزینه = <span class="math_normal">$n$</span>.
      * ...
      * عملیات <span class="math_normal">$n$</span>-ام: `MULTIPUSH(S, n)`. هزینه = <span class="math_normal">$n$</span>.
5.  **هزینه کل (<span class="math_normal">$T(n)$</span>):** هزینه کل برای این <span class="math_normal">$n$</span> عملیات <span class="math_normal">$n \times n = n^2$</span> است.
    <span class="math">$$T(n) = O(n^2)$$</span>
6.  **هزینه سرشکن‌شده:**
    <span class="math">$$\text{Amortized Cost} = T(n) / n = O(n^2) / n = O(n)$$</span>
    بنابراین، هزینه سرشکن‌شده <span class="math_normal">$O(1)$</span> نخواهد بود.
    
-----

### تمرین ۲-۱۷.۱ (DECREMENT) 

<div style="border-right: 4px solid #ccc; padding-right: 15px; margin-right: 0; padding-left: 0; text-align: right; direction: rtl;">
    <p><strong>سوال:</strong> نشان دهید که اگر عملیات <code>DECREMENT</code> (کاهش شمارنده) در مثال شمارنده <strong>k</strong>-بیتی گنجانده شود، <strong>n</strong> عملیات می‌تواند تا <strong>Θ(nk)</strong> زمان هزینه داشته باشد.</p>
</div>

**پاسخ:** تحلیل تجمعی <span class="math_normal">$O(1)$</span> برای `INCREMENT` به این واقعیت بستگی داشت که شمارنده از 0 شروع می‌کند  و بیت <span class="math_normal">$A[i]$</span> تنها زمانی فلیپ می‌شود که *همه* بیت‌های <span class="math_normal">$A[0]$</span> تا <p dir = "ltr"><span class="math_normal">$A[i-1]$</span></p> برابر 1 باشند. `DECREMENT` این الگو را می‌شکند.

**اثبات با ارائه دنباله بدترین حالت:**
ما می‌توانیم یک دنباله از <span class="math_normal">$n$</span> عملیات `INCREMENT` و `DECREMENT` بسازیم که هر عملیات <span class="math_normal">$\Theta(k)$</span> هزینه داشته باشد.

1.  **حالت اولیه:** شمارنده را روی حالتی تنظیم کنید که `INCREMENT` بدترین هزینه را دارد. مثلاً <span class="math_normal">$0111...1$</span> (یک 0 و <span class="math_normal">$k-1$</span> تا 1).
2.  **عملیات ۱:** `INCREMENT(A)` را روی <span class="math_normal">$0111...1$</span> اجرا کنید.
      * این عملیات <span class="math_normal">$k-1$</span> بیت 1 را به 0 فلیپ می‌کند و بیت 0 را به 1 فلیپ می‌کند.
      * نتیجه: <span class="math_normal">$1000...0$</span>.
      * هزینه: <span class="math_normal">$\Theta(k)$</span>.
3.  **عملیات ۲:** `DECREMENT(A)` را روی <span class="math_normal">$1000...0$</span> اجرا کنید. (عملیات `DECREMENT` برعکس `INCREMENT` عمل می‌کند: بیت‌ها را از 0 به 1 فلیپ می‌کند تا به 1 برسد و آن را 0 کند).
      * این عملیات <span class="math_normal">$k-1$</span> بیت 0 را به 1 فلیپ می‌کند و بیت 1 را به 0 فلیپ می‌کند.
      * نتیجه: <span class="math_normal">$0111...1$</span>.
      * هزینه: <span class="math_normal">$\Theta(k)$</span>.
4.  **ادامه دنباله:** ما می‌توانیم این دو عملیات (`INCREMENT` و `DECREMENT`) را <span class="math_normal">$n/2$</span> بار تکرار کنیم.

**تحلیل تجمعی:**

  * هر جفت عملیات (یک `INCREMENT` و یک `DECREMENT`) <span class="math_normal">$\Theta(k) + \Theta(k) = \Theta(k)$</span> هزینه دارد.
  * برای <span class="math_normal">$n$</span> عملیات ( <span class="math_normal">$n/2$</span> جفت)، هزینه کل <span class="math_normal">$T(n)$</span> خواهد بود:
    <span class="math">$$T(n) = (n/2) \times \Theta(k) = \Theta(nk)$$</span>
  * بنابراین، هزینه سرشکن‌شده <span class="math_normal">$T(n)/n = \Theta(k)$</span> است، نه <span class="math_normal">$O(1)$</span>.

-----

### تمرین ۳-۱۷.۱ (هزینه $i$ اگر $i$ توان ۲ باشد) 

<div style="border-right: 4px solid #ccc; padding-right: 15px; margin-right: 0; padding-left: 0; text-align: right; direction: rtl;">
    <p><strong>سوال:</strong> فرض کنید <strong>n</strong> عملیات روی یک ساختمان داده انجام می‌دهیم که هزینه عملیات <strong>i</strong>-ام برابر <strong>i</strong> است اگر <strong>i</strong> توان دقیقی از 2 باشد، و در غیر این صورت 1 است. از تحلیل تجمعی برای تعیین هزینه سرشکن‌شده هر عملیات استفاده کنید.</p>
</div>

**پاسخ:** هزینه سرشکن‌شده هر عملیات $O(1)$ است.

**تحلیل تجمعی:**

1.  ما باید هزینه کل <span class="math_normal">$T(n)$</span> برای <span class="math_normal">$n$</span> عملیات را محاسبه کنیم.
    <span class="math">$$T(n) = \sum_{i=1}^{n} c_i$$</span>

2.  هزینه <span class="math_normal">$c_i$</span> به صورت زیر تعریف شده است:
    <span class="math">$$c_i = \begin{cases} i & \text{if } i \text{ is a power of 2} \\ 1 & \text{otherwise} \end{cases}$$</span>
3.  می‌توانیم <span class="math_normal">$T(n)$</span> را به دو بخش تفکیک کنیم: عملیات‌هایی که توان 2 نیستند و عملیات‌هایی که توان 2 هستند.
    <span class="math">$$T(n) = \sum_{i \text{ not power of 2}}^{n} 1 + \sum_{i \text{ is power of 2}}^{n} i$$</span>
4.  **بخش اول (هزینه‌های 1):** تعداد کل عملیات <span class="math_normal">$n$</span> است. تعداد عملیات‌هایی که توان 2 هستند برابر <span class="math_normal">$\lfloor \lg n \rfloor + 1$</span> است. بنابراین، تعداد عملیات‌هایی که هزینه 1 دارند، <span class="math_normal">$n - (\lfloor \lg n \rfloor + 1)$</span> است. هزینه این بخش دقیقاً <span class="math_normal">$n - (\lfloor \lg n \rfloor + 1)$</span> است که قطعاً <span class="math_normal">$ < n$</span> و <span class="math_normal">$O(n)$</span> است.
5.  **بخش دوم (هزینه‌های <span class="math_normal">$i$</span>):** ما باید مجموع توان‌های 2 تا <span class="math_normal">$n$</span> را محاسبه کنیم.
    <span class="math">$$\sum_{i \text{ is power of 2}}^{n} i = \sum_{k=0}^{\lfloor \lg n \rfloor} 2^k$$</span>
6.  این یک سری هندسی است. ما می‌دانیم که <span class="math_normal">$\sum_{k=0}^{m} 2^k = 2^{m+1} - 1$</span>.
    با جایگذاری <span class="math_normal">$m = \lfloor \lg n \rfloor$</span>، داریم:
    <span class="math">$$\sum_{k=0}^{\lfloor \lg n \rfloor} 2^k = 2^{\lfloor \lg n \rfloor + 1} - 1$$</span>
7.  ما می‌دانیم که <span class="math_normal">$\lfloor \lg n \rfloor \le \lg n$</span>.
    بنابراین <span class="math_normal">$2^{\lfloor \lg n \rfloor} \le 2^{\lg n} = n$</span>.
    در نتیجه <span class="math_normal">$2^{\lfloor \lg n \rfloor + 1} = 2 \cdot 2^{\lfloor \lg n \rfloor} \le 2n$</span>.
    پس، مجموع بخش دوم <span class="math_normal">$ \le 2n - 1$</span> و <span class="math_normal">$O(n)$</span> است.
8.  **هزینه کل (<span class="math_normal">$T(n)$</span>):**
    <span class="math">$$T(n) = (\text{Cost of non-powers of 2}) + (\text{Cost of powers of 2})$$</span>
    <span class="math">$$T(n) < n + (2n - 1) = 3n - 1$$</span>
    بنابراین، <span class="math_normal">$T(n) = O(n)$</span>.
9.  **هزینه سرشکن‌شده:**
    <span class="math">$$\text{Amortized Cost} = T(n) / n = O(n) / n = O(1)$$</span>

<!-- end list -->

</div>
