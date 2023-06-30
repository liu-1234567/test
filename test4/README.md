##   实验四

  

专业___软件工程__班级 **1班**___ 学号___**116052020002** 姓名 **王得任**   

实验日期：2023年 5月 14日  报告退发 (订正 、 重做)              



- 使用训练自定义的图像分类器
- 利用Android Studio导入训练后的模型，并结合CameraX使用
- 利用手机GPU加速模型运行

## 预备工作

安装Android Studio 4.1以上版本

# 下载初始代码

创建工作目录，使用

```powershell
git clone https://github.com/hoitab/TFLClassify.git
1
```

拷贝代码；或者直接[访问github](https://so.csdn.net/so/search?q=访问github&spm=1001.2101.3001.7020)链接下载代码的ZIP包，并解压缩到工作目录

# 运行初始代码

1. 打开Android Studio，选择“Open an Existing Project”

   # 运行初始代码

   1. 打开Android Studio，选择“Open an Existing Project”
   
   2. 选择TFLClassify/build.gradle生成整个项目。项目包含两个module：finish 和 start，finish模块是已经完成的项目，start则是本项目实践的模块。
   
   3. 第一次编译项目时，弹出“Gradle Sync”，将下载相应的gradle wrapper 。
   
   4. 手机通过USB接口连接开发平台，并设置手机开发者选项允许调试。

   5. 选择真实物理机（而不是模拟器）运行start模块

   6. 允许应用获取手机摄像头的权限，得到下述效果图，界面利用随机数表示虚拟的识别结果
   
      <img src="https://github.com/curry030drw/web/blob/master/实验4/markdown/jpg/jpg7.jpg" alt="在这里插入图片描述" style="zoom:50%;" />。
   
   # 向应用中添加TensorFlow Lite
   
   1. 选择"start"模块
      ![在这里插入图片描述](https://github.com/curry030drw/web/blob/master/实验4/markdown/jpg/jpg1.png)
   2. 右键“start”模块，或者选择File，然后New>Other>TensorFlow Lite Model
      ![在这里插入图片描述](https://github.com/curry030drw/web/blob/master/实验4/markdown/jpg/jpg2.png)
   3. 选择已经下载的自定义的训练模型。本教程模型训练任务以后完成，这里选择finish模块中ml文件下的FlowerModel.tflite。
      ![在这里插入图片描述](https://github.com/curry030drw/web/blob/master/实验4/markdown/jpg/jpg3.png)
      点击“Finish”完成模型导入，系统将自动下载模型的依赖包并将依赖项添加至模块的build.gradle文件。
   4. 最终TensorFlow Lite模型被成功导入，并生成摘要信息
      ![在这里插入图片描述](https://github.com/curry030drw/web/blob/master/实验4/markdown/jpg/jpg2.png)
   
   # 检查代码中的TODO项
   
   本项目初始代码中包括了若干的TODO项，以导航项目中未完成之处。为了方便起见，首先查看TODO列表视图，View>Tool Windows>TODO
   ![在这里插入图片描述](C:\Users\DSHH\Desktop\markdown\jpg\jpg5.png)
   默认情况下了列出项目所有的TODO项，进一步按照模块分组（Group By）![在这里插入图片描述](https://github.com/curry030drw/web/blob/master/实验4/markdown/jpg/jpg6.png)

   # 添加代码重新运行APP
   
   1. 定位“start”模块**MainActivity.kt**文件的TODO 1，添加初始化训练模型的代码

   ```kotlin
   private class ImageAnalyzer(ctx: Context, private val listener: RecognitionListener) :
           ImageAnalysis.Analyzer {
   
     ...
     // TODO 1: Add class variable TensorFlow Lite Model
     private val flowerModel = FlowerModel.newInstance(ctx)
   
     ...
   }
   123456789
   ```
   
   1. 在CameraX的analyze方法内部，需要将摄像头的输入`ImageProxy`转化为`Bitmap`对象，并进一步转化为`TensorImage` 对象
   
   ```kotlin
   override fun analyze(imageProxy: ImageProxy) {
     ...
     // TODO 2: Convert Image to Bitmap then to TensorImage
     val tfImage = TensorImage.fromBitmap(toBitmap(imageProxy))
     ...
   }
   123456
   ```
   
   1. 对图像进行处理并生成结果，主要包含下述操作：
   
   - 按照属性`score`对识别结果按照概率从高到低排序
   - 列出最高k种可能的结果，k的结果由常量`MAX_RESULT_DISPLAY`定义
   
   ```kotlin
   override fun analyze(imageProxy: ImageProxy) {
     ...
     // TODO 3: Process the image using the trained model, sort and pick out the top results
     val outputs = flowerModel.process(tfImage)
         .probabilityAsCategoryList.apply {
             sortByDescending { it.score } // Sort with highest confidence first
         }.take(MAX_RESULT_DISPLAY) // take the top results
   
     ...
   }
   12345678910
   ```
   
   1. 将识别的结果加入数据对象`Recognition` 中，包含`label`和`score`两个元素。后续将用于`RecyclerView`的数据显示
   
   ```kotlin
   override fun analyze(imageProxy: ImageProxy) {
     ...
     // TODO 4: Converting the top probability items into a list of recognitions
     for (output in outputs) {
         items.add(Recognition(output.label, output.score))
     }
     ...
   }
   12345678
   ```
   
   1. 将原先用于虚拟显示识别结果的代码注释掉或者删除
   
   ```kotlin
   // START - Placeholder code at the start of the codelab. Comment this block of code out.
   for (i in 0..MAX_RESULT_DISPLAY-1){
       items.add(Recognition("Fake label $i", Random.nextFloat()))
   }
   // END - Placeholder code at the start of the codelab. Comment this block of code out.
   12345
   ```
   
   1. 以物理设备重新运行start模块
   2. 最终运行效果
      <img src="https://github.com/curry030drw/web/blob/master/实验4/markdown/jpg/jpg8.jpg" alt="img" style="zoom:20%;" />

