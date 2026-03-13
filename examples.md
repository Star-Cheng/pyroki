# PyRoki 示例说明

本文档介绍 `examples/` 目录下各示例的用途和用法。PyRoki 是用于机器人运动学优化的 Python 工具库，支持 URDF 正运动学、碰撞检测、轨迹优化和动作重定向等能力。

---

## 基础逆运动学 (IK)

### 01_basic_ik.py
**最简单的 IK 示例**

- 使用 Panda 机械臂
- 通过 Viser 拖动末端目标位姿
- 实时求解关节角使末端到达目标
- 适合作为入门示例

### 02_bimanual_ik.py
**双臂 IK**

- 使用 YuMi 双臂机器人
- 同时满足两个末端执行器的位姿约束
- 对应 snippet：`solve_ik_with_multiple_targets`

### 03_mobile_ik.py
**带移动基座的 IK**

- 使用 Fetch 机器人
- 基座在 xy 平面自由移动，绕 z 轴旋转
- 同时优化基座位姿和手臂关节
- 对应 snippet：`solve_ik_with_base`

---

## 高级 IK 约束

### 04_ik_with_coll.py
**带碰撞避障的 IK**

- Panda 机械臂 + 地面 + 可拖动的球体障碍物
- 支持胶囊 (Capsule) 和球体 (Sphere) 两种机器人碰撞模型
- 可切换碰撞类型并可视化碰撞体
- 对应 snippet：`solve_ik_with_collision`

### 05_ik_with_manipulability.py
**带可操作性优化的 IK**

- 在末端目标约束基础上加入 Yoshikawa 可操作性指标
- 通过 GUI 调节可操作性权重
- 可改善靠近奇异点的姿态
- 对应 snippet：`solve_ik_with_manipulability`

### 08_ik_with_mimic_joints.py
**Mimic 关节 IK**

- 程序生成带 mimic 关节的链式结构
- 验证 PyRoki 对 mimic 关节（联动关节）的支持
- 可切换目标连杆观察不同末端求解效果

### 13_ik_with_locked_joints.py
**带关节锁定的 IK**

- 通过复选框锁定/解锁单个关节
- 锁定关节在优化中保持固定值
- 可查看位置误差等指标

---

## 轨迹规划与优化

### 06_online_planning.py
**在线规划**

- 在有障碍物的环境中实时规划
- 目标位姿可拖动，障碍物可移动
- 规划避障轨迹并显示规划出的轨迹帧
- 对应 snippet：`solve_online_planning`

### 07_trajopt.py
**轨迹优化**

- 机械臂跨越障碍墙，从一侧到达另一侧
- 支持 Panda 和 UR5（通过 `--robot-name` 选择）
- 生成整条无碰撞、平滑的轨迹
- 运行示例：`python 07_trajopt.py --robot-name panda`
- 对应 snippet：`solve_trajopt`

---

## 动作重定向 (Retargeting)

### 09_hand_retargeting.py
**手部动作重定向（基础版）**

- 将 DexYCB 人手关键点重定向到 Shadow Hand
- 需要解压 `retarget_helpers/hand/shadowhand_urdf.zip`
- 支持局部对齐、全局对齐、关节平滑等代价

### 11_hand_retargeting_fancy.py
**手部动作重定向（进阶版）**

- 在基础版上增加**物体接触约束**
- 手在抓握物体时保持接触点约束
- 支持接触权重、接触容差等参数调节

### 10_humanoid_retargeting.py
**人形动作重定向（基础版）**

- 将 SMPL 人体关键点重定向到 G1 人形机器人
- 使用高度图进行地形适配
- 支持脚接触、关节平滑等代价

### 12_humanoid_retargeting_fancy.py
**人形动作重定向（进阶版）**

- 在基础版上增加更多约束：
  - **地面接触**：脚贴合高度图
  - **防滑步**：接触时脚不滑动
  - **自碰撞**：避免肢体自碰
  - **环境碰撞**：避免与场景碰撞

---

## 辅助目录

| 路径 | 说明 |
|------|------|
| `pyroki_snippets/` | 各示例复用的 IK/规划函数封装 |
| `assets/` | 机器人球体分解 JSON、碰撞相关资源 |
| `retarget_helpers/` | 手部、人形重定向的映射和工具函数 |

---

## 依赖与运行

- 需安装 PyRoki、viser、robot_descriptions 等依赖
- 部分示例需要对应机器人描述包（如 `panda_description`、`yumi_description`）
- 手部重定向示例需 Shadow Hand URDF
- 建议在 PyRoki 项目根目录或 examples 目录下运行
