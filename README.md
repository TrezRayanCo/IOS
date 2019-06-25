<div dir="rtl" >
**باسمه تعالی**

در ابتدا کتابخانه را به پروژه خود اضافه کنید. برای استفاده از کتابخانه فایل Raygansms.framework  را در قسمت Embdded Binaries تنظیمات پروژه تان اضافه کنید.

حالا می‌توانید در برنامه iOSتان از آن استفاده کنید.

برای استفاده از کتابخانه ابتدا یک نمونه از کلاس Raygansms ایجاد می کنید. دقت کنید اطلاعات ورودی مورد نیاز برای سازنده این نمونه نام کاربری و رمز سامانه پیامکی خودتان است. در ادامه هر یک از متدهای آنرا در زبان سویفت شرح می دهیم.

**احراز هویت (متد**  **getAuthHeader**** )**

این متد رشته مورد نیاز برای احراز هویت  (فیلد Authorization) را ایجاد می کند. این متد مقدار رشته ای بر می گرداند.

**مقدار برگشتی متدها (شی** **Result)**

متدهای دیگر کتابخانه (به غیر از getAuthHeader ) از این نوع بر می گردانند. این نوع شامل سه متغییر است. یکی Code از نوع ResultCode و بیانگر موفقیت آمیز بودن عملیات یا شماره خطا است. نوع Message متن نتیجه را مشخص می کند. نوع Result نتیجه مربوط به متد را مشخص می‌کند و می‌تواند عدد، رشته و از نوع JSON باشد.
</div>

| نام پارامتر | نوع پارامتر | توضیحات |
| --- | --- | --- |
| Code | ResultCode | کد نتیجه عملیات |
| Message | String | متن نتیجه عملیات |
| Result | Any | اطلاعات دیگر عملیات درخواستی |


در کد زیر نمونه کدی برای دریافت اعتبار حساب استفاده شده است.

```
**private**** let** raygansms: Raygansms = Raygansms(username: &quot;user&quot;, password: &quot;pass&quot;);

**private**** let** Mobiles: [String] = [&quot;09120000000&quot;, &quot;09120000001&quot;];

**private**** var** recipientsMessages: [RecipientsMessage] = [];

**private**** let** MessageIDs: [String] = [&quot;1&quot;, &quot;2&quot;];

**private**** let** PhoneNumber: String = &quot;5000000000&quot;;

**private**** let** UserGroupID: String = &quot;1&quot;;

**private**** let** PORT: Int = 90;

**private**** let** Hello: String = &quot;سلام&quot;;
```

<div dir="rtl" >
 دقت کنید برای اجرا شما باید از کلاس Raygansms یک متغیر ایجاد کرده و متد مربوط به اجرا را در کد فرابخوانید. برای نمونه می‌توانید کد زیر را مشاهده کنید. در این کد اعتبار باقیمانده را دریافت می‌کند و آنرا چاپ می کند.
 </div>
 
```
raygansms.GetCredit()  {  (result) **in**

**        var** text: String = &quot;Code:\t\(String(describing: result?.Code))\nMessage:\t\(String(describing: result?.Message))&quot;

        if(result?.Result != **nil** ){

                text += &quot;\nResult:\t\(String(describing: result?.Result))&quot;

        }            }

                print(&quot;text:\(text)&quot;)

 };
```

<div dir="rtl" >
در ادامه متدهای کتابخانه را شرح می دهیم.

ارسال پیام

ارسال پیام گروهی ( **متد**  **SendMessage** )

از این متد برای ارسال پیام گروهی استفاده می شود. بدیهی است از این پیام برای ارسال پیام تکی نیز میتوان استفاده نمود.
</div>


| نام پارامتر | نوع پارامتر | توضیحات |
| --- | --- | --- |
| phoneNumber | String | شماره اختصاصی |
| message | String | متن پیام ارسالی |
| mobiles | [String] | آرایه ای از شماره موبایل ها برای ارسال پیام |
| UserGroupID | String | گروه پیام |
| SendDateInTimeStamp | CLongLong | تاریخ ارسال پیام به صورتTimeStamp  (به ثانیه) |

<div dir="rtl" >
نمونه کد فراخوانی:
 </div>
 
```
raygansms.SendMessage(phoneNumber: PhoneNumber, message: Hello, mobiles: Mobiles, userGroupID: UserGroupID, SendDateInTimeStamp: CLongLong(Date().timeIntervalSince1970)) { (result) **in**

// Your Code

}
```

<div dir="rtl" >
**ملاحضات:**

در صورتی که تاریخ ارسال، از تاریخ فعلی کمتر باشد یا به عبارتی دیگر از زمان مورد نظر عبور کرده باشید، پیام مورد نظر در لحظه ارسال خواهد شد.

ارسال پیام متناظر ( **متد**  **SendCorrespondingMessage** )

از این متد برای ارسال پیام متناظر استفاده می شود.
</div>

| نام پارامتر | نوع پارامتر | توضیحات |
| --- | --- | --- |
| phoneNumber | String | شماره اختصاصی |
| recipientsMessage | [RecipientsMessage] | آرایه ای از شماره ها و پیام های متناظر |
| UserGroupID | String | گروه پیام |

<div dir="rtl" >
نمونه کد فراخوانی:
 </div>
 
```
raygansms.SendCorrespondingMessage(phoneNumber: PhoneNumber, recipientsMessage: recipientsMessages, userGroupID: UserGroupID) { (result) **in**

// Your Code

}
```

<div dir="rtl" >
ارسال پیام به پورت خاص ( **متد**  **SendMessageToPort** )

از این متد برای ارسال پیام به پورت خاص استفاده می شود.

| نام پارامتر | نوع پارامتر | توضیحات |
| --- | --- | --- |
| phoneNumber | String | شماره اختصاصی |
| recievePortNumber | Int | شماره پورت دریافت پیام |
| sendPortNumber | Int | شماره پورت دریافت پیام |
| UserGroupID | String | گروه پیام |
| recipientsMessage | [RecipientsMessage] | آرایه ای از شماره ها و پیام های متناظر |
</div>

<div dir="rtl" >
نمونه کد فراخوانی:
 </div>
 
```
raygansms.SendMessageToPort(phoneNumber: PhoneNumber, recievePortNumber: PORT, sendPortNumber: PORT, userGroupID: UserGroupID, recipientsMessage: recipientsMessages) { (result) **in**

// Your Code

}
```

<div dir="rtl" >
مشاهده وضعیت ارسال پیام گروهی ( **متد**  **GroupMessageStatus** )

از این متد برای واکشی، وضعیت لیست پیام های ارسالی استفاده می شود.

| نام پارامتر | نوع پارامتر | توضیحات |
| --- | --- | --- |
| groupMessageId | String | شناسه گروه ارسال پیام |
</div>

<div dir="rtl" >
نمونه کد فراخوانی:
</div>
 
```
raygansms.GroupMessageStatus(userGroupID: UserGroupID) { (result) **in**

// Your Code

}
```
مشاهده وضعیت ارسال پیام متناظر ( **متد**  **CorrespondingMessageStatus** )

از این متد برای واکشی ، وضعیت لیست پیام های ارسالی استفاده می شود.

| نام پارامتر | نوع پارامتر | توضیحات |
| --- | --- | --- |
| messageId | [String] | شناسه گروه ارسال پیام |

نمونه کد فراخوانی:
```
raygansms.CorrespondingMessageStatus( messageId:MessageIDs) { (result) **in**

// Your Code

}
```
دریافت شناسه گروه پیام ( **متد**  **GetGroupMessageId** )

از این متد برای دریافت ، شناسه گروه پیام ارسالی استفاده می شود.

| نام پارامتر | نوع پارامتر | توضیحات |
| --- | --- | --- |
| groupId | String | شناسه ارسال پیام کاربر |

نمونه کد فراخوانی:
```
raygansms.GetGroupMessageId(groupId: UserGroupID) { (result) **in**

// Your Code

}
```
پیام های دریافتی ( **متد**  **ReceiveMessages** )

از این متد برای واکشی ، لیست پیام های در یافتی استفاده می شود.

| نام پارامتر | نوع پارامتر | توضیحات |
| --- | --- | --- |
| phoneNumber | String | شماره اختصاصی |
| startDate | CLongLong | تاریخ شروع به صورت TimeStamp   |
| EndDate | CLongLong | تاریخ پایان به صورت TimeStamp |
| page | Int | شماره صفحه |

نمونه کد فراخوانی:
```
raygansms.ReceiveMessages(phoneNumber: PhoneNumber, startDate: CLongLong(Date().timeIntervalSince1970), EndDate: CLongLong(Date().timeIntervalSince1970), page: 1) { (result) **in**

// Your Code

}
```
دریافت اعتبار ( **متد**  **GetCredit** )

از این متد برای واکشی ، اعتبار کاربر استفاده می شود.

نمونه کد فراخوانی:
```
raygansms.GetCredit() { (result) **in**

// Your Code

}
```
قیمت پیامک ( **متد**  **GetPrices** )

از این متد برای واکشی تعرفه ارسال پیامک توسط کاربر استفاده می شود.

نمونه کد فراخوانی:
```
raygansms.GetPrices() { (result) **in**

// Your Code

}
```
بررسی شماره ها در لیست سیاه ( **متد**  **ShowWhiteList** )

خروجی متد زیر لیست شماره موبایل هایی است که در لیست سیاه قرار ندارند.

| نام پارامتر | نوع پارامتر | توضیحات |
| --- | --- | --- |
| Mobiles | [String] | لیستی از شماره موبایل ها برای بررسی |

نمونه کد فراخوانی:
```
raygansms.ShowWhiteList(Mobiles: Mobiles) { (result) **in**

// Your Code

}
```
تفسیر کد های خروجی

| نوع ResultCode | کد خطا | توضیح خطا |
| --- | --- | --- |
| Success | 0 | عملیات با موفقیت انجام شد |
| DocError | 1001 | فرمت سند ارسالی صحیح نمی باشد |
| NumberError | 1002 | شماره اختصاصی وارد شده معتبر نمی باشد |
| DateError | 1003 | فرمت تاریخ ارسالی صحیح نمی باشد   |
| ParamError | 1004 | پارامتر های ارسالی برای درخواست مورد نظر معتبر نمی باشد |
| OwnNumberError | 2001 | مالکیت شماره اختصاصی مورد نظر برای کاربری وارد شده معتبر نمی باشد |
| UserError | 2002 | کاربری مورد نظر مجوز استفاده از وب سرویس را ندارد |
| IPError | 2003 | آدرس آی پی ، درخواست دهنده غیر مجاز می باشد |
| DateRangeError | 2004 | تاریخ ارسال در نظر گرفته شده در محدوده مجاز نمی باشد |
| UserListError | 2005 | تعداد مخاطبین حداکثر می تواند50000عدد باشد |
| MessageLengthError | 2006 | طول پیام نمی تواند بیش از10پیام باشد |
| PortError | 2007 | مقدار وارد شده برای شماره پورت غیر مجار می باشد |
| PageError | 2008 | مقدار وارد شده برای شماره صفحه غیر مجاز می‌باشد |
| UserInfoError | 2009 | خطا در واکشی اطلاعات کاربری |
| RegisterInfoError | 3001 | خطا در ثبت اطلاعات |
| GroupError | 3002 | خطا در دریافت گروه پیام |
| CreditError | 3003 | اعتبار کافی نمی باشد |
| ServiceError | 3004 | سرویس مورد نظر برای اپراتور مد نظر ، تعریف نشده است |
| ServerError | 5001 | به دلیل خطای داخلی ، سرور قادر به پاسخگویی نیست |
| SendError | 5002 | در هنگام ارسال پیام خطایی رخ داده است |
| ReceiveError | 5003 | در هنگام دریافت نتیجه ارسال پیام خطایی رخ داده است |
| ParamSendError | 5004 | برخی پیام ها در هنگام ارسال با خطا مواجه شده اند |

1. ارسال پیامک آنی و سریع (وب سرویس احراز هویت پیامکی)
ارسال خودکار کد فعال سازی بابت احراز هویت(متد AutoSendCode)

| نام پارامتر | نوع پارامتر | توضیحات |
| --- | --- | --- |
| phoneNumber | String | شماره موبایلی که قرار است کد فعال سازی به آن ارسال شود |
| footer | String |  متنی که تمایل دارید در انتهای پیامک فعال سازی شما ارسال شود، مانند SMSPanel.Trez.ir درصورت تمایل می توانید این مقدار را خالی ارسال نمایید |

<div dir="rtl" >
نمونه پیامک ارسالی این متد:

با سلام ،
کد تایید شما : 247944
SMSPanel.Trez.ir

مقدار بازگشتی این متد یک عدد بزرگتر 2000 می باشد که با این عدد می توانید با وب سرویس قدیمی اقدام به دریافت وضعیت پیامک ارسالی نمایید. در ضمن این کد هیچ ارتباطی به کد فعال سازی ندارد و با آن فرق دارد.

متد بررسی صحت کد فعال سازی (متد CheckSendCode)

</div>

| نام پارامتر | نوع پارامتر | توضیحات |
| --- | --- | --- |
| reciptionNumber | String | شماره موبایلی که کد فعال سازی به آن ارسال شده است |
| code | String | کد که برای کاربر ارسال شده و او این کد را در نرم افزار و یا سایت شما وارد کرده است |

<div dir="rtl" >
 ارسال کد فعال سازی دلخواه بابت احراز هویت (متد SendMessageWithCode)
</div>

| نام پارامتر | نوع پارامتر | توضیحات |
| --- | --- | --- |
| reciptionNumber | String | شماره موبایلی که قرار است کد فعال سازی به آن ارسال شود |
| code | String | متنی که شامل کد فعال سازی می باشد مثلا :کد فعال سازی شما : 123456 SMSPanel.Trez.ir |

<div dir="rtl" >
مقدار بازگشتی این متد یک عدد بزرگتر 2000 می باشد که با این عدد می توانید با وب سرویس قدیمی اقدام به دریافت وضعیت پیامک ارسالی نمایید. در ضمن این کد هیچ ارتباطی به کد فعال سازی ندارد و با آن فرق دارد.
 </div>
