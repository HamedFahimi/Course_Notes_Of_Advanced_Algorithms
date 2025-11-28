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
    <p style="font-size: 25px;"><strong>استراتژی تحول و غلبه: کاهش مسئله (Problem Reduction)</strong></p>
    <p style="font-size: 20px;"><strong>دکتر حامد فهیمی</strong></p>
  </div>

  <div class="logo-block">
    <img src="MathmaticaFacultyLogo.jpg" alt="لوگوی دانشکده علوم ریاضی" class="logo-img">
    <div><p><strong>دانشکده علوم ریاضی</strong></p></div>
  </div>

</div>

<br>

مبحث کاهش مسئله یک استراتژی قدرتمند در طراحی الگوریتم‌ها و بخشی از رویکرد کلی **تحول و غلبه (Transform-and-Conquer)** است.

---

### ۱. تعریف و مفهوم کاهش مسئله

**کاهش مسئله (Problem Reduction)** یک استراتژی حل مسئله است که در آن، اگر نیاز به حل **مسئله ۱** باشد، آن را به **مسئله ۲** که روش حل آن مشخص است، **کاهش** می‌دهیم.


به بیان ساده، شما یک مسئله‌ی داده شده را به نمونه‌ای از یک مسئله‌ی دیگر تبدیل می‌کنید که می‌توان آن را با یک الگوریتم از پیش **شناخته شده** حل کرد.

* **اهمیت عملی:** یک الگوریتم مبتنی بر کاهش، زمانی ارزش عملی دارد که اجرای آن (شامل کاهش مسئله ۱ به مسئله ۲ و سپس حل مسئله ۲) **کارآمدتر** از حل مستقیم مسئله ۱ باشد.
* **اهمیت نظری:** این استراتژی در علوم کامپیوتر نظری نقش اساسی دارد و برای **دسته‌بندی مسائل بر اساس پیچیدگی** (که در نظریه NP-Complete مطرح می‌شود) استفاده می‌شود.

---

### ۲. مثال‌های کاربردی کاهش مسئله

این استراتژی در بسیاری از الگوریتم‌ها و حوزه‌های علوم کامپیوتر کاربرد دارد:

#### الف) محاسبه کمترین مضرب مشترک ($\text{lcm}$)

* **مسئله اصلی:** محاسبه **کمترین مضرب مشترک (Least Common Multiple)** دو عدد صحیح مثبت $m$ و $n$، یعنی $\text{lcm}(m, n)$.
* **روش کاهش:** به جای استفاده از روش‌های ناکارآمد مبتنی بر فاکتورگیری اول، این مسئله را به مسئله محاسبه **بزرگترین مقسوم‌علیه مشترک (Greatest Common Divisor - $\text{gcd}$)** کاهش می‌دهیم. الگوریتم اقلیدس یک روش بسیار کارآمد برای محاسبه $\text{gcd}(m, n)$ است.
* **فرمول کاهش:**
    $$\text{lcm}(m, n) = \frac{m \cdot n}{\text{gcd}(m, n)}$$
* **مثال:** $\text{lcm}(24, 60)$: ابتدا $\text{gcd}(24, 60) = 12$ را محاسبه می‌کنیم. سپس $\text{lcm}(24, 60) = \frac{24 \cdot 60}{12} = \frac{1440}{12} = 120$.
* **کارایی:** از آنجا که الگوریتم اقلیدس برای $\text{gcd}$ دارای کارایی زمانی $O(\log n)$ است، کارایی الگوریتم $\text{lcm}$ مبتنی بر این کاهش نیز در همین کلاس خواهد بود.

---

#### ب) شمارش مسیرها در یک گراف

* **مسئله اصلی:** شمارش تعداد مسیرهای با طول <span class="math_normal">$k$</span> بین دو رأس (vertex) در یک گراف (جهت‌دار یا بدون جهت).
* **روش کاهش:** این مسئله به محاسبه توان مناسبی از **ماتریس مجاورت (Adjacency Matrix)** گراف کاهش می‌یابد.
* **قاعده کاهش:** تعداد مسیرهای مختلف با طول <span class="math_normal">$k>0$</span> از رأس <span class="math_normal">$i$</span>-ام به رأس <span class="math_normal">$j$</span>-ام، برابر است با **عنصر <span class="math_normal">$(i, j)$</span>-ام ماتریس <span class="math_normal">$A^k$</span>**، که در آن <span class="math_normal">$A$</span> ماتریس مجاورت گراف است.
* **الگوریتم:** می‌توان از الگوریتم‌های توان‌رسانی دودویی که برای اعداد استفاده می‌شود، برای محاسبه <span class="math_normal">$A^k$</span> نیز استفاده کرد.

مثال خاص: شمارش مسیرها با ماتریس مجاورت

به عنوان یک مثال مشخص، **گراف شکل** را در نظر بگیرید.**ماتریس مجاورت** آن (<span class="math_normal">$A$</span>) و **مربع آن** (<span class="math_normal">$A^2$</span>)، به ترتیب، تعداد مسیرهای به **طول ۱** و **طول ۲** را بین رئوس متناظر گراف نشان می‌دهند.
به طور خاص، **سه مسیر** به طول ۲ وجود دارد که از رأس <span class="math_normal">$a$</span> شروع شده و به رأس <span class="math_normal">$a$</span> ختم می‌شوند: (<span class="math_normal">$a-b-a$</span>, <span class="math_normal">$a-c-a$</span>, و <span class="math_normal">$a-d-a$</span>)؛اما تنها **یک مسیر** به طول ۲ از <span class="math_normal">$a$</span> به <span class="math_normal">$c$</span> وجود دارد که عبارت است از: (<span class="math_normal">$a-d-c$</span>).

<div style="text-align: center;">
    <img src="graph.png" alt="شمارش مسیرها در یک گراف" style="display: block; margin: 0 auto;">
</div>

---

#### ج) کاهش مسائل بهینه‌سازی (Optimization Problems)

مسائل بهینه‌سازی می‌توانند به دو دسته اصلی تقسیم شوند: **ماکزیمم‌سازی** و **مینیمم‌سازی**. این دو مسئله به راحتی به یکدیگر قابل کاهش هستند.

* **کاهش مینیمم‌سازی به ماکزیمم‌سازی:**
    $$\min f(x) = - \max [-f(x)]$$
    * **توضیح:** برای یافتن کمترین مقدار یک تابع ($f(x)$)، می‌توان ابتدا بیشترین مقدار منفی آن ($\max [-f(x)]$) را پیدا کرد و سپس علامت نتیجه را تغییر داد.
* **کاهش ماکزیمم‌سازی به مینیمم‌سازی:**
    $$\max f(x) = - \min [-f(x)]$$

]

**توجه (کاهش در حساب دیفرانسیل):** رویه استاندارد حساب دیفرانسیل برای یافتن نقاط اکسترمم یک تابع ($f(x)$) نیز بر مبنای کاهش مسئله استوار است؛ به این صورت که مسئله بهینه‌سازی به **حل معادله‌ی $f'(x) = 0$** (یافتن نقاط بحرانی) کاهش می‌یابد.


<div style="text-align: center;">
    <img src="minmax.png" alt="Optimization Problems" style="display: block; margin: 0 auto;">
</div>

---

## (مطالعه برنامه ریزی خطی آزاد است.)
#### د) برنامه‌ریزی خطی (Linear Programming) 

* **تعریف:** مسئله‌ای که در آن به دنبال بهینه‌سازی (ماکزیمم یا مینیمم کردن) یک **تابع خطی** از چند متغیر، تحت محدودیت‌هایی به شکل **معادلات خطی** و **نامعادلات خطی** هستیم.
* **اهمیت کاهش:** بسیاری از مسائل تصمیم‌گیری بهینه (مانند زمانبندی خدمه، شبکه‌های حمل و نقل و برنامه‌ریزی تولید) می‌توانند به یک نمونه از مسئله برنامه‌ریزی خطی کاهش داده شوند.
* **فرم کلی مسئله:**
    * ماکزیمم (یا مینیمم) کردن <span class="math_normal">$\sum_{j=1}^{n} c_{j}x_{j}$</span>
    * تحت محدودیت‌های: <span class="math_normal">$a_{i1}x_{1}+\dots+a_{in}x_{n}\le(\text{یا } \ge \text{ یا } =)b_{i}$</span> برای <span class="math_normal">$i=1,\dots,m$</span>
    * و محدودیت‌های عدم منفی بودن: <span class="math_normal">$x_{1}\ge0,\dots,x_{n}\ge0$</span>.

**کاهش مسئله کوله‌پشتی (Knapsack Problem) به برنامه‌ریزی خطی:**

* **مسئله کوله‌پشتی پیوسته (Continuous Knapsack Problem):** این مسئله به یک برنامه‌ریزی خطی استاندارد تبدیل می‌شود.
    * **هدف:** ماکزیمم کردن <span class="math_normal">$\sum_{j=1}^{n} v_{j}x_{j}$</span> (کل ارزش)
    * **محدودیت‌ها:** <span class="math_normal">$\sum_{j=1}^{n} w_{j}x_{j}\le W$</span> (کل وزن کمتر از ظرفیت <span class="math_normal">$W$</span>) و <span class="math_normal">$0\le x_{j}\le1$</span> (<span class="math_normal">$x_j$</span> کسر گرفته شده از شیء <span class="math_normal">$j$</span> است).

* **مسئله کوله‌پشتی صفر-یک (0-1 Knapsack Problem):** این مسئله به یک **برنامه‌ریزی خطی عدد صحیح (Integer Linear Programming)** تبدیل می‌شود.
    * **هدف:** ماکزیمم کردن <span class="math_normal">$\sum_{j=1}^{n} v_{j}x_{j}$</span>
    * **محدودیت‌ها:** <span class="math_normal">$\sum_{j=1}^{n} w_{j}x_{j}\le W$</span> و <span class="math_normal">$x_{j}\in\{0,1\}$</span> (<span class="math_normal">$x_j$</span> یا شیء را می‌گیریم (۱) یا نمی‌گیریم (۰)).
    * **پیچیدگی:** این تغییر به ظاهر کوچک، پیچیدگی مسئله را به شدت افزایش می‌دهد و یافتن الگوریتم زمان چندجمله‌ای برای حل یک نمونه دلخواه از برنامه‌ریزی خطی عدد صحیح، هنوز یک مسئله باز است.

---

#### ه) کاهش به مسائل گراف (State-Space Graphs)

بسیاری از معماها و بازی‌ها با استفاده از کاهش به مسائل گراف حل می‌شوند.

* **گراف فضای حالت (State-Space Graph):** در این نوع کاهش:
    * **رأس‌ها (Vertices):** نمایانگر حالت‌های (وضعیت‌های) ممکن مسئله هستند.
    * **یال‌ها (Edges):** نمایانگر انتقال‌های مجاز بین حالت‌ها هستند.
    * **حل مسئله:** تبدیل می‌شود به یافتن یک **مسیر (Path)** از رأس حالت اولیه (Initial State) به رأس حالت هدف (Goal State).

**مثال: معمای دهقان، گرگ، بز و کلم (The River-Crossing Puzzle)**

* **مسئله:** دهقانی باید یک گرگ، یک بز و یک کلم را به آن طرف رودخانه ببرد. قایق فقط ظرفیت دهقان و یک شیء دیگر را دارد. در غیاب دهقان، گرگ بز را می‌خورد و بز کلم را. راه حلی پیدا کنید.
* **کاهش:** با رسم گراف فضای حالت (مانند شکل) که رأس‌های آن وضعیت‌های ایمن (مانند `Pwgc||` یا `||Pwgc`) و یال‌های آن حرکت‌های مجاز هستند، مسئله به **یافتن مسیر** از حالت اولیه (`Pwgc||`) به حالت هدف (`||Pwgc`) کاهش می‌یابد.
* **راه حل:** در این گراف، دو مسیر ساده مجزا با طول حداقل (۷ عبور از رودخانه) وجود دارد.

<div style="text-align: center;">
    <img src="PWGC.png" alt="معمای دهقان، گرگ، بز، کلم" style="display: block; margin: 0 auto;">
</div>

---

### ۳. تمرین‌های حل شده

#### تمرین ۱: اثبات رابطه <span class="math_normal">$\text{lcm}$</span> و <span class="math_normal">$\text{gcd}$</span>

**سؤال:** تساوی <span class="math_normal">$\text{lcm}(m, n) = \frac{m \cdot n}{\text{gcd}(m, n)}$</span> را که زیربنای الگوریتم <span class="math_normal">$\text{lcm}(m, n)$</span> است، اثبات کنید.

**حل:**

از تجزیه اعداد به عوامل اول استفاده می‌کنیم. فرض کنید تجزیه اول <span class="math_normal">$m$</span> و <span class="math_normal">$n$</span> به صورت زیر باشد:
<span class="math">$$m = p_1^{\alpha_1} p_2^{\alpha_2} \dots p_k^{\alpha_k}$$</span>
<span class="math">$$n = p_1^{\beta_1} p_2^{\beta_2} \dots p_k^{\beta_k}$$</span>
که در آن <span class="math_normal">$p_i$</span> تمام عوامل اول مشترک یا منحصر به فرد <span class="math_normal">$m$</span> و <span class="math_normal">$n$</span> هستند و <span class="math_normal">$\alpha_i, \beta_i \ge 0$</span>.

فرمول‌های <span class="math_normal">$\text{gcd}$</span> و <span class="math_normal">$\text{lcm}$</span> با استفاده از توان‌های عوامل اول به صورت زیر تعریف می‌شوند:
<span class="math">$$\text{gcd}(m, n) = p_1^{\min(\alpha_1, \beta_1)} p_2^{\min(\alpha_2, \beta_2)} \dots p_k^{\min(\alpha_k, \beta_k)}$$</span>
<span class="math">$$\text{lcm}(m, n) = p_1^{\max(\alpha_1, \beta_1)} p_2^{\max(\alpha_2, \beta_2)} \dots p_k^{\max(\alpha_k, \beta_k)}$$</span>

اکنون حاصل ضرب <span class="math_normal">$\text{gcd}(m, n) \cdot \text{lcm}(m, n)$</span> را محاسبه می‌کنیم:
<span class="math">$$\text{gcd}(m, n) \cdot \text{lcm}(m, n) = p_1^{\min(\alpha_1, \beta_1) + \max(\alpha_1, \beta_1)} \dots p_k^{\min(\alpha_k, \beta_k) + \max(\alpha_k, \beta_k)}$$</span>

ما می‌دانیم که برای هر دو عدد دلخواه <span class="math_normal">$a$</span> و <span class="math_normal">$b$</span>:
<span class="math">$$\min(a, b) + \max(a, b) = a + b$$</span>

بنابراین، توان هر عامل اول <span class="math_normal">$p_i$</span> در حاصل ضرب، برابر با مجموع توان‌های آن عامل در <span class="math_normal">$m$</span> و <span class="math_normal">$n$</span> خواهد بود (<span class="math_normal">$\alpha_i + \beta_i$</span>):
<span class="math">$$\text{gcd}(m, n) \cdot \text{lcm}(m, n) = p_1^{\alpha_1 + \beta_1} \dots p_k^{\alpha_k + \beta_k}$$</span>
<span class="math">$$\text{gcd}(m, n) \cdot \text{lcm}(m, n) = (p_1^{\alpha_1} \dots p_k^{\alpha_k}) \cdot (p_1^{\beta_1} \dots p_k^{\beta_k})$$</span>
<span class="math">$$\text{gcd}(m, n) \cdot \text{lcm}(m, n) = m \cdot n$$</span>

با تقسیم طرفین بر <span class="math_normal">$\text{gcd}(m, n)$</span>، تساوی اثبات می‌شود:
<span class="math">$$\text{lcm}(m, n) = \frac{m \cdot n}{\text{gcd}(m, n)}$$</span>

---

#### تمرین ۲: پیاده‌سازی پشته با استفاده از صف

**سؤال:** پشته (Stack) از اصل **آخرین ورودی، اولین خروجی (LIFO)** پیروی می‌کند. صف (Queue) از اصل **اولین ورودی، اولین خروجی (FIFO)** پیروی می‌کند. چگونه می‌توانید عملیات‌های `Push` (اضافه کردن) و `Pop` (حذف کردن) یک پشته را با استفاده از عملیات‌های `Insert` (یا Enqueue) و `Delete` (یا Dequeue) یک صف پیاده‌سازی کنید؟

**حل (کاهش عملیات پشته به عملیات صف):**

برای پیاده‌سازی یک پشته با استفاده از دو صف (<span class="math_normal">$Q_1$</span> و <span class="math_normal">$Q_2$</span>)، می‌توان عملیات `Push` را کارآمد (<span class="math_normal">$O(1)$</span>) و عملیات `Pop` را ناکارآمد (<span class="math_normal">$O(N)$</span>) طراحی کرد.

**عملیات Push (اضافه کردن به پشته):**
هدف این است که عنصر جدید، اولین عنصری باشد که در عملیات `Pop` بعدی حذف می‌شود (LIFO).

1.  عنصر جدید (<span class="math_normal">$x$</span>) را به صف اصلی (<span class="math_normal">$Q_1$</span>) اضافه کنید.
    * **تابع:** `Insert(Q1, x)`
    * **پیچیدگی:** <span class="math_normal">$O(1)$</span>

**عملیات Pop (حذف از پشته):**
هدف این است که آخرین عنصر اضافه‌شده به پشته (که اکنون در انتهای صف <span class="math_normal">$Q_1$</span> است) حذف شود.

1.  تمام عناصر صف <span class="math_normal">$Q_1$</span>، به جز آخرین عنصر، را به صف کمکی (<span class="math_normal">$Q_2$</span>) منتقل کنید.
    * تا زمانی که اندازه <span class="math_normal">$Q_1$</span> بزرگتر از ۱ است:
        * <span class="math_normal">$y = \text{Delete}(Q_1)$</span>
        * <span class="math_normal">$\text{Insert}(Q_2, y)$</span>
2.  عنصری که در <span class="math_normal">$Q_1$</span> باقی مانده (که آخرین عنصر اضافه‌شده به پشته است)، همان عنصر مورد نیاز برای `Pop` است. آن را حذف کرده و برگردانید.
    * <span class="math_normal">$x = \text{Delete}(Q_1)$</span>
3.  نقش صف‌ها را جابجا کنید. (نام <span class="math_normal">$Q_1$</span> و <span class="math_normal">$Q_2$</span> را عوض کنید) تا <span class="math_normal">$Q_1$</span> دوباره صف اصلی باشد.

**پیچیدگی:** عملیات `Push` در زمان ثابت (<span class="math_normal">$O(1)$</span>) و عملیات `Pop` در زمان خطی (<span class="math_normal">$O(N)$</span>) انجام می‌شود، که <span class="math_normal">$N$</span> تعداد عناصر موجود در پشته است. این یک نمونه از کاهش مسئله با تریدآف در کارایی عملیات‌ها است.

</div>