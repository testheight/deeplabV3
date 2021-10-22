（1）搭建环境（前提，双GPU）：
Python=3.x
keras ==2.2.4
Cython == 0.28.2
pydensecrf == 1.0rc3
tensorflow-gpu=1.13.1
（pydensecrf应在Cython后安装）

（2）数据准备（制作自己的数据集）
get_data_new.ipynb
或get_data.ipynb生成自己的pkl

填写已准备好的图像及标签路径：
（img_file = "../123123/95.jpg"
label_file = "../123123/label95.jpg"）

重点： 至少做两个.pkl（train.ipynb训练时需要两个pkl路径）

（3）模型训练（train.ipynb）
调整训练参数（以实际训练图像数量调整参数）：
history = par_model.fit(data_o, label_o,
                    epochs=10, 
                    batch_size=24,
                    callbacks=callbacks,
                    validation_split=0.05,
                    verbose=1)

训练完成后保存模型为.h5文件：
model.save_weights(check_point_file)

tensorboard：
在生成的mytensorboard文件中

（4）图像分割预测（predict.ipynb）
训练好的模型.h5文件路径：
check_point_file = "./deeplabv3_oneGPU_model_256_256_new.h5"

预测图像路径：
files = glob.glob("../1-50/*.jpg")
结果位于1-50result

（5）注意事项
重点：！！！！ keras ==2.2.4   tensorflow-gpu=1.13.1   设置后，如果出现keras找不到gpu的情况，重启jupyter 和xshell

（conda install -c conda-forge pydensecrf）也能安装pydensecrf