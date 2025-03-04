# 全局和静态变量

你肯定受够了局部变量只能在当前脚本使用，有什么方法可以调用其他脚本的变量呢？使用全局变量或静态变量，允许跨脚本调用！

## 声明
声明全局变量或静态变量非常简单。注意`as 类型名` 不能省略，且已定义的全局、静态变量之后**不能再次定义，修改其类型或值**。全局变量可以直接在其他脚本中使用，静态变量还需要跨脚本调用。

```csharp
import crafttweaker.item.IItemStack;

// 定义一个全局变量
global stone as IItemStack = <minecraft:stone>;

// 定义一个静态变量
static dirt as IItemStack = <minecraft:dirt>;
```

* 含有全局变量的脚本需要用优先级预加载器保证其优先加载。
* 局部变量可以覆盖全局变量。
* 全局变量可以在任何地方直接调用，但坏处就是你（或别人）可能不记得（或不知道）该变量的定义处在哪里。
* 静态变量的使用需跨脚本引用，但好处就是很容易知道该变量是在哪个脚本里定义的，容易维护。

## 可修改的全局和静态变量

如果要跨脚本、事件和函数这三个作用域之间操作变量，你会发现它们之间的变量是无法直接操作的。

比方来说，如果你正想暂时保存一个值，并且在脚本中任何地方都可以再次修改或调用它，那么这就是上面所说的情况。

这里有一个方法可以绕过全局、静态变量定义后不能再次修改的窘境。

```csharp
// 在脚本中定义一个静态数组
static array as int[] = [1];

// 修改数组内第一个元素的值
array[0] = 10;

// 输出数组第一个元素的值
print(array[0]);
```

尽管`array as int[]`这个数组不能再次定义和修改其类型，但数组内部的元素还是可以修改的。

不只是数组，你也可以定义一个静态的map，尽管该map不能再次定义和修改类型，但是同样可以多次修改其内部的数据。
