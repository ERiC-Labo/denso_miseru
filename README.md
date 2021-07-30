### 実行方法(ラフ認識) 
```
roslaunch photoneo_setup_sim spawn_object.launch 

roslaunch tf_publish model_tf.launch

roslaunch cloud_practice planar_segmentation.launch

roslaunch estimator pose_estimator.launch

roslaunch tf_publish error_calculate.launch #精度算出
```

### 注意するべきパラメータ 

#### roslaunch photoneo_setup_sim spawn_object.launch objectname:=HV8

roslaunch tf_publish model_tf.launch

roslaunch cloud_practice planar_segmentation.launch

#### roslaunch estimator pose_estimator.launch load_path:=your_pretrained_.pth_file

roslaunch tf_publish error_calculate.launch
