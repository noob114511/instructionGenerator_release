# 软件使用说明

该软件分位两个部分，包括**合法指令录入工具**以及**非法指令生成工具**。

## Ⅰ 合法指令录入工具

合法指令录入工具包含三个步骤：

- **录入文件路径选择**
- **录入指令位宽选择**
- **开始录入**

### 1  录入文件路径选择

​	录入文件路径选择模块用于用户选择自己录入后的文件存放路径。

​	为了规范存放，需要用户指定指令集架构、输入合法指令文件夹名。

### 1.1  指令集架构选择

​	该部分将扫描`InstructionSet`文件夹下的目录结构，以供用户选择指令集架构。

![image-20240924103543384](.\docs\1_1.png)

​	文件夹位于`./InstructionSet/基本架构/子架构`。以上图为例，基本架构`ARM`，子架构`ARMv7-A`指向`InstructionSet/ARM/ARMv7-A`文件夹。

### 1.2 输入合法指令文件夹名

​	该部分用于用户定义自己的合法指令文件夹名。

![image-20240924113255436](D:\Lab\GarduationProject\Project\upper\CodeGenerator\Project\Release\instructionGenerator\docs\1_2.png)

​	**注：**即使确定了**指令集基本架构+子架构**，由于更新的需要，指令集仍然**存在若干不同版本**。

​			**建议用户将指令文件夹名修改为具体的版本名。**

### 2 录入指令位宽选择

​	该部分为用户提供需要录入的合法指令位宽进行选择，当用户需要更加多样的位宽时可自定义输入。

![image-20240924185439424](.\docs\1_3.png)

​	已选择的位宽按键可**点击删除**。

### 3  开始录入

​	录入界面为两个录入表，包括每次能输入一条合法指令的录入表，以及展示所有已录入合法指令的录入总表。

![image-20240924190133637](.\docs\1_4.png)

​	该部分要求用户录入指令各个二进制位的**属性**与**值**。

 - **属性：**包括fixed(固定)、opc(操作码)、opnd(操作数)；
 - **值：**0 、 1、 X（X表示该二进制位0、1均可）

**功能说明：**

	1. **录入表**点击录入，将会把录入表当前指令录入总表。
	1. **录入总表**点击**保存**，将存储录入总表中的**所有位宽的所有指令**至文件夹。
	1. **录入总表**点击**移出并修改**，将存储录入总表中**某一个**指令移出至录入表中进行修改。
	1. **录入总表**点击**保存删除，将选中的若干条（可多条）指令删除。

## Ⅱ 非法指令生成工具

非法指令生成工具包含四个步骤：

	- 合法指令文件选择
	- 保存文件路径选择
	- 生成模式选择配置
	- 运行状态控制台

### 1 合法指令文件选择

​	该部分用于用户选择芯片对应的合法指令集文件。

![image-20240924194547303](.\docs\2_1.png)

​	用户可选择芯片的（也是合法指令集的）基本架构、子架构、合法指令集文件夹名。合法指令集文件将位于由以上信息组成的文件夹：`./InstructionSet/基本架构/子架构/合法指令集文件夹/`下

### 2 保存文件路径选择 

​	该部分用于用户选择生成的非法指令文件夹的存放路径。

​	生成的非法指令将以若干个文件的形式保存。

​	**默认**的非法指令文件夹名为上一步输入的**芯片名称**，用户也可根据个人需求进行修改。

![image-20240924195736708](.\docs\2_2.png)

### 3 生成模式选择配置

​	该部分用于用户选择配置非法指令的生成方式。

![image-20240924200332194](.\docs\2_3.png)

本软件提供了多线程模式用于非法指令的快速生成。

非法指令的生成方式包括以下三种：

- 全遍历模式
- 按二进制位位置属性模式
- 自定义模式	

#### 3.1 全遍历模式

​	程序将读取合法指令文件夹下的文件，获取处理器的位宽，显示于此处。

![image-20240924202857681](.\docs\2_4.png)

​	用户可在**处理器所有位宽**中**选择**需要生成指令的位宽。

#### 3.2 按二进制位置属性模式

​	该模式下，程序将根据用户指定的合法指令文件中的信息，遍历指令的操作码。

​	指令的操作数部分位用户提供三种选择分别为：

		- 遍历
		- 随机
		- 置零

![image-20240927154431842](.\docs\2_5.png)

#### 3.3 自定义模式

​	该模式下，指令将根据自定义规则生成非法指令。

![image-20240927155217496](.\docs\2_6.png)

​	自定义规则文件内容如下：

![image-20240927155809376](.\docs\2_7.png)

**值：**0 、 1、 X（X表示该二进制位0、1均可）。

程序将按照自定义规则文件中每条规则生成非法指令并过滤已定义指令。

### 4 生成

最终生成的非法指令将存在保存路径下，位宽相同的指令存放在一个同一个文件中。

如**16、32**位的非法指令存放在 **16bit.txt、32bit.txt**中，可以用二进制模式观察生成的指令，注意**大小端存储**模式。

## Ⅲ ARM指令集录入说明

#### 1 版本说明

ARM指令集分为ARM-A、ARM-R以及ARM-M。并拥有v7、v8、v9等版本。初次之外还存在之下的小版本。小版本指令集之间仍然存在细微差异，虽细微，但其会影响后续测试结果，故仍然不容忽视。

![image-20240927161318453](.\docs\3_1.png)

****

如：该文档查看脚注可知该文件为 ARMv7-M DDI0403E.e版本。

**注：可在[arm开发者网站](https://developer.arm.com/)中搜索armXXXX Architecture Reference Manual获取文件。**

#### 2 录入细节

##### 2.1 细节一 指令描述

除了关注指令表格，还需要注意有的指令的描述。如此处文档描述说名该部分的其余指令空间被视为NOP（No Operation），因此此处的opA与opB位需要被设置为**全X**，指令名填**If-Then,and hints**。

![image-20240927161839415](.\docs\3_2.png)

##### 2.2 细节二 not 111x的录入

​	文档中的指令存在not 111x这类指令的情况，

![image-20240927162355265](.\docs\3_3.png)

在录入时可考虑使用如下方法：

![image-20240927162825378](.\docs\3_4.png)