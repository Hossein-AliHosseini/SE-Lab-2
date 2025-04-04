# SE-Lab-2

## مرحله دوم

| ردیف  | محل اعمال تغییرات | عنوان تغییر   | شرحی کوتاه از تغییر  |
|-------|-----|----------|------|
| ۱ | `MessageService`  | افزودن تابع ارسال پیام تلگرامی | افزودن تابع  `void` با عنوان `sendTelegramMessage` |
| ۲   | `TelegramMessageService`  | اضافه کردن کلاس جدید با این اسم   |   منطق بررسی قالب نام‌کاربری و ارسال پیام در این کلاس قرار دارد  |
| ۳   | `TelegramMessage`  | کلاس جدید برای پیام‌های تلگرامی    |  ذخیره‌سازی نام‌کاربری مبدا، مقصد و پیام ارسالی به کاربر   |
| ۴ | `Main`  | افزودن امکان ارسال پیام تلگرامی در رابط کاربری |  اضافه شدن گزینه جدید برای ارسال پیام تلگرامی و منطق تشخیص و ارسال مربوط به آن |


## مرحله سوم

#### 2. Open-closed Principle

##### موارد نقض:

۱. واسط `MessageService` به هنگام اضافه کردن یک سرویس پیام‌رسان جدید باید تغییر کند و کلاس جدید و کلاس‌های قبلی نیز مجبور به تغییر هستند.

۲. کلاس `Main` نیز از این قاعده مستثنی نیست. به دلیل استفاده از `switch case` و `instanceof` اضافه کردن هر پیام‌رسانی به رابط کاربری نیاز به تغییر فایل `Main.java` دارد.

##### موارد تحقق:

۱. منطق `validation` برای هر سرویس درون آن قرار دارد و مجزا از بقیه است (همه اعتبارسنجی‌ها در یک تابع انجام نمی‌شود)

#### 3. Liskov Substitution Principle

##### موارد نقض:

۱. تمام کلاس‌هایی که رابط `MessageService` را پیاده‌سازی می‌کنند مجبور هستند توابع مربوط به سرویس‌های دیگر را پیاده‌سازی کنند و تابع خالی در هر سرویس این موضوع را نشان می‌دهد.

۲. توابع `validation` بخشی از واسط نیستند و هر سرویس این تابع را جداگانه پیاده می‌کند که این مورد باعث ناسازگاری در پروژه می‌شود.

##### موارد تحقق:

۱. سرویس‌ها به درستی عملکرد اصلی خود، اعتبارسنجی ورودی و ارسال پیام را به درستی انجام می‌دهند.

#### 4. Interface Segregation Principle

##### موارد نقض:

۱. واسط `MessageService` اصطلاحا `fat` می‌باشد؛ یعنی متدهای همه سرویس‌های پیام‌رسان را دارد که توسعه‌دهنده را مجبور می‌کند همه آن‌ها را با وجود ارتباط نداشتن با سرویس جدید، پیاده‌سازی کند. همچنین رابط کاربری (`Main`) نیز وابسه به توابع اضافی‌ست که از آن‌ها استفاده نمی‌کند.

##### موارد تحقق:

۱. واسط‌ها در حال حاضر از لحاظ عملکردی `cohesive` هستند ولی می‌توان آن را به واسط‌های کوچک‌تری نیز شکست.

#### 5. Dependency Inversion Principle


##### موارد نقض:

۱. در کلاس `Main` مستقیما به پیاده‌سازی `concrete` سرویس‌های مختلف وابسته است؛ یعنی یک `High-Level module` به طراحی‌ یک یا چند `Low-Level module` وابسته است و از انتزاع بهره نبرده است.

۲. استفاده از `instanceof` در کلاس `Main` یک ارتباط مستقیم و شدید با سرویس‌ها و انواع پیام‌ها برقرار می‌کند که تغییرات در سرویس‌ها را دشوار می‌کند.

##### موارد تحقق:

۱. واسط `MessageService` در راستای انتزاع ارسال (و اعتبارسنجی پیام) توسعه داده‌شده ولی این توسعه به دلیل مشکلات ذکرشده در بخش قبل، کامل نیست و انتزاع ذکرشده به صورت کامل استفاده نمی‌شود.