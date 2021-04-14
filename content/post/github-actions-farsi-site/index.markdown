---
title: "توسعه و میزبانی سایت روی صفحات گیت‌هاب"
date: 2021-04-11T13:25:06-07:00
draft: false
ShowToc: true
cover:
   relative: true
   image: 01-pages-settings.png
---

در این پست تجربه خودم در راه‌اندازی یک بلاگ فارسی بر پایه [Hugo][hugo-site] روی صفحات گیت‌هاب ([Github Pages][github-pages]) را می‌نویسم. نوشتن این تجربیات به من کمک می‌کند که اگر در آینده خواستم کاری را تکرار کنم [چرخ را دوباره اختراع نکنم][reinvent-the-wheel].

نگارش انگلیسی این نوشته (با کمی تغییر) را در لینک زیر می‎‌توانید ببینید:

* https://parsiya.net/blog/2021-02-17-automagically-deploying-websites-with-custom-domains-to-github-pages/


[hugo-site]: https://gohugo.io
[github-pages]: https://docs.github.com/en/pages/getting-started-with-github-pages
[reinvent-the-wheel]: https://www.dictionary.com/browse/reinvent-the-wheel

<!-- more -->

## چرا گیت‌هاب؟
در سایت انگلیسی من نمی‌توان فارسی نوشت چون قالب سایت از راست-به-چپ پشتیبانی
نمی‌کند. [سایت اصلی من][parsiya.net] بر روی AWS قرار دارد که متاسفانه در ایران
قابل دسترسی نیست. اما صفحات گیت‌هاب علاوه بر مجانی بودن [دیگر شامل تحریم
نیستند][github-sanctions-removed]. گیت‌هاب پس از دو سال سر و کله زدن توانسته است
مجوز مربوطه را بگیرد.

[parsiya.net]: https://parsiya.net
[github-sanctions-removed]: https://github.blog/2021-01-05-advancing-developer-freedom-github-is-fully-available-in-iran/

## چرا Hugo؟
 صفحات گیت‌هاب به صورت native [از Jekyll پشتیبانی
 می‌کنند][github-jekyll-support] ولی کار با Hugo برای من راحت‌تر است. تقریباً
 تمام سایتهای من توسط Hugo تولید شده‌اند. اکثر اینstatic website generator ها
 (مولّد سایت استاتیک؟) روش کاری یکسانی دارند. شما مطالب را با فرمت markdown
 می‌نویسید و بقیه کار را به آنها می‌سپارید.

[github-jekyll-support]: https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll

لزومی ندارد حتماً از هوگو و یا جِکیل استفاده کنید، هر مولّدی که با آن راحت‌تر
هستید را انتخاب کنید. راهنمای استفاده از آن برای صفحات گیتهاب وجود دارد.
خوشبختانه دیگر نیازی به اجرای دستی بسیاری از مراحل نیست و Github actions به کمک
ما می‌آیند.

## روش استفاده
1. کل سایت در یک repository (مخزن؟) گیت در گیت‌هاب ذخیره می‌شود.
2. مطالب را به فرمت markdown می‌نویسید و در یک یا چند کامیت به مخزن اضافه می‌کنید.
3. پس از هر کامیت یک Github action سایت را تولید می‌کند.
4. سایت تولید شده در یک branch (شاخه؟) مجزا ذخیره می‌شود.
5. گیت‌هاب این شاخه را به عنوان یک سایت serve (فارسیش چی میشه؟) می‌کند.

## دانش پیشین
برای این پست شما باید یکسری موارد را بدانید:

1. [آشنایی با Hugo][hugo-quickstart] (اگر از مولّد سایت دیگری استفاده می‌کنید می‌توانید بخشهای مربوط به Hugo را سرسری رد شوید).
2. آشنایی با گیت

[hugo-quickstart]: https://gohugo.io/getting-started/quick-start/

## انواع صفحات گیت‌هاب
بر روی گیت‌هاب می‌توانیم [سه نوع سایت مختلف][kinds-of-github-pages] داشته باشیم:

1. سایت کاربر یا user site: هر نام کاربری می‌تواند یک سایت در آدرس `username.github.io` داشته باشد.
2. سایت سازمان یا organization site: مشابه صفحه کاربر است. مثلاٌ  https://microsoft.github.io.
3. سایت پروژه یا project site: هر پروژه می‌تواند یک سایت مجزا داشته باشد. آدرس سایت پروژه وابسته به نام کاربری یا سازمانی است که صاحب اکانت است. 

[kinds-of-github-pages]: https://docs.github.com/en/pages/getting-started-with-github-pages/about-github-pages#types-of-github-pages-sites

من از سایت فارسی خودم برای مثال استفاده می‌کنم که یک سایت پروژه است:

* آدرس سایت: https://github.com/parsiya/parsiya.fa
* آدرس مخزن سایت: https://github.com/parsiya/parsiya.fa

## قالب با متن راست-به-چپ
[قالب سایت من][hugo-octopress] قابلیت راست-به-چپ ندارد. آن را خودم از Octopress
به Hugo منتقل کرده‌ام و از css چیز زیادی نمی‌دانم. تصمیم گرفتم از قالب دیگری
استفاده کنم. بعد از چند انتخاب به قالب [hugo-PaperMod][hugo-papermod] رسیدم.
Hugo از زبانهای مختلف در سایت پشتیبانی می‌کند. معمولاً این برای انتشار نسخه‌های
یک صفحه (یا سایت) به چند زبان استفاده می‌شود. شما یک صفحه را به انگلیسی و فارسی
می‌نویسید و Hugo بقیه کار را انجام می‌دهد.

[hugo-octopress]: https://github.com/parsiya/Hugo-Octopress
[hugo-papermod]: https://github.com/adityatelange/hugo-PaperMod

من تنها می‌خواهم به فارسی بنویسم پس نیازی به استفاده از چند زبان ندارم. این
موارد را به `config.yml` سایتم اضافه کردم:

```yml
languageCode: fa
defaultContentLanguage: fa

languages:
  fa:
    languagedirection: rtl
    weight: 1
```

## استفاده از فونت وزیر
کار دیگر استفاده از فونت فارسی [وزیر][vazir-font] بود. ویرگول از این فونت
استفاده می‌کند و من هم می‌خواستم از آن استفاده کنم. خوشبختانه این فونت یک مجوز
باز برای استفاده دارد.

[vazir-font]: https://rastikerdar.github.io/vazir-font/

مرحله اول دانلود فونت وزیر و قراردادن آن [در دایرکتوری static
سایت][parsiya-fa-static] بود. هر چیزی که در static باشد عیناً به خود سایت اضافه
می‌شود. فونت دو بخش دارد یکی خود فایل‌های فونت و دیگر css. اینها را در
دایرکتوری‎‌های جداگانه قرار دادم (این کار لزومی ندارد ولی خوشگل‌تر است).

[parsiya-fa-static]: https://github.com/parsiya/parsiya.fa/tree/main/static


مرحله دوم اضافه کردن css فونت به قالب بود. در Hugo برای شخصی‌سازی قالب نیازی به
دستکاری مستقیم آن نیست. برای اضافه کردن css باید فایل مربوط به بخش head هر صفحه
قالب را دستکاری می‌کردم. در این قالب برای دستکاری این بخش می‌توان از فایل
`extend-head.html` استفاده کرد.

یک کپی از این فایل را در خود سایت ایجاد کردم که در
https://github.com/parsiya/parsiya.fa/blob/main/layouts/partials/extend_head.html
است. هنگام تولید سایت محتویات این فایل مستقیما به تگ head هر صفحه اضافه می‌شود.

استفاده از چنین فایل‌هایی یکی از روش‌های خوب قالب‌ها برای شخصی‌سازی است. اگر
چنین فایلی نبود باید کل `layout/partials/head.html` قالب را کپی و دستکاری می‌کردم
(که البته آخر دنیا هم نبود). تا قبل از نوشتن این مقاله [از همین روش استفاده کرده
بودم][overriding-extend-head-commit].

[overriding-extend-head-commit]: https://github.com/parsiya/parsiya.fa/commit/4b893c994540f20c0de59ddf0df2065a5a3eda07

## ایجاد workflow
اکنون وقت ایجاد Github action است. برای تولید یک سایت توسط Hugo از راهنمای زیر استفاده کردم (که [اشتباهات کوچکی][hugo-github-deploy-pull-req] هم داشت):

* https://gohugo.io/hosting-and-deployment/hosting-on-github/#build-hugo-with-github-action

[hugo-github-deploy-pull-req]: https://github.com/gohugoio/hugoDocs/pull/1329#issuecomment-776411651

نیازی به دستکاری این فایل نبود و عیناً آن را در مخزن سایت کپی کردم.

* https://github.com/parsiya/parsiya.fa/blob/main/.github/workflows/gh-pages.yml

به طور خلاصه، هر کامیت در شاخه `main` باعث شروع action می‌شود و سایت را تولید و
سپس در شاخه `gh-pages` ذخیره می‌کند.

یک نمونه از اجرای این action را می‌توانید در [این لینک][commit-for-this-post] ببینید. با push کردن
کامیتی که حاوی پست جدید (همین پست در بلاگ فارسی است، این action آن را منتشر
کرده). روی هر کدام از مراحل مانند Setup Hugo یا Deploy کلیک کنید تا جزئیات را
ببینید.

[commit-for-this-post]: https://github.com/parsiya/parsiya.fa/runs/2318887782

## تنظیمات صفحه گیت‌هاب
داخل هر مخزن در بخش `settings/pages` می‌توان شاخه‌ای که دارای صفحات سایت است را
مشخص کرد. این کار را باید بعد از ایجاد شاخه در مخزن انجام دهید چون شاخه‌ای که
وجود ندارد را نمی‌توانید انتخاب کنید.

![تنظیمات صفحه گیت‌هاب برای سایت من](01-pages-settings.png)

## دامنه شخصی
کار من در اینجا تمام شد امّا هر کدام از این سایتها می‌توانند دامنه مخصوص به خود
را داشته باشند. مثلاً یکی از سایتهای من به اسم [begbounty.com][begbounty.com] یک سایت پروژه در
مخزن https://github.com/parsiya/begbounty.com است. راهنماهای زیادی برای استفاده
از دامنه شخصی برای سایت‌های کاربران و سازمانها بود ولی تنظیمات برای سایتهای
پروژه نتایج جستجوی زیادی نداشت.

[begbounty.com]: https://begbounty.com

برای این کار باید به تنظیمات DNS دامنه خود دسترسی داشته باشید. چند تا از
دامنه‌های من در namecheap هستند و این قابلیت را دارند. همه رکوردهای DNS دامنه
خود را پاک کنید.

اول چهار `A Record` اضافه کردم. `host` این رکوردها `@` و مقدار آنها ip های زیر است:

* 185.199.108.153
* 185.199.109.153
* 185.199.110.153
* 185.199.111.153

سپس یک `رکورد CNAME` با `host` با مقدار زیر (نقطه اضافی در آخر مقدار را فراموش
نکنید):

```
parsiya.github.io.
```

**نکته امنیتی**: از `wildcard` در این رکورد `CNAME` استفاده نکنید. مثلاً ننویسید:

```
*.whatever.com
```

اگر چنین تنظیمی داشته باشید هر اکانت گیت‌هاب می‌تواند یک سایت را در subdomain
های سایت شما هاست (همون host که نمی‌دونم فارسیش چی میشه) کُنَد. انگلیسی این
اخطار را در [این صفحه][github-pages-cname-security-warning] بخوانید.

[github-pages-cname-security-warning]: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site

کار بعدی رفتن داخل تنظیمات صفحه در گیت‌هاب بود. در بخش `Custom Domain` دامنه را
وارد کردم.

![تنظیمات صفحه گیت‌هاب begbounty.com](02-pages-settings-begbounty.png)

این کار یک کامیت جدید تولید می‌کند. این کامیت یک فایل به نام `CNAME` را به مخزن
اضافه می‌کند. مقدار این فایل همان دامنه‌ای است که در بخش قبل استفاده کردیم.
صفحات گیت‌هاب از این فایل برای تشخیص دامنه شخصی استفاده می‌کند.

اگر راهنمای Hugo برای صفحات گیت‌هاب را دنبال کرده باشید [یک فایل مشابه در دایرکتوری static مخزن دارید][begbounty.com-root-cname-file]. واقعاً نمی‌دانم هر دوی این فایلها لازم هستند و یا خیر. ولی وقتی سایت کار می‌‎‌کند [دستکاری آن فایده‌ای ندارد][if-it-aint-broke].

[begbounty.com-root-cname-file]: https://github.com/parsiya/begbounty.com/blob/main/static/CNAME
[if-it-aint-broke]: https://en.wiktionary.org/wiki/if_it_ain%27t_broke,_don%27t_fix_it

## مشکلات
یک مشکل بزرگ عدم پشتیبانی Visual Studio Code از راست-به-چپ است. تقریباً همه
نوشته‌های من در این ادیتور است. این کار سرعت من را پایین آورد چون مجبور شدم از
ادیتور Notepad++ استفاده کنم. در VS Code من تعداد زیادی snippet و shortcut دارم
که سرعتم را زیاد می‌کنند.

مشکل بعدی انتخاب کم قالب است. قالبهایی که از راست-به-چپ پشتیبانی می‌کنند کم
هستند. علاقه زیادی به PaperMod ندارم (قالب خوبی است ولی من دوست ندارم) ولی از
بقیه بهتر بود.

بزرگترین مشکل هم نوشتن به فارسی است که زبانم (دستم؟) نمی‌چرخد. همین معادلسازی یا
نیم‌فاصله (`ctrl+shift+2`) پدر من را درآورده اند 😂.

## چی یاد گرفتم؟
این بخشی است که من در تقریباً همه مقاله‌هایم می‌نویسم.

یادگرفتم که اگر خواستم بلاگ فارسی بر پایه Hugo در صفحه گیت‌هاب (و با دامنه
مخصوص) داشته باشم چکار کنم.