# Unity常用函数

# 球插值 Slerp(v1,v2,t)

当其中一个向量为零时停止旋转

# 射线检测

## Physics.CapsuleCast(transform.position, transform.position + Vector3.up * playerHeight, playerRadius, moveDirX, moveDistance);

如果moveDirX为zero，实际上不会在任何方向上移动胶囊体，因为它被指示沿着一个零向量移动。在这种情况下， 不会检测到任何碰撞，因为它没有沿着任何方向移动，所以不会与路径上的任何其他碰撞体相交。

‍
