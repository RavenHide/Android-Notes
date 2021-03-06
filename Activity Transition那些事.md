# Activity Transition

> Activity Transition是Material Design中提供的一种动画效果，它通过运动和切换不同状态之间的元素来产生各种动画效果。





## 5.0之前的那些事

Android 5.0之前，Activity可以通过`overridePendingTransition()`和FragmentTransition的`setCustomAnimation()`来实现Activity或Fragment的动画切换。

缺陷：局限于将整个视图一起动画变换

------





## Transition分类

### 普通Transition

- explode :explode: 从场景的中心移入或移出
- slide: 从场景边缘滑入或滑出
- fade: 淡入淡出效果



### 共享元素Transition

> 使两个activity共享一种共同的元素，API要求是5.0以上

- changeBounds: 改变目标视图的布局边界
- changeClipBounds: 裁剪目标视图的边界
- changeTransfrom: 改变目标视图的缩放比例
- changeImageTransfrom: 改变目标图片的大小和缩放比例



## Transition描述

A和B分别是两个Activity，假设activity A 调用activity B。将A代表调用Activity ，B代表被调用Activity。

> Fragment也是相同

1. Activity A的退出变换（exit transition）决定了在A调用B的时候，A中的View是如何播放动画的。
2. Activity B的进入变换（enter transition）决定了在A调用B的时候，B中的View是如何播放动画的。
3. Activity B的返回变换（return transition）决定了在B返回A的时候，B中的View是如何播放动画的。
4. Activity A的再次进入变换（reenter transition）决定了在B返回A的时候，A中的View是如何播放动画的。



## 简单使用

1. 在调用与被调用的activity中，通过设定`Window.FEATURE_ACTIVITY_TRANSITIONS`  和 `Window.FEATURE_CONTENT_TRANSITIONS` 来启用transition api ，可以通过代码也可以通过设置主题来启用：
   代码使用方式，在setContentView之前调用，也可以理解为在view加载之前调用

   ```java
   getWindow().requestFeature(Window.FEATURE_CONTENT_TRANSITIONS);
   ```

   或者主题XML

   ```xml
   <item name="android:windowContentTransitions">true</item>
   ```

2. 分别在调用与被调用的activity中设置exit 和enter transition。Material主题默认会将exit的transition设置成null而enter的transition设置成Fade .如果reenter 或者 return transition没有明确设置，则将用exit 和enter的transition替代。

3. 分别在调用与被调用的activity中设置exit 和enter 共享元素的transition。Material主题默认会将exit的共享元素transition设置成null而enter的共享元素transition设置成`@android:transition/move`.如果reenter 或者 return transition没有明确设置，则将用exit 和enter的共享元素transition替代。

   开始一个activity的**content transaction**需要调用**`startActivity(Context, Bundle)`**方法，将下面的bundle作为第二个参数：

   ```java
   ActivityOptions.makeSceneTransitionAnimation(activity, pairs).toBundle();
   ```

4. 在代码中触发通过`finishAfterTransition()`方法触发返回动画，而不是调用finish()方法。

5. .默认情况下，material主题的应用中**enter/return**的**content transition**会在**exit/reenter**的**content transitions**结束之前开始播放（只是稍微早于），这样会看起来更加连贯。如果你想明确屏蔽这种行为，可以调用`setWindowAllowEnterTransitionOverlap()` 和 `setWindowAllowReturnTransitionOverlap()`方法。



# Fragment  Transition API简单介绍

Fragment Transition大体和上文介绍的Activity Transition一致

1. Content的exit, enter, reenter, 和return transition需要调用fragment的相应方法来设置，或者通过fragment的xml属性来设置。
2. 共享元素的enter和return transition也n需要调用fragment的相应方法来设置，或者通过fragment的xml属性来设置。
3. 虽然在activity中transition是被startActivity()和finishAfterTransition()触发的，但是Fragment的transition却是在其被FragmentTransaction执行下列动作的时候自动发生的。**added**, **removed**, **attached**, **detached**, **shown**, ，**hidden**。
4. 在**Fragment commit**之前，共享元素需要通过调用`addSharedElement(View, String)`方法来成为**FragmentTransaction**的一部分。


# 相应的动画插值器

```
AccelerateDecelerateInterpolator 在动画开始与结束的地方速率改变比较慢，在中间的时候加速

AccelerateInterpolator  在动画开始的地方速率改变比较慢，然后开始加速

AnticipateInterpolator 开始的时候向后然后向前甩

AnticipateOvershootInterpolator 开始的时候向后然后向前甩一定值后返回最后的值

BounceInterpolator   动画结束的时候弹起

CycleInterpolator 动画循环播放特定的次数，速率改变沿着正弦曲线

DecelerateInterpolator 在动画开始的地方快然后慢

LinearInterpolator   以常量速率改变

OvershootInterpolator    向前甩一定值后再回到原来位置
```

# 动画XML属性

```
android:windowContentTransitions                允许使用transitions

android:windowAllowEnterTransitionOverlap        是否覆盖执行，其实可以理解成前后两个页面是同步执行还是顺序执行

android:windowAllowReturnTransitionOverlap        与上面相同。即上一个设置了退出动画，这个设置了进入动画，两者是否同时执行。

android:windowContentTransitionManager            引用TransitionManager XML资源，定义不同窗口内容之间的所需转换。



android:windowEnterTransition                    首次进入显示的动画

android:windowExitTransition                    启动新 Activity ，此页面退出的动画

android:windowReenterTransition                    重新进入的动画。即第二次进入，可以和首次进入不一样。

android:windowReturnTransition                    调用 finishAfterTransition() 退出时，此页面退出的动画



android:windowSharedElementsUseOverlay            指示共享元素在转换期间是否应使用叠加层。

android:windowSharedElementEnterTransition        首次进入显示的动画

android:windowSharedElementExitTransition        启动新 Activity ，此页面退出的动画

android:windowSharedElementReenterTransition    重新进入的动画。即第二次进入，可以和首次进入不一样。

android:windowSharedElementReturnTransition        调用 finishAfterTransition() 退出时，此页面退出的动画
```