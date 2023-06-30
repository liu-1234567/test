# 实验2.1


一.实验目的
构建第一个Kotlin应用
二.实验环境
操作系统：Windows 10;Andorid stdio
三.实验步骤和结果
#创建第一个Kotlin应用程序
创建一个新的工程
打开Android Studio，选择Projects>New Project，然后选择Basic Activity.

![图片描述](https://raw.githubusercontent.com/curry030drw/web/master/%E5%AE%9E%E9%AA%8C2.1/jpg/jpg.png)
点击Next，为应用程序命名（例如：My First App），选择Kotlin语言，然后点击Finish。Android Studio将使用系统中最新的API Level创建应用程序，并使用Gradle作为构建系统，在底部的视窗中可以查看整个过程。
在模拟器上运行应用程序
选择Run>Run ‘app’，在工具栏上可以看到运行程序的一些选择项。
查看布局编辑器:
在Basic Activity中，包含了基本的导航组件，Android app关联两个fragments，第一个屏幕显示了“Hello first fragment”由FirstFragment创建，界面元素的排列由布局文件指定，查看res>layout>fragment_first.xml，
查看布局的代码（Code），修改Textview的Text属性，
```
android:text="@string/hello_first_fragment"
```
右键该代码，选择Go To > Declaration or Usages，跳转到values/strings.xml，看到高亮文本
```
<string name="hello_first_fragment">Hello first fragment</string>
```
修改字符串属性值为“Hello Kotlin!”。更进一步，修改字体显示属性，在Design视图中选择textview_first文本组件，在Common Attributes属性下的textAppearance域，设置相关的文字显示属性，
查看布局的XML代码，可以看到新属性被应用。

```
android:fontFamily="sans-serif-condensed"
android:text="@string/hello_first_fragment"
android:textColor="@android:color/darker_gray"
android:textSize="30sp"
android:textStyle="bold"
```

### 向页面添加更多的布局
本步骤将向第一个Fragment添加更多的视图组件

### 查看视图的布局约束
在fragment_first.xml，查看TextView组件的约束属性：
在约束布局中，每个组件至少需要一个水平方向和一个垂直方向的约束，更多约束布局的内容，请查看ConstraintLayout。

### 添加按钮和约束
从Palette面板中拖动Button到


### 调整Button的约束，设置Button的Top>BottonOf textView，
```
app:layout_constraintTop_toBottomOf="@+id/textview_first" />
```
随后添加Button的左侧约束至屏幕的左侧，Button的底部约束至屏幕的底部。查看Attributes面板，修改将id从button修改为toast_button（注意修改id将重构代码）

### 调整Next按钮
Next按钮是工程创建时默认的按钮，查看Next按钮的布局设计视图，它与TextView之间的连接不是锯齿状的而是波浪状的，表明两者之间存在链（chain），是一种两个组件之间的双向联系而不是单向联系。删除两者之间的链，可以在设计视图右键相应约束，选择Delete（注意两个组件要双向删除）；

###或者在属性面板的Constraint Widget中移动光标到相应约束点击删除。

同时，删除Next按钮的左侧约束。

### 添加新的约束
添加Next的右边和底部约束至父类屏幕（如果不存在的话），Next的Top约束至TextView的底部。最后，TextView的底部约束至屏幕的底部。效果看起来如下图所示：
### 更改组件的文本
fragment_first.xml布局文件代码中，找到toast_button按钮的text属性部分

```
  <Button
   android:id="@+id/toast_button"
   android:layout_width="wrap_content"
   android:layout_height="wrap_content"
   android:text="Button"
```
在Basic Activity中，包含了基本的导航组件，Android app关联两个fragments，第一个屏幕显示了“Hello first fragment”由FirstFragment创建，界面元素的排列由布局文件指定，查看res>layout>fragment_first.xml，
查看布局的代码（Code），修改Textview的Text属性，
### 最终第一个页面的布局代码
```页面一代码： 
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/screenBackground"
    android:text="@string/hello_first_fragment"
    tools:context=".FirstFragment">

    <TextView
        android:id="@+id/textview_first"
        android:layout_width="97dp"
        android:layout_height="77dp"
        android:layout_marginTop="240dp"
        android:fontFamily="sans-serif-condensed"
        android:text="@string/hello_first_fragment"
        android:textColor="@android:color/white"
        android:textSize="48sp"
        app:layout_constraintBottom_toTopOf="@+id/button_second"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.65"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.481" />

    <Button
        android:id="@+id/random_button"
        android:layout_width="wrap_content"
        android:layout_height="0dp"

        android:layout_marginStart="33dp"
        android:layout_marginTop="516dp"
        android:layout_marginEnd="16dp"
        android:background="@color/buttonBackground"
        android:text="@string/random_button_text"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toEndOf="@+id/button_second"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/toast_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="24dp"
        android:layout_marginTop="200dp"


        android:layout_marginEnd="24dp"
        android:background="@color/buttonBackground"
        android:text="@string/toast_button"
        app:layout_constraintEnd_toStartOf="@+id/button_second"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textview_first" />

    <Button
        android:id="@+id/button_second"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="32dp"
        android:layout_marginTop="200dp"
        android:layout_marginEnd="32dp"
        android:background="@color/buttonBackground"
        android:text="Count"
        app:layout_constraintEnd_toStartOf="@+id/random_button"
        app:layout_constraintHorizontal_bias="1.0"
        app:layout_constraintStart_toEndOf="@+id/toast_button"
        app:layout_constraintTop_toBottomOf="@+id/textview_first" />
    />
</androidx.constraintlayout.widget.ConstraintLayout> 
```
### 第一个页面最终的效果
![图片描述](https://github.com/curry030drw/web/blob/master/%E5%AE%9E%E9%AA%8C2.1/jpg/jpg.png)

添加代码完成应用程序交互
设置代码自动补全
Android Studio中，依次点击File>New Projects Settings>Settings for New Projects…，查找Auto Import选项，在Java和Kotlin部分，勾选Add Unambiguous Imports on the fly。
![图片描述](https://raw.githubusercontent.com/curry030drw/web/master/%E5%AE%9E%E9%AA%8C2.1/jpg/import_img.png)

### TOAST按钮添加一个toast消息
打开FirstFragment.kt文件，有三个方法：onCreateView，onViewCreated和onDestroyView，在onViewCreated方法中使用绑定机制设置按钮的响应事件（创建应用程序时自带的按钮）。
```
binding.randomButton.setOnClickListener {
    findNavController().navigate(R.id.action_FirstFragment_to_SecondFragment)
}

接下来，为TOAST按钮添加事件，使用**findViewById()**查找按钮id，代码如下：

// find the toast_button by its ID and set a click listener
view.findViewById<Button>(R.id.toast_button).setOnClickListener {
   // create a Toast with some text, to appear for a short time
   val myToast = Toast.makeText(context, "Hello Toast!", Toast.LENGTH_LONG)
   // show the Toast
   myToast.show()
}
```
代码使用了Lambda表达式的机制。

### 使Count按钮更新屏幕的数字
此步骤向Count按钮添加事件响应，更新Textview的文本显示。
在FirstFragment.kt文件，为count_buttion按钮添加事件：
```
view.findViewById<Button>(R.id.count_button).setOnClickListener {
   countMe(view)
}

countMe()为自定义方法，以View为参数，每次点击增加数字1，具体代码为：

private fun countMe(view: View) {
   // Get the text view
   val showCountTextView = view.findViewById<TextView>(R.id.textview_first)

   // Get the value of the text view.
   val countString = showCountTextView.text.toString()

   // Convert value to a number and increment it
   var count = countString.toInt()
   count++

   // Display the new value in the text view.
   showCountTextView.text = count.toString()
}
```



### 完成第二个页面的代码
向界面添加TextView显示随机数
打开fragment_second.xml的设计视图中，当前界面有两个组件，一个Button和一个TextView（textview_second）。
去掉TextView和Button之间的约束
拖动新的TextView至屏幕的中间位置，用来显示随机数
设置新的TextView的id为**@+id/textview_random**
设置新的TextView的左右约束至屏幕的左右侧，Top约束至textview_second的Bottom，Bottom约束至Button的Top
设置TextView的字体颜色textColor属性为**@android:color/white**，textSize为72sp，textStyle为bold
设置TextView的显示文字为“R”
设置垂直偏移量layout_constraintVertical_bias为0.45
新增TextView最终的属性代码

```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/screenBackground"
    tools:context=".SecondFragment">

    <TextView
        android:id="@+id/textview_second"
        android:layout_width="308dp"
        android:layout_height="92dp"
        android:layout_marginTop="64dp"
        android:text="@string/random_heading"
        android:textColor="@color/design_default_color_primary_dark"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/button_second"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/previous"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/textview_second" />

    <TextView
        android:id="@+id/textview_random"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="200dp"
        android:layout_marginEnd="200dp"
        android:text="R"
        android:textColor="@android:color/white"
        android:textSize="60sp"
        app:layout_constraintBottom_toTopOf="@+id/button_second"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textview_second"
        app:layout_constraintVertical_bias="0.459" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
### 第二个页面的最终效果

![](https://github.com/curry030drw/web/blob/master/%E5%AE%9E%E9%AA%8C2.1/jpg/jpg4.png)


### 检查导航图
本项目选择Android的Basic Activity类型进行创建，默认情况下自带两个Fragments，并使用Android的导航机制Navigation。导航将使用按钮在两个Fragment之间进行跳转，就第一个Fragment修改后的Random按钮和第二个Fragment的Previous按钮。
打开nav_graph.xml文件（res>navigation>nav_graph.xml），形如：
![图片描述](https://github.com/curry030drw/web/blob/master/%E5%AE%9E%E9%AA%8C2.1/jpg/jpg5.png)
### 设置myarg（注意需要两个页面都要设置整形的）
![图片描述](https://github.com/curry030drw/web/blob/master/%E5%AE%9E%E9%AA%8C2.1/jpg/jpg6.png)
### 启用SafeArgs
1.导入依赖
```
def nav_version = "2.3.0-alpha02"
classpath "androidx.navigation:navigation-safe-args-gradle-plugin:$nav_version"
```
2.接着打开 Gradle Scripts > build.gradle (Module: app)
3.apply plugin开头的代码下添加一行
```
apply plugin: 'androidx.navigation.safeargs.kotlin'
```
4.Android Studio开始同步依赖库
5.重新生成工程Build > Make Project

###我的版本是需要使用以下代码的
Gradle的Project部分，在plugins节添加
```
id 'androidx.navigation.safeargs.kotlin' version '2.5.0-alpha01' apply false
```
module部分在plugins节添加
```
id 'androidx.navigation.safeargs'
```
### 创建导航动作的参数
1.打开导航视图，点击FirstFragment，查看其属性。
2.在Actions栏中可以看到导航至SecondFragment
3.同理，查看SecondFragment的属性栏
4.点击Arguments **+**符号
5.弹出的对话框中，添加参数myArg，类型为整型Integer
###FirstFragment添加代码，向SecondFragment发数据
初始应用中，点击FirstFragment的Next/Random按钮将跳转到第二个页面，但没有传递数据。在本步骤中将获取当前TextView中显示的数字并传输至SecondFragment
1.打开FirstFragment.kt源代码文件
2.找到onViewCreated()方法，该方法在onCreateView方法之后被调用，可以实现组件的初始化。找到Random按钮的响应代码，注释掉原先的事件处理代码
3.实例化TextView，获取TextView中文本并转换为整数值
```
val showCountTextView = view.findViewById<TextView>(R.id.textview_first)
val currentCount = showCountTextView.text.toString().toInt()
```
4.将currentCount作为参数传递给actionFirstFragmentToSecondFragment()
```
val action = FirstFragmentDirections.actionFirstFragmentToSecondFragment(currentCount)
```
5添加导航事件代码
```
findNavController().navigate(action)
```


### 添加SecondFragment的代码
本节将更新SecondFragment.kt的代码，接受传递过来的整型参数并进行处理
1.导入navArgs包
```
import androidx.navigation.fragment.navArgs
```
2.onViewCreated()代码之前添加一行

```
val args: SecondFragmentArgs by navArgs()
```
3onViewCreated()中获取传递过来的参数列表，提取count数值，并在textview_header中显示
```
val count = args.myArg
val countText = getString(R.string.random_heading, count)
view.findViewById<TextView>(R.id.textview_header).text = countText

```
4.根据count值生成随机数
```
val random = java.util.Random()
var randomNumber = 0
if (count > 0) {
   randomNumber = random.nextInt(count + 1)
}
```
5.textview_random中显示count值
```
view.findViewById<TextView>(R.id.textview_random).text = randomNumber.toString()

```
## 最终实现了三个按钮的功能的结果演示

### 第一个：Toast显示消息
![图片描述](https://github.com/curry030drw/web/blob/master/%E5%AE%9E%E9%AA%8C2.1/jpg/jpg.png)

### 第二个按钮计数的功能，count每点击一次数字加1
![图片描述](https://github.com/curry030drw/web/blob/master/%E5%AE%9E%E9%AA%8C2.1/jpg/jpg7.png)

### 第三个功能生成随机数
![图片描述](https://github.com/curry030drw/web/blob/master/%E5%AE%9E%E9%AA%8C2.1/jpg/jpg2.png)




