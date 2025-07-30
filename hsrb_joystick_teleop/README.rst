Overview
++++++++

提供機能
--------

- ジョイスティックによるロボット操作

Nodes
-----

- **joystick_control** ジョイスティック操作ノード

Subscribed Topics
^^^^^^^^^^^^^^^^^

- **/hsrb/joy** (:ros:msg:`sensor_msgs/Joy`) ジョイスティック入力

- **/hsrb/joint_states** (:ros:msg:`sensor_msgs/JointState`)

  説明:
    関節情報

  該当クラス:
    -  DynamicStoragePoseControl

Published Topics
^^^^^^^^^^^^^^^^

- **/hsrb/pseudo_velocity_controller/ref_joint_velocity** (:ros:msg:`tmc_msgs/JointVelocity`)

  説明:
    目標関節速度と名前

  該当クラス:
    -  SingleJointControl
    -  MultiJointControl

- **/hsrb/pseudo_endeffector_controller/command_velocity** (:ros:msg:`geometry_msgs::TwistStamped`)

  説明:
    目標の手先速度(台車動作なし)

  該当クラス:
    -  BaseControl

- **/hsrb/pseudo_endeffector_controller/command_velocity_with_base** (:ros:msg:`geometry_msgs::TwistStamped`)

  説明:
    目標の手先速度(台車動作あり)

  該当クラス:
    -  EndeffectorControl

- **/hsrb/command_velocity** (:ros:msg:`geometry_msgs/Twist`)

  説明:
    目標速度

  該当クラス:
    -  BaseControl

- **/hsrb/command_drive_power** (:ros:msg:`std_msgs/Bool`)

  説明:
    サーボOFF/ON

  該当クラス:
    -  DrivePowerControl

- **/hsrb/gripper_controller/apply_force/goal** (:ros:msg:`tmc_control_msgs/GripperApplyEffortActionGoal`)

  説明:
    ハンド握りこみアクションゴール

  該当クラス:
    -  HandControl

- **/hsrb/gripper_controller/command** (:ros:msg:`tmc_control_msgs::GripperApplyEffortActionGoal`)

  説明:
    ハンド操作の指令軌道

  該当クラス:
    -  HandControl

- **/hsrb/gripper_controller/grasp/goal** (:ros:action:`tmc_control_msgs/GripperApplyEffortActionGoal`)

  説明:
    ハンド開閉アクションゴール

  該当クラス:
    -  HandControl

- **/safe_pose_changer/joint_reference** (:ros:msg:`sensor_msgs/JointState`)

  説明:
    遷移先姿勢

  該当クラス:
    -  InitPoseControl
    -  DefaultPoseControl
    -  DynamicStoragePoseControl

- **/talk_request** (:ros:msg:`tmc_msgs/Voice`) 音声発話

Action Client
^^^^^^^^^^^^^

- **/hsrb/suction_control** (:ros:action:`tmc_suction/SuctionControlAction`)

  説明:
    吸引開始/終了アクション

  該当クラス:
    -  SuctionControl

- **/hsrb/autocharge_node/dock** (:ros:action:`hsrb_autocharge/ChargeStationDockControlAction`)

  説明:
    自動充電ドッキングアクション

  該当クラス:
    -  AutoChargeDockControl

Parameter
^^^^^^^^^

- **controls/コントローラ名/type**

  説明:
    コントローラタイプ

  該当クラス:
    -  SingleJointControl
    -  MultiJointControl
    -  BaseControl
    -  EndeffectorControl
    -  InitPoseControl
    -  DefaultPoseControl
    -  DynamicStoragePoseControl
    -  HandControl
    -  SuctionControl
    -  AutoChargeDockControl
    -  DrivePowerControl

- **controls/コントローラ名/button**

  説明:
    ボタン入力仕様
    ジョイスティックのボタンによる操作入力の仕様を与える。

  該当クラス:
    -  SingleJointControl
    -  MultiJointControl
    -  BaseControl
    -  EndeffectorControl
    -  InitPoseControl
    -  DefaultPoseControl
    -  DynamicStoragePoseControl
    -  HandControl
    -  SuctionControl
    -  AutoChargeDockControl
    -  DrivePowerControl

- **controls/コントローラ名/voice_notification**

  説明:
    音声通知が有効の時に通知するかどうか

  該当クラス:
    -  SingleJointControl
    -  MultiJointControl
    -  BaseControl
    -  EndeffectorControl
    -  InitPoseControl
    -  DefaultPoseControl
    -  DynamicStoragePoseControl
    -  HandControl
    -  SuctionControl
    -  AutoChargeDockControl
    -  DrivePowerControl

- **controls/コントローラ名/dead_zone**

  説明:
    多軸を同時に動かす際のジョイスティックの不感帯設定[0.0, 1.0]

  該当クラス:
    -  MultiJointControl
    -  BaseControl
    -  EndeffectorControl

- **controls/コントローラ名/frame**

  説明:
    MoveControlで指定されるフレーム名

  該当クラス:
    -  EndeffectorControl

- **controls/コントローラ名/axis**

  説明:
    軸入力仕様

    ジョイスティックの各軸の操作入力の仕様を下記のようにmapまたは個別で与える。
    省略した場合その軸は操作できない。

    .. code-block:: yaml

       axis:
         x: 1
         y: 2
         z: 3
         roll: 4
         pitch: 5
         yaw: 6

  該当クラス:
    -  BaseControl
    -  EndeffectorControl

- **controls/コントローラ名/scale**

  説明:
    速度変換仕様

    ジョイスティックの操作をTwist型に変換する際のスケール。
    下記のようにmapで与える。
    省略した場合0.0となる。

    .. code-block:: yaml

       scale:
         x: 0.1
         y: 0.1
         z: 0.1
         roll: 0.5
         pitch: 0.5
         yaw: 0.5

  該当クラス:
    -  BaseControl
    -  EndeffectorControl

- **controls/コントローラ名/enable_button**

  説明:
    操作を有効にするためのボタン仕様

  該当クラス:
    -  InitPoseControl
    -  DefaultPoseControl
    -  HandControl
    -  AutoChargeDockControl
    -  DrivePowerControl

- **controls/コントローラ名/pose_save_button**

  説明:
    現在の姿勢を保存するためのボタン仕様

  該当クラス:
    -  DynamicStoragePoseControl

- **controls/コントローラ名/force_enable_button**

  説明:
    握りこみ制御を有効にするためのボタン仕様

  該当クラス:
    -  HandControl

- **controls/コントローラ名/joint_names**

  説明:
    姿勢遷移で使用する関節名

  該当クラス:
    -  InitPoseControl
    -  DefaultPoseControl
    -  DynamicStoragePoseControl

- **controls/コントローラ名/joint_positons**

  説明:
    姿勢遷移で使用する関節位置

  該当クラス:
    -  InitPoseControl
    -  DefaultPoseControl
    -  DynamicStoragePoseControl

- **controls/コントローラ名/関節名/axis**

  説明:
    該当する関節の軸入力仕様

  該当クラス:
    -  SingleJointControl
    -  MultiJointControl

- **controls/コントローラ名/関節名/velocity**

  説明:
    該当する関節の速度入力仕様

  該当クラス:
    -  SingleJointControl
    -  MultiJointControl

- **assisted_voice_notification** (bool: false) 音声によるコントロールモード変更通知

Internal
++++++++

.. ifconfig:: internal

   本パッケージの作成経緯
     * 同様のjoystick制御パッケージにhsrb_interactive_teleopがあるが、プラグインで書かれているため、
       仕組みを理解している人でないと機能の拡張が困難
     * 仕組みを簡略化して、メンテナンスしやすいようにするため

   hsrb_interactive_teleopとの差分
     * プラグイン不使用
     * 1つのyamlファイルでjoystick操作に関するすべての設定を管理

   振る舞い:
     * ボタンは複数指定が可能
     * 操作の判定はボタン数が多い順に行われる
