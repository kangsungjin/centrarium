
소개
<hr/>
ConstraintLayout API9(진저 브레드)로 시작하는 Android 시스템에서 사용할 수 있는 지원 라이브러리로 사용할수 
있ek. 

#[ConstraintLayout](https://developer.android.com/reference/android/support/constraint/ConstraintLayout)


__레이아웃 그룹기능(Guideline, Barrier, Group)__{: style="color: #1b557a"} 

#### Guideline

기준선 가로/세로가 되는 라인을 만들어준다. 

~~~java

android:orientation=vertical | horizontal

~~~


__레이아웃 정렬기능(Guideline, Barrier, Group)__{: style="color: #1b557a"} 

### Relative Positioning(상대 위치 지정)

<strong>app:layout_constraint(Positioning)</strong>
<strong>상대적 위치는 @+id 또는 parent 로 구분한다.</strong>
~~~java
layout_constraintTop_toBottomOf = "@+id/HEAD | parent"
> 현재 나의 Top Point를 HEAD bottom Point와 연결한다.

layout_constraintLeft_toLeftOf
layout_constraintLeft_toRightOf
--
layout_constraintRight_toLeftOf
layout_constraintRight_toRightOf
--
layout_constraintTop_toTopOf
layout_constraintTop_toBottomOf
--
layout_constraintBottom_toTopOf
layout_constraintBottom_toBottomOf
--
layout_constraintBaseline_toBaselineOf
--
layout_constraintStart_toEndOf
layout_constraintStart_toStartOf
--
layout_constraintEnd_toStartOf
layout_constraintEnd_toEndOf
~~~

### Margins
<strong> 0 또는 양수값을 사용한다. Dimens에서도 값을 불러올수 있다. </strong>

~~~java
보통 사용하는 여백
android:layout_marginStart
android:layout_marginEnd
android:layout_marginLeft
android:layout_marginTop
android:layout_marginRight
android:layout_marginBottom
--
GONE 위젯에 연결될때 여백값
layout_goneMarginStart
layout_goneMarginEnd
layout_goneMarginLeft
layout_goneMarginTop
layout_goneMarginRight
layout_goneMarginBottom

~~~

#### Bias
~~~java

~~~

#### 비율
width & height 크기를 넓히는 작업을 할때 이런식으로 비율로 넓혀도 된다. 

~~~java
android:layout_width="0dp"
android:layout_height="0dp"
--
app:layout_constraintDimensionRatio="H,16:9" ||app:layout_constraintDimensionRatio="W,9:16"
OR
app:layout_constraintHorizontal_weight="1"
app:layout_constraintVertical_weight="1"
--
SUM Area Parent Height 16 : head area 1 : content area: 15

<button 
android:id="@+id/btn1"
android:layout_width="0dp"
android:layout_height="0dp"
app:layout_constraintDimensionRatio="H,3:3"
OR
app:layout_constraintHorizontal_weight="1"
app:layout_constraintVertical_weight="1"
>

<button 
android:id="@+id/btn2"
android:layout_width="0dp"
android:layout_height="0dp"
app:layout_constraintDimensionRatio="H,3:3"
OR
app:layout_constraintHorizontal_weight="1"
app:layout_constraintVertical_weight="1"
>

<button 
android:id="@+id/btn3"
android:layout_width="0dp"
android:layout_height="0dp"
app:layout_constraintDimensionRatio="H,3:3"
OR
app:layout_constraintHorizontal_weight="1"
app:layout_constraintVertical_weight="1"
>

<button 
android:id="@+id/btn4"
android:layout_width="0dp"
android:layout_height="0dp"
app:layout_constraintDimensionRatio="H,3:3"
OR
app:layout_constraintHorizontal_weight="1"
app:layout_constraintVertical_weight="1"
>

<button 
android:id="@+id/btn5"
android:layout_width="0dp"
android:layout_height="0dp"
app:layout_constraintDimensionRatio="H,3:3"
OR
app:layout_constraintHorizontal_weight="1"
app:layout_constraintVertical_weight="1"
>


~~~~


