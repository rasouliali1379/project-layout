# چیدمان استاندارد پروژه ی Go

ترجمه ها :

* [한국어 문서](README_ko.md)
* [简体中文](README_zh.md)
* [正體中文](README_zh-TW.md)
* [简体中文](README_zh-CN.md) - ???
* [Français](README_fr.md)
* [日本語](README_ja.md)
* [Portuguese](README_ptBR.md)
* [Español](README_es.md)
* [Română](README_ro.md)
* [Русский](README_ru.md)
* [Türkçe](README_tr.md)
* [فارسی](README_fa.md)



 ## &#x202b; بررسی اجمالی

&#x202b;این یک چیدمان ابتدایی برای پروژه هایست که با Go نوشته می شوند . **`این یک استاندارد رسمی تعیین شده توسط تیم اصلی توسعه دهنده ی Go نمیباشد`**؛ به هر حال این مجموعه ای از الگو های رایج چیدمان پروژه های قدیمی و در حال گسترش اکوسیستم Go می باشد. بعضی از این الگو ها از دیگری محبوب تر هستند . همچنین دارای چند بهبود جزئی در کنار تعدادی پوشه ی پشتیبانی که در هر پروژه ی بزرگ در دنیای واقعی رایج است .

&#x202b;**`اگر در حال یادگیری زبان Go هستید یا در حال ساخت یک PoC (Proof of Concept یا اثبات فرضیه) و یا یک پروژه ی ساده برای خودتان ٬این چیدمان زیاد از حد است . بجای آن با یک چیز ساده تر شروع کنید (یک فایل 'main.go' و 'go.mod' هم بیش از حد نیاز شماست ) .`** همین طور که پروژه ی شما در حال گسترش است مطمئن شوید که کد شما ساختار خوبی پیدا کرده است در غیر این در انتها با یک کد نا مرتب با تعداد زیادی وابستگی پنهان و گلوبال استیت مواجه میشوید. هر چقدر تعداد افراد بیشتری روی پروژه ی شما کار میکنند به ساختار بیشتری نیاز دارید. این زمانی است که شما نیاز دارید یه راه حل معمول برای مدیریت پیکج ها/کتابخانه ها معرفی کنید . وقتی که یک پروژه ی open source انجام میدهید و یا میدانید که افراد دیگری هم کد شما را در پروژه ی خود ایمپورت میکنند آن زمان مهم است که پکیج ها و کد های خصوصی (internal) داشته باشید . این ریپازیتوری را کلون کنید هر چیز که نیاز دارید را نگه دارید و بقیه را حذف کنید . هر چیزی که اینجا قرار داده شده دلیلش آن نیست که باید حتما از آن استفاده کنید . تمام این الگو ها برای همه ی پروژه ها مورد نیاز نیستند . حتی الگو ی `vendor` هم در تمام پروژه ها رایج نیست .

&#x202b;با استفاده از Go ورژن ۱.۱۴ [`Go Modules`](https://github.com/golang/go/wiki/Modules) بالاخره آماده انجام کار هستیم . از [`Go Modules`](https://blog.golang.org/using-go-modules)  استفاده کنید مگر اینکه دلیل خاصی برای عدم استفاده از آن دارید و اگر استفاده میکنید لازم نیست نگران $GOPATH باشید و یا جایی که پروژه را ذخیره میکنید . فایل پایه ی `go.mod` میزبانی ریپازیتوری شما را در گیتهاب در نظر میگیرد ولی این الزامی نیست . مسیر ماژول ٬ هر چیزی میتواند باشد اگر چه که اولین بخش مسیر باید یک نقطه در نام خود داشته باشد (در نسخه ی فعلی Go دیگر مجبور به اعمال این نیستید ولی اگر از نسخه های کمی قدیمی تر استفاده میکنید اگر بیلد شما شکست خورد تعحب نکنید).اگر میخواهید بیشتر درباره آن بخوانید ٬ به این issue ها رجوع کنید [`37554`](https://github.com/golang/go/issues/37554) و [`32819`](https://github.com/golang/go/issues/32819) .

&#x202b;این چیدمان پروژه از عمد عمومی است و سعی در تحمیل ساختار خاصی را در Go ندارد .

&#x202b;این ریپازیتوری حاصل تلاش جمعی از افراد داخل انجمن Go میباشد . اگر الگو ی جدیدی مد نظر دارید یا اینکه الگوی قبلی نیاز به بروزرسانی دارد یک issue باز کنید.

&#x202b;اگر برای نامگذاری یا فرمت کردن و یا استایل به کمک نباز دارید رجوع کنید به [`gofmt`](https://golang.org/cmd/gofmt/) and [`golint`](https://github.com/golang/lint). همچنین این دستورالعمل ها و توصیه ها سبک کد زدن Go را حتما مطالعه کنید :
* https://talks.golang.org/2014/names.slide
* https://golang.org/doc/effective_go.html#names
* https://blog.golang.org/package-names
* https://github.com/golang/go/wiki/CodeReviewComments
* [دستورالعمل سبک کد زنی Go](https://rakyll.org/style-packages) (rakyll/JBD)

&#x202b;برای اطلاعات بیشتر به این مقاله رجوع کنید : [`چیدمان پروژه Go`](https://medium.com/golang-learn/go-project-layout-e5213cdcfaa2).

&#x202b;اطلاعات بیشتر درباره نامگذاری و سازماندهی پکیج ها و همچنین سایر توصیه های ساختار کد:
* [GopherCon EU 2018: Peter Bourgon - Best Practices for Industrial Programming (بهترین روش ها برای برنامه نویسی صنعتی)](https://www.youtube.com/watch?v=PTE4VJIdHPg)
* [GopherCon Russia 2018: Ashley McNamara + Brian Ketelsen - Go best practices (روش های منتخب گو).](https://www.youtube.com/watch?v=MzTcsI6tn-0)
* [GopherCon 2017: Edward Muller -  Go Anti-Patterns (ضد الگو های گو)](https://www.youtube.com/watch?v=ltqV6pDKZD8)
* [GopherCon 2018: Kat Zien - How Do You Structure Your Go Apps (چگونه برنامه های گو خود را ساختاربندی کنید)](https://www.youtube.com/watch?v=oL6JBUk6tj0)

## &#x202b; پوشه های Go

### `/cmd`

&#x202b;برنامه های اصلی پروژه

&#x202b;نام پوشه ٬ برای هر برنامه ٬ باید با نام فایل اجرایی (executable) که میخواهید داشته باشید تطابق داشته باشد (بطور مثال `/cmd/myapp`).

&#x202b;داخل پوشه ی برنامه کد زیادی قرار ندهید . اگر فکر میکنید که کد میتواند داخل پروژه های دیگر هم ایمپورت و استفاده شود آن را در پوشه ی `/pkg` قرار دهید. اگر کد قابل استفاده مجدد نیست یا اینکه نمیخواهید دیگران از آن استفاده کنند داخل پوشه `/internal` قرارش دهید . اگر بفهمید دیگران توانایی انجام چه کارهایی را دارند شگفت زده خواهید شد بنابراین در رابطه با نیات خود صریح باشید!

&#x202b; داشتن یک فایل `main` برای ایمپورت و فراخوانی کد های پوشه های `/internal` و `/pkg` و اینکه هیچ کار دیگری انجام ندهد بسیار رایج است.

&#x202b;رجوع کنید به  [`/cmd`](cmd/README.md) برای دیدن مثال ها .

### `/internal`

&#x202b;برنامه ها و کد های خصوصی . این کدی است که شما نمیخواهید دیگران از آن استفاده کنند . توجه کنید که این الگو توسط خود کامپایلر Go اعمال شده است . برای اطلاعات بیشتر رجوع کنید به  1.4 [`release notes`](https://golang.org/doc/go1.4#internalpackages) . توجه کنید که شما فقط به یک پوشه `internal` در روت پروژه محدود نیستید . شما میتوانید در پوشه بندی پروژه ی خود بیشتر از یک پوشه ی `internal` داشته باشید.

&#x202b;می توانید به صورت اختیاری کمی ساختار اضافی به پکیج های internal خود اضافه کنید تا کد داخلی اشتراک گذاری شده و اشتراک گذاری نشده خود را جدا کنید. در کل نیازی نیست (مخصوصا برای پروژه های کوچک), اما خوب است که سرنخ های دیداری از نحوه ی استفاده از کد مد نظر داشته باشید . کد برنامه ی اصلی شما میتواند در پوشه `/internal/app` قرار بگیرد (مثال `/internal/app/myapp`) و کد مشترک این برنامه ها در  `/internal/pkg` قرار بگیرد (مثال `/internal/pkg/myprivlib`).

### `/pkg`

&#x202b;کد کتابخانه هایی که برنامه های خارجی هم میتوانند استفاده کنند (e.g., `/pkg/mypubliclib`). پروژه های دیگر این کد را ایمپورت میکنند با اطمینان از اینکه این کدها کار میکنند, پس قبل از اینکه چیزی در این پوشه قرار دهید حتما از کاکردشان اطمینان حاصل کنید :-) توجه کنید که پوشه ی  `internal` راه بهتری برای اطمینان حاصل کردن از اینکه دیگران نمیتوانند آن کد را ایمپورت کنند هستند ٬ چون توسط خود Go اعمال شده است. پوشه ی  `/pkg` همچنان راه خوبی است که صریح بیان کنید که کد داخل آن قابل استفاده برای دیگران است. مقاله ی [`I'll take pkg over internal`](https://travisjeffery.com/b/2019/11/i-ll-take-pkg-over-internal/) نوشته شده توسط  Travis Jeffery بررسی اجمالی خوبی از دایرکتوری های `pkg` و `internal` و زمانی که ممکن است استفاده از آنها منطقی باشد ارائه می دهد.
همچنین راهی برای دسته بندی کد Go در یک مکان  برای زمانی که پوشه ی اصلی پروژه ی شما حاوی تعداد زیادی مؤلفه (component) و پوشه غیر Go است که اجرای ابزارهای مختلف Go را آسان تر می کند. (همانطور که در این گفتگو ها به آن اشاره شد :
* [GopherCon EU 2018: Best Practices for Industrial Programming(بهترین روش های برنامه نویسی صنعتی)](https://www.youtube.com/watch?v=PTE4VJIdHPg) 
* [GopherCon 2018: Kat Zien - How Do You Structure Your Go Apps(چگونه برنامه های گو خود را ساختار بندی کنید)](https://www.youtube.com/watch?v=oL6JBUk6tj0) 
* [GoLab 2018 - Massimiliano Pippi - Project layout patterns in Go(الگوی چیدمان پروژه در گو)](https://www.youtube.com/watch?v=3gQa1LWwuzk)

&#x202b;به پوشه ی  [`/pkg`](pkg/README.md) رجوع کنید اگر میخواهید بدانید کدام یک از ریپازیتوری های معروف Go از این الگو ی چیدمان استفاده میکنند . این یک الگوی چیدمان رایج است، اما توسط همه پذیرفته نشده است و برخی در جامعه ی Go آن را توصیه نمی‌کنند.

&#x202b;اگر پروژه ی شما کوچک است و اضافه کردن یک پوشه چندان تاثیرگذار نخواهد بود مشکلی ندارد که از آن استفاده نکنید (مگر اینکه خیلی تمایل داشته باشید :-)). وقتی به اندازه کافی بزرگ شد و دایرکتوری ریشه شما بسیار شلوغ شد، به آن فکر کنید (مخصوصا زمانی که مولفه های زیادی به زبانی غیر از Go دارید).

&#x202b;ریشه یابی نامگذاری پوشه `pkg` : سورس قدیمی Go از `pkg` برای پکیج هایش استفاده میکرد و بعد از آن تعداد زیادی از پروژه های Go شروع به کپی برداری (اسکلی حلال) از روی آن کردند (رجوع کنید به [`این`](https://twitter.com/bradfitz/status/1039512487538970624) توییت از Brad Fitzpatrick ).

### `/vendor`

&#x202b;وابستگی های برنامه (به صورت دستی یا توسط ابزار مدیریت وابستگی مورد علاقه شما مانند ابزار داخلی جدید مدیریت می شود [`Go Modules`](https://github.com/golang/go/wiki/Modules)). دستور `go mod vendor` پوشه ی  `/vendor` را برای شما خواهد ساخت. توجه کنید که شاید نیاز داشته باشید بیرق (flag :)) `mod=vendor-` را به دستور  `go build` تان اضافه کنید اگر از Go ورژن 1.14 ٬ که در آن به صورت پیش فرض فعال است ٬ استفاده نمیکنید .

&#x202b;اگر در حال ساخت لایبری هستید ٬ وابستگی های برنامه خود را کامیت نکنید .

&#x202b;توجه کنید که از ورژن [`1.13`](https://golang.org/doc/go1.13#modules) Go قابلیت پروکسی ماژول را اضافه کرد (از [`https://proxy.golang.org`](https://proxy.golang.org) به عنوان ماژول پراکسی پیش فرض استفاده می شود). در این باره بیشتر بخوانید [`here`](https://blog.golang.org/module-mirror-launch) برای اینکه ببینید آیا با تمام نیازها و محدودیت های شما مطابقت دارد یا خیر. اگر مطابقت پیدا کرد به پوشه ی `vendor` به طور کل نیاز پیدا نخواهید کرد.

## پوش های سرویس برنامه

### `/api`

&#x202b;مشخصات OpenAPI/Swagger، فایل های JSON schema، فایل های تعریف پروتکل.

&#x202b;رجوع کنید به پوشه ی  [`/api`](api/README.md) برای دیدن مثال ها.

## پوشه های وب اپلیکیشن ها

### `/web`

&#x202b;اجزا ی اختصاصی وب اپلیکیشن : asset های استاتیک وب , قالب های سمت سرور و SPAs.

## پوشه های رایج برنامه

### `/configs`

&#x202b;پیکربندی قالب های فایل یا پیکربندی های پیش فرض .

&#x202b;فایل `confd` یا `consul-template` های خود را در اینجا قرار دهید.

### `/init`

&#x202b;مقداردهی اولیه ی سیستم (systemd, upstart, sysv) و پراسس منیجر ها (runit, supervisord) پیکربندی.

### `/scripts`

&#x202b;اسکریپت هایی برای انجام عملیات های مختلف ساخت، نصب، تجزیه و تحلیل و غیره .

&#x202b;این اسکریپت ها Makefile سطح ریشه (root) را کوچک و ساده نگه می دارند (مثال [`https://github.com/hashicorp/terraform/blob/master/Makefile`](https://github.com/hashicorp/terraform/blob/master/Makefile)).

&#x202b;رجوع کنید به پوشه ی  [`/scripts`](scripts/README.md) در دیدن مثال ها.

### `/build`

&#x202b;بسته بندی و ادغام مداوم (Packaging and Continuous Integration).

&#x202b;پیکربندی سرور ابری  (AMI), کانتینر (Docker), سیستم عامل (deb, rpm, pkg) خود را در پوشه ی  `/build/package` قرار دهید.

&#x202b;پیکربندی و اسکریپت های CI (travis, circle, drone) خود را در پوشه ی  `/build/ci` قرار دهید. توجه کنید که بعضی از ابزار های CI در رابطه با پوشه ی پیکربندی هایشان خیلی حساس هستند (مثال Travis CI) . سعی کنید فایل های پیکربندی را در پوشه ی `/build/ci` قرار دهید و وصلشان کنید به پوشه ای که ابزار CI انتظار دارد آن ها را در آنجا بیابد (زمانی که ممکن است).

### `/deployments`

&#x202b;پیکربندی ها و الگوهای استقرار سیستم IaaS، PaaS و container orchestration (docker-compose, kubernetes/helm, mesos, terraform, bosh). توجه کنید که در گروهی از ریپازیتوری ها (مخصوصا آن هایی که با kubernates دیپلوی شده اند) این پوشه `/deploy` نام دارد.

### `/test`

&#x202b;برنامه‌های تست خارجی اضافی و داده‌های آزمایشی. هر طور که تمایل دارید پوشه ی  `/test` را ساختار بندی کنید. برای پروژه های بزرگتر داشتن یک پوشه data منطقی است. بطور مثال میتوانید `/test/data` یا `/test/testdata` را استفاده کنید اگر میخواهید که Go داده ها را نادیده بگیرد. توجه کنید که Go فایل ها یا پوشه هایی که با  "." یا "_" شروع شده اند هم نادیده میگیرد, بنابراین از نظر نحوه نامگذاری پوشه های داده های آزمایشی خود انعطاف بیشتری دارید.

&#x202b;رجوع کنید به پوشه ی [`/test`](test/README.md) برای دیدن مثال ها.

## بقیه ی پوشه ها

### `/docs`

&#x202b;طراحی و مستندات کاربر (علاوه بر مستندات ایجاد شده توسط godoc).

&#x202b;رجوع کنید به پوشه ی [`/docs`](docs/README.md) برای دیدن مثال ها.

### `/tools`

&#x202b;ابزارهای پشتیبانی این پروژه توجه داشته باشید که این ابزارها می توانند کد را از دایرکتوری های `/pkg` و `/internal` ایمپورت شوند.

&#x202b;رجوع کنید به پوشه ی  [`/tools`](tools/README.md) برای دیدن مثال ها.

### `/examples`

&#x202b;مثال های برنامه ها و/یا کتابخانه های عمومی شما.


&#x202b;رجوع کنید به پوشه ی  [`/examples`](examples/README.md) برای دیدن مثال ها.

### `/third_party`

&#x202b;ابزارهای کمکی خارجی، کد فورک شده و سایر ابزارهای شخص ثالث (مانند Swagger UI).

### `/githooks`

&#x202b;هوک های گیت .

### `/assets`

&#x202b;سایر asset ها برای همراهی با ریپازیتوری شما (تصاویر، لوگو ها و غیره).

### `/website`

&#x202b;اگر از  GitHub Pages استفاده نمی کنید، اینجا جاییست که می توانید داده های وب سایت پروژه خود را قرار دهید.

&#x202b;رجوع کنید به پوشه ی  [`/website`](website/README.md) برای دیدن مثال ها.

## پوشه هایی که نباید داشته باشید

### `/src`

&#x202b; البته بعضی از پروژه های Go پوشه ی  `src` را دارند, ولی این زمانی اتفاق میافتد که توسعه دهنده از دنیای جاوا آمده باشد ٬ در آنجا این الگو ی رایج است. اگر می توانید به خودتان کمک کنید سعی کنید از این الگوی جاوا استفاده نکنید. شما واقعاً نمی خواهید کد یا پروژه های Go شما شبیه جاوا باشد :-)

&#x202b;این پوشه  `/src` که در بالاترین سطح پوشه بندی پروژه قرار دارد را با پوشه ی `src/` که Go در اینجا ([`How to Write Go Code`](https://golang.org/doc/code.html)) برای فضاهای کاری خود استفاده می کند اشتباه نگیرید . متغیر محیطی `$GOPATH` اشاره میکند به محطی کاری (فعلی) شما  (در سیستم عامل های غیر از ویندوز به صورت پیش فرض به `$HOME/go` اشاره میکند). این فضای کاری شامل پوشه های سطح بالای `/pkg` ٬ `bin` و `/src` می شود. پروژه ی شما در نهایت زیرمجموعه پوشه ی  `/src` قرار میگیرد ٬ پس اگر شما پوشه ی `/src` در پروژه ی خود داشته باشید مسیر پروژه ی شما به این صورت در می آید: `/some/path/to/workspace/src/your_project/src/your_code.go`. توجه داشته باشید که در Go ورژن 1.11 میتوانید خارج از `GOPATH` پروژه داشته باشید ٬ اما هنوز به این معنی نیست که استفاده از این الگوی چیدمان ایده خوبی است.


## Badges

&#x202b;* [Go Report Card](https://goreportcard.com/) - کد شما را با `gofmt`, `go vet`, `gocyclo`, `golint`, `ineffassign`, `license` و `misspell` اسکن میکند. `github.com/golang-standards/project-layout` را با مرجع پروژه خود تعویض کنید.

&#x202b; [![Go Report Card](https://goreportcard.com/badge/github.com/golang-standards/project-layout?style=flat-square)](https://goreportcard.com/report/github.com/golang-standards/project-layout)

&#x202b;* ~~[GoDoc](http://godoc.org) - این نسخه آنلاین مستندات تولید شده GoDoc شما را ارائه می دهد. لینک را تغییر دهید تا به پروژه شما اشاره کند.~~

&#x202b;  [![Go Doc](https://img.shields.io/badge/godoc-reference-blue.svg?style=flat-square)](http://godoc.org/github.com/golang-standards/project-layout)

&#x202b;* [Pkg.go.dev](https://pkg.go.dev) - Pkg.go.dev یک مکان جدید برای اکتشاف Go و مستندات است. شما میتواد یک badge با استفاده از [badge generation tool](https://pkg.go.dev/badge) درست کنید.

&#x202b;  [![PkgGoDev](https://pkg.go.dev/badge/github.com/golang-standards/project-layout)](https://pkg.go.dev/github.com/golang-standards/project-layout)

&#x202b;* release - اخرین شماره از منتشر شده ی شما را نشان خواهد داد. لینک گیتهاب را عوض کنید تا به سمت پروژه ی شما هدایت کند.

&#x202b;  [![Release](https://img.shields.io/github/release/golang-standards/project-layout.svg?style=flat-square)](https://github.com/golang-standards/project-layout/releases/latest)

## &#x202b; یادداشت

&#x202b; یک قالب پروژه ی خود رای با مثال ها یا تنظیمات قابل استفاده مجدد٬ اسکریپت و کد های بیشتر در دست ساخت است
