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
    <p style="font-size: 25px;"><strong>جستجوی کامل (Exhaustive Search)</strong></p>
    <p style="font-size: 20px;"><strong>دکتر حامد فهیمی</strong></p>
  </div>

  <div class="logo-block">
    <img src="MathmaticaFacultyLogo.jpg" alt="لوگوی دانشکده علوم ریاضی" class="logo-img">
    <div><p><strong>دانشکده علوم ریاضی</strong></p></div>
  </div>

</div>

### روش‌های Brute-Force

---

### ۱. مقدمه: جستجوی کامل چیست؟

بسیاری از مسائل مهم در علوم کامپیوتر نیازمند یافتن یک عنصر با ویژگی‌های خاص در دامنه‌ای هستند که اندازه آن با رشد ورودی به صورت **نمایی (Exponential)** رشد می‌کند. این مسائل معمولاً شامل اشیاء **ترکیبیاتی (Combinatorial)** مانند جایگشت‌ها (Permutations)، ترکیب‌ها (Combinations) و زیرمجموعه‌ها (Subsets) هستند.

**تعریف:** جستجوی کامل (Exhaustive Search) در واقع همان رویکرد Brute-force برای مسائل ترکیبیاتی است. این روش پیشنهاد می‌کند که:
1.  تک‌تک عناصر دامنه مسئله (فضای حالت) تولید شوند.
2.  عناصری که قیود مسئله را ارضا می‌کنند انتخاب شوند.
3.  عنصر مطلوب (مثلاً عنصری که تابع هدف را ماکزیمم یا مینیمم می‌کند) پیدا شود.

اگرچه ایده این روش ساده است، اما پیاده‌سازی آن نیازمند الگوریتمی برای تولید اشیاء ترکیبیاتی (مانند تولید تمام جایگشت‌ها) است.

---

### ۲. بررسی مسائل کلاسیک

در این بخش سه مسئله معروف را که با روش جستجوی کامل قابل حل هستند، بررسی می‌کنیم.

#### الف) مسئله فروشنده دوره‌گرد (Traveling Salesman Problem - TSP)
**صورت مسئله:** یافتن کوتاه‌ترین توری که از مجموعه‌ای از <span class="math_normal">$n$</span> شهر عبور کند، به طوری که هر شهر دقیقاً یک بار بازدید شود و در نهایت به شهر مبدأ بازگردد.
* **مدل‌سازی:** این مسئله با یک گراف وزن‌دار مدل می‌شود و هدف یافتن کوتاه‌ترین **دور همیلتونی (Hamiltonian circuit)** است.

**الگوریتم جستجوی کامل:**
از آنجا که هر دور یک جایگشت از شهرهاست و جهت دور یا نقطه شروع تأثیری در طول دور ندارد، می‌توانیم:
1.  یک شهر را ثابت در نظر بگیریم.
2.  تمام جایگشت‌های <span class="math_normal">$n-1$</span> شهر باقی‌مانده را تولید کنیم.
3.  طول تور را برای هر جایگشت محاسبه کرده و کمترین را انتخاب کنیم.

**تحلیل پیچیدگی:**
تعداد تورهایی که باید بررسی شوند برابر است با <span class="math_normal">$\frac{1}{2}(n-1)!$</span>. این تعداد حتی برای مقادیر کوچک <span class="math_normal">$n$</span> بسیار بزرگ است و الگوریتم را در عمل غیرکاربردی می‌کند.

#### ب) مسئله کوله‌پشتی (Knapsack Problem)
**صورت مسئله:** <span class="math_normal">$n$</span> کالا با وزن‌های <span class="math_normal">$w_1, ..., w_n$</span> و ارزش‌های <span class="math_normal">$v_1, ..., v_n$</span> داریم. یک کوله‌پشتی با ظرفیت <span class="math_normal">$W$</span> موجود است. هدف انتخاب زیرمجموعه‌ای از کالاهاست که در کوله جا شوند و بیشترین ارزش ممکن را داشته باشند.

**الگوریتم جستجوی کامل:**
1.  تولید تمام **زیرمجموعه‌های** ممکن از <span class="math_normal">$n$</span> کالا.
2.  برای هر زیرمجموعه، محاسبه وزن کل و بررسی اینکه آیا از <span class="math_normal">$W$</span> کمتر است یا خیر (Feasibility).
3.  انتخاب زیرمجموعه‌ای که بیشترین ارزش را در میان زیرمجموعه‌های مجاز دارد.

**تحلیل پیچیدگی:**
تعداد زیرمجموعه‌های یک مجموعه <span class="math_normal">$n$</span> عضوی برابر با <span class="math_normal">$2^n$</span> است. بنابراین پیچیدگی این روش <span class="math_normal">$\Omega(2^n)$</span> خواهد بود.
* **نکته:** هر دو مسئله TSP و کوله‌پشتی جزو مسائل **NP-hard** هستند و الگوریتم چندجمله‌ای شناخته‌شده‌ای برای حل دقیق آن‌ها وجود ندارد.

#### ج) مسئله تخصیص (Assignment Problem)
**صورت مسئله:** <span class="math_normal">$n$</span> نفر و <span class="math_normal">$n$</span> شغل داریم. هزینه تخصیص نفر <span class="math_normal">$i$</span> به شغل <span class="math_normal">$j$</span> برابر با <span class="math_normal">$C[i, j]$</span> است. می‌خواهیم یک تخصیص یک‌به‌یک (هر نفر دقیقاً یک شغل) انجام دهیم تا هزینه کل مینیمم شود.

**چرا روش حریصانه کار نمی‌کند؟**
نمی‌توانیم صرفاً کوچکترین عدد هر سطر را انتخاب کنیم، زیرا ممکن است دو نفر کاندیدای یک شغل باشند.

**الگوریتم جستجوی کامل:**
هر تخصیص مجاز متناظر با یک جایگشت از اعداد <span class="math_normal">$1$</span> تا <span class="math_normal">$n$</span> است (تخصیص نفر <span class="math_normal">$i$</span> به شغل <span class="math_normal">$j_i$</span>).
1.  تولید تمام جایگشت‌های ستون‌ها (<span class="math_normal">$n!$</span>).
2.  محاسبه هزینه برای هر جایگشت.
3.  انتخاب کمترین هزینه.

**نکته مهم:** برخلاف TSP و کوله‌پشتی، برای مسئله تخصیص الگوریتم کارآمدی به نام **روش مجاری (Hungarian Method)** وجود دارد، بنابراین استفاده از جستجوی کامل برای این مسئله توجیهی ندارد.

---

### ۳. حل تمرین‌های منتخب

#### تمرین ۱ (صفحه ۱۴۶): تحلیل کارایی مسئله کوله‌پشتی
**سوال:**
الف) با فرض اینکه تولید هر زیرمجموعه و بررسی وزن آن زمان ثابتی ببرد، مرتبه کارایی الگوریتم جستجوی کامل چقدر است؟
ب) اگر کامپیوتر بتواند ۱۰ میلیارد (<span class="math_normal">$10^{10}$</span>) محاسبات در ثانیه انجام دهد، ماکزیمم تعداد کالا (<span class="math_normal">$n$</span>) که می‌توان در ۱ ساعت حل کرد چقدر است؟

**پاسخ:**
**الف)** تعداد کل زیرمجموعه‌ها برای <span class="math_normal">$n$</span> کالا برابر با <span class="math_normal">$2^n$</span> است. بنابراین کلاس کارایی الگوریتم برابر است با:
<span class="math">$$O(2^n)$$</span>

**ب)**
* تعداد عملیات در یک ساعت:
    <span class="math">$$\text{Ops} = 3600 \times 10^{10} = 3.6 \times 10^{13}$$</span>
* ما باید <span class="math_normal">$n$</span> را چنان پیدا کنیم که <span class="math_normal">$2^n \approx 3.6 \times 10^{13}$</span>.
* با گرفتن لگاریتم در مبنای ۲:
    <span class="math">$$n \approx \log_2(3.6 \times 10^{13})$$</span>
    <span class="math">$$n \approx \log_2(3.6) + 13 \times \log_2(10)$$</span>
    <span class="math">$$n \approx 1.85 + 13(3.32) \approx 1.85 + 43.16 \approx 45$$</span>
**نتیجه:** با این ابرکامپیوتر تنها می‌توان مسئله‌ای با حدود **۴۵ کالا** را در یک ساعت حل کرد. این نشان‌دهنده محدودیت شدید الگوریتم‌های نمایی است.

#### تمرین ۹ (صفحه ۱۴۷): مسئله هشت وزیر (8-Queens)
**سوال:** در مسئله قرار دادن ۸ وزیر در صفحه شطرنج <span class="math_normal">$8 \times 8$</span>، اندازه فضای جستجو در حالات زیر چقدر است؟
الف) هیچ دو وزیری در یک خانه نباشند.
ب) هیچ دو وزیری در یک سطر نباشند.
ج) هیچ دو وزیری در یک سطر یا ستون نباشند.

**پاسخ:**
این تمرین نشان می‌دهد چطور فرمول‌بندی مسئله می‌تواند اندازه فضای جستجو را تغییر دهد.

**الف) هیچ دو وزیری در یک خانه نباشند:**
ما باید ۸ خانه را از ۶۴ خانه انتخاب کنیم.
<span class="math">$$\binom{64}{8} = \frac{64!}{8!56!} \approx 4.4 \times 10^9$$</span>
تعداد حالات حدود ۴.۴ میلیارد است.

**ب) هیچ دو وزیری در یک سطر نباشند:**
در این حالت فرض می‌کنیم در هر سطر دقیقاً یک وزیر قرار می‌دهیم. وزیر سطر اول ۸ انتخاب دارد، سطر دوم ۸ انتخاب و ... .
<span class="math">$$8^8 \approx 16.7 \times 10^6$$</span>
تعداد حالات حدود ۱۶ میلیون است. می‌بینید که با یک قید ساده، فضای جستجو بسیار کوچکتر شد.

**ج) هیچ دو وزیری در یک سطر یا ستون نباشند:**
در این حالت مسئله تبدیل به یافتن یک جایگشت از ستون‌ها می‌شود (مانند مسئله تخصیص). وزیر سطر اول ۸ انتخاب، وزیر سطر دوم ۷ انتخاب و ... .
<span class="math">$$8! = 40,320$$</span>
تعداد حالات تنها ۴۰ هزار است. جستجوی کامل در این فضا بسیار سریع‌تر از حالت اول است.

</div>