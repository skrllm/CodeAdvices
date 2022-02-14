# Advices to writing code
## Naming rules
1) Стоит избегать неявной типизации типа ```var```.
2) Переменные должны иметь осмысленные названия.  
**```string Name``` лучше, чем ```var a```.**
3) Объекты должны иметь имена, которые легко произносить.  
**```string IntervalInMilliseconds``` лучше, чем ```string IntvrlInMs```.** 
4) Однобуквенные имена только для для локальных переменных в коротких методах.  
```
private void Keyboard_KeyUp(object sender, KeyRoutedEventArgs e)
  {
    if (e.key == VirtualKey.A)
      {
        // do something
      }
  }        
```
5) Не использовать сокращение имен.  
**```AudioGraphService``` лучше, чем ```AudioGraphSVC```.**
6) Не использовать тип переменной в названии.
7) Имена классов и объектов - имена существительные и их комбинации.  
8) Имена методов - глаголы и их комбинации.  
9) Использовать одинаковые названия методов и полей для одинаковой функциональности в разных классов.  
**Если в классах есть метод с одинаковой функциональность, например, получение экземпляра, то во всех классах его необходимо назвать одинаково - ```GetInstance().``` Потому что методы ```GetInstance()``` и ```Get()``` могут дезориентировать того, кто будет читать этот код.**
  
## Methods advices
1) Методы должны насчитывать не более 40 строк.
2) Метод должен выполнять только одну операцию.  
Метод, выполняющий одну операцию, невозможно разделить на логические секции.
3) Содержимое метода должно находиться на одном уровне абстракций.  
**Метод ниже выполняет операции на разных уровнях абстракций.**
``` 
        /// <summary>
        /// Загружает тексты.
        /// </summary>
        protected override void LoadTexts()
        {
            ///Инициализация объектов.
            ResourceLoader resourceLoader = ResourceLoader.GetForCurrentView();
            
            //Инициализация строк.
            string conditions = resourceLoader.GetString("offerConditionsUid");
            InappProduct saleProduct = _appManager.GetInappProduct(ProductType.OneMonthSale);
            string saleProductPriceString = saleProduct.PriceString;
            
            //Обновление UI.
            Conditions = string.Format(conditions, saleProduct.PriceString);
        }
```
4) Чем меньше аргументов содержит метод, тем лучше.  
Следует избегать 3-х и более аргументов.
5) Если метод принимает аргумент типа ```bool```, то стоит проверить - выполняет ли метод одну задачу.  
Если нет, то метод стоит разбить на несколько методов.
6) Стоит избегать выходных аргументов типа ```out```.
7) Метод должен либо что-то делать, либо отвечать на поставленный вопрос.
8) Обработка ```Try/catch``` должна происходить в отдельном методе.  
Если метод обрабатывает ошибки, то внутри него до и после блока ```try/catch``` не должно быть кода.
9) Следует избегать оператора ```goto```.

## Comments and documentation advices
1) «Не комментируйте плохой код — перепишите его» — Брайан Керниган.
2) Информация, которую несет комментарий, должна быть исчерпыващей и понятной.  После прочтения комментария не должно оставаться вопросов.
3) Комментарий должен быть максимально краток и четок.
4) Необходимо удалять закомментированный код.
5) Необходимо оставлять комментарии к логическим элементам в разметке (```XAML```, ```HTML```) т.к. по ним проще ориентироваться в документе.
6) Комментарий должен быть утверждением.
7) Необходимо документировать классы, конструкторы, методы, переменные и автосвойства. 
8) Если необходим рефакторинг или реализация фичи, которую в данный момент нет возможности выполнить - необходимо отставить ```TODO``` комментарий.
9) Необходимо комментировать неочевидные проблемы, которые решает код.

## General advices
- Проверять и документировать код перед каждым коммитом и Merge Request-ом.
- ```DRY``` принцип (Don’t repeat yourself - не повторяйся) - В коде не должно быть повторений логики, иначе при измении логики, придется делать изменения в нескольких местах.
- ```KISS``` принцип (Keep it simple stupid- Делай проще, тупица) - Код должен оставаться простым для понимания и дальнейшего раcширения.
- ```YAGNI``` принцип (You aren't gonna need it - Тебе это не понадобится) - В коде не должно быть неиспользуемых строк, методов, классов, ненужной документации.
