Overview
++++++++

提供機能
--------

- 位置制御を使用して手先(``hand_palm_link``)の擬似速度を行う(主にジョイスティック等のUIからの入力を想定している)

  1. 擬似速度制御

     指令は、 :ros:msg:`geometry_msgs/TwistStamped` で与え、速度の座標系は指令トピックの ``header/frame_id`` で与えることができる。
     また、軌道演算時の時間は、 ``header/stamp`` で与えることが可能である(**Durationで与えること**)。
      ``header/stamp`` が0の場合、デフォルトの値(``velocity_duration``)が使用される。

      ジョイスティックで、連続的に手先を動かすことを想定している。

- 以下のような制約がある

  * 上記 ``frame_id`` はロボットのボディリンクしか指定できない
  * 制御周期は指令トピックの周期に準ずる
  * 自己干渉は考慮されない
  * 関節角度レベルでの速度制限はかけていない
  * 手先速度が出せない場合はコマンドを出さない(successトピックに ``False`` が発行される)

ROS Interface
++++++++++++++

Nodes
-----

- **hsrb_endeffector_contoller** 手先の擬似速度制御ノード

Subscribed Topics
^^^^^^^^^^^^^^^^^

- **~command_velocity** (:ros:msg:`geometry_msgs/TwistStamped`) 目標の手先速度(台車は動作しない)

- **~command_velocity_with_base** (:ros:msg:`geometry_msgs/TwistStamped`) 目標の手先速度(台車も動作する)

- **joint_states** (:ros:msg:`sensor_msgs/JointState`) 現在の関節角

- **odom** (:ros:msg:`nav_msgs/Odometry`) 現在のオドメトリ

Published Topics
^^^^^^^^^^^^^^^^

- **arm_trajectory_controller/command** (:ros:msg:`trajectory_msgs/JointTrajectory`) arm_trajectory_controllerに対する関節軌道

- **omni_base_controller/command** (:ros:msg:`trajectory_msgs/JointTrajectory`) omni_base_controllerに対する関節軌道

- **~success** (:ros:msg:`std_msgs/Bool`) 手先指令が生成できた場合、 ``True`` を発行し、それ以外は ``False`` を発行する

Service Client
^^^^^^^^^^^^^^

特に無し。

Service Server
^^^^^^^^^^^^^^

特に無し。

Parameter
^^^^^^^^^

- **~velocity_duration** (float64: 0.5) 何秒先の軌道を生成するか[s]
- **~ik_delta** (float64: 0.001) 数値IK許容誤差
- **~discontinuous_period** (float64: 0.5) 指令が途切れたと判断するしきい値[s]，指令が途切れない限り，指令開始時の位置・姿勢を基準に計算する

How to use
++++++++++

Internal
++++++++

.. ifconfig:: internal

   * 手先位置を求めるのは数値IKを用いている
   * *TODO* : 位置コマンドにも対応する
   * *TODO* : 関節の速度制約を考慮した制御時間にする
   * *TODO* : 台車を考慮した手先速度の生成
   * *TODO* : 成功、失敗を通知するインターフェースの設計
