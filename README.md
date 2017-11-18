#### 原 Materialish-Progress项目更新维护。
#### 参考原项目地址:[https://github.com/pnikosis/materialish-progress](https://github.com/pnikosis/materialish-progress)

# Material-ish Progress

> I needed to keep a consistent (or as close as possible) look in an app across all Android Versions. The progress wheel is quite cool in Lollipop, and pretty horrible on Gingerbread.

> So I created this. This view uses Progress Wheel as a base, but has been almost completely rewritten (the original view uses handlers for updating the wheel).

> This implementation tries to follow as close as possible the guidelines for the circular progress as described here.

> This is how it looks in indeterminate mode (the spinSpeed here is 0.64 which is the default, look below how to change it):

![](http://img.blog.csdn.net/20171117144437662?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvV2lzdG9ybXM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

> And in determinate mode (here the spinSpeed is set to 0.333):

![](http://img.blog.csdn.net/20171117144547761?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvV2lzdG9ybXM=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### Download

> You can create your own progress wheel in xml like this
>  (remeber to add `xmlns:wheel="http://schemas.android.com/apk/res-auto"`):

```
compile 'com.github.cazaea:materialish-progress:1.0.2'
```
> Add it in your root build.gradle at the end of repositories:
```
allprojects {
		repositories {
			...
			maven { url 'https://jitpack.io' }
		}
	}
```
### Usage

```
<com.cazaea.materialishprogress.ProgressWheel
        android:id="@+id/progress_wheel"
        android:layout_width="80dp"
        android:layout_height="80dp"
        android:layout_centerHorizontal="true"
        android:layout_centerVertical="true"
        wheel:matProg_barColor="#5588FF"
        wheel:matProg_progressIndeterminate="true" />
```

> Or in code:

```
ProgressWheel wheel = new ProgressWheel(context);
wheel.setBarColor(Color.BLUE);
...
```
### Callback 
> Use `setCallback(ProgressCallback)` to assign a callback that will be called each time the progress changes. This way you can update a value on the progress alongside with the progress animation, or execute an action once the progress reaches a certain value. in the indeterminatge wheel, the callback is called with a value of -1.0f every time the animation cycle finishes (when the wheel shrinks back to its smaller size).

### Indeterminate wheel 

> For making the wheel indeterminate, just call the `spin()` method. If you set a progress value, the wheel will stop spinning.

> You have two methods for setting the progress:
```
progressWheel.setProgress(float value)
```
> Sets the value, and the wheel will smoothly animate to that value. The speed of the animation is defined by the spinSpeed (can be set with`setSpinSpeed` , which number is the number of full turns per second)
```
progressWheel.setInstantProgress(float value)
```
> Sets the value, and the wheel will instantly move to that value.

> You can change other wheel properties such as the progress bar color, the wheel's background or the wheel's size and width.

### Fill radius 
> In case you want the spinning wheel to fill the whole layout instead of having a fixed size, you can use `matProg_fillRadius`.
```
<com.cazaea.materialishprogress.ProgressWheel
        android:id="@+id/progress_wheel"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_centerHorizontal="true"
        android:layout_centerVertical="true"
        wheel:matProg_barColor="#5588FF"
        wheel:matProg_progressIndeterminate="true"
        wheel:matProg_fillRadius="true" />
```
> This way, the wheel will be as big as the parent layout. Be warned though, if the parentlayout is not square, the wheel will become an oval since the wheel will always adapt to fill the parent view.

### Other options 
>In the xml definition, besides the fillRadius property, you can set:

 - matProg_progressIndeterminate: boolean, if you want the wheel to spin right away.
 - matProg_barColor: color, sets the small bar's color (the spinning bar in the indeterminate wheel, or the progress bar)
 - matProg_barWidth: dimension, the width of the spinning bar
 - matProg_rimColor: color, the wheel's border color
 - matProg_rimWidth: dimension, the wheel's width (not the bar)
 - matProg_spinSpeed: float, the base speed for the bar in indeterminate mode, and the animation speed when setting a value on progress. The speed is in full turns per second, this means that if you set speed as 1.0, means that the bar will take one second to do a full turn.
 - matProg_barSpinCycleTime: integer, the time in milliseconds the indeterminate progress animation takes to complete (extending and shrinking the bar while spinning)
 - matProg_circleRadius: dimension, the radius of the progress wheel, it will be ignored if you set fillRadius to true
 - matProg_fillRadius: boolean, set to true if you want the progress wheel to fill the whole layout
 - matProg_linearProgress: boolean, set to true if you want a linear animation on the determinate progress (instead of the interpolated default one).

### License 
```
Copyright 2017 Cazaea

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
