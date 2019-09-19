测试场景中从左到右的粒子分别为：
- ### simulation_local_limit_local
粒子在局部空间中模拟，限速施加在局部空间中，正确表现结果，平移粒子，粒子会跟着一起平移，旋转粒子，粒子运动轨迹也跟着一起旋转
- ### simulation_world_limit_local
粒子在世界空间中模拟，限速施加在局部空间中，正确表现结果，平移粒子，粒子不会跟着一起平移，旋转粒子，粒子运动轨迹也跟着一起旋转
- ### simulation_local_limit_world
粒子在局部空间中模拟，限速施加在世界空间中，正确表现结果，平移粒子，粒子会跟着一起平移，旋转粒子，粒子运动轨迹不跟着一起旋转
- ### simulation_world_limit_world
粒子在世界空间中模拟，限速施加在世界空间中，正确表现结果，平移粒子，粒子不会跟着一起平移，旋转粒子，粒子运动轨迹不跟着一起旋转