<div dir="rtl">

# بخش ۳ - مفاهیم طراحی
یک سیستم نرم‌افزاری خوب با نوشتن کدهای تمیز شروع می‌شوند. بنابراین معماری خوب بدون کد تمیز محقق نمی‌شود. بنابراین در این فصل مفاهیم بسیار مهمی در مورد چگونگی ارتباط  داده‌ها و توابع(کلاس‌ها) با هم مطرح می‌شود که به اختصار SOLID گفته می‌شود. هدف مفاهیم SOLID ایجاد ساختارهای نرم‌افزاری mid-level است تا:
  - تغییرات را تحمل کند
  - فهم آن‌ها آسان باشد
  - اساس کامپوننت‌هایی هستند که بسیاری از سیستم‌های نرم‌افزاری استفاده می‌شوند</br>
  
مفاهیم SOLID در سال ۲۰۰۴ توسط آقای Feahters بوجود آمد
  
## فصل ۷ - مفهوم تک مسئولیتی (The Single Responsibility)
  اسم این مفهوم غلط انداز است و بسیاری از برنامه نویس‌ها فکر می‌کنند که یعنی هر تابع یا کامپوننت فقط باید یک وظیفه داشته باشد که این برداشت اشتباه است. درواقع این مفهوم می‌گوید که یک و تنها یک دلیل برای تغییر یک ماژول باید وجود داشته باشد و آن تنها راضی کردن مشتریان و ذینفعان است. 
نکته‌ی دیگری که این مفهوم به آن اشاره می‌کند آن است که کدی که به بازیگران متفاوتی وابسته است باید جدا شوند. به عنوان مثال در یک برنامه دو تابع به اسم calculatePay و reportHours وجود دارند. این دو تابع یک تابع دیگر به نام regularHours را صدا می‌زنند. تابع calculatePay مربوط به یک بازیگر مانند CFO شرکت و reportHours مربوط به COO است. در صورتی که توسعه دهنده بخواهد تابع regularHours را متناسب با خواسته‌ی بازیگر CFO تغییر دهد آنگاه این تغییر برروی reportHours نیز تاثیر می‌گذارد و اطلاعاتی که بازیگر COO باید ببیند اشتباه می‌شود
  مثال دیگری که در آن جداسازی رعایت نشده است مربوط به ادغام کدها می‌شود. فرض کنید یک توسعه دهنده برروی تابع calculatePay کار می‌کند و آن را تغییر می‌دهد. توسعه دهنده‌ی دیگر نیز به صورت همزمان برروی reportHours. هنگامی که این کدها برای deploy آماده می‌شوند آنگاه به مشکل ادغام می‌خورند. خود ادغام مشکلی ندارد ولی به هرحال ریسکی است و ممکن است در اثر ناهماهنگی میان توسعه دهندگان کدهای یکی از آن‌ها حذف شود و تاثیر بدی برروی سیستم بگذارد
 
  راه حلی که برای حل این دو مشکل در انتهای این فصل ارائه شد آن است که توابع در دو کلاس جدا پیاده سازی شوند.

## فصل ۸ - مفهوم باز-بسته (The Open-Closed)

> نرم‌افزارها باید برای گسترش باز باشند و برای تغییرات بسته

این جمله‌ای بود که آقای Meyer ابداع کننده این مفهوم در سال ۱۹۸۸ گفتند</br>
منظور ایشون آن بود که نرم‌افزار برای گسترش و اضافه کردن ویژگی باید تغییر کند آن هم تنها قسمت‌های مورد نیاز نه تمام آن. دلیل اصلی معماری نرم‌افزار نیز همین موردی است آقای Meyer گفت.
در طراحی یک سیستم، ماژول‌هایی که قوانین کسب و کار در آن‌ها پیاده سازی می‌شود باید ایزوله باشند و وابسته به ماژول‌ها نباشند. بلکه سایر ماژول‌ها به آن‌ها باید وابسته باشند زیرا تمام حرفه در آن‌ها است و حیاتی‌ترین قسمت سیستم هستند. درواقع 
در طراحی سیستم می‌توان ماژول‌هایی که وظایف مشخص دارند را در یک مجموعه‌ای به نام کامپوننت در نظر گرفت مانند تصویر زیر. به عنوان مثال ماژول‌های کسب و کار که به آن‌ها اشاره شد را می‌توان یک کامپوننت به نام interactor در نظر گرفت مانند تصویر زیر. ماژول‌هایی که مربوط به پایگاه داده هستند را کامپوننت database
نکته‌ای که در تصویر زیر قابل مشاهده است آن است که اگر تغییری در قسمت view نیاز باشد یعنی جایی که کاربر با آن در ارتباط است، دیگر نیازی به ایجاد تغییر در سایر ماژول‌ها نیست و فقط همان کامپوننت Screen و view تغییر می‌کنند و deploy می‌شوند و بدین طریق سلسله مراتب تغییر اجزا نیز مشخص است

![open_close_image]

> به طور کلی هدف مفهوم باز-بسته آن است که سیستمی برای گسترش راحت، بدون تحمیل تاثیر زیاد تغییر ایجاد کند و این هدف را با تقسیم بندی سیستم به کامپوننت‌ها و مرتب کردن آن‌ها در یک سلسله مراتب وابستگی به گونه‌ای که کامپوننت‌های سطح بالا مانند interactor در برابر تغییرات در کامپوننت‌های سطح پایین مانند screen محافظت شوند، محقق می‌کند.


# فصل ۹ - مفهوم تعویض Liskov (The Liskov Substitution)
این مفهوم می‌گوید که تا حد امکان سیستم به گونه‌ای طراحی شود که برای یک عمل ثابت به ازای نوع داده‌ای خاص نیازی به تغییر و اضافه کردن کد نباشد. اگر تعوض‌پذیری رعایت نشود، کدهای اضافه زیادی تولید می‌شود که همین امر می‌تواند منجر به آن شود که معماری سیستم آلوده شود

# فصل ۱۰ - مفهوم جداسازی واسط (The Interface Segregation)
این مفهوم تنها به این مورد اشاره دارد که سیستم را باید به گونه‌ای طراحی کرد که برای تغییر یک ماژول نیازی نباشد تا تمام سیستم را deploy کرد و از recomplie شدن و deploy قسمت‌هایی که تغییر نکردند باید جلوگیری کرد

# فصل ۱۱ - مفهوم وارونگی وابستگی (The Dependency Inversion)
این مفهوم می‌گوید که منعطف‌ترین سیستم‌ها آنهایی هستند که وابستگی کد منبع فقط به انتزاعات (abstractions) مربوط می‌شوند نه به concretions. در این concretion به کلاس‌هایی گفته می‌شود abstract نیستند. مفهوم DI زمانی اهمیت پیدا می‌کند که یک ماژول(یا کلاس) خیلی بخواهد تغییر کند. به عنوان مثال *String* در جاوا ک از *java.lang.string* import می‌شود یک کلاس ثابت است و منطقی است که abstract نباشد. </br>
طراحان و معماران خوب نرم‌افزار تلاش می‌کنند تا فرار بودن واسط‌ها را کاهش دهند. منظور از فرار بودن آن است که وقتی پیاده سازی یک کلاس concrete تغییر می‌کند دیگر نیازی نباشد تا واسط‌ها نیز تغییر کنند. بنابراین سعی می‌کنند تا بدون ایجاد تغییر در واسط‌ها به پیاده سازی کلاس یک عملکرد جدید اضافه کنند.</br>
برای آنکه پیاده سازی این مفهوم باید نکاتی را رعایت کرد:
- به کلاس‌های concrete فرار اشاره نباید کرد. به جای آن به وسط‌های انتزاعی باید اشاره کرد
- از کلاس‌های concrete قرار نباید مشتق کرد
- در کل هرگز نباید به اسم هر چیز فرار و concrete اشاره کرد  

</div>


[open_close_image]: ./images/c_8.png
