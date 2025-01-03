# گزارش پروژه: تشخیص بیماری قلبی با استفاده از یادگیری ماشین

## ۱. مقدمه
بیماری‌های قلبی یکی از علل اصلی مرگ و میر در سطح جهانی هستند. شناسایی زودهنگام و پیش‌بینی بیماری‌های قلبی می‌تواند به طور قابل توجهی نرخ مرگ و میر را کاهش دهد و نتایج درمانی را بهبود بخشد. در این پروژه، از تکنیک‌های یادگیری ماشین برای پیش‌بینی اینکه آیا یک فرد در معرض خطر بیماری قلبی قرار دارد یا خیر، بر اساس ویژگی‌های پزشکی مانند سن، فشار خون، سطح کلسترول و غیره استفاده می‌شود. هدف، ساخت یک مدل پیش‌بینی است که می‌تواند به متخصصان مراقبت‌های بهداشتی در اتخاذ تصمیمات به موقع کمک کند. این گزارش ابزارها، تکنیک‌ها و روش‌های استفاده‌شده برای دستیابی به هدف پیش‌بینی بیماری قلبی را تشریح می‌کند. بخش‌های بعدی توضیحاتی دقیق در مورد تکنولوژی‌ها و مدل‌های استفاده‌شده، به همراه دلایل انتخاب آن‌ها، ارائه می‌دهند.

## ۲. تکنولوژی‌ها و ابزارهای استفاده‌شده

### ۲.۱. زبان برنامه‌نویسی پایتون
پایتون به دلیل سادگی و خوانایی بالا، انتخاب مناسبی برای تحلیل داده‌ها و یادگیری ماشین است و به همین دلیل هم برای مبتدیان و هم برای متخصصان مناسب می‌باشد. پایتون دارای اکوسیستم وسیعی از کتابخانه‌ها و فریم‌ورک‌ها برای یادگیری ماشین (مانند scikit-learn و TensorFlow)، دستکاری داده‌ها (مانند pandas و NumPy) و مصورسازی داده‌ها (مانند matplotlib و seaborn) است که آن را برای پروتوتایپ‌سازی و تولید مدل‌های پیچیده بسیار کارآمد می‌سازد.

### ۲.۲. Scikit-learn
scikit-learn یک کتابخانه قدرتمند و ساده برای یادگیری ماشین است که مجموعه‌ای از الگوریتم‌ها را برای طبقه‌بندی، رگرسیون و خوشه‌بندی ارائه می‌دهد. این کتابخانه شامل ابزارهایی برای ارزیابی مدل، اعتبارسنجی متقابل (cross-validation) و تنظیم پارامترهای مدل (hyperparameter tuning) است که آن را برای پروژه‌هایی مانند پیش‌بینی بیماری قلبی بسیار مناسب می‌سازد. الگوریتم‌هایی مانند Logistic Regression، Decision Trees و Random Forest در این کتابخانه موجود هستند که برای مسائل طبقه‌بندی دودویی (مانند پیش‌بینی بیماری قلبی: بله یا خیر) بسیار موثر هستند.

### ۲.۳. Pandas و NumPy
Pandas یک کتابخانه ضروری برای دستکاری داده‌ها است که ساختارهای داده مانند DataFrame را فراهم می‌آورد که امکان مدیریت، پاکسازی و تحلیل آسان داده‌های جدولی را می‌دهد. NumPy برای مدیریت داده‌های عددی و انجام عملیات ریاضی کارآمد روی داده‌های بزرگ استفاده می‌شود. این دو کتابخانه برای پیش‌پردازش داده‌ها، مانند مدیریت مقادیر گم‌شده، مقیاس‌بندی ویژگی‌ها و انجام تحلیل‌های آماری ضروری هستند.

### ۲.۴. Matplotlib و Seaborn
Matplotlib یک کتابخانه محبوب برای رسم نمودارها و گراف‌های ایستا، متحرک و تعاملی است. Seaborn بر اساس Matplotlib ساخته شده و یک رابط کاربری سطح بالا برای ایجاد گرافیک‌های آماری جذاب و مفید، مانند heatmap برای ماتریس‌های سردرگمی (Confusion Matrix) و نمودارهای میله‌ای برای نمایش اهمیت ویژگی‌ها فراهم می‌کند.

## ۳. روش‌شناسی

### ۳.۱. پیش‌پردازش داده‌ها
پیش‌پردازش داده‌ها یک مرحله حیاتی در هر پروژه یادگیری ماشین است. در این پروژه، مجموعه داده‌ای استفاده شده است که ویژگی‌های پزشکی مرتبط با بیماری قلبی را شامل می‌شود. مراحل پیش‌پردازش به شرح زیر انجام شده است:
- **بارگذاری و تمیز کردن داده‌ها:** با استفاده از pandas، داده‌ها به یک DataFrame بارگذاری شد و مقادیر گم‌شده یا نادرست مدیریت شدند.
- **انتخاب ویژگی‌ها:** ویژگی‌های مرتبط مانند سن، سطح کلسترول، فشار خون و سایر ویژگی‌ها برای ساخت مدل انتخاب شدند.
- **مقیاس‌بندی ویژگی‌ها:** از آنجا که برخی ویژگی‌ها (مانند سطح کلسترول) مقیاس‌های مختلفی دارند، این ویژگی‌ها با استفاده از StandardScaler استانداردسازی شدند تا عملکرد مدل بهبود یابد.

### ۳.۲. انتخاب مدل
برای این پروژه، Logistic Regression به عنوان الگوریتم اصلی پیش‌بینی انتخاب شد. این الگوریتم یک الگوریتم ساده و در عین حال قدرتمند است که برای مسائل طبقه‌بندی دودویی مانند پیش‌بینی بیماری قلبی مؤثر است. Logistic Regression یکی از الگوریتم‌های ساده و در عین حال قدرتمند برای مسائل طبقه‌بندی دودویی است که می‌تواند با استفاده از یک تابع لجستیک پیش‌بینی کند که آیا فرد دچار بیماری قلبی است یا خیر. این مدل به دلیل سادگی، کارایی و تفسیرپذیری مناسب برای کاربردهای پزشکی مانند پیش‌بینی بیماری‌های قلبی است.

### ۳.۳. ارزیابی مدل
برای ارزیابی عملکرد مدل از چندین معیار استفاده شد:
- **دقت (Accuracy):** درصد پیش‌بینی‌های درست مدل.
- **ماتریس سردرگمی (Confusion Matrix):** برای تحلیل نتایج پیش‌بینی و تفکیک اشتباهات مدل.
- **گزارش طبقه‌بندی (Classification Report):** شامل معیارهایی مانند دقت (precision)، فراخوانی (recall) و نمره F1 است که برای ارزیابی مدل‌های طبقه‌بندی مؤثر هستند.

### ۳.۴. پیش‌بینی و نتایج
پس از آموزش مدل، از آن برای پیش‌بینی داده‌های جدید (مجموعه آزمون) استفاده شد و سپس نتایج پیش‌بینی با مقادیر واقعی مقایسه گردید.

## ۴. نتایج و تحلیل
مدل Logistic Regression توانست نتایج نسبتاً دقیقی در پیش‌بینی بیماری‌های قلبی ارائه دهد. ماتریس سردرگمی و گزارش طبقه‌بندی به ما کمک کرد تا عملکرد مدل را از جنبه‌های مختلف بررسی کنیم و تعیین کنیم که مدل چه میزان دقت و حساسیت دارد. برای مثال، دقت مدل (accuracy) نشان‌دهنده درصد پیش‌بینی‌های درست است، در حالی که فراخوانی (recall) و دقت (precision) نشان‌دهنده توانایی مدل در شناسایی بیماران واقعی و تفکیک درست آن‌ها از دیگر گروه‌ها هستند.

## ۵. نتیجه‌گیری
در این پروژه، از تکنیک‌های یادگیری ماشین برای پیش‌بینی بیماری قلبی استفاده شد و نتایج خوبی به‌دست آمد. انتخاب مدل مناسب مانند Logistic Regression و استفاده از ابزارهای پیش‌پردازش داده‌ها و ارزیابی مدل‌های مختلف مانند ماتریس سردرگمی و گزارش طبقه‌بندی باعث بهبود دقت و عملکرد مدل شد. این پروژه می‌تواند به پزشکان کمک کند تا تصمیمات درمانی بهتری برای بیماران خود اتخاذ کنند. این مدل می‌تواند در آینده با استفاده از داده‌های بیشتر و بهبود تکنیک‌های یادگیری ماشین، دقت بیشتری داشته باشد و در سیستم‌های بهداشتی مورد استفاده قرار گیرد.

## منابع:
- "Machine Learning Yearning" by Andrew Ng
- Scikit-learn documentation (https://scikit-learn.org)
- "Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow" by Aurélien Géron
