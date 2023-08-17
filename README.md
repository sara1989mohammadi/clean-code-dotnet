# اصول کد نویسی تمیز در .NET/.NET Core

اگر پروژه clean-code-dotnet را دوست داشتید یا اگر به شما کمک کرد، لطفاً یک ستاره ⭐ برای این مخزن بدهید. این نه تنها به تقویت جامعه دات نت ما کمک می کند، بلکه مهارت های مربوط به کد نویسی تمیز را برای توسعه دهندگان دات نت در سراسر جهان بهبود می بخشد. بسیار از شما متشکرم

# فهرست محتوا
- [Clean Code concepts adapted for .NET/.NET Core](#clean-code-concepts-adapted-for-netnet-core)
- [فهرست محتوا](#فهرست-محتوا)
- [مقدمه](#مقدمه)
- [کد تمیز دات نت](#کد-تمیز-دات-نت)
  - [نام گذاری](#نام-گذاری)
  - [متغیرها](#متغیرها)
  - [توابع](#توابع)
  - [ اشیا و ساختار داده ها](#اشیاوساختاردادهها)
  - [کلاس ها](#کلاس-ها)
  - [سالید](#سالید)
  - [تستهای واحد](#تستهای-واحد)
  - [همروندی](#همروندی)
  - [مدیریت خطا](#مدیریت-خطا)
  - [Formatting](#formatting)
  - [کامنت ها](#کامنت-ها)
- [Other Clean Code Resources](#other-clean-code-resources)
  - [Other Clean Code Lists](#other-clean-code-lists)
  - [Style Guides](#style-guides)
  - [Tools](#tools)
  - [Cheatsheets](#cheatsheets)
- [Contributors](#contributors)
- [Backers](#backers)
- [Sponsors](#sponsors)
- [License](#license)

# مقدمه

![Humorous image of software quality estimation as a count of how many expletives you shout when reading code](http://www.osnews.com/images/comics/wtfm.jpg)

اصول مهندسی نرم افزار, از کتاب  [_Clean Code_](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) رابرت سی مارتین اقتباس و سازگار شده برای .NET/.NET Core. این اصول یک سبک برنامه نویسی نیست. این یک راهنما برای تولید کد هایی با قابلیت خواندن مجدد، استفاده مجدد و قابلیت باز سازی در  .NET/.NET Core است.

لزومی نداره همه این اصول به طور دقیق رعایت بشن، حتی تعداد کمی از اون‌ها مورد توافق جهانی قرار می‌گیرن. این اصول صرفا تعدادی دستورالعمل هستند و نه بیشتر، اما این دستورالعمل‌ها طی سال‌ها تجربه جمعی، توسط نویسندگان Clean Code تدوین شدن.

الهام گرفته شده از [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript) و [clean-code-php](https://github.com/jupeter/clean-code-php).

# کد تمیز دات نت

## نام گذاری

<details>
  <summary><b>از نوشتن نام بد خودداری کنید</b></summary>
یک نام خوب اجازه میدهد توسط تعداد زیادی از برنامه نویسان استفاده شود. نام باید نشان دهنده کار و مورد استفاده آن باشد.

**بد:**

```csharp
int d;
```

**خوب:**

```csharp
int daySinceModification;
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از نوشتن نام های گمراه کننده خودداری کنید</b></summary>

نام متغیر باید نشان دهد برای چه چیزی استفاده میشود.

**بد:**

```csharp
var dataFromDb = db.GetFromService().ToList();
```

**خوب:**

```csharp
var listOfEmployee = _employeeService.GetEmployees().ToList();
```
**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از نشان گذاری مجارستانی خود داری کنید</b></summary>

نشان گذاری مجارستانی نوع متغییر را در نام آن اعلام میکند. این کار بیهوده است چون محیط های توسعه مدرن (IDEs) نوع را شناسایی و نمایش میدهند.

**بد:**

```csharp
int iCounter;
string strFullName;
DateTime dModifiedDate;
```

**خوب:**

```csharp
int counter;
string fullName;
DateTime modifiedDate;
```

همچنین نماد مجارستانی نباید در پارامترهای ورودی متد استفاده شود.

**بد:**

```csharp
public bool IsShopOpen(string pDay, int pAmount)
{
    // some logic
}
```

**خوب:**

```csharp
public bool IsShopOpen(string day, int amount)
{
    // some logic
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از حروف بزرگ استفاده کنید</b></summary>

حروف بزرگ اطلاعات زیادی در رابطه با متغیر، توابع و ... به شما میدهند. این قوانین ذهنی هستند و تیم شما میتواند هر کدام را انتخاب کند. نکته مهم این است مهم نیست که کدام را انتخاب میکنید فقط در انتخاب خود ثابت قدم باشید.

**بد:**

```csharp
const int DAYS_IN_WEEK = 7;
const int daysInMonth = 30;

var songs = new List<string> { 'Back In Black', 'Stairway to Heaven', 'Hey Jude' };
var Artists = new List<string> { 'ACDC', 'Led Zeppelin', 'The Beatles' };

bool EraseDatabase() {}
bool Restore_database() {}

class animal {}
class Alpaca {}
```

**خوب:**

```csharp
const int DaysInWeek = 7;
const int DaysInMonth = 30;

var songs = new List<string> { 'Back In Black', 'Stairway to Heaven', 'Hey Jude' };
var artists = new List<string> { 'ACDC', 'Led Zeppelin', 'The Beatles' };

bool EraseDatabase() {}
bool RestoreDatabase() {}

class Animal {}
class Alpaca {}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از نام های قابل تلفظ استفاده کنید</b></summary>

تحقیق در رابطه با متغیر ها و توابعی که نام آنها قابل تلفظ نیست میتواند زمان بر باشد.

**بد:**

```csharp
public class Employee
{
    public Datetime sWorkDate { get; set; } // what the heck is this
    public Datetime modTime { get; set; } // same here
}
```

**خوب:**

```csharp
public class Employee
{
    public Datetime StartWorkingDate { get; set; }
    public Datetime ModificationTime { get; set; }
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از نشانه گذاری Camelcase استفاده کنید</b></summary>

از نشانه گذاری [Camelcase Notation](https://en.wikipedia.org/wiki/Camel_case) برای متغیر و توابع استفاده کنید.

**بد:**

```csharp
var employeephone;

public double CalculateSalary(int workingdays, int workinghours)
{
    // some logic
}
```

**خوب:**

```csharp
var employeePhone;

public double CalculateSalary(int workingDays, int workingHours)
{
    // some logic
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از نام دامنه استفاده کنید</b></summary>

کسانی که کد شما را میخوانند مانند شما برنامه نویس هستند. نام گذاری درست به همه کمک میکند که در رابطه با یک موضوع فکر کنند. ما نمیخواهیم زمان برای توضیح دادن در رابطه با متغیر و توابع خود بگذاریم.

**خوب**

```csharp
public class SingleObject
{
    // create an object of SingleObject
    private static SingleObject _instance = new SingleObject();

    // make the constructor private so that this class cannot be instantiated
    private SingleObject() {}

    // get the only object available
    public static SingleObject GetInstance()
    {
        return _instance;
    }

    public string ShowMessage()
    {
        return "Hello World!";
    }
}

public static void main(String[] args)
{
    // illegal construct
    // var object = new SingleObject();

    // Get the only object available
    var singletonObject = SingleObject.GetInstance();

    // show the message
    singletonObject.ShowMessage();
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>


## متغیرها

<details>
  <summary><b>از دندانه کردن عمیق و بازگشت سریع خودداری کنید</b></summary>

استفاده بیش از حد از if/esle میتواند خوانایی و دنبال کردن کد را سخت کند. **صریح بهتر از ضمنی است**.

 **بد:**

```csharp
public bool IsShopOpen(string day)
{
    if (!string.IsNullOrEmpty(day))
    {
        day = day.ToLower();
        if (day == "friday")
        {
            return true;
        }
        else if (day == "saturday")
        {
            return true;
        }
        else if (day == "sunday")
        {
            return true;
        }
        else
        {
            return false;
        }
    }
    else
    {
        return false;
    }

}
```

**خوب:**

```csharp
public bool IsShopOpen(string day)
{
    if (string.IsNullOrEmpty(day))
    {
        return false;
    }

    var openingDays = new[] { "friday", "saturday", "sunday" };
    return openingDays.Any(d => d == day.ToLower());
}
```

 **بد:**

```csharp
public long Fibonacci(int n)
{
    if (n < 50)
    {
        if (n != 0)
        {
            if (n != 1)
            {
                return Fibonacci(n - 1) + Fibonacci(n - 2);
            }
            else
            {
                return 1;
            }
        }
        else
        {
            return 0;
        }
    }
    else
    {
        throw new System.Exception("Not supported");
    }
}
```

**خوب:**

```csharp
public long Fibonacci(int n)
{
    if (n == 0)
    {
        return 0;
    }

    if (n == 1)
    {
        return 1;
    }

    if (n > 50)
    {
        throw new System.Exception("Not supported");
    }

    return Fibonacci(n - 1) + Fibonacci(n - 2);
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از نام گذاری ذهنی خودداری کنید</b></summary>

خواننده کد را مجبور نکنید که نیاز به ترجمه نام متغیر داشته باشد که این متغییر به چه معناست. **صریح بهتر از ضمنی است**.

 **بد:**

```csharp
var l = new[] { "Austin", "New York", "San Francisco" };

for (var i = 0; i < l.Count(); i++)
{
    var li = l[i];
    DoStuff();
    DoSomeOtherStuff();

    // ...
    // ...
    // ...
    // Wait, what is `li` for again?
    Dispatch(li);
}
```

**خوب:**

```csharp
var locations = new[] { "Austin", "New York", "San Francisco" };

foreach (var location in locations)
{
    DoStuff();
    DoSomeOtherStuff();

    // ...
    // ...
    // ...
    Dispatch(location);
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از رشته های جادویی خودداری کنید</b></summary>

رشته های جادویی، رشته هایی هستند که در مستقیم در کد قرار دارند و روی رفتار اپلیکیشن ما تاثیر مستقیم دارند. چنین رشته های چندین بار در کد ما تکرار میشوند, و چون نمیتوانند به صورت اتوماتیک توسط ابزار تغییر کنند, آنها به منبع خطا ایجاد میشوند زمانی که تغییراتی در برخی از رشته ها ایجاد میشود.

**بد**

```csharp
if (userRole == "Admin")
{
    // logic in here
}
```

**خوب**

```csharp
const string ADMIN_ROLE = "Admin"
if (userRole == ADMIN_ROLE)
{
    // logic in here
}
```

با استفاده از این ما باید فقط محل اصلی را تغییر دهیم و همگی با مقدار جدید سازگار میشوند.

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>محتوای غیر ضروری را اضافه نکنید</b></summary>

اگر نام object/class شما نشان دهنده چیزی است اون رو در اسم متغییر هاتون اضافه نکنید.

 **بد:**

```csharp
public class Car
{
    public string CarMake { get; set; }
    public string CarModel { get; set; }
    public string CarColor { get; set; }

    //...
}
```

**خوب:**

```csharp
public class Car
{
    public string Make { get; set; }
    public string Model { get; set; }
    public string Color { get; set; }

    //...
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از نام متغییر معنی دار و قابل تلفظ استفاده کنید</b></summary>

 **بد:**

```csharp
var ymdstr = DateTime.UtcNow.ToString("MMMM dd, yyyy");
```

**خوب:**

```csharp
var currentDate = DateTime.UtcNow.ToString("MMMM dd, yyyy");
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از کلمات یکسان برای تایپ های یکسان استفاده کنید</b></summary>

 **بد:**

```csharp
GetUserInfo();
GetUserData();
GetUserRecord();
GetUserProfile();
```

**خوب:**

```csharp
GetUser();
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از نام های قابل جستجو استفاده کنید (پارت 1)</b></summary>

ما بیشتر از آنچه کد بنویسیم کد ها را میخوانیم. این خیلی مهم است کدی که مینویسیم قابلیت خواندن و جستجو کردن را داشته باشد. با نامگذاری نکردن از متغیرهایی که در نهایت برای درک برنامه ما معنادار هستند، به خوانندگان خود صدمه می زنیم. نام خود را قابل جستجو کنید. از نام های قابل جستجو استفاده کنید.

 **بد:**

```csharp
// What the heck is data for?
var data = new { Name = "John", Age = 42 };

var stream1 = new MemoryStream();
var ser1 = new DataContractJsonSerializer(typeof(object));
ser1.WriteObject(stream1, data);

stream1.Position = 0;
var sr1 = new StreamReader(stream1);
Console.Write("JSON form of Data object: ");
Console.WriteLine(sr1.ReadToEnd());
```

**خوب:**

```csharp
var person = new Person
{
    Name = "John",
    Age = 42
};

var stream2 = new MemoryStream();
var ser2 = new DataContractJsonSerializer(typeof(Person));
ser2.WriteObject(stream2, data);

stream2.Position = 0;
var sr2 = new StreamReader(stream2);
Console.Write("JSON form of Data object: ");
Console.WriteLine(sr2.ReadToEnd());
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از نام های قابل جستجو استفاده کنید (پارت 2)</b></summary>

 **بد:**

```csharp
var data = new { Name = "John", Age = 42, PersonAccess = 4};

// What the heck is 4 for?
if (data.PersonAccess == 4)
{
    // do edit ...
}
```

**خوب:**

```csharp
public enum PersonAccess : int
{
    ACCESS_READ = 1,
    ACCESS_CREATE = 2,
    ACCESS_UPDATE = 4,
    ACCESS_DELETE = 8
}

var person = new Person
{
    Name = "John",
    Age = 42,
    PersonAccess= PersonAccess.ACCESS_CREATE
};

if (person.PersonAccess == PersonAccess.ACCESS_UPDATE)
{
    // do edit ...
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از متغیرهای توضیحی استفاده کنید</b></summary>

 **بد:**

```csharp
const string Address = "One Infinite Loop, Cupertino 95014";
var cityZipCodeRegex = @"/^[^,\]+[,\\s]+(.+?)\s*(\d{5})?$/";
var matches = Regex.Matches(Address, cityZipCodeRegex);
if (matches[0].Success == true && matches[1].Success == true)
{
    SaveCityZipCode(matches[0].Value, matches[1].Value);
}
```

**خوب:**

Decrease dependence on regex by naming subpatterns.

```csharp
const string Address = "One Infinite Loop, Cupertino 95014";
var cityZipCodeWithGroupRegex = @"/^[^,\]+[,\\s]+(?<city>.+?)\s*(?<zipCode>\d{5})?$/";
var matchesWithGroup = Regex.Match(Address, cityZipCodeWithGroupRegex);
var cityGroup = matchesWithGroup.Groups["city"];
var zipCodeGroup = matchesWithGroup.Groups["zipCode"];
if(cityGroup.Success == true && zipCodeGroup.Success == true)
{
    SaveCityZipCode(cityGroup.Value, zipCodeGroup.Value);
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>به جای شرط های تک خطی از آرگومان های پیشفرض استفاده کنید</b></summary>

**Not good:**

این خوب نیست چون `breweryName` میتواند `NULL`.

این روش نسبت به نسخه قبلی قابل درکتر است اما مقدار متغییر را بهتر کنترل میکند.

```csharp
public void CreateMicrobrewery(string name = null)
{
    var breweryName = !string.IsNullOrEmpty(name) ? name : "Hipster Brew Co.";
    // ...
}
```

**خوب:**

```csharp
public void CreateMicrobrewery(string breweryName = "Hipster Brew Co.")
{
    // ...
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

## توابع

<details>
  <summary><b>از عوارض جانبی خودداری کنید</b></summary>

یک تابع باعث ایجاد عوارض جانبی میشود اگر کاری بیشتر از دریافت یک ورودی و بازگشت یک یا چند مقدار انجام دهد. این اثر جانبی میتونه نوشتن در یک فایل، تغییر متغییر های سراسری (global) و یا انتقال پول از حساب شما به حساب شخص دیگر باشد.

حالا شما نیاز به عوراض جانبی در یک برنامه در مواردی دارید. به عنوان نمونه در مثال قبلی, شما ممکن است نیاز به نوشتن در یک فایل داشته باشید. کاری که باید انجام دهید این است که عملکرد را متمرکز یک جا بکنید. تابع و کلاس های مختلفی نداشته باشید که در یک فایل خاص امکان نوشتن داشته باشند. فقط و فقط سرویس داشته باشید که این کار را انجام دهد.

نکته اصلی این است که از تله‌های رایج مانند اشتراک‌گذاری حالت بین اشیاء بدون هیچ ساختاری، استفاده از انواع داده‌های قابل تغییر که می‌تواند توسط هر چیزی روی آن نوشته شود، و متمرکز نکردن مکان‌هایی که عوارض جانبی شما رخ می‌دهد، اجتناب کنید. اگر بتوانید این کار را انجام دهید از اکثر برنامه نویس ها خوشحال تر خواهید بود.

 **بد:**

```csharp
// Global variable referenced by following function.
// If we had another function that used this name, now it'd be an array and it could break it.
var name = "Ryan McDermott";

public void SplitAndEnrichFullName()
{
    var temp = name.Split(" ");
    name = $"His first name is {temp[0]}, and his last name is {temp[1]}"; // side effect
}

SplitAndEnrichFullName();

Console.WriteLine(name); // His first name is Ryan, and his last name is McDermott
```

**خوب:**

```csharp
public string SplitAndEnrichFullName(string name)
{
    var temp = name.Split(" ");
    return $"His first name is {temp[0]}, and his last name is {temp[1]}";
}

var name = "Ryan McDermott";
var fullName = SplitAndEnrichFullName(name);

Console.WriteLine(name); // Ryan McDermott
Console.WriteLine(fullName); // His first name is Ryan, and his last name is McDermott
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از شروط منفی خودداری کنید</b></summary>

 **بد:**

```csharp
public bool IsDOMNodeNotPresent(string node)
{
    // ...
}

if (!IsDOMNodeNotPresent(node))
{
    // ...
}
```

**خوب:**

```csharp
public bool IsDOMNodePresent(string node)
{
    // ...
}

if (IsDOMNodePresent(node))
{
    // ...
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از شرط ها خودداری کنید</b></summary>

ممکن است این کار غیر ممکن بنظر برسد. اکثر مردم برای اولین بار این حرف را میشنوند میگویند, "چگونه میتوانم هر کاری را بدون دستور `if` انجام دهم؟" جواب این است که شما میتوانید با استفاده از چندریختی (polymorphism) در بسیاری از موارد به همان نتیجه برسید. معمولا دومین سوال این است, "خب این عالیه ولی چرا من باید بخواهم که این کار را انجام دهم؟" جواب مفهوم قبلی کلین کد است که یاد گرفتیم: تابع باید یک کار انجام دهم. زمانی که ما یک کلاس یا تابه داریم که دارای دستور `if` است, شما به کاربر خود میگوید که تابع شما بیشتر از یک کار انجام میدهد. به یاد داشته باشید فقط یک کار انجام دهم.

 **بد:**

```csharp
class Airplane
{
    // ...

    public double GetCruisingAltitude()
    {
        switch (_type)
        {
            case '777':
                return GetMaxAltitude() - GetPassengerCount();
            case 'Air Force One':
                return GetMaxAltitude();
            case 'Cessna':
                return GetMaxAltitude() - GetFuelExpenditure();
        }
    }
}
```

**خوب:**

```csharp
interface IAirplane
{
    // ...

    double GetCruisingAltitude();
}

class Boeing777 : IAirplane
{
    // ...

    public double GetCruisingAltitude()
    {
        return GetMaxAltitude() - GetPassengerCount();
    }
}

class AirForceOne : IAirplane
{
    // ...

    public double GetCruisingAltitude()
    {
        return GetMaxAltitude();
    }
}

class Cessna : IAirplane
{
    // ...

    public double GetCruisingAltitude()
    {
        return GetMaxAltitude() - GetFuelExpenditure();
    }
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از چک کردن نوع خودداری کنید (پارت 1)</b></summary>

 **بد:**

```csharp
public Path TravelToTexas(object vehicle)
{
    if (vehicle.GetType() == typeof(Bicycle))
    {
        (vehicle as Bicycle).PeddleTo(new Location("texas"));
    }
    else if (vehicle.GetType() == typeof(Car))
    {
        (vehicle as Car).DriveTo(new Location("texas"));
    }
}
```

**خوب:**

```csharp
public Path TravelToTexas(Traveler vehicle)
{
    vehicle.TravelTo(new Location("texas"));
}
```

or

```csharp
// pattern matching
public Path TravelToTexas(object vehicle)
{
    if (vehicle is Bicycle bicycle)
    {
        bicycle.PeddleTo(new Location("texas"));
    }
    else if (vehicle is Car car)
    {
        car.DriveTo(new Location("texas"));
    }
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از چک کردن نوع خودداری کنید (پارت 2)</b></summary>

 **بد:**

```csharp
public int Combine(dynamic val1, dynamic val2)
{
    int value;
    if (!int.TryParse(val1, out value) || !int.TryParse(val2, out value))
    {
        throw new Exception('Must be of type Number');
    }

    return val1 + val2;
}
```

**خوب:**

```csharp
public int Combine(int val1, int val2)
{
    return val1 + val2;
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>از استفاده از ورودی های تابع به عنوان flag خودداری کنید</b></summary>

یک flag نشان میدهد که تابع بیش از یک مسئولیت دارد. این خوب است که متد فقط یک وظیفه داشته باشد. اگر شرط باعث میشود که تابع چند مسئولیت داشته باشد آن را به توابع م
کوچکتر بشکنید.

 **بد:**

```csharp
public void CreateFile(string name, bool temp = false)
{
    if (temp)
    {
        Touch("./temp/" + name);
    }
    else
    {
        Touch(name);
    }
}
```

**خوب:**

```csharp
public void CreateFile(string name)
{
    Touch(name);
}

public void CreateTempFile(string name)
{
    Touch("./temp/"  + name);
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>روی تابع های سراسری(global) چیزی ننویسید</b></summary>

تغییر دادن مقادیر سراسری در بسیاری از زبان ها عمل بدی  است چون ممکنه با کتابخانه‌های دیگه تداخل ایجاد کند و کاربری که از API شما استفاده میکند، تا وقتی به خطایی برنخورد، متوجه اون نخواهد شد. بیاید یک مثال را ببینیم: چه میشود اگر شما بخواهید یک آرایه از تنظیمات داشته باشید.
میتوانید یک تابع با عنوان `Config()` بنویسید, اما این ممکن است با یک کتابخانه دیگر که تلاش میکند کار یکسانی انجام دهد تداخل داشته باشد.

 **بد:**

```csharp
public Dictionary<string, string> Config()
{
    return new Dictionary<string,string>(){
        ["foo"] = "bar"
    };
}
```

**خوب:**

```csharp
class Configuration
{
    private Dictionary<string, string> _configuration;

    public Configuration(Dictionary<string, string> configuration)
    {
        _configuration = configuration;
    }

    public string[] Get(string key)
    {
        return _configuration.ContainsKey(key) ? _configuration[key] : null;
    }
}
```

یک کلاس `Configuration` بسازید و تنظیمات را از آن بخوانید.

```csharp
var configuration = new Configuration(new Dictionary<string, string>() {
    ["foo"] = "bar"
});
```

و شما باید یک نمونه از کلاس `Configuration` در برنامه خود بسازید.

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Don't use a Singleton pattern</b></summary>

Singleton is an [anti-pattern](https://en.wikipedia.org/wiki/Singleton_pattern). Paraphrased from Brian Button:

1. They are generally used as a **global instance**, why is that so bad? Because **you hide the dependencies** of your application in your code, instead of exposing them through the interfaces. Making something global to avoid passing it around is a [code smell](https://en.wikipedia.org/wiki/Code_smell).
2. They violate the [single responsibility principle](#single-responsibility-principle-srp): by virtue of the fact that **they control their own creation and lifecycle**.
3. They inherently cause code to be tightly [coupled](https://en.wikipedia.org/wiki/Coupling_%28computer_programming%29). This makes faking them out under **test rather difficult** in many cases.
4. They carry state around for the lifetime of the application. Another hit to testing since **you can end up with a situation where tests need to be ordered** which is a big no for unit tests. Why? Because each unit test should be independent from the other.

There is also very good thoughts by [Misko Hevery](http://misko.hevery.com/about/) about the [root of problem](http://misko.hevery.com/2008/08/25/root-cause-of-singletons/).

 **بد:**

```csharp
class DBConnection
{
    private static DBConnection _instance;

    private DBConnection()
    {
        // ...
    }

    public static GetInstance()
    {
        if (_instance == null)
        {
            _instance = new DBConnection();
        }

        return _instance;
    }

    // ...
}

var singleton = DBConnection.GetInstance();
```

**خوب:**

```csharp
class DBConnection
{
    public DBConnection(IOptions<DbConnectionOption> options)
    {
        // ...
    }

    // ...
}
```

Create instance of `DBConnection` class and configure it with [Option pattern](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/options?view=aspnetcore-2.1).

```csharp
var options = <resolve from IOC>;
var connection = new DBConnection(options);
```

And now you must use instance of `DBConnection` in your application.

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Function arguments (2 or fewer ideally)</b></summary>

Limiting the amount of function parameters is incredibly important because it makes testing your function easier. Having more than three leads to a combinatorial explosion where you have to test tons of different cases with each separate argument.

Zero arguments is the ideal case. One or two arguments is ok, and three should be avoided. Anything more than that should be consolidated. Usually, if you have more than two arguments then your function is trying to do too much. In cases where it's not, most of the time a higher-level object will suffice as an argument.

 **بد:**

```csharp
public void CreateMenu(string title, string body, string buttonText, bool cancellable)
{
    // ...
}
```

**خوب:**

```csharp
public class MenuConfig
{
    public string Title { get; set; }
    public string Body { get; set; }
    public string ButtonText { get; set; }
    public bool Cancellable { get; set; }
}

var config = new MenuConfig
{
    Title = "Foo",
    Body = "Bar",
    ButtonText = "Baz",
    Cancellable = true
};

public void CreateMenu(MenuConfig config)
{
    // ...
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Functions should do one thing</b></summary>

This is by far the most important rule in software engineering. When functions do more than one thing, they are harder to compose, test, and reason about. When you can isolate a function to just one action, they can be refactored easily and your code will read much
cleaner. If you take nothing else away from this guide other than this, you'll be ahead of many developers.

 **بد:**

```csharp
public void SendEmailToListOfClients(string[] clients)
{
    foreach (var client in clients)
    {
        var clientRecord = db.Find(client);
        if (clientRecord.IsActive())
        {
            Email(client);
        }
    }
}
```

**خوب:**

```csharp
public void SendEmailToListOfClients(string[] clients)
{
    var activeClients = GetActiveClients(clients);
    // Do some logic
}

public List<Client> GetActiveClients(string[] clients)
{
    return db.Find(clients).Where(s => s.Status == "Active");
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Function names should say what they do</b></summary>

 **بد:**

```csharp
public class Email
{
    //...

    public void Handle()
    {
        SendMail(this._to, this._subject, this._body);
    }
}

var message = new Email(...);
// What is this? A handle for the message? Are we writing to a file now?
message.Handle();
```

**خوب:**

```csharp
public class Email
{
    //...

    public void Send()
    {
        SendMail(this._to, this._subject, this._body);
    }
}

var message = new Email(...);
// Clear and obvious
message.Send();
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Functions should only be one level of abstraction</b></summary>

> Not finished yet

When you have more than one level of abstraction your function is usually doing too much. Splitting up functions leads to reusability and easier testing.

 **بد:**

```csharp
public string ParseBetterJSAlternative(string code)
{
    var regexes = [
        // ...
    ];

    var statements = explode(" ", code);
    var tokens = new string[] {};
    foreach (var regex in regexes)
    {
        foreach (var statement in statements)
        {
            // ...
        }
    }

    var ast = new string[] {};
    foreach (var token in tokens)
    {
        // lex...
    }

    foreach (var node in ast)
    {
        // parse...
    }
}
```

**Bad too:**

We have carried out some of the functionality, but the `ParseBetterJSAlternative()` function is still very complex and not testable.

```csharp
public string Tokenize(string code)
{
    var regexes = new string[]
    {
        // ...
    };

    var statements = explode(" ", code);
    var tokens = new string[] {};
    foreach (var regex in regexes)
    {
        foreach (var statement in statements)
        {
            tokens[] = /* ... */;
        }
    }

    return tokens;
}

public string Lexer(string[] tokens)
{
    var ast = new string[] {};
    foreach (var token in tokens)
    {
        ast[] = /* ... */;
    }

    return ast;
}

public string ParseBetterJSAlternative(string code)
{
    var tokens = Tokenize(code);
    var ast = Lexer(tokens);
    foreach (var node in ast)
    {
        // parse...
    }
}
```

**خوب:**

The best solution is move out the dependencies of `ParseBetterJSAlternative()` function.

```csharp
class Tokenizer
{
    public string Tokenize(string code)
    {
        var regexes = new string[] {
            // ...
        };

        var statements = explode(" ", code);
        var tokens = new string[] {};
        foreach (var regex in regexes)
        {
            foreach (var statement in statements)
            {
                tokens[] = /* ... */;
            }
        }

        return tokens;
    }
}

class Lexer
{
    public string Lexify(string[] tokens)
    {
        var ast = new[] {};
        foreach (var token in tokens)
        {
            ast[] = /* ... */;
        }

        return ast;
    }
}

class BetterJSAlternative
{
    private string _tokenizer;
    private string _lexer;

    public BetterJSAlternative(Tokenizer tokenizer, Lexer lexer)
    {
        _tokenizer = tokenizer;
        _lexer = lexer;
    }

    public string Parse(string code)
    {
        var tokens = _tokenizer.Tokenize(code);
        var ast = _lexer.Lexify(tokens);
        foreach (var node in ast)
        {
            // parse...
        }
    }
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Function callers and callees should be close</b></summary>

If a function calls another, keep those functions vertically close in the source file. Ideally, keep the caller right above the callee. We tend to read code from top-to-bottom, like a newspaper. Because of this, make your code read that way.

 **بد:**

```csharp
class PerformanceReview
{
    private readonly Employee _employee;

    public PerformanceReview(Employee employee)
    {
        _employee = employee;
    }

    private IEnumerable<PeersData> LookupPeers()
    {
        return db.lookup(_employee, 'peers');
    }

    private ManagerData LookupManager()
    {
        return db.lookup(_employee, 'manager');
    }

    private IEnumerable<PeerReviews> GetPeerReviews()
    {
        var peers = LookupPeers();
        // ...
    }

    public PerfReviewData PerfReview()
    {
        GetPeerReviews();
        GetManagerReview();
        GetSelfReview();
    }

    public ManagerData GetManagerReview()
    {
        var manager = LookupManager();
    }

    public EmployeeData GetSelfReview()
    {
        // ...
    }
}

var  review = new PerformanceReview(employee);
review.PerfReview();
```

**خوب:**

```csharp
class PerformanceReview
{
    private readonly Employee _employee;

    public PerformanceReview(Employee employee)
    {
        _employee = employee;
    }

    public PerfReviewData PerfReview()
    {
        GetPeerReviews();
        GetManagerReview();
        GetSelfReview();
    }

    private IEnumerable<PeerReviews> GetPeerReviews()
    {
        var peers = LookupPeers();
        // ...
    }

    private IEnumerable<PeersData> LookupPeers()
    {
        return db.lookup(_employee, 'peers');
    }

    private ManagerData GetManagerReview()
    {
        var manager = LookupManager();
        return manager;
    }

    private ManagerData LookupManager()
    {
        return db.lookup(_employee, 'manager');
    }

    private EmployeeData GetSelfReview()
    {
        // ...
    }
}

var review = new PerformanceReview(employee);
review.PerfReview();
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Encapsulate conditionals</b></summary>

 **بد:**

```csharp
if (article.state == "published")
{
    // ...
}
```

**خوب:**

```csharp
if (article.IsPublished())
{
    // ...
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Remove dead code</b></summary>

Dead code is just as bad as duplicate code. There's no reason to keep it in your codebase. If it's not being called, get rid of it! It will still be safe in your version history if you still need it.

 **بد:**

```csharp
public void OldRequestModule(string url)
{
    // ...
}

public void NewRequestModule(string url)
{
    // ...
}

var request = NewRequestModule(requestUrl);
InventoryTracker("apples", request, "www.inventory-awesome.io");
```

**خوب:**

```csharp
public void RequestModule(string url)
{
    // ...
}

var request = RequestModule(requestUrl);
InventoryTracker("apples", request, "www.inventory-awesome.io");
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

## اشیاوساختاردادهها

<details>
  <summary><b>Use getters and setters</b></summary>

In C# / VB.NET you can set `public`, `protected` and `private` keywords for methods.
Using it, you can control properties modification on an object.

- When you want to do more beyond getting an object property, you don't have to look up and change every accessor in your codebase.
- Makes adding validation simple when doing a `set`.
- Encapsulates the internal representation.
- Easy to add logging and error handling when getting and setting.
- Inheriting this class, you can override default functionality.
- You can lazy load your object's properties, let's say getting it from a server.

Additionally, this is part of Open/Closed principle, from object-oriented design principles.

 **بد:**

```csharp
class BankAccount
{
    public double Balance = 1000;
}

var bankAccount = new BankAccount();

// Fake buy shoes...
bankAccount.Balance -= 100;
```

**خوب:**

```csharp
class BankAccount
{
    private double _balance = 0.0D;

    pubic double Balance {
        get {
            return _balance;
        }
    }

    public BankAccount(balance = 1000)
    {
       _balance = balance;
    }

    public void WithdrawBalance(int amount)
    {
        if (amount > _balance)
        {
            throw new Exception('Amount greater than available balance.');
        }

        _balance -= amount;
    }

    public void DepositBalance(int amount)
    {
        _balance += amount;
    }
}

var bankAccount = new BankAccount();

// Buy shoes...
bankAccount.WithdrawBalance(price);

// Get balance
balance = bankAccount.Balance;
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Make objects have private/protected members</b></summary>

 **بد:**

```csharp
class Employee
{
    public string Name { get; set; }

    public Employee(string name)
    {
        Name = name;
    }
}

var employee = new Employee("John Doe");
Console.WriteLine(employee.Name); // Employee name: John Doe
```

**خوب:**

```csharp
class Employee
{
    public string Name { get; }

    public Employee(string name)
    {
        Name = name;
    }
}

var employee = new Employee("John Doe");
Console.WriteLine(employee.Name); // Employee name: John Doe
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

## کلاس ها

<details>
  <summary><b>Use method chaining</b></summary>

This pattern is very useful and commonly used in many libraries. It allows your code to be expressive, and less verbose.
For that reason, use method chaining and take a look at how clean your code will be.

**خوب:**

```csharp
public static class ListExtensions
{
    public static List<T> FluentAdd<T>(this List<T> list, T item)
    {
        list.Add(item);
        return list;
    }

    public static List<T> FluentClear<T>(this List<T> list)
    {
        list.Clear();
        return list;
    }

    public static List<T> FluentForEach<T>(this List<T> list, Action<T> action)
    {
        list.ForEach(action);
        return list;
    }

    public static List<T> FluentInsert<T>(this List<T> list, int index, T item)
    {
        list.Insert(index, item);
        return list;
    }

    public static List<T> FluentRemoveAt<T>(this List<T> list, int index)
    {
        list.RemoveAt(index);
        return list;
    }

    public static List<T> FluentReverse<T>(this List<T> list)
    {
        list.Reverse();
        return list;
    }
}

internal static void ListFluentExtensions()
{
    var list = new List<int>() { 1, 2, 3, 4, 5 }
        .FluentAdd(1)
        .FluentInsert(0, 0)
        .FluentRemoveAt(1)
        .FluentReverse()
        .FluentForEach(value => value.WriteLine())
        .FluentClear();
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Prefer composition over inheritance</b></summary>

As stated famously in [_Design Patterns_](https://en.wikipedia.org/wiki/Design_Patterns) by the Gang of Four,
you should prefer composition over inheritance where you can. There are lots of good reasons to use inheritance and lots of good reasons to use composition.

The main point for this maxim is that if your mind instinctively goes for inheritance, try to think if composition could model your problem better. In some cases it can.

You might be wondering then, "when should I use inheritance?" It
depends on your problem at hand, but this is a decent list of when inheritance makes more sense than composition:

1. Your inheritance represents an "is-a" relationship and not a "has-a" relationship (Human->Animal vs. User->UserDetails).
2. You can reuse code from the base classes (Humans can move like all animals).
3. You want to make global changes to derived classes by changing a base class (Change the caloric expenditure of all animals when they move).

 **بد:**

```csharp
class Employee
{
    private string Name { get; set; }
    private string Email { get; set; }

    public Employee(string name, string email)
    {
        Name = name;
        Email = email;
    }

    // ...
}

// Bad because Employees "have" tax data.
// EmployeeTaxData is not a type of Employee

class EmployeeTaxData : Employee
{
    private string Name { get; }
    private string Email { get; }

    public EmployeeTaxData(string name, string email, string ssn, string salary)
    {
         // ...
    }

    // ...
}
```

**خوب:**

```csharp
class EmployeeTaxData
{
    public string Ssn { get; }
    public string Salary { get; }

    public EmployeeTaxData(string ssn, string salary)
    {
        Ssn = ssn;
        Salary = salary;
    }

    // ...
}

class Employee
{
    public string Name { get; }
    public string Email { get; }
    public EmployeeTaxData TaxData { get; }

    public Employee(string name, string email)
    {
        Name = name;
        Email = email;
    }

    public void SetTax(string ssn, double salary)
    {
        TaxData = new EmployeeTaxData(ssn, salary);
    }

    // ...
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

## سالید

<details>
  <summary><b>سالید چیست؟</b></summary>

  کلمه SOLID مخفف که توسط Michael Feathers ساخته بر اساس اول حرف پنج اصل Robert Martin معرفی شده است ، که به معنای پنج اصل اساسی برنامه نویسی و طراحی شی گرا است.

- [**S**: Single Responsibility Principle (SRP)](#single-responsibility-principle-srp)
- [**O**: Open/Closed Principle (OCP)](#openclosed-principle-ocp)
- [**L**: Liskov Substitution Principle (LSP)](#liskov-substitution-principle-lsp)
- [**I**: Interface Segregation Principle (ISP)](#interface-segregation-principle-isp)
- [**D**: Dependency Inversion Principle (DIP)](#dependency-inversion-principle-dip)

</details>

<details>
  <summary><b>اصل تک مسئولیتی (Single Responsibility Principle) (SRP)</b></summary>

As stated in Clean Code, "There should never be more than one reason for a class to change". It's tempting to jam-pack a class with a lot of functionality, like when you can only take one suitcase on your flight. The issue with this is that your class won't be conceptually cohesive and it will give it many reasons to change. Minimizing the amount of times you need to change a class is important.

It's important because if too much functionality is in one class and you modify a piece of it, it can be difficult to understand how that will affect other dependent modules in your codebase.

 **بد:**

```csharp
class UserSettings
{
    private User User;

    public UserSettings(User user)
    {
        User = user;
    }

    public void ChangeSettings(Settings settings)
    {
        if (verifyCredentials())
        {
            // ...
        }
    }

    private bool VerifyCredentials()
    {
        // ...
    }
}
```

**خوب:**

```csharp
class UserAuth
{
    private User User;

    public UserAuth(User user)
    {
        User = user;
    }

    public bool VerifyCredentials()
    {
        // ...
    }
}

class UserSettings
{
    private User User;
    private UserAuth Auth;

    public UserSettings(User user)
    {
        User = user;
        Auth = new UserAuth(user);
    }

    public void ChangeSettings(Settings settings)
    {
        if (Auth.VerifyCredentials())
        {
            // ...
        }
    }
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Open/Closed Principle (OCP)</b></summary>

As stated by Bertrand Meyer, "software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification." What does that mean though? This principle basically states that you should allow users to add new functionalities without changing existing code.

 **بد:**

```csharp
abstract class AdapterBase
{
    protected string Name;

    public string GetName()
    {
        return Name;
    }
}

class AjaxAdapter : AdapterBase
{
    public AjaxAdapter()
    {
        Name = "ajaxAdapter";
    }
}

class NodeAdapter : AdapterBase
{
    public NodeAdapter()
    {
        Name = "nodeAdapter";
    }
}

class HttpRequester : AdapterBase
{
    private readonly AdapterBase Adapter;

    public HttpRequester(AdapterBase adapter)
    {
        Adapter = adapter;
    }

    public bool Fetch(string url)
    {
        var adapterName = Adapter.GetName();

        if (adapterName == "ajaxAdapter")
        {
            return MakeAjaxCall(url);
        }
        else if (adapterName == "httpNodeAdapter")
        {
            return MakeHttpCall(url);
        }
    }

    private bool MakeAjaxCall(string url)
    {
        // request and return promise
    }

    private bool MakeHttpCall(string url)
    {
        // request and return promise
    }
}
```

**خوب:**

```csharp
interface IAdapter
{
    bool Request(string url);
}

class AjaxAdapter : IAdapter
{
    public bool Request(string url)
    {
        // request and return promise
    }
}

class NodeAdapter : IAdapter
{
    public bool Request(string url)
    {
        // request and return promise
    }
}

class HttpRequester
{
    private readonly IAdapter Adapter;

    public HttpRequester(IAdapter adapter)
    {
        Adapter = adapter;
    }

    public bool Fetch(string url)
    {
        return Adapter.Request(url);
    }
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Liskov Substitution Principle (LSP)</b></summary>

This is a scary term for a very simple concept. It's formally defined as "If S is a subtype of T, then objects of type T may be replaced with objects of type S (i.e., objects of type S may substitute objects of type T) without altering any of the desirable properties of that program (correctness, task performed,
etc.)." That's an even scarier definition.

The best explanation for this is if you have a parent class and a child class, then the base class and child class can be used interchangeably without getting incorrect results. This might still be confusing, so let's take a look at the classic Square-Rectangle example. Mathematically, a square is a rectangle, but if you model it using the "is-a" relationship via inheritance, you quickly
get into trouble.

 **بد:**

```csharp
class Rectangle
{
    protected double Width = 0;
    protected double Height = 0;

    public Drawable Render(double area)
    {
        // ...
    }

    public void SetWidth(double width)
    {
        Width = width;
    }

    public void SetHeight(double height)
    {
        Height = height;
    }

    public double GetArea()
    {
        return Width * Height;
    }
}

class Square : Rectangle
{
    public double SetWidth(double width)
    {
        Width = Height = width;
    }

    public double SetHeight(double height)
    {
        Width = Height = height;
    }
}

Drawable RenderLargeRectangles(Rectangle rectangles)
{
    foreach (rectangle in rectangles)
    {
        rectangle.SetWidth(4);
        rectangle.SetHeight(5);
        var area = rectangle.GetArea(); // BAD: Will return 25 for Square. Should be 20.
        rectangle.Render(area);
    }
}

var rectangles = new[] { new Rectangle(), new Rectangle(), new Square() };
RenderLargeRectangles(rectangles);
```

**خوب:**

```csharp
abstract class ShapeBase
{
    protected double Width = 0;
    protected double Height = 0;

    abstract public double GetArea();

    public Drawable Render(double area)
    {
        // ...
    }
}

class Rectangle : ShapeBase
{
    public void SetWidth(double width)
    {
        Width = width;
    }

    public void SetHeight(double height)
    {
        Height = height;
    }

    public double GetArea()
    {
        return Width * Height;
    }
}

class Square : ShapeBase
{
    private double Length = 0;

    public double SetLength(double length)
    {
        Length = length;
    }

    public double GetArea()
    {
        return Math.Pow(Length, 2);
    }
}

Drawable RenderLargeRectangles(Rectangle rectangles)
{
    foreach (rectangle in rectangles)
    {
        if (rectangle is Square)
        {
            rectangle.SetLength(5);
        }
        else if (rectangle is Rectangle)
        {
            rectangle.SetWidth(4);
            rectangle.SetHeight(5);
        }

        var area = rectangle.GetArea();
        rectangle.Render(area);
    }
}

var shapes = new[] { new Rectangle(), new Rectangle(), new Square() };
RenderLargeRectangles(shapes);
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Interface Segregation Principle (ISP)</b></summary>

ISP states that "Clients should not be forced to depend upon interfaces that they do not use."

A good example to look at that demonstrates this principle is for
classes that require large settings objects. Not requiring clients to setup huge amounts of options is beneficial, because most of the time they won't need all of the settings. Making them optional helps prevent having a "fat interface".

 **بد:**

```csharp
public interface IEmployee
{
    void Work();
    void Eat();
}

public class Human : IEmployee
{
    public void Work()
    {
        // ....working
    }

    public void Eat()
    {
        // ...... eating in lunch break
    }
}

public class Robot : IEmployee
{
    public void Work()
    {
        //.... working much more
    }

    public void Eat()
    {
        //.... robot can't eat, but it must implement this method
    }
}
```

**خوب:**

Not every worker is an employee, but every employee is an worker.

```csharp
public interface IWorkable
{
    void Work();
}

public interface IFeedable
{
    void Eat();
}

public interface IEmployee : IFeedable, IWorkable
{
}

public class Human : IEmployee
{
    public void Work()
    {
        // ....working
    }

    public void Eat()
    {
        //.... eating in lunch break
    }
}

// robot can only work
public class Robot : IWorkable
{
    public void Work()
    {
        // ....working
    }
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Dependency Inversion Principle (DIP)</b></summary>

This principle states two essential things:

1. High-level modules should not depend on low-level modules. Both should depend on abstractions.
2. Abstractions should not depend upon details. Details should depend on abstractions.

This can be hard to understand at first, but if you've worked with .NET/.NET Core framework, you've seen an implementation of this principle in the form of [Dependency Injection](https://martinfowler.com/articles/injection.html) (DI). While they are not identical concepts, DIP keeps high-level modules from knowing the details of its low-level modules and setting them up.
It can accomplish this through DI. A huge benefit of this is that it reduces the coupling between modules. Coupling is a very bad development pattern because it makes your code hard to refactor.

 **بد:**

```csharp
public abstract class EmployeeBase
{
    protected virtual void Work()
    {
        // ....working
    }
}

public class Human : EmployeeBase
{
    public override void Work()
    {
        //.... working much more
    }
}

public class Robot : EmployeeBase
{
    public override void Work()
    {
        //.... working much, much more
    }
}

public class Manager
{
    private readonly Robot _robot;
    private readonly Human _human;

    public Manager(Robot robot, Human human)
    {
        _robot = robot;
        _human = human;
    }

    public void Manage()
    {
        _robot.Work();
        _human.Work();
    }
}
```

**خوب:**

```csharp
public interface IEmployee
{
    void Work();
}

public class Human : IEmployee
{
    public void Work()
    {
        // ....working
    }
}

public class Robot : IEmployee
{
    public void Work()
    {
        //.... working much more
    }
}

public class Manager
{
    private readonly IEnumerable<IEmployee> _employees;

    public Manager(IEnumerable<IEmployee> employees)
    {
        _employees = employees;
    }

    public void Manage()
    {
        foreach (var employee in _employees)
        {
            _employee.Work();
        }
    }
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Don’t repeat yourself (DRY)</b></summary>

Try to observe the [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) principle.

Do your absolute best to avoid duplicate code. Duplicate code is bad because it means that there's more than one place to alter something if you need to change some logic.

Imagine if you run a restaurant and you keep track of your inventory: all your tomatoes, onions, garlic, spices, etc. If you have multiple lists that you keep this on, then all have to be updated when you serve a dish with tomatoes in them. If you only have one list, there's only one place to update!

Oftentimes you have duplicate code because you have two or more slightly different things, that share a lot in common, but their differences force you to have two or more separate functions that do much of the same things. Removing duplicate code means creating an abstraction that can handle this set of different things with just one function/module/class.

Getting the abstraction right is critical, that's why you should follow the SOLID principles laid out in the [Classes](#classes) section. Bad abstractions can be worse than duplicate code, so be careful! Having said this, if you can make a good abstraction, do it! Don't repeat yourself, otherwise you'll find yourself updating multiple places anytime you want to change one thing.

 **بد:**

```csharp
public List<EmployeeData> ShowDeveloperList(Developers developers)
{
    foreach (var developers in developer)
    {
        var expectedSalary = developer.CalculateExpectedSalary();
        var experience = developer.GetExperience();
        var githubLink = developer.GetGithubLink();
        var data = new[] {
            expectedSalary,
            experience,
            githubLink
        };

        Render(data);
    }
}

public List<ManagerData> ShowManagerList(Manager managers)
{
    foreach (var manager in managers)
    {
        var expectedSalary = manager.CalculateExpectedSalary();
        var experience = manager.GetExperience();
        var githubLink = manager.GetGithubLink();
        var data =
        new[] {
            expectedSalary,
            experience,
            githubLink
        };

        render(data);
    }
}
```

**خوب:**

```csharp
public List<EmployeeData> ShowList(Employee employees)
{
    foreach (var employee in employees)
    {
        var expectedSalary = employees.CalculateExpectedSalary();
        var experience = employees.GetExperience();
        var githubLink = employees.GetGithubLink();
        var data =
        new[] {
            expectedSalary,
            experience,
            githubLink
        };

        render(data);
    }
}
```

**Very good:**

It is better to use a compact version of the code.

```csharp
public List<EmployeeData> ShowList(Employee employees)
{
    foreach (var employee in employees)
    {
        render(new[] {
            employee.CalculateExpectedSalary(),
            employee.GetExperience(),
            employee.GetGithubLink()
        });
    }
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

## تستهای واحد

<details>
  <summary><b>Basic concept of testing</b></summary>

Testing is more important than shipping. If you have no tests or an
inadequate amount, then every time you ship code you won't be sure that you didn't break anything. Deciding on what constitutes an adequate amount is up to your team, but having 100% coverage (all statements and branches) is how you achieve very high confidence and developer peace of mind. This means that in addition to having a great testing framework, you also need to use a [good coverage tool](https://docs.microsoft.com/en-us/visualstudio/test/using-code-coverage-to-determine-how-much-code-is-being-tested).

There's no excuse to not write tests. There's [plenty of good .NET test frameworks](https://github.com/thangchung/awesome-dotnet-core#testing), so find one that your team prefers. When you find one that works for your team, then aim to always write tests for every new feature/module you introduce. If your preferred method is Test Driven Development (TDD), that is great, but the main point is to just make sure you are reaching your coverage goals before launching any feature, or refactoring an existing one.

</details>

<details>
  <summary><b>Single concept per test</b></summary>

Ensures that your tests are laser focused and not testing miscellaenous (non-related) things, forces [AAA patern](http://wiki.c2.com/?ArrangeActAssert) used to make your codes more clean and readable.

 **بد:**

```csharp

public class MakeDotNetGreatAgainTests
{
    [Fact]
    public void HandleDateBoundaries()
    {
        var date = new MyDateTime("1/1/2015");
        date.AddDays(30);
        Assert.Equal("1/31/2015", date);

        date = new MyDateTime("2/1/2016");
        date.AddDays(28);
        Assert.Equal("02/29/2016", date);

        date = new MyDateTime("2/1/2015");
        date.AddDays(28);
        Assert.Equal("03/01/2015", date);
    }
}

```

**خوب:**

```csharp

public class MakeDotNetGreatAgainTests
{
    [Fact]
    public void Handle30DayMonths()
    {
        // Arrange
        var date = new MyDateTime("1/1/2015");

        // Act
        date.AddDays(30);

        // Assert
        Assert.Equal("1/31/2015", date);
    }

    [Fact]
    public void HandleLeapYear()
    {
        // Arrange
        var date = new MyDateTime("2/1/2016");

        // Act
        date.AddDays(28);

        // Assert
        Assert.Equal("02/29/2016", date);
    }

    [Fact]
    public void HandleNonLeapYear()
    {
        // Arrange
        var date = new MyDateTime("2/1/2015");

        // Act
        date.AddDays(28);

        // Assert
        Assert.Equal("03/01/2015", date);
    }
}

```

> Soure https://www.codingblocks.net/podcast/how-to-write-amazing-unit-tests

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

## همروندی

<details>
  <summary><b>Use Async/Await</b></summary>

**Summary of Asynchronous Programming Guidelines**

| Name              | Description                                       | Exceptions                      |
| ----------------- | ------------------------------------------------- | ------------------------------- |
| Avoid async void  | Prefer async Task methods over async void methods | Event handlers                  |
| Async all the way | Don't mix blocking and async code                 | Console main method (C# <= 7.0) |
| Configure context | Use `ConfigureAwait(false)` when you can          | Methods that require con­text   |

**The Async Way of Doing Things**

| To Do This ...                           | Instead of This ...        | Use This             |
| ---------------------------------------- | -------------------------- | -------------------- |
| Retrieve the result of a background task | `Task.Wait or Task.Result` | `await`              |
| Wait for any task to complete            | `Task.WaitAny`             | `await Task.WhenAny` |
| Retrieve the results of multiple tasks   | `Task.WaitAll`             | `await Task.WhenAll` |
| Wait a period of time                    | `Thread.Sleep`             | `await Task.Delay`   |

**Best practice**

The async/await is the best for IO bound tasks (networking communication, database communication, http request, etc.) but it is not good to apply on computational bound tasks (traverse on the huge list, render a hugge image, etc.). Because it will release the holding thread to the thread pool and CPU/cores available will not involve to process those tasks. Therefore, we should avoid using Async/Await for computional bound tasks.

For dealing with computational bound tasks, prefer to use `Task.Factory.CreateNew` with `TaskCreationOptions` is `LongRunning`. It will start a new background thread to process a heavy computational bound task without release it back to the thread pool until the task being completed.

**Know Your Tools**

There's a lot to learn about async and await, and it's natural to get a little disoriented. Here's a quick reference of solutions to common problems.

**Solutions to Common Async Problems**

| Problem                                         | Solution                                                                          |
| ----------------------------------------------- | --------------------------------------------------------------------------------- |
| Create a task to execute code                   | `Task.Run` or `TaskFactory.StartNew` (not the `Task` constructor or `Task.Start`) |
| Create a task wrapper for an operation or event | `TaskFactory.FromAsync` or `TaskCompletionSource<T>`                              |
| Support cancellation                            | `CancellationTokenSource` and `CancellationToken`                                 |
| Report progress                                 | `IProgress<T>` and `Progress<T>`                                                  |
| Handle streams of data                          | TPL Dataflow or Reactive Extensions                                               |
| Synchronize access to a shared resource         | `SemaphoreSlim`                                                                   |
| Asynchronously initialize a resource            | `AsyncLazy<T>`                                                                    |
| Async-ready producer/consumer structures        | TPL Dataflow or `AsyncCollection<T>`                                              |

Read the [Task-based Asynchronous Pattern (TAP) document](http://www.microsoft.com/download/en/details.aspx?id=19957).
It is extremely well-written, and includes guidance on API design and the proper use of async/await (including cancellation and progress reporting).

There are many new await-friendly techniques that should be used instead of the old blocking techniques. If you have any of these Old examples in your new async code, you're Doing It Wrong(TM):

| Old                | New                                  | Description                                                   |
| ------------------ | ------------------------------------ | ------------------------------------------------------------- |
| `task.Wait`        | `await task`                         | Wait/await for a task to complete                             |
| `task.Result`      | `await task`                         | Get the result of a completed task                            |
| `Task.WaitAny`     | `await Task.WhenAny`                 | Wait/await for one of a collection of tasks to complete       |
| `Task.WaitAll`     | `await Task.WhenAll`                 | Wait/await for every one of a collection of tasks to complete |
| `Thread.Sleep`     | `await Task.Delay`                   | Wait/await for a period of time                               |
| `Task` constructor | `Task.Run` or `TaskFactory.StartNew` | Create a code-based task                                      |

> Source https://gist.github.com/jonlabelle/841146854b23b305b50fa5542f84b20c

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

## مدیریت خطا

<details>
  <summary><b>Basic concept of error handling</b></summary>

Thrown errors are a good thing! They mean the runtime has successfully identified when something in your program has gone wrong and it's letting you know by stopping function execution on the current stack, killing the process (in .NET/.NET Core), and notifying you in the console with a stack trace.

</details>

<details>
  <summary><b>Don't use 'throw ex' in catch block</b></summary>

If you need to re-throw an exception after catching it, use just 'throw'
By using this, you will save the stack trace. But in the bad option below,
you will lost the stack trace.

 **بد:**

```csharp
try
{
    // Do something..
}
catch (Exception ex)
{
    // Any action something like roll-back or logging etc.
    throw ex;
}
```

**خوب:**

```csharp
try
{
    // Do something..
}
catch (Exception ex)
{
    // Any action something like roll-back or logging etc.
    throw;
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Don't ignore caught errors</b></summary>

Doing nothing with a caught error doesn't give you the ability to ever fix or react to said error. Throwing the error isn't much better as often times it can get lost in a sea of things printed to the console. If you wrap any bit of code in a `try/catch` it means you think an error may occur there and therefore you should have a plan, or create a code path, for when it occurs.

 **بد:**

```csharp
try
{
    FunctionThatMightThrow();
}
catch (Exception ex)
{
    // silent exception
}
```

**خوب:**

```csharp
try
{
    FunctionThatMightThrow();
}
catch (Exception error)
{
    NotifyUserOfError(error);

    // Another option
    ReportErrorToService(error);
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Use multiple catch block instead of if conditions.</b></summary>

If you need to take action according to type of the exception,
you better use multiple catch block for exception handling.

 **بد:**

```csharp
try
{
    // Do something..
}
catch (Exception ex)
{

    if (ex is TaskCanceledException)
    {
        // Take action for TaskCanceledException
    }
    else if (ex is TaskSchedulerException)
    {
        // Take action for TaskSchedulerException
    }
}
```

**خوب:**

```csharp
try
{
    // Do something..
}
catch (TaskCanceledException ex)
{
    // Take action for TaskCanceledException
}
catch (TaskSchedulerException ex)
{
    // Take action for TaskSchedulerException
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Keep exception stack trace when rethrowing exceptions</b></summary>

C# allows the exception to be rethrown in a catch block using the `throw` keyword. It is a bad practice to throw a caught exception using `throw e;`. This statement resets the stack trace. Instead use `throw;`. This will keep the stack trace and provide a deeper insight about the exception.
Another option is to use a custom exception. Simply instantiate a new exception and set its inner exception property to the caught exception with throw `new CustomException("some info", e);`. Adding information to an exception is a good practice as it will help with debugging. However, if the objective is to log an exception then use `throw;` to pass the buck to the caller.

 **بد:**

```csharp
try
{
    FunctionThatMightThrow();
}
catch (Exception ex)
{
    logger.LogInfo(ex);
    throw ex;
}
```

**خوب:**

```csharp
try
{
    FunctionThatMightThrow();
}
catch (Exception error)
{
    logger.LogInfo(error);
    throw;
}
```

**خوب:**

```csharp
try
{
    FunctionThatMightThrow();
}
catch (Exception error)
{
    logger.LogInfo(error);
    throw new CustomException(error);
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

## Formatting

<details>
  <summary><b>Uses <i>.editorconfig</i> file</b></summary>

 **بد:**

Has many code formatting styles in the project. For example, indent style is `space` and `tab` mixed in the project.

**خوب:**

Define and maintain consistent code style in your codebase with the use of an `.editorconfig` file

```csharp
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

# C# files
[*.cs]
indent_size = 4
# New line preferences
csharp_new_line_before_open_brace = all
csharp_new_line_before_else = true
csharp_new_line_before_catch = true
csharp_new_line_before_finally = true
csharp_new_line_before_members_in_object_initializers = true
csharp_new_line_before_members_in_anonymous_types = true
csharp_new_line_within_query_expression_clauses = true

# Code files
[*.{cs,csx,vb,vbx}]
indent_size = 4

# Indentation preferences
csharp_indent_block_contents = true
csharp_indent_braces = false
csharp_indent_case_contents = true
csharp_indent_switch_labels = true
csharp_indent_labels = one_less_than_current

# avoid this. unless absolutely necessary
dotnet_style_qualification_for_field = false:suggestion
dotnet_style_qualification_for_property = false:suggestion
dotnet_style_qualification_for_method = false:suggestion
dotnet_style_qualification_for_event = false:suggestion

# only use var when it's obvious what the variable type is
# csharp_style_var_for_built_in_types = false:none
# csharp_style_var_when_type_is_apparent = false:none
# csharp_style_var_elsewhere = false:suggestion

# use language keywords instead of BCL types
dotnet_style_predefined_type_for_locals_parameters_members = true:suggestion
dotnet_style_predefined_type_for_member_access = true:suggestion

# name all constant fields using PascalCase
dotnet_naming_rule.constant_fields_should_be_pascal_case.severity = suggestion
dotnet_naming_rule.constant_fields_should_be_pascal_case.symbols  = constant_fields
dotnet_naming_rule.constant_fields_should_be_pascal_case.style    = pascal_case_style

dotnet_naming_symbols.constant_fields.applicable_kinds   = field
dotnet_naming_symbols.constant_fields.required_modifiers = const

dotnet_naming_style.pascal_case_style.capitalization = pascal_case

# static fields should have s_ prefix
dotnet_naming_rule.static_fields_should_have_prefix.severity = suggestion
dotnet_naming_rule.static_fields_should_have_prefix.symbols  = static_fields
dotnet_naming_rule.static_fields_should_have_prefix.style    = static_prefix_style

dotnet_naming_symbols.static_fields.applicable_kinds   = field
dotnet_naming_symbols.static_fields.required_modifiers = static

dotnet_naming_style.static_prefix_style.required_prefix = s_
dotnet_naming_style.static_prefix_style.capitalization = camel_case

# internal and private fields should be _camelCase
dotnet_naming_rule.camel_case_for_private_internal_fields.severity = suggestion
dotnet_naming_rule.camel_case_for_private_internal_fields.symbols  = private_internal_fields
dotnet_naming_rule.camel_case_for_private_internal_fields.style    = camel_case_underscore_style

dotnet_naming_symbols.private_internal_fields.applicable_kinds = field
dotnet_naming_symbols.private_internal_fields.applicable_accessibilities = private, internal

dotnet_naming_style.camel_case_underscore_style.required_prefix = _
dotnet_naming_style.camel_case_underscore_style.capitalization = camel_case

# Code style defaults
dotnet_sort_system_directives_first = true
csharp_preserve_single_line_blocks = true
csharp_preserve_single_line_statements = false

# Expression-level preferences
dotnet_style_object_initializer = true:suggestion
dotnet_style_collection_initializer = true:suggestion
dotnet_style_explicit_tuple_names = true:suggestion
dotnet_style_coalesce_expression = true:suggestion
dotnet_style_null_propagation = true:suggestion

# Expression-bodied members
csharp_style_expression_bodied_methods = false:none
csharp_style_expression_bodied_constructors = false:none
csharp_style_expression_bodied_operators = false:none
csharp_style_expression_bodied_properties = true:none
csharp_style_expression_bodied_indexers = true:none
csharp_style_expression_bodied_accessors = true:none

# Pattern matching
csharp_style_pattern_matching_over_is_with_cast_check = true:suggestion
csharp_style_pattern_matching_over_as_with_null_check = true:suggestion
csharp_style_inlined_variable_declaration = true:suggestion

# Null checking preferences
csharp_style_throw_expression = true:suggestion
csharp_style_conditional_delegate_call = true:suggestion

# Space preferences
csharp_space_after_cast = false
csharp_space_after_colon_in_inheritance_clause = true
csharp_space_after_comma = true
csharp_space_after_dot = false
csharp_space_after_keywords_in_control_flow_statements = true
csharp_space_after_semicolon_in_for_statement = true
csharp_space_around_binary_operators = before_and_after
csharp_space_around_declaration_statements = do_not_ignore
csharp_space_before_colon_in_inheritance_clause = true
csharp_space_before_comma = false
csharp_space_before_dot = false
csharp_space_before_open_square_brackets = false
csharp_space_before_semicolon_in_for_statement = false
csharp_space_between_empty_square_brackets = false
csharp_space_between_method_call_empty_parameter_list_parentheses = false
csharp_space_between_method_call_name_and_opening_parenthesis = false
csharp_space_between_method_call_parameter_list_parentheses = false
csharp_space_between_method_declaration_empty_parameter_list_parentheses = false
csharp_space_between_method_declaration_name_and_open_parenthesis = false
csharp_space_between_method_declaration_parameter_list_parentheses = false
csharp_space_between_parentheses = false
csharp_space_between_square_brackets = false

[*.{asm,inc}]
indent_size = 8

# Xml project files
[*.{csproj,vcxproj,vcxproj.filters,proj,nativeproj,locproj}]
indent_size = 2

# Xml config files
[*.{props,targets,config,nuspec}]
indent_size = 2

[CMakeLists.txt]
indent_size = 2

[*.cmd]
indent_size = 2

```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

## کامنت ها

<details>
  <summary><b>Avoid positional markers</b></summary>

They usually just add noise. Let the functions and variable names along with the proper indentation and formatting give the visual structure to your code.

 **بد:**

```csharp
////////////////////////////////////////////////////////////////////////////////
// Scope Model Instantiation
////////////////////////////////////////////////////////////////////////////////
var model = new[]
{
    menu: 'foo',
    nav: 'bar'
};

////////////////////////////////////////////////////////////////////////////////
// Action setup
////////////////////////////////////////////////////////////////////////////////
void Actions()
{
    // ...
};
```

 **بد:**

```csharp

#region Scope Model Instantiation

var model = {
    menu: 'foo',
    nav: 'bar'
};

#endregion

#region Action setup

void Actions() {
    // ...
};

#endregion
```

**خوب:**

```csharp
var model = new[]
{
    menu: 'foo',
    nav: 'bar'
};

void Actions()
{
    // ...
};
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Don't leave commented out code in your codebase</b></summary>

Version control exists for a reason. Leave old code in your history.

 **بد:**

```csharp
doStuff();
// doOtherStuff();
// doSomeMoreStuff();
// doSoMuchStuff();
```

**خوب:**

```csharp
doStuff();
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Don't have journal comments</b></summary>

Remember, use version control! There's no need for dead code, commented code, and especially journal comments. Use `git log` to get history!

 **بد:**

```csharp
/**
 * 2018-12-20: Removed monads, didn't understand them (RM)
 * 2017-10-01: Improved using special monads (JP)
 * 2016-02-03: Removed type-checking (LI)
 * 2015-03-14: Added combine with type-checking (JR)
 */
public int Combine(int a,int b)
{
    return a + b;
}
```

**خوب:**

```csharp
public int Combine(int a,int b)
{
    return a + b;
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>Only comment things that have business logic complexity</b></summary>

Comments are an apology, not a requirement. Good code _mostly_ documents itself.

 **بد:**

```csharp
public int HashIt(string data)
{
    // The hash
    var hash = 0;

    // Length of string
    var length = data.length;

    // Loop through every character in data
    for (var i = 0; i < length; i++)
    {
        // Get character code.
        const char = data.charCodeAt(i);
        // Make the hash
        hash = ((hash << 5) - hash) + char;
        // Convert to 32-bit integer
        hash &= hash;
    }
}
```

**Better but still Bad:**

```csharp
public int HashIt(string data)
{
    var hash = 0;
    var length = data.length;
    for (var i = 0; i < length; i++)
    {
        const char = data.charCodeAt(i);
        hash = ((hash << 5) - hash) + char;

        // Convert to 32-bit integer
        hash &= hash;
    }
}
```

If a comment explains WHAT the code is doing, it is probably a useless comment and can be implemented with a well named variable or function. The comment in the previous code could be replaced with a function named `ConvertTo32bitInt` so this comment is still useless.
However it would be hard to express by code WHY the developer chose djb2 hash algorithm instead of sha-1 or another hash function. In that case a comment is acceptable.

**خوب:**

```csharp
public int Hash(string data)
{
    var hash = 0;
    var length = data.length;

    for (var i = 0; i < length; i++)
    {
        var character = data[i];
        // use of djb2 hash algorithm as it has a good compromise
        // between speed and low collision with a very simple implementation
        hash = ((hash << 5) - hash) + character;

        hash = ConvertTo32BitInt(hash);
    }
    return hash;
}

private int ConvertTo32BitInt(int value)
{
    return value & value;
}
```

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

# Other Clean Code Resources

## Other Clean Code Lists

- [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript) - Clean Code concepts adapted for JavaScript
- [clean-code-php](https://github.com/jupeter/clean-code-php) - Clean Code concepts adapted for PHP
- [clean-code-ruby](https://github.com/uohzxela/clean-code-ruby) - Clean Code concepts adapted for Ruby
- [clean-code-python](https://github.com/zedr/clean-code-python) - Clean Code concepts adapted for Python
- [clean-code-typescript](https://github.com/labs42io/clean-code-typescript) - Clean Code concepts adapted for TypeScript
- [clean-go-article](https://github.com/Pungyeon/clean-go-article) - Clean Code concepts adapted for Golang and an example how to apply [clean code in Golang](https://github.com/Pungyeon/clean-go)
- [clean-abap](https://github.com/SAP/styleguides) - Clean Code concepts adapted for ABAP
- [programming-principles](https://github.com/webpro/programming-principles) - Categorized overview of Programming Principles & Patterns
- [Elixir-Code-Smells](https://github.com/lucasvegi/Elixir-Code-Smells) - Catalog of Elixir-specific code smells
- [awesome-clean-code](https://github.com/kkisiele/awesome-clean-code) - Design principles, featured articles, tutorials, videos, code examples, blogs and books

## Style Guides
- [Google Styleguides](https://github.com/google/styleguide) - This project holds the C++ Style Guide, Swift Style Guide, Objective-C Style Guide, Java Style Guide, Python Style Guide, R Style Guide, Shell Style Guide, HTML/CSS Style Guide, JavaScript Style Guide, AngularJS Style Guide, Common Lisp Style Guide, and Vimscript Style Guide
- [Django Styleguide](https://github.com/HackSoftware/Django-Styleguide) - Django styleguide used in HackSoft projects

## Tools

- [codemaid](https://github.com/codecadwallader/codemaid) - open source Visual Studio extension to cleanup and simplify our C#, C++, F#, VB, PHP, PowerShell, JSON, XAML, XML, ASP, HTML, CSS, LESS, SCSS, JavaScript and TypeScript coding
- [Sharpen](https://github.com/sharpenrocks/Sharpen) - Visual Studio extension that intelligently introduces new C# features into your existing code base
- [tslint-clean-code](https://github.com/Glavin001/tslint-clean-code) - TSLint rules for enforcing Clean Code

## Cheatsheets

- [AspNetCoreDiagnosticScenarios](https://github.com/davidfowl/AspNetCoreDiagnosticScenarios) - Examples of broken patterns in ASP.NET Core applications
- [Clean Code](cheatsheets/Clean-Code-V2.4.pdf) - The summary of [Clean Code: A Handbook of Agile Software Craftsmanship](https://www.amazon.com/dp/0132350882) book
- [Clean Architecture](cheatsheets/Clean-Architecture-V1.0.pdf) - The summary of [Clean Architecture: A Craftsman's Guide to Software Structure and Design](https://www.amazon.com/dp/0134494164) book
- [Modern JavaScript Cheatsheet](https://github.com/mbeaudru/modern-js-cheatsheet) - Cheatsheet for the JavaScript knowledge you will frequently encounter in modern projects
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org) - Cheatsheet was created to provide a concise collection of high value information on specific application security topics
- [.NET Memory Performance Analysis](https://github.com/Maoni0/mem-doc/blob/master/doc/.NETMemoryPerformanceAnalysis.md) - This document aims to help folks who develop applications in .NET with how to think about memory performance analysis and finding the right approaches to perform such analysis if they need to. In this context .NET includes .NET Framework and .NET Core. In order to get the latest memory improvements in both the garbage collector and the rest of the framework I strongly encourage you to be on .NET Core if you are not already, because that’s where the active development happens
- [naming-cheatsheet](https://github.com/kettanaito/naming-cheatsheet) - Comprehensive language-agnostic guidelines on variables naming
- [101 Design Patterns & Tips for Developers](https://sourcemaking.com/design-patterns-and-tips)
- [Go Concurrency Guide](https://github.com/luk4z7/go-concurrency-guide)

---

# Contributors



# Backers

# Sponsors

# License

[![CC0](http://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, [thangchung](https://github.com/thangchung) has waived all copyright and related or neighboring rights to this work.
