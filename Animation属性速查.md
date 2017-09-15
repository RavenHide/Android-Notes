# Animator属性速查

## XML属性

| 属性              | 解释                                       |
| --------------- | ---------------------------------------- |
| fromXScale      | 动画开始时X轴的缩放比例                             |
| toXScale        | 动画结束时X轴的缩放比例                             |
| fromYScale      | 动画开始时Y轴的缩放比例                             |
| toYScale        | 动画结束时Y轴的缩放比例                             |
| fromDegrees     | 动画开始时的旋转角度，正值为顺时针，负值为逆时针                 |
| toDegrees       | 动画结束时的旋转角度，正值为顺时针，负值为逆时针                 |
| fromAlpha       | 动画开始时的透明度，0.0为全透明，1.0为完全不透明              |
| toAlpha         | 动画结束时的透明度，0.0为全透明，1.0为完全不透明              |
| pivotX          | 动画起点X轴坐标，可以是数值、百分数、百分数p 三种样式，比如 50、50%、50%p，当为数值时，表示在当前View的左上角，即原点处加上50px，做为起始缩放点；如果是50%，表示在当前控件的左上角加上自己宽度的50%做为起始点；如果是50%p，那么就是表示在当前的左上角加上父控件宽度的50%做为起始点x轴坐标。 |
| pivotY          | 动画起点Y轴坐标，取值及意义跟android:pivotX一样          |
| fromXDelta      | 取值及意义跟android:pivotX一样                   |
| toXDelta        | 取值及意义跟android:pivotX一样                   |
| fromYDelta      | 取值及意义跟android:pivotX一样                   |
| toYDelta        | 取值及意义跟android:pivotX一样                   |
| fillAfter       | 如果设置为true，控件动画结束时，将保持动画最后时的状态            |
| fillBefore      | 如果设置为true,控件动画结束时，还原到开始动画前的状态            |
| fillEnabled     | 与android:fillBefore 效果相同，都是在动画结束时，将控件还原到初始化状态 |
| repeatCount     | 重复次数,如果为infinite或者-1就表示无限循环              |
| repeatMode      | 重复类型，有reverse和restart两个值，reverse表示倒序回放，restart表示重新放一遍，必须与repeatCount一起使用才能看到效果。因为这里的意义是重复的类型，即回放时的动作。 |
| startOffset     | 延时多少毫秒后，开始播放动画                           |
| interpolator    | 插值器，影响的动画的执行效果                           |
| detachWallpaper | 是否在壁纸上运行                                 |
| duration        | 动画持续时间                                   |
| zAdjustment     | 表示被设置动画的内容运行时在Z轴上的位置（top/bottom/normal），默认为normal |

------

## **Interpolator(插值器)**类型

| java                             | xml                                      | 解释              |
| -------------------------------- | ---------------------------------------- | --------------- |
| AccelerateDecelerateInterpolator | @android:anim/accelerate_decelerate_interpolator | 先加速后减速          |
| AccelerateInterpolator           | @android:anim/accelerate_interpolator    | 从0开始加速运动        |
| AnticipateInterpolator           | @android:anim/anticipate_interpolator    | 先退后再加速向前        |
| AnticipateOvershootInterpolator  | @android:anim/anticipate_overshoot_interpolator | 先退后再加速超过终点再返回终点 |
| BounceInterpolator               | @android:anim/bounce_interpolator        | 到终点的时候回弹直到停止    |
| CycleInterpolator                | @android:anim/cycle_interpolator         | 以正弦的方式运动        |
| DecelerateInterpolator           | @android:anim/decelerate_interpolator    | 减速向前            |
| LinearInterpolator               | @android:anim/linear_interpolator        | 匀速运动            |
| OvershootInterpolator            | @android:anim/overshoot_interpolator     | 加速运动超过终点再返回终点   |