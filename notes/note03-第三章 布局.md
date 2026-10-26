# 1.常用布局控件

##  **Grid（网格布局）**

  - **特点**：通过自定义行（RowDefinitions）和列（ColumnDefinitions）来划分网格，控件可以指定在某行某列中。它是 WPF 中最强大、最常用的布局控件。

## **StackPanel（栈式面板）**
  - **特点**：将子元素按水平方向（Horizontal）或垂直方向（Vertical）排成一条直线。

## **WrapPanel（自动折行面板）**
  - **特点**：子元素按水平或垂直方向顺序排列，当空间不足时会自动折行到下一行或下一列。

## **DockPanel（停靠面板）**
  - **特点**：子元素根据设置停靠在面板的**上、下、左、右**边缘，最后一个子元素（通常设置 `LastChildFill="True"`）可以填充剩余的所有空间。 

## **UniformGrid（均布网格）**
  - **特点**：所有网格单元格的大小完全均等，不需要手动设置行高和列宽，系统会自动平均分配。

## **Canvas（画布）**
  - **特点**：使用显式的坐标（通过 `Canvas.Left`、`Canvas.Top` 等附加属性）来精确定位子元素，类似于 WinForms 的绝对定位。 

## **ScrollViewer（滚动条视图）**
  - **特点**：当子内容超出容器可视区域时，为其提供水平或垂直滚动条支持（常与其他布局控件嵌套使用）。

## **Viewbox（缩放框）**
  - **特点**：自动对包含的子元素进行等比例缩放，使内容能够完全适应容器的大小。 

## **Border（边框容器）**
  - **特点**：主要用于给单个子元素绘制边框、背景色或设置圆角（通常也归类为辅助布局/装饰容器）。

# 2.Grid控件学习

## 2.1定义行和列

![image-20261024120820037](./note03-第三章 布局.assets/image-20261024120820037.png)

## 2.2给控件指定行和列，第1行第一列可以不写，因为他是默认值

![image-20261024121127642](./note03-第三章 布局.assets/image-20261024121127642.png)

## 注意，不能够把多个控件直接放到MainWindow里面，需要一个面板对象作为window的内容元素，然后其它控件作为面板的子元素。也不能把一个控件放在面板元素外面

![image-20261024121736769](./note03-第三章 布局.assets/image-20261024121736769.png)

## 2.2 行高的设置，`Grid` 的行高通过 `RowDefinition` 的 `Height` 属性进行设置，主要分为三种模式：**固定高度**、**自动调整（Auto）**和**比例分配（Star, \*）**

![image-20261024133100974](./note03-第三章 布局.assets/image-20261024133100974.png)

### 注意：列宽也是一样的设置方法，如果一个Grid有n行，有固定高度也有比例高度，是先分配给固定高度的行，剩余的高度再按比例分配。

## 2.3.让Grid显示网格线

![image-20261024134137956](./note03-第三章 布局.assets/image-20261024134137956.png)



## 2.4，Grid中控件的跨行通过Grid.RowSpan设置，跨列通过Grid.ColumnSpan的设置

![image-20261024135329806](./note03-第三章 布局.assets/image-20261024135329806.png)

## 演练1.创建一个项目layout-ctrls，然后在MainWindow中输入下面的代码

![image-20261024145113118](./note03-第三章 布局.assets/image-20261024145113118.png)

### 运行程序，效果如下

![image-20261024150059622](./note03-第三章 布局.assets/image-20261024150059622.png)



# 3.GridSplitter的使用

![image-20261024144624749](./note03-第三章 布局.assets/image-20261024144624749.png)

## 参考文档：https://www.cnblogs.com/guxin/p/csharp-wpf-how-to-use-gridsplitter.html

***\*GridSplitter\**** 是 WPF 中用于在 `Grid` 布局的行或列之间提供**动态拖拽调整大小**的控件。用户在运行时可以通过鼠标拖动分割线来改变相邻行或列的宽度或高度。

------

### 核心使用规则与方向

1. 调整“列”（左右分割）

- **放置位置**：将 `GridSplitter` 放在某一个**列**中（通常单独占用一列，宽度设为固定值如 `Width="5"`）。 [[1](https://www.cnblogs.com/guxin/p/csharp-wpf-how-to-use-gridsplitter.html)]
- **尺寸模式**：与其相邻的列宽度不能仅用 `Auto`，最好使用 `*`（星号比例）或固定数值。
- **关键属性**：
  - 设置 `VerticalAlignment="Stretch"`（让分割线垂直方向拉满）。
  - 设置 `HorizontalAlignment="Center"` 或 `Stretch`。
  - 如果 `Grid` 有多行，通常需要设置 `Grid.RowSpan="行数"` 以覆盖整个高度。 [[1](https://www.cnblogs.com/guxin/p/csharp-wpf-how-to-use-gridsplitter.html)]

**示例代码（左右分割）：**

xml

```
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="200" />
        <ColumnDefinition Width="5" />
        <ColumnDefinition Width="*" />
    </Grid.ColumnDefinitions>

    <!-- 左侧内容 -->
    <TextBlock Text="左侧面板" Grid.Column="0" Background="LightBlue"/>

    <!-- 垂直分割线 -->
    <GridSplitter Grid.Column="1" Width="5" HorizontalAlignment="Center" VerticalAlignment="Stretch" Background="Gray"/>

    <!-- 右侧内容 -->
    <TextBlock Text="右侧面板" Grid.Column="2" Background="LightGreen"/>
</Grid>
```

 

2. 调整“行”（上下分割）

- **放置位置**：将 `GridSplitter` 放在某一个**行**中（通常单独占一行，高度设为固定值如 `Height="5"`）。
- **尺寸模式**：相邻行高度建议使用 `*` 或固定值。
- **关键属性**：
  - 设置 `HorizontalAlignment="Stretch"`（让分割线水平方向拉满）。
  - 设置 `VerticalAlignment="Center"` 或 `Stretch`。
  - 如果 `Grid` 有多列，通常需要设置 `Grid.ColumnSpan="列数"` 以跨越所有列。

**示例代码（上下分割）：**

xml

```
<Grid>
    <Grid.RowDefinitions>
        <RowDefinition Height="*" />
        <RowDefinition Height="5" />
        <RowDefinition Height="150" />
    </Grid.RowDefinitions>

    <!-- 上方内容 -->
    <TextBlock Text="上方区域" Grid.Row="0" Background="LightYellow"/>

    <!-- 水平分割线 -->
    <GridSplitter Grid.Row="1" Height="5" HorizontalAlignment="Stretch" VerticalAlignment="Center" Background="Gray"/>

    <!-- 下方内容 -->
    <TextBlock Text="下方区域" Grid.Row="2" Background="LightCoral"/>
</Grid>
```

常见避坑指南

1. **拖不动或无效**：
   - 检查是否遗漏了对齐属性：调整列宽时必须设置 `VerticalAlignment="Stretch"`；调整行高时必须设置 `HorizontalAlignment="Stretch"`。
   - 检查 `Width` 或 `Height` 是否漏写（如左右分割时忘写 `GridSplitter` 的 `Width`）。 [[1](https://www.cnblogs.com/guxin/p/csharp-wpf-how-to-use-gridsplitter.html)]
2. **跨行/跨列覆盖**：
   - 如果 `Grid` 结构复杂（有多行多列），务必配置 `Grid.RowSpan` 或 `Grid.ColumnSpan`，否则 `GridSplitter` 可能只在一个小格子中缩成一个小方块。 [[1](https://learn.microsoft.com/zh-cn/dotnet/desktop/wpf/controls/how-to-resize-rows-with-a-gridsplitter), [2](https://learn.microsoft.com/zh-cn/dotnet/desktop/wpf/controls/how-to-resize-columns-with-a-gridsplitter)]
3. **视觉不明显**：
   - 默认的 `GridSplitter` 是透明的或很不显眼，建议为其设置 `Background="Gray"` 或者通过 `Template` 自定义好看的拖拽样式。

## 演练GridSplitter

### 1》还是上面的项目，新建一个wpf窗口，起名：GridSplitterExampleWindow.xaml，并且在App.xaml中把它设置为启动窗口

![image-20261024150503617](./note03-第三章 布局.assets/image-20261024150503617.png)

#### 启动程序，应该显示一个空白窗口，标题是GridSplitterExampleWindow

![image-20261024150540866](./note03-第三章 布局.assets/image-20261024150540866.png)

### 2》把Grid划分3列

![image-20261024153908436](./note03-第三章 布局.assets/image-20261024153908436.png)

### 3.然后添加一些代码，修改后的代码如下

```
<Window x:Class="layout_ctrls.GridSplitterExampleWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:layout_ctrls"
        mc:Ignorable="d"
        Title="GridSplitterExampleWindow" Height="450" Width="800">
    <Grid Cursor="">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="*"/>
            <ColumnDefinition Width="auto"/>
            <ColumnDefinition Width="2*"/>
        </Grid.ColumnDefinitions>
        <TextBlock TextWrapping="WrapWithOverflow" FontSize="16" Foreground="DeepPink" >
            好好学习，天天向上 好好学习，天天向上 好好学习，天天向上 好好学习，天天向上 好好学习，天天向上好好学习，天天向上 好好学习，天天向上 好好学习，天天向上 好好学习，天天向上 好好学习，天天向上 好好学习，天天向上
        </TextBlock>
        <GridSplitter Grid.Column="1" Width="5" HorizontalAlignment="Center" VerticalAlignment="Stretch"/>
        <WrapPanel Grid.Column="2">
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
            <TextBlock FontSize="16">恭喜发财，红包拿来</TextBlock>
        </WrapPanel>
    </Grid>
</Window>

```

#### 需要注意，必须正确设置GridSplitter的水平对齐和垂直对齐，否则效果不好

### 4.运行程序，效果如下，还是不错的

![image-20261024154239536](./note03-第三章 布局.assets/image-20261024154239536.png)

![image-20261024154301786](./note03-第三章 布局.assets/image-20261024154301786.png)

![image-20261024154331611](./note03-第三章 布局.assets/image-20261024154331611.png)

### 5.可以开启GridSplitter的预览效果

![image-20261024160130347](./note03-第三章 布局.assets/image-20261024160130347.png)

#### 效果

![image-20261024160218332](./note03-第三章 布局.assets/image-20261024160218332.png)

# 4.StackPanel

## 布局面板对比

![image-20261025104735268](./note03-第三章 布局.assets/image-20261025104735268.png)

### 说明

![image-20261025105027928](./note03-第三章 布局.assets/image-20261025105027928.png)

## 面板都有的布局属性

![image-20261025105219106](./note03-第三章 布局.assets/image-20261025105219106.png)

## 演练，

### 1.还是上面的项目新建一个窗口，起名StackPanelDemoWindow

![image-20261025105926422](./note03-第三章 布局.assets/image-20261025105926422.png)



### 2.然后在App.xaml中把它设置为启动窗口

![image-20261025110218695](./note03-第三章 布局.assets/image-20261025110218695.png)

### 3.简单布局，注意：StackPanel默认的排列方向是垂直方向排列代码如下。

![image-20261025113130900](./note03-第三章 布局.assets/image-20261025113130900.png)

### 效果

![image-20261025113201595](./note03-第三章 布局.assets/image-20261025113201595.png)

### 4.如果需要它沿着水平方向排列，可以把Orientation属性改为horizontal，不过此时你需要修改一下控件的宽高

![image-20261025113747289](./note03-第三章 布局.assets/image-20261025113747289.png)

#### 效果

![image-20261025113814288](./note03-第三章 布局.assets/image-20261025113814288.png)

#### 注意：StackPanel没有滚动功能，也不好换行，显示不下就看不见。控件也有一个Padding属性，就是内边距

![image-20261025115639143](./note03-第三章 布局.assets/image-20261025115639143.png)



#### Margin属性的值的写法

在 WPF 中，`Margin` 属性用于设置元素与其父容器或相邻元素之间的**外边距（Outer Space）**，它的类型是 `Thickness`。 [[1](https://learn.microsoft.com/zh-cn/dotnet/desktop/wpf/advanced/alignment-margins-and-padding-overview), [2](https://zhuanlan.zhihu.com/p/638766571)]

------

一、 语法格式与赋值方式

`Margin` 可以通过以下几种方式进行赋值（单位为**设备独立像素 Device-Independent Pixels**）： [[1](https://learn.microsoft.com/zh-cn/dotnet/desktop/wpf/advanced/alignment-margins-and-padding-overview)]

1. **统一设置四个方向（上下左右相同）**：

   

   xml

   ```
   <Button Margin="20" Content="四周外边距都为20" />
   ```

    

2. **分别设置左右和上下（水平与垂直）**：

   

   xml

   ```
   <Button Margin="10, 20" Content="左右10，上下20" />
   ```

    

3. **分别设置左、上、右、下（顺时针方向：`Left, Top, Right, Bottom`）**：

   xml

   ```
   <Button Margin="10, 20, 30, 40" Content="左10, 上20, 右30, 下40" />
   ```

#  5、Border控件的使用

## Border控件的额外属性

![image-20261025120512764](./note03-第三章 布局.assets/image-20261025120512764.png)



## 1.新建一个窗口，起名BorderDemoWindow

![image-20261025120921282](./note03-第三章 布局.assets/image-20261025120921282.png)

## 2.在App.xaml中把它设置为启动窗口

![image-20261025121154756](./note03-第三章 布局.assets/image-20261025121154756.png)



## 3.创建一个Border元素，设置他的一下属性，展示最基本的使用

![image-20261025121624715](./note03-第三章 布局.assets/image-20261025121624715.png)

#### 效果

![image-20261025121713272](./note03-第三章 布局.assets/image-20261025121713272.png)



## 4.Border元素的边框宽度可以设置4条边的厚度一样，也可以设置左右和上下的厚度不一样，先在左右，再设置上下，也可以设置4条边的厚度都不一样，元素遵循左上右下的顺时针方向设置

![image-20261025125551909](./note03-第三章 布局.assets/image-20261025125551909.png)



![image-20261025125658287](./note03-第三章 布局.assets/image-20261025125658287.png)

#### 注意：不能设置3个值，会报错

## 5、利用整个特性，我们可以把它设置成只有下面的边有厚度，其它边没有厚度，实现下划线的效果

![image-20261025130020989](./note03-第三章 布局.assets/image-20261025130020989.png)

## 6.可以把Border的高度设置为1或者2等非常小的数字，此时它就会变为一条分割线

![image-20261025130409232](./note03-第三章 布局.assets/image-20261025130409232.png)



## 7.可以在Border里面放置其它布局控件，可以把Border直接放在Window里面，然后可以在它里面放置一个Grid，此时你就可以通过调整Border的圆角半径实现一个圆角效果

![image-20261025131051841](./note03-第三章 布局.assets/image-20261025131051841.png)

## 8.Border的第三个作用是用来实现一个圆角按钮，注意，默认wpf的按钮没有圆角半径属性，注意需要TextBlock元素的配合，而且此时是不能用Click的，可以使用MouseDown或者MouseUp事件，这里使用MouseUp事件

![image-20261025134530626](./note03-第三章 布局.assets/image-20261025134530626.png)

## 9，添加事件处理代码

![image-20261025134604317](./note03-第三章 布局.assets/image-20261025134604317.png)

### 效果

![image-20261025134633829](./note03-第三章 布局.assets/image-20261025134633829.png)

### 注意：Border元素里面只能有一个元素，再放置一个就会报错

![image-20261025134859250](./note03-第三章 布局.assets/image-20261025134859250.png)



## 演练：Border作为Grid的网格线，因为Grid自带的网格线不好看

### 1.新建一个窗口，起名BorderAsGridLineForGrid.xaml

![image-20261025140934980](./note03-第三章 布局.assets/image-20261025140934980.png)





### 2.在App.xaml中把它设置为启动窗口

![image-20261025140957065](./note03-第三章 布局.assets/image-20261025140957065.png)

### 3.然后给Grid划分为3行3列，其中有一行和一列是给Border使用的。边框作为分割线需要跨行或者跨列来使用，还有垂直分割要设置上边或者下边的边框宽度，水平分割设置左边或者右边的边框宽度

![image-20261025190353729](./note03-第三章 布局.assets/image-20261025190353729.png)

###  效果

![image-20261025190459322](./note03-第三章 布局.assets/image-20261025190459322.png)

## 总结

![image-20261025185151312](./note03-第三章 布局.assets/image-20261025185151312.png)





# 扩展：Window是根控件，不可用作为子控件

注意Window是顶级控件，也就是根控件，把一个window元素添加到一个面板里面，编译不报错，运行报错，也就是说，不能把Window作为其他元素的子控件

![image-20261025133347513](./note03-第三章 布局.assets/image-20261025133347513.png)