使用yolov5训练自己数据集（以VOC数据为例）

1.环境配置
pip install -r requirements.txt 

2.数据准备

使用labelimg标注数据 #（https://blog.csdn.net/didiaopao/article/details/119808973?spm=1001.2014.3001.5501）

VOC格式标签xml文件和yolo格式标签txt文件相互转换（https://blog.csdn.net/didiaopao/article/details/119910139?spm=1001.2014.3001.5501）

数据最好放在最外一级目录中，然后数据集的目录格式如下图所示

<img width="158" alt="image" src="https://github.com/xuesonghua/yolov5/assets/128601211/983d49c2-2016-4106-bcc5-49eba649bd4f">


下载预训练权重 （https://gitcode.com/ultralytics/yolov5/releases?utm_source=csdn_github_accelerator&isLogin=1）

3.模型训练

3.1修改数据配置文件

修改data目录下的相应的VOCyaml文件

1中需要将训练和测试的数据集的路径填上（最好要填绝对路径，有时候由目录结构的问题会莫名奇妙的报错）

2中需要检测的类别数

3中填写需要识别的类别的名字（必须是英文，否则会报错）

<img width="951" alt="屏幕截图 2024-06-02 132308" src="https://github.com/xuesonghua/yolov5/assets/128601211/5052b882-9cec-4063-8c84-1a625b12f63b">


3.2修改模型配置文件

修改models目录下的yolov5s.yaml文件中的相应参数，这里是你要识别的类别，如图

<img width="473" alt="image" src="https://github.com/xuesonghua/yolov5/assets/128601211/7460166d-b0eb-4618-9e94-d5a5a1856174">


3.3训练模型

1.weights权重的路径填写到对应的参数里面，然后将修好好的models模型的yolov5s.yaml文件路径填写到相应的参数里面，最后将data数据的VOC.yaml文件路径填写到相对于的参数里面
<img width="1044" alt="image" src="https://github.com/xuesonghua/yolov5/assets/128601211/861d469d-aaf1-4ec3-889c-19d971d39b63">



    parser.add_argument('--weights', type=str, default='weights/yolov5s.pt', help='initial weights path')
    parser.add_argument('--cfg', type=str, default='models/yolov5s_hat.yaml', help='model.yaml path')
    parser.add_argument('--data', type=str, default='data/hat.yaml', help='data.yaml path')


2.根据自己电脑性能选择模型的训练轮次
<img width="995" alt="image" src="https://github.com/xuesonghua/yolov5/assets/128601211/6dcd6cd8-818c-4a80-bb62-87504feba799">



parser.add_argument('--epochs', type=int, default=300)

4 推理测试

 等到数据训练好了以后，就会在主目录下产生一个run文件夹，在run/train/exp/weights目录下会产生两个权重文件，一个是最后一轮的权重文件，一个是最好的权重文件，一会我们就要利用这个最好的权重文件来做推理测试。除此以外还会产生一些验证文件的图片等一些文件。
 
<img width="224" alt="image" src="https://github.com/xuesonghua/yolov5/assets/128601211/f114cf0e-5738-4ba6-8a2c-6ffb5a97abd1">


找到主目录下的detect.py文件，打开该文件。

<img width="1115" alt="image" src="https://github.com/xuesonghua/yolov5/assets/128601211/14d1e8ca-e09c-4850-8b73-35319b7ea772">


需要将刚刚训练好的最好的权重传入到推理函数中去
对图片进行测试推理，将如下参数修改成图片的路径，然后运行detect.py就可以进行测试了。

parser.add_argument('--weights', nargs='+', type=str, default='runs/train/exp/weights/best.pt', help='model.pt path(s)')

parser.add_argument('--source', type=str, default='000295.jpg', help='source') 

理测试结束以后，在run下面会生成一个detect目录，推理结果会保存在exp目录下

<img width="248" alt="image" src="https://github.com/xuesonghua/yolov5/assets/128601211/62cbf7ba-00cd-48e4-ab13-eed7ccd0b10b">


参考
https://github.com/ultralytics/yolov5

