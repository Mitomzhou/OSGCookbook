# OSGCh02Ex01
* 实现左键点击删除一个Drawable
* osgUtil::LineSegmentIntersector::Intersection
	- nodePath: 节点路径
	- drawable: 可绘制对象
* 相机可以直接添加节点.
* osg::Node 可以添加相机节点
* osg::Viewer 添加事件处理器
* osg::Geode
	- removeDrawable: 删除一个可绘制对象

# OSGCh02Ex02
* 演示两种拷贝效果(浅拷贝深拷贝)
* osg::ShapeDrawable::setColor 设置颜色
* osg::Node::clone 拷贝

# OSGCh02Ex03
* 演示一个围绕盒如何随物体运动而变化
* osg::ComputeBoundsVisitor 计算一个节点的围绕盒
* osg::NodePath 节点路径
* osg::computeLocalToWorld(node->getParent(0)->getParentalNodePaths()[0]) 获取本地到世界的矩阵
* osg::BoundingBox::expandBy 扩展围绕盒
* 这里是矩阵右乘
* 在回调中使用缩放也是一种更新几何体的办法
* osg::MatrixTransform 设置动画路径回调, 动画路径回调设置动画路径, 动画路径则为列表, 每个列表为元素为时间与位置方位的组合

# OSGCh02Ex04
* 动画路径实现轮子滚动
* osg::AnimationPath
	- insert()
	- setLoopMode()
* osg::AnimationPathCallback
	- setAnimationPath

# OSGCh02Ex05
* 使用 clipNode 和 clipPlane 裁剪物体
* osg::MatrixTransform --- 矩阵变换
	- preMult: 在父坐标系中进行变换, 倒序乘以矩阵
	- postMult 和上面的代码在程序里面无甚区别
* osg::ClipNode
	- addClipPlane: 添加一个裁剪平面
	- addChild: 添加一个子节点,会应用裁剪平面

# OSGCh02Ex06
* 广度优先访问遍历(BFS)
* 重写 osg::NodeVisitor 的 apply 函数实现广度优先遍历, 使用 node 的 accept 访问下一个节点
	- 不要调用 traverse() 进行遍历, 而是调用自己的 traverseBFS() 进行遍历

# OSGCh02Ex07
* 设置背景图像
* osg::createTexturedQuadGeometry 创建带纹理的四边形
* 创建一个HUD(2纬正交)相机绘制一个四边形,
* 关键是背景四边形节点设置属性 osg::Depth(osg::Depth::LEQUAL, 1.0, 1.0)

# OSGCh02Ex08
* 始终朝向屏幕, 将父节点视图矩阵里的旋转矩阵逆转就可以始终面向屏幕.
* osgUtil::CullVisitor --- Cull 回调设置的回调类其 operator() 的参数类型
	- getModelViewMatrix() --- 得到模型视图矩阵
		- decompose --- 可以分解

# OSGCh02Ex10
* 指南针
* osg::WGS_84_RADIUS_POLAR: WGS84 的地球半径大小
* 地球通过绘地球半径大小的球体实现
* osg::Camera, 使用相机绘制指南针 HUD
	- 可重写函数 void traverse()
* 根据相机计算出北极向量

# OSGCh02Ex11
* 使用 CG
* 下载 CG
	- http://developer.nvidia.com/cg-toolkit
* CMake
```
FIND_PATH(CG_INCLUDE_PATH Cg/cg.h)
FIND_LIBRARY(CG_GL_LIBRARY CgGL)
FIND_LIBRARY(CG_LIBRARY Cg)
INCLUDE_DIRECTORIES(${CG_INCLUDE_PATH })
TARGET_LINK_LIBRARIES(${EXAMPLE_NAME}
  ${CG_LIBRARY} ${CG_GL_LIBRARY})
```