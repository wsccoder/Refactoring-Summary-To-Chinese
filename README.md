这是一篇《重构 》的总结 ，我在学习的同时并使用它作为参考。这不是一本书的替代品，所以你要想真的想学习里面的内容，买一本书使用这个文章作为参考和指南。

另外： 建议 评论 还 PR 都是十分欢迎的

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

# 1. TABLE OF CONTENT 
# 1. 内容目录
- [1. TABLE OF CONTENT](#1-table-of-content)
- [3. BAD SMELLS IN CODE](#3-bad-smells-in-code)
	- [1. Duplicated code（重复的代码）](#1-duplicated-code-重复的代码)
	- [2. Long Method（很长的方法）](#2-long-method-很长的方法)
	- [3. arge Classes（超级大的类）](#3-large-classes-超级大的类)
	- [4. Long Parameter List(长参数列表)](#4-long-parameter-list-长参数列表)
	- [5. Divergent Change（发散的改变）](#5-divergent-change-发散的改变)
	- [6. Shotgun Surgery（散弹枪修改）](#6-shotgun-surgery-散弹枪修改)
	- [7. Feature Envy（依恋情结）](#7-feature-envy-依恋情结)
	- [8. Data Clumps（数据泥团）](#8-data-clumps-数据泥团)
	- [9. Primitive Obsession（基本类型偏执）](#9-primitive-obsession-基本类型偏执)
	- [10. Switch Statements（Switch 惊悚现身）](#10-switch-statements-Switch 惊悚现身)
	- [11. Parallel Inheritance Hierarchies（平行继承类）](#11-parallel-inheritance-hierarchies-平行继承类)
	- [12. Lazy Class（冗余类）](#12-lazy-class-冗余类)
	- [13. Speculative Generality（夸夸其谈未来性）](#13-speculative-generality-夸夸其谈未来性)
	- [14. Temporary Field（令人迷惑的临时变量）](#14-temporary-field-令人迷惑的临时变量)
	- [15. Message Chain（过长的消息链）](#15-message-chain-过长的消息链)
	- [16. Middle Man（中间人）](#16-middle-man-中间人)
	- [17. Inappropriate Intimacy（不恰当的亲密关系）](#17-inappropriate-intimacy-不恰当的亲密关系)
	- [18. Alternative Classes with Different Interfaces（异曲同工的类）](#18-alternative-classes-with-different-interfaces-异曲同工的类)
	- [19. Incomplete Library Class （不完美的库）](#19-incomplete-library-class-不完美的库)
	- [20. Data Class（数据类](#20-data-class-数据类)
	- [21. Refused Bequest（被拒绝的遗赠）](#21-refused-bequest-被拒绝的遗赠)
	- [22. Comments （过多没用的注释）](#22-comments-过多没用的注释)
- [6. COMPOSING METHODS](#6-composing-methods)
	- [1. Extract Method](#1-extract-method)
	- [2. Inline Method](#2-inline-method)
	- [3. Inline Temp](#3-inline-temp)
	- [4. Replace Temp with Query](#4-replace-temp-with-query)
	- [5. Introduce Explaining Variable](#5-introduce-explaining-variable)
	- [6. Split Temporary Variable](#6-split-temporary-variable)
	- [7. Remove Assignments to Parameters](#7-remove-assignments-to-parameters)
	- [8. Replace Method with Method Object](#8-replace-method-with-method-object)
	- [9. Substitute Algorithm](#9-substitute-algorithm)
- [7. Moving features between elements](#7-moving-features-between-elements)
	- [10. Move method](#10-move-method)
	- [11. Move field](#11-move-field)
	- [12. Extract Class](#12-extract-class)
	- [13. Inline Class](#13-inline-class)
	- [14. Hide Delegate](#14-hide-delegate)
	- [15. Remove Middle Man](#15-remove-middle-man)
	- [16. Introduce Foreign Method](#16-introduce-foreign-method)
	- [17. Introduce Local Extension](#17-introduce-local-extension)
- [8. ORGANIZING DATA](#8-organizing-data)
	- [18. Self Encapsulate Field](#18-self-encapsulate-field)
	- [19. Replace Data Value with Object](#19-replace-data-value-with-object)
	- [20. Change Value to Reference](#20-change-value-to-reference)
	- [21. Change Reference to Value](#21-change-reference-to-value)
	- [22. Replace Array with Object](#22-replace-array-with-object)
	- [23. Duplicate Observed Data](#23-duplicate-observed-data)
	- [24. Change Unidirectional Association to Bidirectional](#24-change-unidirectional-association-to-bidirectional)
	- [25. Change Bidirectional Association to Unidirectional](#25-change-bidirectional-association-to-unidirectional)
	- [26. Replace Magic Number with Symbolic Constant](#26-replace-magic-number-with-symbolic-constant)
	- [27. Encapsulate Field](#27-encapsulate-field) 
	- [28. Encapsulate Collection](#28-encapsulate-collection)
	- [29. Remove Record with data class](#29-remove-record-with-data-class)
	- [30. Replace Type Code with Class](#30-replace-type-code-with-class)
	- [31. Replace Type Code with Subclasses](#31-replace-type-code-with-subclasses)
	- [32. Replace Type Code with State/Strategy](#32-replace-type-code-with-statestrategy)
	- [32. Replace Subclass with Fields](#32-replace-subclass-with-fields)
- [9. SIMPLIFYING CONDITIONAL EXPRESSIONS](#9-simplifying-conditional-expressions)
	- [33. Decompose Conditional](#33-decompose-conditional)
	- [34. Consolidate Conditional Expression](#34-consolidate-conditional-expression)
	- [35. Consolidate Duplicate Conditional Fragments](#35-consolidate-duplicate-conditional-fragments)
	- [36. Remove Control Flag](#36-remove-control-flag)
	- [37. Replace Nested Conditional with Guard Clauses](#37-replace-nested-conditional-with-guard-clauses)
	- [38. Replace Conditional with Polymorphism](#38-replace-conditional-with-polymorphism)
	- [39. Introduce Null Object](#39-introduce-null-object)
	- [40. Introduce Assertion](#40-introduce-assertion)
- [10. MAKING METHOD CALLS SIMPLER](#10-making-method-calls-simpler)
	- [41. Rename method](#41-rename-method)
	- [42. Add Parameter](#42-add-parameter)
	- [43. Remove Parameter](#43-remove-parameter)
	- [44. Separate Query from Modifier](#44-separate-query-from-modifier)
	- [45. Parameterize Method](#45-parameterize-method)
	- [46. Replace Parameter with Explicit Methods](#46-replace-parameter-with-explicit-methods)
	- [47. Preserve Whole Object](#47-preserve-whole-object)
	- [48. Replace Parameter with Method](#48-replace-parameter-with-method)
	- [49. Introduce Parameter Object](#49-introduce-parameter-object)
	- [50. Remove Setting Method](#50-remove-setting-method)
	- [51. Hide Method](#51-hide-method)
	- [52. Replace Constructor with Factory Method](#52-replace-constructor-with-factory-method)
	- [53. Encapsulate Downcast](#53-encapsulate-downcast)
	- [54. Replace Error Code with Exception](#54-replace-error-code-with-exception)
	- [55. Replace Exception with Test](#55-replace-exception-with-test)
- [11. DEALING WITH GENERALIZATION](#11-dealing-with-generalization)
	- [56. Pull up field](#56-pull-up-field)
	- [57. Pull Up Method](#57-pull-up-method)
	- [58. Pull Up Constructor Body](#58-pull-up-constructor-body)
	- [59. Push Down Method](#59-push-down-method)
	- [60. Push Down Field](#60-push-down-field)
	- [61. Extract Subclass](#61-extract-subclass)
	- [62. Extract Superclass](#62-extract-superclass)
	- [63. Extract Interface](#63-extract-interface)
	- [64. Collapse Hierarchy](#64-collapse-hierarchy)
	- [65. Form Template Method](#65-form-template-method)
	- [66. Replace Inheritance with Delegation](#66-replace-inheritance-with-delegation)
	- [67. Replace Delegation with Inheritance](#67-replace-delegation-with-inheritance)
- [12. BIG REFACTORINGS](#12-big-refactorings)
	- [68. Tease Apart Inheritance](#68-tease-apart-inheritance)
	- [69. Convert Procedural Design to Objects](#69-convert-procedural-design-to-objects)
	- [70. Separate Domain from Presentation](#70-separate-domain-from-presentation)
	- [71. Extract Hierarchy](#71-extract-hierarchy)

<!-- /TOC -->

# 3. BAD SMELLS IN CODE（代码的坏味道）
### 1. Duplicated code （重复的代码）
多个地方使用相同的代码

### 2. Long Method（很长的方法）
一个很长的程序是很难被理解的

### 3. Large Classes（超级大的类）
当一个类变的越来越大的时候，是难以阅读的

### 4. Long Parameter List(长参数列表)
长参数是很难去理解，不符合也较难使用

### 5. Divergent Change（发散的改变）
当一个类经常因为不同原因发生在不同的方向发生变化

### 6. Shotgun Surgery（散弹枪修改）
每次你做一小部分修改时，都不的不需要做大量的修改在很多不同的类中

### 7. Feature Envy（依恋情结）
某个方法似乎在另外的类的兴趣高于自己所处的类

### 8. Data Clumps（数据泥团）
一堆数据杂糅在一起（字段， 参数）

### 9. Primitive Obsession（基本类型偏执）
使用基本类型替代小对象

### 10. Switch Statements（Switch 惊悚现身）
当程序中出现很多 switch 语句在很多地方，使用多态来进行替换

### 11. Parallel Inheritance Hierarchies（平行继承类）
每当你为一个类增加一个子类，你不得不为另一个类增加相应的一个子类

### 12. Lazy Class（冗余类）
当一个类不足与为其自身买单它就应该被删除

### 13. Speculative Generality（夸夸其谈未来性）
所有的钩子和特殊情况处理那些不需要的

### 14. Temporary Field（令人迷惑的临时变量）
一个临时变量仅仅为某种特殊情况做而定，这样的代码让人难以理解

### 15. Message Chain（过长的消息链）
当一个类请求调用一个对象，但是这个类又在调用其他的方法

### 16. Middle Man（中间人）
当一个对象委托大部分功能，开发中可能会过度的使用委托模式，导致某个类中的方法大都委托给其他方法处理

### 17. Inappropriate Intimacy（不恰当的亲密关系）
当两个类过度的亲密，需要将其拆散

### 18. Alternative Classes with Different Interfaces（异曲同工的类）
类的方法过度相似

### 19. Incomplete Library Class（不完美的库）
当我们使用外部依赖库时

### 20. Data Class（数据类）
不要操作数据类，我们通过封装它的不变性

### 21. Refused Bequest（被拒绝的遗赠）
子类不想使用父类的方法

### 22. Comments（过多没用的注释）
当一个方法使用过度的注释解释其中的逻辑时，说明这个方法应该被重构了。

# 6. COMPOSING METHODS(重新组织函数))
## 1. Extract Method（提炼函数）
你可以将一些代码组合起来，然后放到一个方法中
```java

	void printOwing(double amount) {
		printBanner();
		//print details
		System.out.println ("name:" + _name);
		System.out.println ("amount" + amount);
	}
```

to

```java

	void printOwing(double amount) {
		printBanner();
		printDetails(amount);
	}

	void printDetails (double amount) {
		System.out.println ("name:" + _name);
	System.out.println ("amount" + amount);
	}
```

**动机**
* 增加代码被复用的机会 
* 阅读方法就像阅读一系列声明一样简单

```java

	void printOwing(double previousAmount) {
		Enumeration e = _orders.elements();
		double outstanding = previousAmount * 1.2;
		printBanner();

		// calculate outstanding
		while (e.hasMoreElements()) {
			Order each = (Order) e.nextElement();
			outstanding += each.getAmount();
		}
		printDetails(outstanding);
	}
```

to

```java

	void printOwing(double previousAmount) {
		printBanner();
		double outstanding = getOutstanding(previousAmount * 1.2);
		printDetails(outstanding);
	}

	double getOutstanding(double initialValue) {
		double result = initialValue;
		Enumeration e = _orders.elements();

		while (e.hasMoreElements()) {
			Order each = (Order) e.nextElement();
			result += each.getAmount();
		}
		return result;
	}
```

## 2. Inline Method （内联函数）
一个函数本体和函数名称一样容易理解

```java

	int getRating() {
		return (moreThanFiveLateDeliveries()) ? 2 : 1;
	}

	boolean moreThanFiveLateDeliveries() {
		return _numberOfLateDeliveries > 5;
	}
```

to

```java

	int getRating() {
		return (_numberOfLateDeliveries > 5) ? 2 : 1;
	}
```
**动机**

* 当间接不是必要的时候
* 当一组方法被严格的分解，会使这个方法变得清晰

## 3. Inline Temp （内联临时变量）
你申明了一个临时的变量在一段表达里面，然后临时的变量将会阻挡你重构

```java

	double basePrice = anOrder.basePrice();
	return (basePrice > 1000)
```

to

```java

	return (anOrder.basePrice() > 1000)
```
**Motivation**

* Use it with [4. Replace Temp with Query](#4-replace-temp-with-query)
* 使用这个 [4. Replace Temp with Query](#4-replace-temp-with-query)

## 4. Replace Temp with Query （以查询取代临时变量）
你正在使用临时变量来保存表达式的结果

```java

	double basePrice = _quantity * _itemPrice;
	if (basePrice > 1000){
		return basePrice * 0.95;
	}
	else{
		return basePrice * 0.98;
	}
```
to

```java

	if (basePrice() > 1000){
		return basePrice() * 0.95;
	}
	else{
		return basePrice() * 0.98;
	}
	...
	double basePrice() {
		return _quantity * _itemPrice;
	}
```

**动机**

* 使用方法代替临时变量，类中的任何方法都可以获取信息
* 这是一个十分重要的步骤在其之前[1. Extract Method](#1-extract-method)

## 5. Introduce Explaining Variable （引入解释性变量）

有一个复杂的表达式
```java

	if ( (platform.toUpperCase().indexOf("MAC") > -1) &&
		(browser.toUpperCase().indexOf("IE") > -1) &&
		wasInitialized() && resize > 0 )
	{
		// do something
	}
```
to

```java

	final boolean isMacOs = platform.toUpperCase().indexOf("MAC") >-1;
	final boolean isIEBrowser = browser.toUpperCase().indexOf("IE") >-1;
	final boolean wasResized = resize > 0;
	if (isMacOs && isIEBrowser && wasInitialized() && wasResized) {
		// do something
	}

```

**动机**

* 当一个表达式难以理解时

## 6. Split Temporary Variable （分解临时变量）
你能有一个临时变量声明不止一次，但是它不是循环体中的变量或者要被存储的变量
```java

	double temp = 2 * (_height + _width);
	System.out.println (temp);
	temp = _height * _width;
	System.out.println (temp);
```
to
```java

	final double perimeter = 2 * (_height + _width);
	System.out.println (perimeter);
	final double area = _height * _width;
	System.out.println (area);
```

**动机**

* 变量不应该有多次的声明
* 使用临时变量在两次不同的地方，是阅读者十分迷惑的

## 7. Remove Assignments to Parameters（移除对参数的赋值）
下的代码将对参数进行了赋值
```java

	int discount (int inputVal, int quantity, int yearToDate) {
		if (inputVal > 50) {
			inputVal -= 2;
		}
	}
```
to
```java

	int discount (int inputVal, int quantity, int yearToDate) {
		int result = inputVal;
		if (inputVal > 50) {
			result -= 2;
		}
	}
```

**动机**

* 改变内部的对象时可以的，但是不能将这个对象指向别的对象
* 参数的作用仅仅是表达传递对象

## 8. Replace Method with Method Object （以函数对象取代函数）
将这个函数放进一个单独的对象，如此一来局部变量就变成对象内部的字段，然后你可以在同一个对象中将这个大型函数分解为多个小型函数
```java

	class Order...
		double price() {
			double primaryBasePrice;
			double secondaryBasePrice;
            double tertiaryBasePrice;
            // long computation;
			...
		}
```
to
```java

	class Order...
		double price(){
			return new PriceCalculator(this).compute()
		}
	}

	class PriceCalculato...
	compute(){
		double primaryBasePrice;
		double secondaryBasePrice;
		double tertiaryBasePrice;
		// long computation;
		return ...
	}

```

**动机**

* 当一个方法有很多的本地变量时进行分解时不容易的

_它的样本本不应该这样的重构，但是为显示这样做的方法_
```java

	Class Account
		int gamma (int inputVal, int quantity, int yearToDate) {
			int importantValue1 = (inputVal * quantity) + delta();
			int importantValue2 = (inputVal * yearToDate) + 100;
			if ((yearToDate - importantValue1) > 100)
			importantValue2 -= 20;
			int importantValue3 = importantValue2 * 7;
			// and so on.
			return importantValue3 - 2 * importantValue1;
		}
	}
```
to
```java

	class Gamma...
		private final Account _account;
		private int inputVal;
		private int quantity;
		private int yearToDate;
		private int importantValue1;
		private int importantValue2;
		private int importantValue3;

		Gamma (Account source, int inputValArg, int quantityArg, int yearToDateArg) {
			_account = source;
			inputVal = inputValArg;
			quantity = quantityArg;
			yearToDate = yearToDateArg;
		}

		int compute () {
			importantValue1 = (inputVal * quantity) + _account.delta();
			importantValue2 = (inputVal * yearToDate) + 100;
			if ((yearToDate - importantValue1) > 100)
			importantValue2 -= 20;
			int importantValue3 = importantValue2 * 7;
			// and so on.
			return importantValue3 - 2 * importantValue1;
		}

		int gamma (int inputVal, int quantity, int yearToDate) {
			return new Gamma(this, inputVal, quantity,yearToDate).compute();
		}
```

## 9. Substitute Algorithm (算法替换)
你想更换一个更为清晰高效的算法

```java

	String foundPerson(String[] people){
		for (int i = 0; i < people.length; i++) {
			if (people[i].equals ("Don")){
				return "Don";
			}
			if (people[i].equals ("John")){
				return "John";
			}
			if (people[i].equals ("Kent")){
				return "Kent";
			}
		}
		return "";
	}
```
to
```java

	String foundPerson(String[] people){
		List candidates = Arrays.asList(new String[] {"Don", "John","Kent"});
	for (int i = 0; i<people.length; i++)
		if (candidates.contains(people[i]))
			return people[i];
	return "";
	}
```

**动机**

* 打破一些复杂的概念
* 使算法更容易修改
* 替换一个大的复杂的算法是十分困难的，让算法变的简单更容易对算法进行替换


# 7. Moving features between elements（移动对象）
## 10. Move method （移动方法）
在进行方法的初始定义的时候要想下以后会不会有其他的类也将会用到它

_一个类它通常会创建一个新的简单的方法体， 同时它会将9⃣旧的方法做一个简单的委托或者移除它_
```java

	class Class1 {
		aMethod()
	}

	class Class2 {	}
```
to


```java

	class Class1 {	}

	class Class2 {
		aMethod()
	}
```

**动机**

当一个类做了很多工作，或者这个类过度的耦合

## 11. Move field （移动字段）
当一个字段被定义的时候，可能不仅被不止一个类使用。
_创建一个字段在一个目标类中，然后改变所有的拥有者 _

```java

	class Class1 {
		aField
	}

	class Class2 {	}
```
to


```java

	class Class1 {	}

	class Class2 {
		aField
	}
```

**动机**

如果一个字段被超过多个类引用 


## 12. Extract Class （提取类）
你有一个类，但是这个类做了它份外的事情

_创建一个新的类，然后将相关字段移入到新的类中 _

```java

	class Person {
		name,
		officeAreaCode,
		officeNumber,
		getTelephoneNumber()
	}
```
to
```java

	class Person {
		name,
		getTelephoneNumber()
	}

	class TelephoneNumber {
		areaCode,
		number,
		getTelephoneNumber()
	}
```

**动机**

类随着业务的增长在变化

_在合适的时候进行分解它_

* 相似的方法组合在一起
* 数据子集通常一起变化或者相互依赖

## 13. Inline Class （一致的类）
一个其实没做多少事情的类

_将这个类整合到另外一个类中，然后删除这个类 _
```java

	class Person {
		name,
		getTelephoneNumber()
	}

	class TelephoneNumber {
		areaCode,
		number,
		getTelephoneNumber()
	}
```
to
```java

	class Person {
		name,
		officeAreaCode,
		officeNumber,
		getTelephoneNumber()
	}
```


**动机**

在重构的时候将这个类的基本信息移入到另外一个类中，然后在移除这个类

## 14. Hide Delegate （隐藏委托）
客户端其实调用的是对象的委托类
_在服务端创建一个方法，然后隐藏这个委托类_
```java

	class ClientClass {
		//Dependencies
		Person person = new Person()
		Department department = new Department()
		person.doSomething()
		department.doSomething()
	}
```
to
```java

	class ClientClass {
		Person person = new Person()
		person.doSomething()
	}

	class Person{
		Department department = new Department()
		department.doSomething()
	}
```

_解决方法_
```java

	class ClientClass{
		Server server = new Server()
		server.doSomething()
	}

	class Server{
		Delegate delegate = new Delegate()
		void doSomething(){
			delegate.doSomething()
		}
	}
	//委托类其实隐藏在客户类里面
	// 改变不会传播到客户端那边，因为它之后影响到服务端这边
	class Delegate{
		void doSomething(){...}
	}

```

**动机**

*关键在于封装*
*类应该尽量的使用其他的类*
`> manager = john.getDepartment().getManager();`
```java



	class Person {
		Department _department;
		public Department getDepartment() {
			return _department;
		}
		public void setDepartment(Department arg) {
			_department = arg;
			}
		}

	class Department {
		private String _chargeCode;
		private Person _manager;
		public Department (Person manager) {
			_manager = manager;
		}
		public Person getManager() {
			return _manager;
		}
		...
```
to

`> manager = john.getManager();`
```java

	class Person {
		...
		public Person getManager() {
			return _department.getManager();
		}
	}
```

## 15. Remove Middle Man （移除中间人）
一个类通过代理干了太多的事情
_让客户直接调用委托_
```java

	class ClientClass {
		Person person = new Person()
		person.doSomething()
	}

	class Person{
		Department department = new Department()
		department.doSomething()
	}
```
to

```java

	class ClientClass {
		//Dependencies
		Person person = new Person()
		Department department = new Department()
		person.doSomething()
		department.doSomething()
	}
```


**动机**

当客户类使用过多的中间人调用委托的方法

## 16. Introduce Foreign Method （引入外加的函数）
一个类是引用的外部开源包，但是不能修改其内部的逻辑
_创建一个新的方法在这个类中，并以第一个参数的形式传入一个服务类实例_

```java

	Date newStart = new Date(previousEnd.getYear(),previousEnd.getMonth(),previousEnd.getDate()+1);
```
to
```java

	Date newStart = nextDay(previousEnd);

	private static Date nextDay(Date date){
		return new Date(date.getYear(),date.getMonth(),date.getDate()+1);
	}
```

**动机**

当你使用一个类，这个类你又不能对其进行修改的时候可以采用这样方式


## 17. Introduce Local Extension （引入本地扩展）
你需要为一个服务类提供一些额外的方法，但是你无法修改这个子类
_创建一个新的类，使它包含这些额外的方法。这个扩展的类成为源类的子类或者包装类_
```java

	class ClientClass(){

		Date date = new Date()
		nextDate = nextDay(date);

		private static Date nextDay(Date date){
			return new Date(date.getYear(),date.getMonth(),date.getDate()+1);
		}
	}
```
to
```java

	class ClientClass() {
		MfDate date = new MfDate()
		nextDate = nextDate(date)
	}
	class MfDate() extends Date {
		...
		private static Date nextDay(Date date){
			return new Date(date.getYear(),date.getMonth(),date.getDate()+1);
		}
	}
```

**动机**

当我们使用 [16. Introduce Foreign Method](#16-introduce-foreign-method) 我们需要在这个类中添加额外的方法

# 8. ORGANIZING DATA （组织数据）
## 18. Self Encapsulate Field （对字段获取进行封装）
你可以直接获取对象，但是这样的话会变得越来越复杂
_通过创建setting getting 方法来获取这些字段_
```java

	private int _low, _high;
	boolean includes (int arg) {
		return arg >= _low && arg <= _high;
	}
```
to

```java

	private int _low, _high;
	boolean includes (int arg) {
		return arg >= getLow() && arg <= getHigh();
	}
	int getLow() {return _low;}
	int getHigh() {return _high;}
```

**动机**  

允许子类可以覆盖如何get方法，并且这样的话它更加的支持灵活的管理，例如延迟加载

## 19. Replace Data Value with Object （用对象替换数据值）
当你有个数据项需要进行添加数据或行为
_将数据项转换为对象_

```java

	class Order...{
		private String _customer;
		public Order (String customer) {
			_customer = customer;
		}
	}
```
to
```java

	class Order...{
		public Order (String customer) {
			_customer = new Customer(customer);
		}
	}

	class Customer {
		public Customer (String name) {
			_name = name;
		}
	}
```
**动机**  
简单的数据对象并不简单

## 20. Change Value to Reference （将值改为引用）
你有个类拥有很多单个对象，这些对象需要用一个单独的对象替代 
_将这个对象转换为引用对象_
```java

	class Order...{
		public Order (String customer) {
			_customer = new Customer(customer);
		}
	}

	class Customer {
		public Customer (String name) {
			_name = name;
		}
	}
```
to
```java

	//Use Factory Method
	//使用工厂方法
	class Customer...
		static void loadCustomers() {
			new Customer ("Lemon Car Hire").store();
			new Customer ("Associated Coffee Machines").store();
			new Customer ("Bilston Gasworks").store();
		}
		private void store() {
			_instances.put(this.getName(), this);
		}
		public static Customer create (String name) {
			return (Customer) _instances.get(name);
		}
```
**动机**  
引用对象是类似于消费者或者账单这样的对象，每个对象代表这一类对象在一个真实的世界，并使用对象表示来测试它们是否相同

## 21. Change Reference to Value （将引用改为值）
你有一个有一个引用对象是很小，不变，难以管理的
_将其转换为值对象_
```java

	new Currency("USD").equals(new Currency("USD")) // returns false
```
to
```java

	new Currency("USD").equals(new Currency("USD")) // now returns true
```
**动机**  
使用引用对象是变得越来月复杂，并且引用对象是不变和单一的。尤其在分布式和并发系统中

## 22. Replace Array with Object （用对象代替数组）
_你拥有一个数组，其中这些元素是不同的_
_使用一个对象来替换这个数组，将数组的元素赋值在对象的属性上_
```java

	String[] row = new String[3];
	row [0] = "Liverpool";
	row [1] = "15";
```
to
```java

	Performance row = new Performance();
	row.setName("Liverpool");
	row.setWins("15");
```
**动机**  

数组应该被用在一些相似的集合对象序列中

## 23. Duplicate Observed Data （监控数据对象）
可能你有一些domain数据是通过GUI控制的与此同时这些domain数据是需要访问的
_往一些实体对象复制一些数据，通过设置观察者来同步两部分数据_

**动机**  
为了将代码从用户界面分解到业务处理层

## 24. Change Unidirectional Association to Bidirectional（将单向联系改为双向联系）
你有两个对象，这两个对象需要使用对方的特征属性，但是目前只有一种连接方式
_添加返回指针，然后更改修饰符已更改两个对象_
```java

	class Order...
		Customer getCustomer() {
			return _customer;
		}
		void setCustomer (Customer arg) {
			_customer = arg;
		}
		Customer _customer;
	}
```
to
```java

	class Order...
		Customer getCustomer() {
			return _customer;
		}
		void setCustomer (Customer arg) {
			if (_customer != null) _customer.friendOrders().remove(this);
			_customer = arg;
			if (_customer != null) _customer.friendOrders().add(this);
		}
		private Customer _customer;

		class Customer...
			void addOrder(Order arg) {
				arg.setCustomer(this);
			}
			private Set _orders = new HashSet();

			Set friendOrders() {
				/** should only be used by Order */
				return _orders;
			}
		}
	}

	// Many to Many
	class Order... //controlling methods
		void addCustomer (Customer arg) {
			arg.friendOrders().add(this);
			_customers.add(arg);
		}
		void removeCustomer (Customer arg) {
			arg.friendOrders().remove(this);
			_customers.remove(arg);
		}
	class Customer...
		void addOrder(Order arg) {
			arg.addCustomer(this);
		}
		void removeOrder(Order arg) {
			arg.removeCustomer(this);
		}
	}
```
**动机**  
当对象引用需要互相引用的时候，你应该采用这种方法

## 25. Change Bidirectional Association to Unidirectional （将单向改为双向的联系）
当你有个双向联系的类，但是在后期一个类不在需要另一个类中的属性了
_扔掉不需要的联系_

**动机**  
当双向联系不在需要，减少复杂度，移除僵尸对象，消除相互依赖

## 26. Replace Magic Number with Symbolic Constant （使用符号来替代魔法字符串）
你有一个特定含义的字符串

_创建一个常量，名称根据它的意思命名然后替换那个数字_
```java

	double potentialEnergy(double mass, double height) {
		return mass * 9.81 * height;
	}
```
to
```java

	double potentialEnergy(double mass, double height) {
		return mass * GRAVITATIONAL_CONSTANT * height;
	}
	static final double GRAVITATIONAL_CONSTANT = 9.81;
```
**动机**  
避免使用魔法数字

## 27. Encapsulate Field  （封装字段）
这里有一个公共的字段
_将它改为私有的并提供访问函数_
```java

	public String _name
```
to
```java

	private String _name;
	public String getName() {
		return _name;
	}
	public void setName(String arg) {
		_name = arg;
	}
```
**动机**  
你应该将你数据公开

## 28. Encapsulate Collection （封装集合）
一个返回几个的方法
_确保返回一个只读的影像对象，然后提供添加和移除方法_
```java

	class Person {
		Person (String name){
			HashSet set new HashSet()
		}
		Set getCourses(){}
		void setCourses(:Set){}
	}
```
to
```java

	class Person {
		Person (String name){
			HashSet set new HashSet()
		}
		Unmodifiable Set getCourses(){}
		void addCourses(:Course){}
		void removeCourses(:Course){}
	}
```
**动机**   
* 封装减少了拥有类和和其客户端的耦合
* getter 方法不应该返回集合的本身
* getter方法应返回对集合进行操作的内容并隐藏其中不必要的细节
* 这个几个不应该有setter方法，只能添加和移除操作

## 29. Remove Record with data class (在数据类中移除 记录值)
你必须面对一个记录值在传统的编程环境中
_使用一个僵尸数据对象代替记录值_

**动机**  
* 复制一个传奇代码
* 使用传统的API编程和数据库来代替一个记录值

## 30. Replace Type Code with Class (使用类来替代类别代码)
一个类拥有数字类别码，不能影响其行为  
_使用类来代替数字_
```java

	class Person{
		O:Int;
		A:Int;
		B:Int;
		AB:Int;
		bloodGroup:Int;
	}
```
to
```java

	class Person{
		bloodGroup:BloodGroup;
	}

	class BloodGroup{
		O:BloodGroup;
		A:BloodGroup;
		B:BloodGroup; 
		AB:BloodGroup;
	}
```
**动机**    
静态类别检查

## 31. Replace Type Code with Subclasses （使用子类来替代类别代码）
在一个类中拥有一个不变的类型码影响整个类的行为  
_使用子类来替代这个不变的类型码_
```java

	class Employee...
		private int _type;

		static final int ENGINEER = 0;
		static final int SALESMAN = 1;
		static final int MANAGER = 2;

		Employee (int type) {
			_type = type;
		}
	} 
```
to
```java

	abstract int getType();
	static Employee create(int type) {
		switch (type) {
			case ENGINEER:
				return new Engineer();
			case SALESMAN:
				return new Salesman();
			case MANAGER:
				return new Manager();
			default:
				throw new IllegalArgumentException("Incorrect type code value");
		}
	}
```
**动机**  

* 执行不同的代码逻辑取决于这个type的值
* 当每个type对象有着唯一的特征
* 应用于架构体

## 32. Replace Type Code with State/Strategy（通过状态模式或者策略模式来代替类型码）
在类中有个类型码，并通过这个类型码来影响行为，但是你不能使用子类 
_通过状态对象来代替这个类型码_
```java

	class Employee {
		private int _type;

		static final int ENGINEER = 0;
		static final int SALESMAN = 1;
		static final int MANAGER = 2;

		Employee (int type) {
			_type = type;
		}
		int payAmount() {
			switch (_type) {
				case ENGINEER:
					return _monthlySalary;
				case SALESMAN:
					return _monthlySalary + _commission;
				case MANAGER:
					return _monthlySalary + _bonus;
				default:
					throw new RuntimeException("Incorrect Employee");
				}
			}
		}
	}
```
to
```java

	class Employee...
		static final int ENGINEER = 0;
		static final int SALESMAN = 1;
		static final int MANAGER = 2;

		void setType(int arg) {
			_type = EmployeeType.newType(arg);
		}
		class EmployeeType...
			static EmployeeType newType(int code) {
				switch (code) {
					case ENGINEER:
						return new Engineer();
					case SALESMAN:
						return new Salesman();
					case MANAGER:
						return new Manager();
					default:
						throw new IllegalArgumentException("Incorrect Employee Code");
				}
			}
		}
		int payAmount() {
			switch (getType()) {
				case EmployeeType.ENGINEER:
					return _monthlySalary;
				case EmployeeType.SALESMAN:
					return _monthlySalary + _commission;
				case EmployeeType.MANAGER:
					return _monthlySalary + _bonus;
				default:
					throw new RuntimeException("Incorrect Employee");
			}
		}
	}
```
**动机**  

* 和[31. Replace Type Code with Subclasses](#31-replace-type-code-with-subclasses) 是相似的，但是它可以使用在类型码发生了改变在对象的生命周期发生了变化或者另一个原因阻止了子类的变化，则可以使用它
* 它通常是和状态模式或者策略模式配合使用

## 32. Replace Subclass with Fields（用字段代替子类）
你的子类仅在返回常数变量数据变量的方法中有所不同
_将这个方法提升到父类中，并移除这个子类_
```java

	abstract class Person {
		abstract boolean isMale();
		abstract char getCode();
		...
	}
	class Male extends Person {
			boolean isMale() {
			return true;
		}
		char getCode() {
			return 'M';
		}
	}
	class Female extends Person {
		boolean isMale() {
			return false;
		}
		char getCode() {
			return 'F';
		}
	}
```
to
```java

	class Person{
		protected Person (boolean isMale, char code) {
			_isMale = isMale;
			_code = code;
		}
		boolean isMale() {
			return _isMale;
		}
		static Person createMale(){
			return new Person(true, 'M');
		}
		static Person createFemale(){
			return new Person(false, 'F');
		}
	}
```
**动机**  

* 当子类的某个方法不足与继续存在
* 将这个子类彻底删除，并将这个字段上移到父类中
* 删除额外的子类

# 9. SIMPLIFYING CONDITIONAL EXPRESSIONS（简化条件表达式）

## 33. Decompose Conditional （分解条件）
你有一个复杂的条件（大量的if else then ）
_使用额外的方法代替这个表达式，将then 放在一部分，else 放在一部分_
```java

	if (date.before (SUMMER_START) || date.after(SUMMER_END))
		charge = quantity * _winterRate + _winterServiceCharge;
	else 
		charge = quantity * _summerRate;
```
to
```java

	if (notSummer(date))
		charge = winterCharge(quantity);
	else 
		charge = summerCharge (quantity);
```
**动机**  

* 将条件表达式高亮，这样的话你能清楚将其分开
* 对分叉之后的结果进行高亮

## 34. Consolidate Conditional Expression
```java

	double disabilityAmount() {
	if (_seniority < 2) return 0;
	if (_monthsDisabled > 12) return 0;
	if (_isPartTime) return 0;
	// compute the disability amount
```
to
```java

	double disabilityAmount() {
	if (isNotEligableForDisability()) return 0;
	// compute the disability amount
```

## 35. Consolidate Duplicate Conditional Fragments （合并重复的条件片段）
在条件表达式的每个分支上有着相同的一片代码
_将这段重复代搬移到条件表达式之外_
```java

	if (isSpecialDeal()) {
		total = price * 0.95;
		send();
	}
	else {
		total = price * 0.98;
		send();
	}
```
to
```java

	if (isSpecialDeal()) {
		total = price * 0.95;
	}
	else {
		total = price * 0.98;
	}
	send();

```
**动机**  
使得变量清晰并保持相同

## 36. Remove Control Flag （移除控制标记）
在一系列的布尔表达式中，某个变量带有“控制标记”的作用
_已break或者return语句取代控制标记_
```java

	void checkSecurity(String[] people) {
		boolean found = false;
			for (int i = 0; i < people.length; i++) {
				if (! found) {
					if (people[i].equals ("Don")){
						sendAlert();
						found = true;
					}
					if (people[i].equals ("John")){
						sendAlert();
						found = true;
					}
				}
		}
	}
```
to
```java

	void checkSecurity(String[] people) {
		for (int i = 0; i < people.length; i++) {
			if (people[i].equals ("Don")){
				sendAlert();
				break; // or return
			}
			if (people[i].equals ("John")){
				sendAlert();
				break; // or return
			}
		}
	}
```
**动机**  

* 控制标记的作用是在于决定是否继续下面流程，但是现代语言注重于使用`break` 和 `continue`
* 确保真实的条件表达式是清晰的

## 37. Replace Nested Conditional with Guard Clauses （以卫语句取代嵌套的条件表达式）
函数的条件逻辑使人难以看清正常的执行路径
_使用卫语句表现所有的特殊情况_
```java

	double getPayAmount() {
		double result;
		if (_isDead) result = deadAmount();
		else {
			if (_isSeparated) result = separatedAmount();
			else {
				if (_isRetired) result = retiredAmount();
				else result = normalPayAmount();
			};
		}
		return result;
	};
```
to
```java

	double getPayAmount() {
		if (_isDead) return deadAmount();
		if (_isSeparated) return separatedAmount();
		if (_isRetired) return retiredAmount();
		return normalPayAmount();
	};
```
**动机**  

* 如果这个条件是非同寻常的条件，检查这条件是否符合然后返回true
* 这样大度的检查被称为“卫语句”
* 对某一条分支已特别的重，如果使用if-then-else 结构，你对if分支和else分支的重要性是同等的
* 各个分支具有同一样的重要性
* 取代之前的观念 “每个函数只能有一个入口和一个出口”

## 38. Replace Conditional with Polymorphism （以多态取代条件表达式）
你手上有一个条件表达式，它根据对象的类型的不同选择不同的行为
_将条件表达式的所有分支放进一个子类内的覆盖函数中，然后将原始函数声明为抽象函数_
```java

	class Employee {
		private int _type;

		static final int ENGINEER = 0;
		static final int SALESMAN = 1;
		static final int MANAGER = 2;

		Employee (int type) {
			_type = type;
		}
		int payAmount() {
			switch (_type) {
				case ENGINEER:
					return _monthlySalary;
				case SALESMAN:
					return _monthlySalary + _commission;
				case MANAGER:
					return _monthlySalary + _bonus;
				default:
					throw new RuntimeException("Incorrect Employee");
				}
			}
		}
	}
```
to
```java

	class Employee...
		static final int ENGINEER = 0;
		static final int SALESMAN = 1;
		static final int MANAGER = 2;

		void setType(int arg) {
			_type = EmployeeType.newType(arg);
		}
		int payAmount() {
			return _type.payAmount(this);
		}
	}

	class Engineer...
		int payAmount(Employee emp) {
			return emp.getMonthlySalary();
		}
	}
```
**动机**  

* 如果对象的行为因其类型而异，请避免编写显示的条件
* Switch 声明在面向对象语言中应该尽量少的被使用

## 39. Introduce Null Object （引入Null 对象）
你不得不检查对象是否为Null对象
_将null值替换为null对象_
```java

	if (customer == null){
		plan = BillingPlan.basic();
	} 
	else{
		plan = customer.getPlan();
	}

```
to
```java

	class Customer {

	}

	class NullCusomer extends Customer {

	}
```
**动机**

* 对象根据其类型做正确的事情，Null对象也应该遵守这个规则

## 40. Introduce Assertion （引入断言）
某段代码需要对程序状态做出某种假设  
_已断言明确表现这种假设_
```java

	double getExpenseLimit() {
		// should have either expense limit or a primary project
		return (_expenseLimit != NULL_EXPENSE) ?
			_expenseLimit:
			_primaryProject.getMemberExpenseLimit();
	}
```
to
```java

	double getExpenseLimit() {
		Assert.isTrue (_expenseLimit != NULL_EXPENSE || _primaryProject	!= null);
		return (_expenseLimit != NULL_EXPENSE) ?
			_expenseLimit:
			_primaryProject.getMemberExpenseLimit();
	}
```
**动机**  

* 断言是一种明确表达会为true的行为
* 当断言失败时往往是一个非受控的异常
* 断言往往在生产代码中移除
* 交流层面 ： 断言能使程序的阅读者理解代码所做的假设
* 在调试的角度 ： 断言能使编程者尽可能近的接触bug

# 10. MAKING METHOD CALLS SIMPLER (简化函数的调用)
## 41. Rename method （函数改名）
函数的名称不能表达函数的用途
_修改函数名称_
```java
	getinvcdtlmt()
```
to
```java
	getInvoiceableCreditLimit
```
**动机**   
函数的名称最好能表达函数的意图

## 42. Add Parameter （添加参数）
某个函数需要从调用端得到更多的信息
_为此函数添加一个对象函数，让改对象带进函数所需要信息_
```java
	getContact()
```
to
```java
	getContact(:Date)
```
**动机**    
在改变方法之后，你获得更多的信息

## 43. Remove Parameter（移除参数）
一个参数不在函数中使用了
_移除它_
```java
	getContact(:Date)
```
to
```java
	getContact()
```
**动机**    
一个参数不再使用还留着它干嘛？

## 44. Separate Query from Modifier （将查询函数和修改函数分离）
某个函数即返回函数的状态值，又修改对象的状态
_创建两个不同的函数，其中一个负责查询，另一个负责修改_
```java
	getTotalOutStandingAndSetReadyForSummaries()
```
to
```java
	getTotalOutStanding()
	SetReadyForSummaries()
```
**动机**    
将有副作用的方法和没有副作用的方法分开

## 45. Parameterize Method （令函数携带参数）
若干函数做了类似的工作，但在函数本体中却包含了不同的值
_创建单一函数，已参数表达那些不同的值_
```java
	fivePercentRaise()
	tenPercentRaise()
```
to
```java
	raise(percentage)
```
**动机**    
移除重复的代码提高灵活度

## 46. Replace Parameter with Explicit Methods （已明确函数取代参数）
🈶一个函数，其中完全取决于参数值而采取不同的行为
_针对该函数的每一个可能值，建立一个独立函数_
```java

	void setValue (String name, int value) {
		if (name.equals("height")){}
			_height = value;
			return;
		}
		if (name.equals("width")){
			_width = value;
			return;
		}
		Assert.shouldNeverReachHere();
	}
```
to
```java

	void setHeight(int arg) {
		_height = arg;
	}
	void setWidth (int arg) {
		_width = arg;
	}
```
**动机**

* 避免条件行为
* 在编译器进行检查
* 清晰的接口

## 47. Preserve Whole Object （保持对象的完整）
你从某个对象支行取出若干值，将他们作为某一次函数调用时的参数
_改为传递一整个对象_
```java

	int low = daysTempRange().getLow();
	int high = daysTempRange().getHigh();
	withinPlan = plan.withinRange(low, high);
```
to
```java

	withinPlan = plan.withinRange(daysTempRange());
```
**动机**

* 使参数列表在变化的时候具有鲁棒性
* 使代码更与易读
* 在代码中移除相似的重复的代码
*  消极的 ： 增加了函数参数在调用时的依赖

## 48. Replace Parameter with Method （已函数取代参数）
对象调用某个函数，并将其所得的结果作为参数，传递给另一个函数。而接受该参数的函数本身也能够调用钱一个函数
_将函数接受者去除该项参数，并直接调用前一个函数_
```java

	int basePrice = _quantity * _itemPrice;
	discountLevel = getDiscountLevel();
	double finalPrice = discountedPrice (basePrice, discountLevel);
```
to
```java

	int basePrice = _quantity * _itemPrice;
	double finalPrice = discountedPrice (basePrice);
```
**动机**

* 如果一个函数可以通过其他的途径获得参数值，那么它就不应该通过参数取得该值
* 如果你能有其他的方法或者相同的计算值
* 如果要在对调用对象的引用的其他对象上调用方法

## 49. Introduce Parameter Object （引入参数对象）
某些参数总是很自然的同时出现
_以一个对象取代这些参数_
```java

	class Customer{
		amountInvoicedIn (start : Date, end : Date)
		amountReceivedIn (start : Date, end : Date)
		amountOverdueIn (start : Date, end : Date)
	}
```
to
```java

	class Customer{
		amountInvoicedIn (: DateRange)
		amountReceivedIn (: DateRange)
		amountOverdueIn (: DateRange)
	}
```
**动机**

* 减少参数列表的长度
* 使代码看的更加简洁

## 50. Remove Setting Method （移除设值函数）
类中的某个字段应该在对象创建时被设值，然后就不再改变 
_去掉该字段的所有设值函数_
```java

	class Employee{
		setImmutableValue()
	}
```
to
```java

	class Employee{
		¯\_(ツ)_/¯
	}
```
**动机**   
确保你的清晰的目的 ： 如果你想你的字段在创建之后就不要被改变了，你就不应该提供一个setting方法用于确保你的字段是否不被改变的

## 51. Hide Method （隐藏函数）
有一个函数，从来没有被其他任何类用到
_将这个函数修改为 private_
```java

	class Employee{
		public method()
	}
```
to
```java

	class Employee{
		private method()
	}
```
**动机**   
如果一个方法不需要被外部调用，那么就应该讲这个方法隐藏

## 52. Replace Constructor with Factory Method （已工厂函数取代构造函数）
在创建对象时不仅仅是做简单的健够动作
_将构造函数替换为工厂函数_
```java

	Employee (int type) {
		_type = type;
	}
```
to
```java

	static Employee create(int type) {
		return new Employee(type);
	}
```

创建一个对象依赖于其子类，构造函数只能返回单一类型的对象，因此你需要将构造函数替换为一个工厂函数

## 53. Encapsulate Downcast （封装向下转型）
某个函数返回的对象，需要由调用者执行向下转型
_将向下转型动作转移到函数中_

```java

	Object lastReading() {
		return readings.lastElement();
	}
```
to
```java

	Reading lastReading() {
		return (Reading) readings.lastElement();
	}
```
**动机**   
将一个方法最有效的返回值进行返回给函数的调用者  
如果类型是准确的，检查使用这个对象的方法并提供一个更为有效的方法

## 54. Replace Error Code with Exception （以异常取代错误码）
某个函数返回一个特定的代码，用以表示某种错误情况
_改用异常将其抛出去_
```java

	int withdraw(int amount) {
		if (amount > _balance)
			return -1;
		else {
			_balance -= amount;
			return 0;
		}
	}
```
to
```java

	void withdraw(int amount) throws BalanceException {
		if (amount > _balance)
			throw new BalanceException();
		_balance -= amount;
	}
```
**动机**
当一个程序在发生了一个不可处理的错误时，你需要使这个函数的调用者知道。向上抛出异常，让上层调用者知道

## 55. Replace Exception with Test （已测试取代异常）
面对一个调用者可以预先检查的条件，你抛出了一个异常
_修改调用者，使它在调用函数之前先做检查_
```java

	double getValueForPeriod (int periodNumber) {
		try {
			return _values[periodNumber];
		} catch (ArrayIndexOutOfBoundsException e) {
			return 0;
		}
	}
```
to
```java

	double getValueForPeriod (int periodNumber) {
		if (periodNumber >= _values.length)
			return 0;
		return _values[periodNumber];
}
```
**动机**

* 不要过度使用异常，它们应该被用在检查异常上
* 不要用它来代替条件测试
* 检查异常错误条件在调用方法之前

# 11. DEALING WITH GENERALIZATION （处理概括关系）
## 56. Pull up field （字段上移）
两个子类拥有相同的字段   
_将该字段移到超类中_
```java

	class Salesman extends Employee{
		String name;
	}
	class Engineer extends Employee{
		String name;
	}
```
to
```java

	class Employee{
		String name;
	}
	class Salesman extends Employee{}
	class Engineer extends Employee{}

```
**动机**

* 删除重复的代码
* 允许将子类的行为转移到父类中

## 57. Pull Up Method （构造函数本体上移）
你在各个子类中拥有一些构造函数，他们的本体几乎完全一致 
_在超类中新建一个构造函数，并在子类构造函数中调用它_
```java

	class Salesman extends Employee{
		String getName();
	}
	class Engineer extends Employee{
		String getName();
	}
```
to
```java

	class Employee{
		String getName();
	}
	class Salesman extends Employee{}
	class Engineer extends Employee{}

```
**动机**

* 消除重复的行为

## 58. Pull Up Constructor Body （构造函数本体上移）
在子类中的构造函数与父类中的构造函数是相同的
_在超类中创建一个构造函数，并在子类构造函数中调用它_
```java

	class Manager extends Employee...
		public Manager (String name, String id, int grade) {
		_name = name;
		_id = id;
		_grade = grade;
	}

```
to
```java

	public Manager (String name, String id, int grade) {
		super (name, id);
		_grade = grade;
	}
```
**动机**

* 构造函数与方法不同
* 消除重复的代码

## 59. Push Down Method （方法下移）
父类的某个方法至于某个子类相关
_将其移到子类中_   
```java

	class Employee{
		int getQuota();
	}
	class Salesman extends Employee{}
	class Engineer extends Employee{}
```
to
```java

	class Salesman extends Employee{
		int getQuota();
	}
	class Engineer extends Employee{}
```
**动机**
当方法只在子类中显现

## 60. Push Down Field （字段下移）
超类的字段只在某个子类中用到 
_将这个字段移到需要它的那些子类中去_
```java

	class Employee{
		int quota;
	}
	class Salesman extends Employee{}
	class Engineer extends Employee{}
```
to
```java

	class Salesman extends Employee{
		int quota;
	}
	class Engineer extends Employee{}
```
**动机**
当一个字段只在子类中使用时

## 61. Extract Subclass （提炼子类）
类中的某些特性只被某些实例用到
_新建一个子类，将上面所说的那一部分特性移到子类中去_
```java

	class JobItem	{
		getTotalPrices()
		getUnitPrice()
		getEmployee()
	}
```
to
```java

	JobItem	{
		getTotalPrices()
		getUnitPrice()
	}
	class class LabotItem extends JobItem	{
		getUnitPrice()
		getEmployee()
	}
```
**动机**
当一个类的行为只用在某些实例中而不用在其他类中

## 62. Extract Superclass （提炼超类）
两个类具有相似特性 
_创建一个父类，然后将这两个类中相同的部分移到父类中，然后在继承这个父类_
```java

	class Department{
		getTotalAnnualCost()
		getName()
		getHeadCount
	}
	class Employee{
		getAnnualCost()
		getName()
		getId
	}

```
to
```java

	class Party{
		getAnnualCost()
		getName()
	}
	class Department {
		getAnnualCost()
		getHeadCount
	}
	class Employee {
		getAnnualCost()
		getId
	}

```
**动机**	 
当两个类有过多相似的地方的时候，就需要考虑下是否需要将这个类进行下抽象了

## 63. Extract Interface （提炼接口）
若干客户使用类接口中的同一个子类，或者两个类的接口有相同的部分
_将相同的子集提炼到一个独立接口中_
```java

	class Employee {
		getRate()
		hasSpecialSkill()
		getName()
		getDepartment()
	}
```
to  
```java

	interface Billable	{
		getRate()
		hasSpecialSkill()
	}
	class Employee implements Billable	{
		getRate
		hasSpecialSkill()
		getName()
		getDepartment()
	}
```	
**动机**

* 若一个类的子集明确被一系列的客户使用
* 如果一个类需要和多个类处理并能处理确定的请求

## 64. Collapse Hierarchy （折叠继承体系）
超类和子类无太大区别
_将它们合为一个_
```java

	class Employee{	}
	class Salesman extends Employee{	}
```
to
```java

	class Employee{	}
```		
**动机**	 
该子类没有带来任何价值

## 65. Form Template Method （塑造模板函数）
有些子类，其中对应的某些函数以相同顺序执行类似的操作，但各个操作的细节上有所不同
_将这些操作分别放进独立函数中，并保持它们都有相同的签名，于是原函数也就变得相同了。然后将原函数上移到超类_
```java

	class Site{}
	class ResidentialSite extends Site{
		getBillableAmount()
	}
	class LifelineSite extends Site{
		getBillableAmount()
	}
```
to
```java

	class Site{ 	
		getBillableAmount()
		getBaseAmount()
		getTaxAmount()
	}
	class ResidentialSite extends Site{
		getBaseAmount()
		getTaxAmount()
	}
	class LifelineSite extends Site{
		getBaseAmount()
		getTaxAmount()
	}
```
**动机**
* 继承是避免重复行为的一个强大工具
* 当发现两个相似的方法时，将其都放入到父类中
* [Template Method](https://www.wikiwand.com/en/Template_method_pattern)[[Gang of Four]]
(https://www.wikiwand.com/en/Design_Patterns)
* 模板方法

## 66. Replace Inheritance with Delegation （以委托取代继承）
某个子类只使用了超类接口中的一部分，或是根本不需要继承而来的数据
_在子类中创建一个字段用以保存超类，调整子类函数，令它改2而委托超类：然后去除两者之间的继承关系
```java

	class Vector{
		isEmpty()
	}

	class Stack extends Vector {}

```
to
```java

	class Vector {
		isEmpty()
	}

	class Stack {
		Vector vector
		isEmpty(){
			return vector.isEmpty()
		}
	}

```
**动机**
* 当你使用委托类的时候会对你使用的数据字段更加的清晰
* 在你控制之外的方法都会被忽略，你只需要关注于自身

## 67. Replace Delegation with Inheritance （以继承取代委托）
你在两个类之间使用简单的委托关系，并经常为整个接口编写许多很多简单的委托函数  
_让委托类继承委托类_
```java

	class Person {
		getName()
	}

	class Employee {
		Person person
		getName(){
			return person.getName()
		}
	}
```
to
```java

	class Person{
		getName()
	}
	class Employee extends Person{}

```
**动机**	 

* 如果你使用所有的方法在委托类中
* 如果你不能使用委托类的所有函数，那么久不应该使用它
 

# 12. BIG REFACTORINGS （大型重构）
## 68. Tease Apart Inheritance （梳理并分解继承体系）
某个继承体系同时承担两项责任
_建立两个继承体系，并通过委托关系让其中一个可以调用另外一个_
```java

	class Deal{}
	class ActiveDeal extends Deal{}
	class PassiveDeal extends Deal{}
	class TabularActiveDeal extends ActiveDeal{}
	class TabularPassiveDeal extends PassiveDeal{}
```
to
```java

	class Deal{
		PresentationStyle presettationStyle;
	}
	class ActiveDeal extends Deal{}
	class PassiveDeal extends Deal{}

	class PresentationStyle{}
	class TabularPresentationStyle extends PresentationStyle{}
	class SinglePresentationStyle extends PresentationStyle{}

```
**动机**
* 过度的继承会导致代码重复
* 如果继承体系中的某一特定层级上的所有类，其子类名称都已相同的形容词开始，那么这个体系可能肩负着两项不同的责任。
           |              |

## 69. Convert Procedural Design to Objects （过程化设计转为对象设计）
你手上有些传统过程化风格的代码
_将数据记录变成对象，将大块的行为分成小块，并将行为移入相关对象中_
```java

	class OrderCalculator{
		determinePrice(Order)
		determineTaxes(Order)
	}
	class Order{}
	class OrderLine{}
```
to
```java

	class Order{
		getPrice()
		getTaxes()
	}
	class OrderLine{
		getPrice()
		getTaxes()
	}
```
**动机**
使用面向对象思想进行变成

## 70. Separate Domain from Presentation （将领域和表述/显示分离）
某些GUI类中包含了领域逻辑
_将领域逻辑分离出来吗，为他们创建独立的领域类_
```java

	class OrderWindow{}
```
to
```java

	class OrderWindow{
		Order order;
}
```
**动机**
* 分裂两个过于复杂的代码，使他们更易于修改
* 允许多层风格编写的程序
* 这是值得被使用的

## 71. Extract Hierarchy （提炼继承体系）
有某个类做了太多的工作其中一部分工作是以大量的条件表达式完成的
_创建一个继承体系，已一个子类来表达某一种特殊的情况_
```java

	class BillingScheme{}
```
to
```java

	class BillingScheme{}
	class BusinessBillingScheme extends BillingScheme{}
	class ResidentialBillingScheme extends BillingScheme{}
	class DisabilityBillingScheme extends BillingScheme{}
```
**动机**   

* 一个类实现一个概念演变成实现多个概念
* 保持单一责任