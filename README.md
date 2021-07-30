### 環境のセットアップ
Ubuntu20.04でないと、ROS1をpython3で実行することができないので注意してください。
したがって、まず、以下の手順にしたがってROSのインストールをお願いします。
<p align="center"><a href="http://wiki.ros.org/noetic/Installation/Ubuntu">ROSのインストール</a></p>

また、今後のために以下のコマンドで必要なパッケージをインストールしてください

```
sudo apt install python3-catkin-tools
sudo apt install python3-catkin-pkg
sudo apt install python3-osrf-pycommon
sudo apt install pcl-tools
sudo apt install -y libpcl-dev
sudo apt install -y python3-pip
sudo apt install -y python3-pcl
sudo apt install -y python3-h5py
pip3 install open3d
sudo apt install -y ros-noetic-tf2-sensor-msgs
```

ROSのディレクトリを作ります。
```
mkdir -p ros_ws/src
cd ros_ws/src
```
srcディレクトリ上に今回お渡ししたデータを保存します。
そして、コンパイルを行います。

```
cd ros_ws
rosdep update
rosdep install --from-paths src --ignore-src -r -y
catkin build
```


これ以降のコンパイルの手順は
```
catkin build (コンパイルしたいパッケージ)
```

次に私が作成したGazeboモデルファイルを読み取れるように環境変数にディレクトリを追加してください。(一度だけで大丈夫です)
```
echo "export GAZEBO_MODEL_PATH=$GAZEBO_MODEL_PATH:${HOME}/ros_ws/src/photoneo_setup_sim/models" >> ~/.bashrc
```
##### シミュレーション環境の立ち上げ方(HV8)
```
roslaunch photoneo_setup_sim spawn_object.launch object_name:=HV8
```
object_nameに他にはHV7などの別物体やHV8_barazumiでばら積みの物体、HV8_box_barazumiで箱付きのばら積みです。
例えば箱付きばら積みは
```
roslaunch photoneo_setup_sim spawn_object.launch object_name:=HV8_box_barazumi
```
<img src="https://github.com/ERiC-Labo/denso_miseru/blob/main/image/HV8_barazumi_box.png" width="100" height="100">

##### モデルの座標のtf(groud_truth)を出す
モデル単体
```
roslaunch tf_publish model_tf.launch object_name:=(物体の種類)
```
モデルが複数
```
roslaunch tf_publish bara_model_tf.launch object_count:=(物体の数) object_name:=(物体の種類)
```
##### 平面部分を除去する
```
roslaunch cloud_practice planar_segmentation.launch
```





### 実行方法(ラフ認識) 
```

roslaunch estimator pose_estimator.launch

roslaunch tf_publish error_calculate.launch #精度算出
```

### 注意するべきパラメータ 
```
roslaunch photoneo_setup_sim spawn_object.launch objectname:=HV8

roslaunch estimator pose_estimator.launch load_path:=your_pretrained_.pth_file
```