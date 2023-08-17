# اصول کد نویسی تمیز در .NET/.NET Core

اگر پروژه clean-code-dotnet را دوست داشتید یا اگر به شما کمک کرد، لطفاً یک ستاره ⭐ برای این مخزن بدهید. این نه تنها به تقویت جامعه دات نت ما کمک می کند، بلکه مهارت های مربوط به کد نویسی تمیز را برای توسعه دهندگان دات نت در سراسر جهان بهبود می بخشد. بسیار از شما متشکرم

# فهرست محتوا
 [مفاهیم کد تمیز در .NET/.NET Core ](#clean-code-concepts-adapted-for-netnet-core)
 
 [فهرست محتوا](#فهرست-محتوا)
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
  - [قالب بندی](#قالب-بندی)
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
  <summary><b>عدم استفاده از الگوی سینگلتون Don't use a Singleton pattern</b></summary>

Singleton is an [anti-pattern](https://en.wikipedia.org/wiki/Singleton_pattern). Paraphrased from Brian Button:
الگوی Singleton یک ضد الگوی است[anti-pattern](https://en.wikipedia.org/wiki/Singleton_pattern).تفسیر از Brian Button:
1-آنها به عنوان یک **global instance** مورد استفاده قرار می گیرند ،چرا اینقدر بد است؟از آنجا که **وابستگی برنامه** را در **کد پنهان** می کنید ،به جای نمایش آنها از طریق interface ها. ایجاد چیزی global برای جلوگیری از عبور آن در اطراف بوی کد[code smell](https://en.wikipedia.org/wiki/Code_smell) است.

2-آنها اصل مسئولیت واحد [single responsibility principle](#single-responsibility-principle-srp) را نقض می کنند:**به این دلیل که آنها کنترل ایجاد و چرخه زندگی خود را کنترل می کنند.**

3-اینها ذاتاً باعث می شوند كه كد به هم اتصال محکم و سفت [coupled](https://en.wikipedia.org/wiki/Coupling_%28computer_programming%29) داشته باشند.این امر باعث می شود که در بسیاری از موارد **test آنها بسیار دشوار شود.**

4-آنها حول و حوش lifetime برنامه کاربرد دارند.ضربه دیگر به test کردن از آنجا که می توانید با شرایطی روبرو شوید که تست ها باید سفارشی شوند که به بزرگی unit test ها نیستند. چرا؟ زیرا هر تست واحد باید از دیگری مستقل باشد.
همچنین خاطرات بسیار خوبی توسط [Misko Hevery](http://misko.hevery.com/about/) در مورد ریشه مشکل[root of problem](http://misko.hevery.com/2008/08/25/root-cause-of-singletons/) وجود دارد.



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
نمونه ای از کلاس DBConnection ایجاد کنید و آن را با [Option pattern](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/configuration/options?view=aspnetcore-2.1) پیکربندی کنید.

```csharp
var options = <resolve from IOC>;
var connection = new DBConnection(options);
```

و اکنون شما باید از DBConnection در برنامه خود استفاده کنید.

**[⬆ بازگشت به بالا](#فهرست-محتوا)**

</details>

<details>
  <summary><b>آرگومان های تابع(دو یا کمتر ایده آل است) Function arguments (2 or fewer ideally)</b></summary>

محدود کردن مقدار پارامترهای تابع یا متد فوق العاده مهم است زیرا test متد شما را آسان تر می کند.داشتن بیش از سه مورد منجر به یک انفجار ترکیبی می شود که در آن باید موارد مختلفی را با هر آرگومان جداگانه test کنید.

آرگومان صفر مورد ایده آل است.یک یا دو آرگومان خوب است ،و از سه آرگومان باید اجتناب شود.هر چیزی بیشتر از این تعداد باشد باید یکی شوند.معمولاً اگر بیش از دو آرگومان داشته باشید ، متد شما در تلاش بیش از حد است.در مواردی که اینگونه نباشد ، بیشتر اوقات یک شی سطح بالاتر به عنوان یک آرگومان کافی خواهد بود.

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
  <summary><b>توابع باید یک کار را انجام دهند Functions should do one thing</b></summary>

این مهمترین قانون در مهندسی نرم افزار است.وقتی متدها بیش از یک کار را انجام دهند ، نوشتن ، آزمایش و استدلال در مورد آنها سخت تر است.هنگامی که می توانید یک عملکرد را تنها با یک عمل جدا کنید ، می توان آنها را به راحتی refactored کرد و کد شما بسیار تمیز تر خوانده می شود.اگر این راهنما را رعایت کنید، شما از بسیاری از توسعه دهندگان جلوتر خواهید بود.

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
  <summary><b>اسامی تابع باید آنچه را انجام می دهند بگویند Function names should say what they do</b></summary>

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
  <summary><b>توابع فقط باید یک سطح انتزاع داشته باشند Functions should only be one level of abstraction</b></summary>

> هنوز تمام نشده

هنگامی که بیش از یک سطح انتزاع دارید متد شما معمولاً خیلی زیاد انجام می شود.تقسیم توابع منجر به قابلیت استفاده مجدد و آزمایش آسانتر می شود.

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


ما برخی از functionality را انجام داده ایم ، اما عملکرد ()ParseBetterJSAlternative هنوز بسیار پیچیده است و قابل آزمایش نیست
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


بهترین راه حل این است که وابستگی های تابع () ParseBetterJSAlternativeرا خارج کنید.

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
  <summary><b>تابع صدا زننده و توابع فراخوانی شده باید نزدیک هم باشند Function callers and called should be close</b></summary>

اگر یک تابع، تابع دیگری را صدا می کند ، آن توابع را به صورت عمودی در فایل منبع نگه دارید.در حالت ایده آل ، متد صدا زننده را درست بالای متد فراخوانی شده نگه دارید.ما تمایل داریم مانند روزنامه کد را از بالا به پایین بخوانیم.به همین دلیل ، کد خود را به این روش بخوانید.

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
  <summary><b>کپسوله کردن شرط ها Encapsulate conditionals</b></summary>

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
  <summary><b>حذف کدهای مرده Remove dead code</b></summary>

کد مرده به همان اندازه کد تکراری بد است.هیچ دلیلی برای نگه داشتن آن در codebase شما وجود ندارد.اگر آن را صدا نمیزنید ، از شر آن خلاص شوید! اگر هنوز به آن نیاز دارید ، در version history شما ایمن خواهد بود.

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
  <summary><b>استفاده از گتر و ستر Use getters and setters</b></summary>

در C # / VB.NET می توانید کلمات کلیدی public ، protected و private را برای متدها تنظیم کنید.با استفاده از آن ، می توانید modification پراپرتی ها در یک شی را کنترل کنید.


- وقتی می خواهید کارهای دیگری فراتر از get کردن(دریافت) یک property شی انجام دهید ، لازم نیست که همه accessor را در codebase خود جستجو کنید و تغییر دهید.
- اضافه کردن اعتبارسنجی هنگام set کردن، ساده است.
- نمایش-representation داخلی را کپسوله میکند.
- هنگام get و set کردن ، اضافه کردن logging و مدیریت خطاها آسان است.
- با ارث بردن این کلاس ، می توانید عملکرد پیش فرض را override کنید.
- میتوانید پراپرتی های شی خود را lazy load کنید،بیایید بگوییم که آن را از یک سرور get می کنیم.

علاوه بر این ، این بخشی از اصل Open/Closed است (solid)، از اصول طراحی شی گرا.

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
  <summary><b>ایجاد اشیایی که را دارای اعضای خصوصی / محافظت هستند Make objects have private/protected members</b></summary>

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
  <summary><b>استفاده از زنجیره متدها Use method chaining </b></summary>

این الگوی بسیار مفید است و معمولاً در بسیاری از کتابخانه ها مورد استفاده قرار می گیرد.این اجازه می دهد تا کد شما واضح تر ، و واژگان کمتری داشته باشد.به همین دلیل ، از روش زنجیره ای استفاده کنید و نگاهی بیندازید که کد شما چقدر تمیز خواهد بود.

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
  <summary><b>ترجیح دادن ترکیب بجای وراثت Prefer composition over inheritance</b></summary>

همانطور که معروف است در الگوهای طراحی[_Design Patterns_](https://en.wikipedia.org/wiki/Design_Patterns) Design Patterns توسط Gang of Four ، شما ترکیب را بر وراثت تا جایی که می توانید ترجیح دهید.دلایل خوب زیادی برای استفاده از وراثت و دلایل خوب زیادی برای استفاده از ترکیب وجود دارد.

نکته اصلی حداکثر این است که اگر ذهن شما به طور غریزی به سمت ارث بری می رود ، سعی کنید فکر کنید که آیا ترکیب می تواند مشکل شما را بهتر مدل کند. در بعضی موارد می تواند.

ممکن است تعجب کنید ،"چه موقع باید از ارث بری استفاده کنم؟"بستگی به مشکل شما دارد ،اما این یک لیست مناسب در زمانی است که ارث بری از ترکیب بیشتر معنی می دهد:

1-وراث شما نمایانگر یک رابطه "is-a" (هست یک)است و نه یک رابطه "has-a" (دارد یک) (انسان->حیوان در مقابل کاربر->اطلاعات کاربر) (Human->Animal درمقابل User->UserDetails).
2-می توانید از کد کلاس های پایه (base classes) استفاده مجدد کنید (انسانها مانند همه حیوانات می توانند حرکت کنند).
3-شما می خواهید با تغییر یک کلاس پایه ، تغییرات global در کلاسهای مشتق شده ایجاد کنید(هزینه کالری همه حیوانات را هنگام حرکت تغییر دهید).

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

همانطور که در Clean Code بیان شده است ،"هرگز نباید بیش از یک دلیل برای تغییر کلاس وجود داشته باشد". ایجاد یک کلاس با قابلیت های زیادی وسوسه انگیز است ، مانند زمانی که فقط می توانید یک چمدان را در پرواز بگیرید.مسئله این است که کلاس شما از نظر مفهومی منسجم نخواهد بود و دلایل زیادی برای تغییر ایجاد می کند.به حداقل رساندن مقدار زمان لازم برای تغییر یک کلاس مهم است.

این مهم است زیرا اگر عملکرد(functionality) بیش از حد در یک کلاس باشد و شما یک تکه از آن را تغییر دهید ،درک این مسئله که سایر ماژولهای وابسته در codebase شما چه تاثیری خواهد داشت دشوار خواهد بود.

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
  <summary><b>اصل باز – بسته (Open/Closed Principle) (OCP)</b></summary>

همانطور که Bertrand Meyer گفته است،"موجودیت های نرم افزاری (کلاس ها ، ماژول ها ، توابع و غیره) باید برای گسترش باز اما برای اصلاح بسته باشند.". معنی این چیست؟این اصل اساساً بیان می کند که شما باید به کاربران اجازه دهید بدون تغییر کد موجود ، ویژگی های جدیدی(functionalities) اضافه کنند.

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
  <summary><b>اصل جایگزینی لیسکوف (Liskov Substitution Principle)(LSP)</b></summary>

این یک اصطلاح ترسناک برای یک مفهوم بسیار ساده است.به طور رسمی اینگونه تعریف می شود "اگر S زیر مجموعه ای از T باشد ، ممکن است اشیاء از نوع T با اشیاء از نوع S جایگزین شوند (به عنوان مثال اشیاء از نوع S می توانند اشیاء نوع T را جایگزین کنند) بدون اینکه هیچ یک از خصوصیات مطلوب آن برنامه را تغییر دهند. (از نظر درستی ، انجام کار و غیره). ". حتی این یک تعریف ترسناک است.

بهترین توضیح برای این امر، اگر کلاس parent و کلاس child دارید ،پس کلاس پایه و کلاس child بدون گرفتن نتایج نادرست قابل تعویض است.ممکن است هنوز هم گیج کننده باشد ،بنابراین اجازه دهید نگاهی به مثال کلاسیک مربع-مستطیل بیندازیم.از نظر ریاضی ، یک مربع ،مستطیل است اما اگر آن را با استفاده از مدل رابطه "is-a" (هست یک) از طریق وراثت الگوبرداری کنید ، به سرعت دچار مشکل می شوید.

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
  <summary><b>اصل تفکیک رابط‌ها (Interface Segregation Principle) (ISP)</b></summary>

اصل ISP میگوید که "Client ها نباید مجبور شوند به Interface هایی که از آنها استفاده نمی کنند وابستگی داشته باشند.".

یک مثال خوب برای نشان دادن این اصل است کلاسهایی است که به اشیاء تنظیمات بزرگ احتیاج دارند(large settings objects).عدم نیاز به clientها برای تنظیم مقدار زیادی از گزینه ها مفید است ، زیرا بیشتر اوقات به همه تنظیمات نیاز نخواهند داشت. ایجاد اختیاری آنها در جلوگیری از داشتن "رابط چاق"("fat interface") کمک می کند.

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
  <summary><b>اصل وارونگی وابستگی (Dependency Inversion Principle) (DIP)</b></summary>

این اصل دو چیز اساسی را بیان می کند:

1-ماژول های سطح بالا (High-level) نباید به ماژول های سطح پایین (low-level) بستگی داشته باشند.هر دو باید به انتزاع(abstractions) بستگی داشته باشند.

2-انتزاع (abstractions) نباید به جزئیات بستگی داشته باشد.جزئیات باید به انتزاع بستگی داشته باشد.

درک این در ابتدا دشوار است ،اما اگر با NET/.NET Core framework کار کرده اید ، شما شاهد پیاده سازی این اصل در قالب [Dependency Injection](https://martinfowler.com/articles/injection.html) (DI) هستید.در حالی که مفاهیم آنها یکسان نیستند ،DIP ماژول های سطح بالا را از دانستن جزئیات ماژول های سطح پایین و تنظیم آنها حفظ می کند.می تواند این کار را از طریق DI انجام دهد.فایده بزرگ این امر این است که اتصال بین ماژول ها را کاهش می دهد. کوپلینگ (Coupling - اتصال)یک الگوی توسعه خیلی بد است زیرا باعث می شود تا کد شما سخت refactor شود.



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
  <summary><b>خود را تکرار نکنید Don’t repeat yourself(DRY)</b></summary>
**
Try to observe the [DRY](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) principle.

  
سعی کنید اصل (https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) را رعایت کنید.**


تمام تلاش خود را بکنید تا از کپی کردن کد جلوگیری کنید.کپی تکراری بد است زیرا به این معنی است که در صورت نیاز به تغییر بخشی از منطق ، بیش از یک مکان برای تغییر چیزی وجود دارد.

تصور کنید اگر رستوران اداره می کنید و موجودی خود را پیگیری می کنید: تمام گوجه فرنگی ، پیاز ، سیر ، ادویه جات، ترشی جات و غیره.اگر چندین لیست دارید که این کار را روی آنها انجام می دهید ، باید وقتی که یک ظرف را با گوجه فرنگی سرو می کنید ، همه آنها را به روز کنید.اگر فقط یک لیست دارید ، فقط یک مکان برای به روزرسانی وجود دارد!

بیشتر اوقات شما کد تکراری دارید زیرا شما دو یا چند مورد کمی متفاوت دارید ،که کد های مشترک زیادی دارند ،اما تفاوتهای آنها شما را مجبور به داشتن دو یا چند توابع/متد مجزا می کند که بیشتر کارهای مشابه را انجام می دهند.حذف کد تکراری به معنای ایجاد انتزاعی(abstraction) است که می تواند تنها با یک تابع/ماژول/کلاس ، این مجموعه موارد مختلف را کنترل کند.

**گرفتن حق انتزاع بسیار مهم است ،به همین دلیل باید از اصول SOLID که در بخش کلاس ها [Classes](#classes) ارائه شده است پیروی کنید.انتزاع بد می تواند بدتر از کد تکراری باشد ،خیلی مراقب باشید!با گفتن این حرف ، اگر می توانید انتزاع خوبی ایجاد کنید ، این کار را انجام دهید!خود را تکرار نکنید ،در غیر این صورت خودتان را در هر زمان که می خواهید یک چیز را تغییر دهید ، به روز می کنید.**

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
  <summary><b>مفهوم پایه آزمایش کردن Basic concept of testing</b></summary>
آزمایش کردن از ارسال کد اهمیت بیشتری دارد.اگر بدون test یا test های ناکافی دارید ،بعد از هر بار که کد ارسال می کنید مطمئن نیستید که هیچ چیزی را شکستید.تصمیم گیری در مورد مقدار کافی به تیم شما بستگی دارد ،اما داشتن 100٪ پوشش (همه بخش ها و شاخه ها) به این صورت است که اعتماد به شما نفس بسیار بالا و ایجاد آرامش ذهنی توسعه دهند می کند.این بدان معنی است که علاوه بر داشتن یک چارچوب تست عالی ،شما همچنین باید از یک ابزار پوشش مناسب استفاده کنید [good coverage tool](https://docs.microsoft.com/en-us/visualstudio/test/using-code-coverage-to-determine-how-much-code-is-being-tested).

بهانه ای برای نوشتن test وجود ندارد.[pچهارچوب های تست خوب زیادی برای دات نت وجود دارد(https://github.com/thangchung/awesome-dotnet-core#testing) ،بنابراین یکی از آنها را که تیم شما ترجیح دهد پیدا کنید.وقتی کسی را پیدا کردید که برای تیم شما کار کند ،بعد هدف خود را برای همیشه به نوشتن تست برای هر ویژگی/ماژول جدیدی که معرفی می کنید ، قرار دهید.اگر روش مورد نظر شما Test Driven Development (TDD) است ،عالی است،اما نکته اصلی این است که فقط مطمئن شوید که قبل از راه اندازی هر ویژگی یا اصلاح ویژگی های موجود ، به اهداف تحت پوشش خود رسیده اید.


</details>

<details>
  <summary><b>مفهوم هر آزمون Single concept per test</b></summary>
اطمینان حاصل کند که آزمایشات شما با لیزر متمرکز است و موارد غیرمستقیم (غیر مرتبط) را آزمایش نمی کند ،استفاده از [AAA patern](http://wiki.c2.com/?ArrangeActAssert) برای تمیز تر و خوانا کردن کدها شما را مجبور می کند.
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
  <summary><b>استفاده از Async/Await</b></summary>

**خلاصه دستورالعمل های برنامه نویسی غیرهمزمان**

| Name              | Description                                       | Exceptions                      |
| ----------------- | ------------------------------------------------- | ------------------------------- |
| Avoid async void  | Prefer async Task methods over async void methods | Event handlers                  |
| Async all the way | Don't mix blocking and async code                 | Console main method (C# <= 7.0) |
| Configure context | Use `ConfigureAwait(false)` when you can          | Methods that require con­text   |

**(غیرهمزمان) Async راه انجام کارها**

| To Do This ...                           | Instead of This ...        | Use This             |
| ---------------------------------------- | -------------------------- | -------------------- |
| Retrieve the result of a background task | `Task.Wait or Task.Result` | `await`              |
| Wait for any task to complete            | `Task.WaitAny`             | `await Task.WhenAny` |
| Retrieve the results of multiple tasks   | `Task.WaitAll`             | `await Task.WhenAll` |
| Wait a period of time                    | `Thread.Sleep`             | `await Task.Delay`   |

**Best practice**

کلمات کلیدی async/await برای کارهای مرتبط با IO bound tasks (ارتباطات شبکه ای ، ارتباط بانک اطلاعاتی ، درخواست http ، و غیره) است. اما استفاده برای کارهای مرتبط computational bound tasks (چرخش از لیست عظیم ، پردازش تصاویر بزرگ و غیره) مناسب نسیت. زیرا thread نگهدارنده را به قسمت thread pool منتقل می کند و CPU/cores های موجود برای پردازش آن کارها(tasks) دخالتی ندارند.بنابراین ، ما باید از استفاده از Async/Await برای کارهای محاسباتی (computional bound tasks) خودداری کنیم.

برای رسیدگی به کارهای محاسباتی (computational bound tasks)،ترجیح می دهید از Task.Factory.CreateNew با TaskCreationOptions که LongRunning است ،استفاده کنید.این یک thread پس زمینه جدید را برای پردازش یک کار محدود محاسباتی سنگین و بدون رها کردن آن بهthread pool شروع می کند تا اینکه کار انجام شود.

**ابزار های خودت را بشناس**

چیزهای زیادی برای آموختن در مورد async و await وجود دارد و طبیعی است که کمی از منحرف شوید.در اینجا سریع به راه حل های مربوط به مشکلات رایج اشاره می شود.

**راه حل هایی برای مشکلات مشترک Async**

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


سند [Task-based Asynchronous Pattern (TAP) document](http://www.microsoft.com/download/en/details.aspx?id=19957) را بخوانید.بسیار خوب نوشته شده است ،و شامل راهنمایی در مورد طراحی API و استفاده صحیح از async / await (از جمله لغو و گزارش پیشرفت).

بسیاری از تکنیک های جدید منتظر await وجود دارد که باید به جای تکنیک های قدیمی مورد استفاده قرار گیرند.اگر در کد async جدید خود هر یک از این مثال های قدیمی را دارید ، این کار را اشتباه انجام می دهید (TM):

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
  <summary><b>مفهوم پایه مدیریت خطا Basic concept of error handling</b></summary>

خطاهای پرتاب شده چیز خوبی است!این بدان معناست که زمان اجرا با موفقیت تشخیص داده شده است که چیزی در برنامه شما اشتباه رخ داده است و به شما این امکان را می دهد تا با متوقف کردن اجرای عملکرد روی پشته (stack) فعلی ، این process را بکشید (در NET / .NET Core) ،و از طریق stack trace در کنسول به اطلاع شما می رساند.

</details>

<details>
  <summary><b>عدم استفاده از 'throw ex' در بلوک کچ Don't use 'throw ex' in catch block</b></summary>

اگر شما نیاز به پرتاب دوباره خطا بعد از به دام انداختن ان را دارید،فقط از "throw" استفاده کنید ، با استفاده از این ، شما stack trace ذخیره می کنید.اما در گزینه بد زیر ، stack trace را از دست خواهید داد.

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
  <summary><b>عدم نادیده گرفتن خطاهای گرفتار شده Don't ignore caught errors</b></summary>

انجام ندادن کاری با خطای گرفتار شده، همیشه امکان اصلاح یا واکنش نشان داده به خطای گفته شده را نمی دهد. پرتاب خطا خیلی خوب نیست چون اغلب اوقات می توانید در دریا از چیزهایی که روی کنسول چاپ می شود گم شوید.اگر هر بخشی از کد را در try/catch قرار دهید ، به این معنی است که فکر می کنید ممکن است خطایی در آنجا رخ دهد و بنابراین باید برنامه ای داشته باشید ،یا یک مسیر کد ایجاد کنید،برای وقتی اتفاق می افتد.

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
  <summary><b>استفاده از چند بلوک catch بجای استفاده از شرط ها Use multiple catch block instead of if conditions.</b></summary>

اگر شما نیاز به انجام کاری نسبت به نوع استثناء دارید ،بهتر است از بلوک چندگانه catch برای مدیریت کردن استثنا استفاده کنید.

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
  <summary><b>هنگام رخ دادن استثنا stack trace را حفظ کنید Keep exception stack trace when rethrowing exceptions</b></summary>

سی شارپ C# اجازه می دهد تا استثناء در یک catch block با استفاده از کلمه کلیدی throw دوباره مورد استفاده قرار گیرد. یک کار بد این است که یک استثناء گرفتار شده را با استفاده از throw e; پرتاپ کنید.این عبارت ردیابی پشته (stack trace) را reset می کند.بجای آن از throw; استفاده کنید.این باعث می شود ردیابی پشته حفظ شود و بینشی عمیق تر درباره این استثنا ارائه دهد.گزینه دیگر استفاده از یک استثناء سفارشی است.به سادگی نمونه سازی یک استثناء جدید و پرتاب new CustomException("some info", e); خاصیت استثنایی درونی خود را به استثناء گرفتار شده تبدیل کنید.اضافه کردن اطلاعات به استثناء یک عمل خوب است زیرا به اشکال زدایی کمک می کند.با این حال،اگر هدف این است که یک استثنا را log کنید ، از throw; استفاده کنید. برای انتقال buck به صدا زننده.

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

## قالب-بندی

<details>
  <summary><b>از فایل .editorconfig استفاده کنید.</b></summary>

 **بد:**

دارای بسیاری از سبک های قالب بندی کد در پروژه است. به عنوان مثال ، سبک تورفتگی space و tab مخلوط شده در پروژه است.

**خوب:**

با استفاده از یک فایل .editorconfig سبک کد سازگار را در codebase خود تعریف و حفظ کنید.

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
  <summary><b>خودداری از نشانگرهای موقعیتی Avoid positional markers</b></summary>

آنها معمولاً فقط سر و صدا می کنند.بگذارید توابع و نام های متغیر به همراه تورفتگی و قالب بندی مناسب ، ساختار بصری را به کد شما بدهند.

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
  <summary><b>کامنت ها را در خارج از کد اصلی قرار ندهید Don't leave commented out code in your codebase</b></summary>

کنترل نسخهVersion control به یک دلیل وجود دارد.کد قدیمی را در history بگذارید.

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
  <summary><b>کامنت ژورنالی نداشته باشید Don't have journal comments</b></summary>

به یاد داشته باشید ، از کنترل نسخه استفاده کنید! دیگر نیازی به کدهای مرده ، کد comment شده و به خصوص comment های ژورنالی نیست.برای دریافت تاریخچه از log git استفاده کنید! 

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
  <summary><b>فقط چیزهایی را کامنت کنید که پیچیدگی منطق تجاری دارند Only comment things that have business logic complexity </b></summary>

نظرات عذرخواهی است ، نه یک الزام.کد خوب اغلب خود را مستند می کند.


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

اگر یک کامنت توضیح داد که کد درحال انجام چیست ،احتمالاً این یک کامنت بی فایده است و می تواند با یک نام متغیر یا تابعی که به خوبی شناخته شده باشد ، پیاده سازی شود.کامنت در کد قبلی می تواند با تابعی به نام ConvertTo32bitInt جایگزین شود ، بنابراین این کامنت هنوز بی فایده است.با این وجود دشوار است که با کدی بیان کنید چرا توسعه دهنده الگوریتم هش djb2 را به جای sha-1 یا یک تابع هش دیگر انتخاب می کند.در این صورت یک کامنت قابل قبول است.

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
