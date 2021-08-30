# C#
#### 1. Что выведет данная программа?
Код:
  ```csharp
    public struct s
    {
        public int i { get; set; }
    }

    class Program
    {
        static void Inc(s ss)
        {
            ++ss.i;
        }

        static void Main(string[] args)
        {
            var sss = new s();
            Inc(sss);
            Console.WriteLine(sss.i);
        }
    }

  ```
#### 2. Код ниже предполагается применить, чтобы перемещать чётные элементы из одной коллекции в другую. Видите ли вы какие-то проблемы в  этом коде?
Код:
  ```csharp
var listInt = new List<int>()
            {
                1, 2, 3, 4, 3, 3, 5
            };

var listStr = new List<string>();

foreach (var elem in listInt)
    {
      if ((elem % 2) == 0)
      {
        listStr.Add(elem.ToString());
        listInt.Remove(elem);
      }
    }
  ```

#### 3. Каков будет результат работы программы?
*Примечание. Если вы не работали с Tuple, рассматривайте его как максимально примитивный дженерик, содержащий в себе то, что указано в аргументах дженерика*

Код:
  ```csharp
  var a = new Tuple<object, object, object>(1, 1, 1);
  var b = new Tuple<object, object, object>(1, 1, 1);
  Console.WriteLine(a.Item1 == b.Item1 ? "Равны" : "Не равны");
  Console.WriteLine(a.Equals(b) ? "Равны" : "Не равны");
  Console.WriteLine(a == b ? "Равны" : "Не равны");
  ```

#### 4. Каким будет результат выполнения программы?
Код:
  ```csharp
  var firstResult = numbers
                .Skip(3)
                .Select(e =>
                {
                    Console.WriteLine(e);
                    return e;
                });
            Console.WriteLine("55");

  var secondResult = firstResult
                .OrderByDescending(r => r)
                .Distinct()
                .ToList();

  foreach (var e in secondResult)
            {
                Console.WriteLine(e);
            }
  ```

#### 5. Как отработает этот код?

Код:
  ```csharp
   int i = 5;
   object o = i;
   long j = (long)o;
  ```

#### 6. Что выведут на консоль выводы метода `Foo()`?

Код:

```csharp
    public class A
    {
        public virtual void Foo()
        {
            Console.WriteLine("Class A");
        }
    }
    
    public class B : A
    {
        public virtual void Foo()
        {
            Console.WriteLine("Class B");
        }
    }
    
    public class C : B
    {
        public new void Foo()
        {
            Console.WriteLine("Class C");
        }
    }
    
    public class D : A
    {
        public new void Foo()
        {
            Console.WriteLine("Class D");
        }
    }

    public class Program
    {
        static void Main(string[] args)
        {
            B obj1 = new A();
            obj1.Foo();
            
            var obj2 = new B();
            obj2.Foo();
            
            A obj3 = new B();
            obj3.Foo();
            
            var obj4 = new C();
            obj4.Foo();
            
            A obj5 = new C();
            obj5.Foo();
            
            B obj6 = new C();
            obj6.Foo();
            
            A obj7 = new D();
            obj7.Foo();
        }
    }
```

#### 7. Произведите рефакторинг данного кода.

Код:

```csharp
public class OrderProcessor : IOrderProcessor
    {
        private SmsSender _sms;

        static OrderProccessor()
        {
            var prov = AppSettingsHelper.GetValue("Order.DefaultSMSProvider", "Megafon");
            _sms = new SmsSender(prov);
        }

        public Order Proccessor()
        {
            
        }

        public void Process(OrderRequest z)
        {
            var reserved = Reserve(HttpListenerContext.UserId, r.Number, r.Items);
            if (!reserved)
            {
                throw new Exception("Не хватает товара");
            }

            try
            {
                ProcessPayment(HttpContext.UserId, r.Total);
            }
            catch (Exception e)
            {
                CancelReservation(HttpContext.UserId, r.Number);
                throw new InvalidOperationException("Оплата не прошла");
            }

            var sms = AppSettingsHelper.GetValue("Order.SendSMS", false);
            if (sms)
            {
                string phone = FindPhoneNumber(HttpContext.UserId);
                _sms.Send("phone", $"Заказ №{r.Number} обработан!");
            }

            SendEmail(HttpContext.UserId, r.Number, r.Items, r.Total);
        }
    }
```


#### 8. Напишите на C# библиотеку для поставки внешним клиентам, которая умеет вычислять площадь круга по радиусу и треугольника по трем сторонам.

Условие:

Дополнительно к работоспособности оценим:
* Юнит-тесты;
* Легкость добавления других фигур;
* Вычисление площади фигуры без знания типа фигуры в compile-time;
* Проверку на то, является ли треугольник прямоугольным.

#### 9. Реализовать на языке C# задачу **FizzBuzz**.
Напишите программу, которая выводит на экран числа от 1 до 100. При этом вместо чисел, кратных трем, программа должна выводить слово Fizz, а вместо чисел, кратных пяти — слово Buzz. 
Если число кратно и пяти, и трем, то программа должна выводить слово FizzBuzz

#### 10. Реализовать один из сценариев на игровом поле.

Условие:

Представьте себе некое игровое поле, на котором могут располагаться игровые юниты разных типов: автомобиль(Car), танк(Tank) и забор(Fence).
Танк должен уметь двигаться(MoveCommand) и стрелять(FireCommand), машина может только двигаться(MoveCommand), а забор вообще ничего не может делать.
Теперь представим ситуацию, что вы мышкой выделили часть игрового поля и в этой выделенной части находилось некоторое колличество юнитов каждого типа.
После этого вы хотите отдать всем выделенным юнитам одну и ту же команду(например, двигайтесь(MoveCommand)).
По этой команде те юниты, которые могут двигаться(танк и автомобиль), исполняют эту команду, а те, кто не могут(забор) - игнорируют её и ничего не делают.
Следует иметь ввиду, что исполнение одной и той же команды может отличаться для разных юнитов и зависеть от их внутреннего состояния.
Например, применение одной и той же команды двигаться(MoveCommand), может завставить танк сдвинуться на 3 "клетки" влево, а машину - на 2 "клетки" вверх.

Необходимо доработать библиотеку RST.Command по следующим направлениям:
 1) Должна быть возможность создать новую команду(например, поворот(RotateCommand)) вне библиотеки RST.Command. Старые юниты не должны поддерживать новую команду.
 2) Должна быть возможность создать нового юнита(например, вертолёт), который умеет двигаться(MoveCommand) и вращаться(RotateCommand) вне библиотеки RST.Command.

Данные требование аналогичны ситуации, когда другой разработчик берёт вашу библиотеку
и пытается расширять её для своих целей не имея возможности модифицировать исходный код вашей библиотеки.

Варианты сценариев "Вариант 1" и "Вариант 2" эмулирую выделение и применение команд в группе юнитов.
Необходимо реализовать ТОЛЬКО ОДИН из приведённых ниже сценариев на ваше усмотрение.
Дорабатывать код можно по своему усмотрению.

Требования:
 1) Необходимо избегать Reflection там, где это возможно.
 2) Использовать DI контейнеры запрещено.
 3) Код избранного для реализации варианта("Вариант 1" и "Вариант 2") должен оставаться неизменным.

#### 11. Реализовать один из сценариев на игровом поле.

Условие:

Представьте себе некое игровое поле, на котором могут располагаться игровые юниты разных типов: автомобиль(Car), танк(Tank) и забор(Fence).
Танк должен уметь двигаться(MoveCommand) и стрелять(FireCommand), машина может только двигаться(MoveCommand), а забор вообще ничего не может делать.
Теперь представим ситуацию, что вы мышкой выделили часть игрового поля и в этой выделенной части находилось некоторое колличество юнитов каждого типа.
После этого вы хотите отдать всем выделенным юнитам одну и ту же команду(например, двигайтесь(MoveCommand)).
По этой команде те юниты, которые могут двигаться(танк и автомобиль), исполняют эту команду, а те, кто не могут(забор) - игнорируют её и ничего не делают.
Следует иметь ввиду, что исполнение одной и той же команды может отличаться для разных юнитов и зависеть от их внутреннего состояния.
Например, применение одной и той же команды двигаться(MoveCommand), может завставить танк сдвинуться на 3 "клетки" влево, а машину - на 2 "клетки" вверх.

Необходимо доработать библиотеку RST.Command по следующим направлениям:
 1) Должна быть возможность создать новую команду(например, поворот(RotateCommand)) вне библиотеки RST.Command. Старые юниты не должны поддерживать новую команду.
 2) Должна быть возможность создать нового юнита(например, вертолёт), который умеет двигаться(MoveCommand) и вращаться(RotateCommand) вне библиотеки RST.Command.

Данные требование аналогичны ситуации, когда другой разработчик берёт вашу библиотеку
и пытается расширять её для своих целей не имея возможности модифицировать исходный код вашей библиотеки.

Варианты сценариев "Вариант 1" и "Вариант 2" эмулирую выделение и применение команд в группе юнитов.
Необходимо реализовать ТОЛЬКО ОДИН из приведённых ниже сценариев на ваше усмотрение.
Дорабатывать код можно по своему усмотрению.

Требования:
 1) Необходимо избегать Reflection там, где это возможно.
 2) Использовать DI контейнеры запрещено.
 3) Код избранного для реализации варианта("Вариант 1" и "Вариант 2") должен оставаться неизменным.

#### 12. Отрефакторить данные код.

Код:

```csharp
public class SalaryController : Controller
    {
        [HttpGet("api/salary/ChangeSalary")]
        [RetryFilter(typeof(DataException), attempts: 3)]
        public IActionResult ChangeSalary(string userId, int delta) {
            try {
                if ((new[] {0, 6}).Contains((int) DateTime.Now.DayOfWeek) {
                    return BadRequest("Can't change salaries on weekend");
                }
 
                var da = new DataAccess("localhost:3336;password=123;catalog=production");
                var addQuery = $"UPDATE Salaries SET Salary = Salary + {delta},
                                                                UPDATED_AT = NOW() WHERE UserId = '{userId}'";
                da.ExecuteAsync(addQuery).Wait();
 
                var readQuery = $"SELECT * FROM users WHERE Id LIKE '%{userId}%'";
                dynamic found = da.ExecuteAsync(readQuery).Result.ListAll().First();
 
                da.Dispose();
                return Json(found);
            }
            catch(DataException ex) {
                //TODO: add logging here
                throw ex;
            }
        }
    }
```


# SQL

#### 1. В базе данных MS SQL Server есть продукты и категории. Одному продукту может соответствовать много категорий, в одной категории может быть много продуктов. Напишите SQL запрос для выбора всех пар «Имя продукта – Имя категории». Если у продукта нет категорий, то его имя все равно должно выводиться.

#### 2. Самые дорогие заказы (дороже 500 рублей) за определенную дату (2018-12-23), отсортированные по цене (по убыванию). Сумма заказа = сумма стоимости всех продуктов в заказе. Колонки в результате order_id, total_price.

#### 3. Суммарные продажи каждого продукта по дням, в диапазоне от 2018-12-24 до 2018-12-25. Колонки: date, product_id, sum_price. “Дырки” в датах недопустимы.
