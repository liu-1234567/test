```
!pip install tflite-model-maker
```

![jpg4](https://github.com/curry030drw/web/blob/master/%E5%AE%9E%E9%AA%8C5.1/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/jpg1.png)

接下来，导入相关的库。

```
import os

import numpy as np

import tensorflow as tf
assert tf.__version__.startswith('2')

from tflite_model_maker import model_spec
from tflite_model_maker import image_classifier
from tflite_model_maker.config import ExportFormat
from tflite_model_maker.config import QuantizationConfig
from tflite_model_maker.image_classifier import DataLoader

import matplotlib.pyplot as plt
```

# 模型训练

## 获取数据

本实验先从较小的数据集开始训练，当然越多的数据，模型精度更高。

```
image_path = tf.keras.utils.get_file(
      'flower_photos.tgz',
      'https://storage.googleapis.com/download.tensorflow.org/example_images/flower_photos.tgz',
      extract=True)
image_path = os.path.join(os.path.dirname(image_path), 'flower_photos')
```

模型训练
获取数据
本实验先从较小的数据集开始训练，当然越多的数据，模型精度更高。

```
image_path = tf.keras.utils.get_file(
      'flower_photos.tgz',
      'https://storage.googleapis.com/download.tensorflow.org/example_images/flower_photos.tgz',
      extract=True)
image_path = os.path.join(os.path.dirname(image_path), 'flower_photos')

```

这里从storage.googleapis.com中下载了本实验所需要的数据集。image_path可以定制，默认是在用户目录的.keras\datasets中。

运行示例
一共需4步完成。
第一步：加载数据集，并将数据集分为训练数据和测试数据。

```
data = DataLoader.from_folder(image_path)
train_data, test_data = data.split(0.9)
```

```
INFO:tensorflow:Load image with size: 3670, num_label: 5, labels: daisy, dandelion, roses, sunflowers, tulips.
第二步：训练Tensorflow模型
```

```
model = image_classifier.create(train_data)
```

```
INFO:tensorflow:Load image with size: 3670, num_label: 5, labels: daisy, dandelion, roses, sunflowers, tulips.
INFO:tensorflow:Load image with size: 3670, num_label: 5, labels: daisy, dandelion, roses, sunflowers, tulips.
3303
367
INFO:tensorflow:Retraining the models...
INFO:tensorflow:Retraining the models...
Model: "sequential"
```


_________________________________________________________________
```
 Layer (type)        Output Shape       Param #  
=================================================================

 hub_keras_layer_v1v2 (HubKe (None, 1280)       3413024  
 rasLayerV1V2)                          
                                 
 dropout (Dropout)      (None, 1280)       0     
                                 
 dense (Dense)        (None, 5)         6405   
                                 
=================================================================
Total params: 3,419,429
Trainable params: 6,405
Non-trainable params: 3,413,024

_________________________________________________________________

None
Epoch 1/5
E:\acroda\envs\tf\lib\site-packages\keras\optimizers\optimizer_v2\gradient_![img](file:///C:\Users\DSHH\AppData\Roaming\Tencent\QQTempSys\%W@GJ$ACOF(TYDYECOKVDYB.png)descent.py:108: UserWarning: The `lr` argument is deprecated, use `learning_rate` instead.
 super(SGD, self).__init__(name, **kwargs)
103/103 [==============================] - 67s 636ms/step - loss: 0.8742 - accuracy: 0.7661
Epoch 2/5
103/103 [==============================] - 68s 663ms/step - loss: 0.6533 - accuracy: 0.8956
Epoch 3/5
103/103 [==============================] - 67s 654ms/step - loss: 0.6308 - accuracy: 0.9093
Epoch 4/5
103/103 [==============================] - 55s 534ms/step - loss: 0.6030 - accuracy: 0.9290
Epoch 5/5
103/103 [==============================] - 52s 505ms/step - loss: 0.5943 - accuracy: 0.9302
```



第三步：评估模型

```
loss, accuracy = model.evaluate(test_data)
```

```
12/12 [==============================] - 12s 749ms/step - loss: 0.6107 - accuracy: 0.9155
```


第四步，导出Tensorflow Lite模型

```
model.export(export_dir='.')
```

```
current_dir = os.getcwd()
print(current_dir)



```

![jp4](https://github.com/curry030drw/web/blob/master/%E5%AE%9E%E9%AA%8C5.1/%E6%96%B0%E5%BB%BA%E6%96%87%E4%BB%B6%E5%A4%B9/jp4.png)
