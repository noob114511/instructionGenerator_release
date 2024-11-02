# 关于.txt文件与.csv文件
- IllegalInrustions文件夹下存放是软件生成结果（未定义指令），文件后缀虽然为.txt但是其内容本质是一系列二进制数据，所以如果用文本编辑器打开后会得到一串乱码，推荐使用拥有二进制打开模式的编辑器打开，比如VScode的hex editor插件。**注意：数据采用小端存储。**若不清楚什么是大小端请看：[何为大小端](https://blog.csdn.net/wwwlyj123321/article/details/100066463)
- InstructionSet文件夹与Rules文件夹下存放的是录入的合法指令与自定义规则指令，文件后缀为.csv，可以用文本编辑器和Excel打开。其文件内容是按照掩码的数据格式存放，一行就等于录入的一条指令。**注意：用Excel打开时Excel可能会自动将原来的数据转换为科学计数法，这会导致后续程序读取文件内容时崩溃，所以打开或修改文件时请注意数据的格式是否正确。**

# Q&A
### 为什么生成模式配置界面问号点着没反应？
- 生成模式配置界面的问号不是用来点的，当鼠标悬停到该图标上时会自动出现提示。
### 在生成32bit或64bit指令时生成的文件很大，高达几个G，这是正常现象吗？
- 这属于正常现象。以32bit为例，在全遍历不剔除的情况下得到的文件大小为2^32(指令数) * 4Byte(一条指令大小) = 2^34Byte 约等于16GB。
### 为什么生成16bit指令时一下子就完成了，而生成32bit时进度条很久都没有变化？
- 因为从16bit到32bit耗费的时间并不是线性增加的，而是大约呈指数上升；从32bit到64bit同理。另外进度条也不是线性增加的，这个和生成时选择的线程数有关，一般是一整个线程的任务完成后进度条才会变化。线程数越多进度条增长越快，耗费的时间越少。
- 如果进度条长时间没有变化可以打开电脑任务管理器，当程序正在进行生成任务时至少有10%的CPU占用率（单线程），此时说明程序正在正常运行，请耐心等待。但是如果进度条在相当长的时间内没有变化并且CPU占有率为个位数那么有可能是软件出现了bug，遇到此类情况请@黄福鑫或付正。
### 选择8线程进行生成任务时CPU占用率会达到80%以上，这是正常现象吗？
- 这属于正常现象，CPU的占有率主要取决于电脑的CPU内核数量，一般情况下电脑CPU内核数越少占用率越高。如果想一边进行生成任务一边使用电动做其他事可以选择单线程或双线程，这样可以避免电脑卡顿。
### 文件夹下的.gitkeep文件是什么？
- 这个是为了保证git上传远程仓库时会记录空文件夹，不影响软件正常使用，删了也完全没问题。