# 面试一般会问到的问题 #
1. 开发中遇到的一些问题，怎么解决的
2. 开发中怎样做一些内存方面的优化
3. 一些成熟的开源框架  图片加载，网络（https）,eventbus 回掉
4. handler
5. 自定义控件
6. 音视频相关的东西
7. 锁机制
8. 线程池（多线程）
9. 5.0的一些新特性（recyleView）
10. 一些借助第三方实现的东西（百度地图，支付，推送，数据统计）
11. 热修复
12. 时间分发

## 事件分发 ##

参考：[http://www.jianshu.com/p/3d4e425d6ca7](http://www.jianshu.com/p/3d4e425d6ca7 "事件分发")

### 事件分发的三个方法 ###



public boolean dispatchTouchEvent


public boolean onInterceptTouchEvent

public boolean onTouchEvent



![图解事件的传递](http://upload-images.jianshu.io/upload_images/966283-d01a5845f7426097.png?imageMogr2/auto-orient/strip%7CimageView2/2)

## 自定义控件 ##

### 三个方法 ###

onMeasure

onLayout

onDraw

![测量模式的判断](http://upload-images.jianshu.io/upload_images/2622762-b1fcf2b9d6e21a54.png?imageMogr2/auto-orient/strip%7CimageView2/2)

### 流式布局的书写 ###

参考：[http://www.jianshu.com/p/a5b1e778744f](http://www.jianshu.com/p/a5b1e778744f "流式布局")

主要在onmeasure的书写（child.layout）

在onmeasure中测量子控件的大小（measureChild）

        int hadUsedHorizontal = 0;//水平已经使用的距离
        int hadUsedVertical = 0;//垂直已经使用的距离

        int width = getMeasuredWidth();//如果使用getWidth返回值为0，因为只有测量之后才会有值

        for(int i = 0;i<getChildCount();i++){
            View child = getChildAt(i);
            if(child.getMeasuredWidth()+hadUsedHorizontal>width){
                hadUsedVertical = hadUsedVertical+child.getMeasuredHeight()+verticalSpace;
                hadUsedHorizontal = 0;
            }

            child.layout(hadUsedHorizontal,hadUsedVertical,hadUsedHorizontal+child.getMeasuredWidth(),hadUsedVertical+child.getMeasuredHeight());
            hadUsedHorizontal = hadUsedHorizontal+horizontalSpace+child.getMeasuredWidth();
        }



**问题1.一个自定义控件，即使定义wraContent,依然是填充父窗体的**

解决方式就是重写onmeasure方法

    @Override
    protected void onMeasure(int widthMeasureSpec, int heightMeasureSpec) {
        super.onMeasure(widthMeasureSpec, heightMeasureSpec);
	//        for(int i = 0; i < getChildCount();i++){
	//            View child = getChildAt(i);
	////            child.measure(widthMeasureSpec,heightMeasureSpec);
	//            measureChild(child,widthMeasureSpec,heightMeasureSpec);
	//        }
        //父布局的宽高和模式
        int sizeWidth = MeasureSpec.getSize(widthMeasureSpec);
        int modeWidth = MeasureSpec.getMode(widthMeasureSpec);
        int sizeHeight = MeasureSpec.getSize(heightMeasureSpec);
        int modeHeight = MeasureSpec.getMode(heightMeasureSpec);

        //行高和行宽
        int lineWidth = 0;
        int lineHeight = 0;

        //实际的宽高
        int width = 0;
        int height = 0;

        int childWidth = 0;
        int childHeight = 0;

        for(int i = 0; i <getChildCount();i++){
            View child = getChildAt(i);
            measureChild(child,widthMeasureSpec,heightMeasureSpec);
            MarginLayoutParams lp = (MarginLayoutParams) child.getLayoutParams();
            childWidth = child.getMeasuredWidth()+lp.leftMargin+lp.rightMargin;
            childHeight = child.getMeasuredHeight()+lp.topMargin+lp.bottomMargin;
            if(lineWidth+childWidth>sizeWidth){
                //换行操作
               width = Math.max(lineWidth,width);
               height = height+childHeight;
                //更新行宽和行高
                lineWidth = childWidth;
                lineHeight = childHeight;
            }else{
                //不换行
                lineWidth += childWidth;
                lineHeight = Math.max(childWidth,lineHeight);
            }
        }

        setMeasuredDimension(width,height);

    }

**问题2 让控件支持margin属性，Layoutparams,不同的LayoutParams可以让子控件自持不同的属性**

解决方式，重写父类方法

    @Override
    public LayoutParams generateLayoutParams(AttributeSet attrs) {
        return new MarginLayoutParams(getContext(),attrs);
    }


## 线程池和锁机制 ##












