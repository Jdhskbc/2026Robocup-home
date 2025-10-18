启动底盘，雷达，顶部相机节点
roslaunch tracer_bringup tracer_robot_base.launch
启动ur机械臂
roslaunch tracer_bringup tracer_ur_bringup.launch

机械臂二次上电
tra_ur3_power_on

释放刹车
tra_ur3_brake_release

加载程序
tra_ur3_load

执行程序
tra_ur3_play

抓取控制代码
手动将graspnet输出粘贴到输入变量中
~/tracer_ws/src/my_ur_control/scripts/ur3_grab.py（如果执行有问题，ctrl c重新执行）

拍照程序
~/tracer_ws/src/camera_ros/camera_control/scripts/get_photo.py
保存在
~/tracer_ws/src/camera_ros/images

python3 ~/tracer_ws/src/camera_ros/camera_control/scripts/get_photo.py

graspnet
~/graspnet-baseline/doc/d405_data/cola 输入文件夹
输入四个文件，color，depth由相机拍，workspace_mask由sam给出，meta.mat固定
CUDA_VISIBLE_DEVICES=0 python demo.py --checkpoint_path logs/log_rs/checkpoint-rs.tar


 python3 demo1.py --checkpoint_path logs/log_rs/checkpoint-rs.tar \
    --data_dir doc/d405_data/cola \
    --median_ksize 5 --mask_kernel 5 \
    --voxel_downsample 0.003 \
    --remove_outlier --outlier_nb_neighbors 30 --outlier_std_ratio 1.5 \
    --top_k 10 --score_thresh 0.2

sam2
输入文件夹~/Grounded-SAM-2/notebooks/images/my_images
输出文件加~/Grounded-SAM-2/outputs/test_output
  cd ~/Desktop/tracer_ws/Grounded-SAM-2（复件）
  python3 grounded_sam2_local_demo.py


关电只关底盘和机械臂，其他不用关，机械臂关电中间的绿色按钮

机械臂开电先按左边的绿色按钮，过大概一分钟听到连续几声动静后再开机械臂节点

