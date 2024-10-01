# no-contact-face-vedio-capture
助力工作人员利用摄像头采集人脸面部的视频信息，本软件是由QT编写的非接触式生理指标人脸面部信号收集软件。主要返回波形文件，对应血压的标签以及被采集人员的病史。

项目环境：
	本项目基于windows 11 下的QT软件编写，主要使用语言为C++
	其他环境：Opencv 3.4.11 ，Cmake 3.28.4
	想要在QT上跑代码，需要先配open环境，具体参考bilibili教程，或者该博客	https://blog.csdn.net/Mr_robot_strange/article/details/110677323


项目说明：
	本项目默认使用电脑外置的摄像头，是1，如果使用自带摄像头，修改以下代码中的cam_id=0
		Camera_Cap->open(cam_id, cv::CAP_DSHOW);

	本项目录制的图像分辨率为30fps，640*480，MJPG格式 如果想修改相关属性，修改以下代码
	应当注意的是需要关注您的摄像头支持，不同的摄像头在不同的编码条件下支持的fps也不同
		int codec = cv::VideoWriter::fourcc('M', 'J', 'P', 'G');  // 视频编解码器
        	double fps = 30.0;  // 视频帧率
        	cv::Size frameSize(640, 480);  // 视频帧大小
	
	本项目由于懒没有写窗口伸缩的代码，也即默认为1000，600；如果想调整的话，您可以自己补充该方面代码
	另本文没有写arm等嵌入式平台的屏幕代码，直接移植可能导致嵌入式设备的屏幕局部显示，无法适应，若想修改
	加上以下代码：
		QList <QScreen *> list_screen = QGuiApplication::screens();
		#if __arm__
			 /* 重设大小 */
			this->resize(list_screen.at(0)->geometry().width(),
			list_screen.at(0)->geometry().height());
		 #else
			/* 否则则设置主窗体大小为 1000x600 */
			this->resize(1000, 600);
	
	本项目的文件路径需要您自己输入，没有设置打开选择文件界面的功能，如果您先实现，请先设置一个打开按钮
	然后在槽函数里编辑以下代码：
		QString fileName = QFileDialog::getOpenFileName(this);
		QString fileName = QFileDialog::getOpenFileName(this);


项目使用方法及注意事项：（请尽可能遵循，不然有一定几率出现bug）
	1、请先在信息部分填写相关信息，否则开始录制的按钮会被禁止，填写完整后才可以点击开始录制，这也是项目为了防止创建文件失败的措施
	2、开始录制时，允许随时进行重新录制，而重新录制时，开始按钮被禁止
	3、高低压必须在录制完视频后才能填写，防止文件之间错位
	4、录制下个视频时，必须重新填写信息，防止覆盖原视频，每一个数据集都来之不易
	5、重要：：：：：：填写文件路径时不要有中文路径
	6、录制结束后会在您选择的路径下生成一个文件夹，文件夹名字为序号，文件里是食品和血压
		视频的名字是序号+男女+年龄+是否高压，血压文件里先高压，后低压

  

