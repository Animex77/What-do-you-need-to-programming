# 编程需要下载什么软件

> 在大学新生群问这个问题的人太tm多了，但是回答的基本都是已读乱回，根本不考虑编程一整环需要的一切工具然后随便回答一个编辑器或者IDE，甚至有回答Anaconda这种离大谱的答案，至于怎么Make it works疑似不考虑一点，因此个人决定写一个一站式答疑解惑

> 如果你有任何疑问希望请教别人，请：1）确认自己认真读完了本文 2）通过Google搜索了相关信息（不是百度，如果没有条件请使用必应国际版 __并确保你使用了英语进行了搜索__ 3）全文观看这个[关于怎么问问题的教程](https://github.com/tangx/Stop-Ask-Questions-The-Stupid-Ways/tree/master) 4）根据你在3）所学到的内容，__简洁高效__ 的提问。

> 如有关于本文改进的建议，欢迎各位大佬在Issue里斧正。同时，也欢迎各位同学在Issue提出自己的观点和疑问。

#### 你需要学习什么样的编程语言？
对计算机技术有一些了解的同学可能会知道各种类型奇奇怪怪的语言：C/C++，Java，Python，html，CSS，JS，或者Matlab，lua，Go，R，甚至Pascal，Basic甚至COBOL这种上古语言。一些同学可能学过其中的一些，最近几年应该基本都开始转Python了，不知道现在高考生还有没有和笔者一样当年学过Visual Basic。

但是对于初学者而言，这只是一个三选一甚至二选一的问题：C/C++，Python，或者Matlab。对于计算机、电气工程相关专业的学生而言，C/C++是 __最基础__ 的知识储备。而对于其他的理工类专业，譬如航天工程、土木工程、建筑等等，你们很有可能需要一个工具进行数学建模，而这是Matlab所擅长的领域。对于商科或者金融的学生，或许也需要一个数学运算工具去处理数据，而Python包含了大量适合用于运算的库。

> 尽管Python有大量和机器学习相关的库可以方便的使用，但是如果你想作为机器学习相关内容的研究者， __请不要将它作为你的第一门学习的语言，具体原因我在后面会详细解释。__ 当然，如果你将它作为你的一种工具，譬如说你是数学家，那么Python十分适合你。

当然，Matlab和Python在很多地方是十分相似的。它们都有强大且易于使用的库来帮你完成数据处理的工作，也都可以胜任机器学习的任务。相对而言，我更推荐Python作为你学习的第一门编程语言，这也是我为什么说甚至是一个“二选一”的问题。

> Java和Rust就让他们见鬼去吧。

>关于C和C++我会在最后稍微解释一下它们的区别......但是你可以直接学C++，C++教程会包括所有的C语言基础内容。 

 #### C/C++和Python/Matlab的区别是什么？

首先对于为什么会发展出C/C++以及Python做一个简单的介绍。

 C/C++是编译式的语言，而Python/Matlab则是脚本语言。相信大家在计算机课上都有了解过，计算机运行的底层逻辑是二进制寄存器指令，但是通过输入0101010101给计算机编程无疑造成了大量困难，因此，较为高级的汇编语言诞生了。汇编语言将010101变成了包括MOV，ADD在内的指令，他们都有对应的二进制命令，如ADD对应00000011。当然，这样的操作需要使用者 __十分了解计算机组成原理__，同时完成一项操作是十分麻烦的，这也意味着在这一阶段，计算机编程有着巨大的学习成本。因此，__高级计算机语言__ 应运而生，对于其简便性，以下有一个C++和汇编语言的对比：
 

> 下面这些又臭又长的代码你完全可以跳过。当我写完这一部分的时候我意识到了一个错误，因为它们并不是本文需要讲解的内容。

 ```C++
#include <iostream>
#include <future>
#include <thread>

#define SETNAME_SUCCESS 1
#define FAULT -1

class Person{
    private:
        int name;
    public:
        int setName(int name_in);
        int getName(void);
};

int Person::setName(int name_in){
    name = name_in;
    return SETNAME_SUCCESS;
}

int Person::getName(void){
    return name;
}

int main () {
    auto personPtr_ = std::make_shared<Person>();
    if(personPtr_->setName(47) == SETNAME_SUCCESS){
        return 0;
    }else{
        return FAULT;
    }
}
 ```
这样的代码在使用``` g++ -S -o output.asm main.cpp -O3```命令转换为汇编语言后，一共生成了310行指令。同时，```-O3```参数的使用已经让g++编译器生成了最佳优化的结果，如果不使用该参数，也就是完全按照以上程序的逻辑规则、不优化掉不可能发生的分支和未使用的特性的情况下，则总共会生成2303行指令！以下节选一些生成后的汇编语言指令：
```
.LFE4761:
	.size	_ZNSt23_Sp_counted_ptr_inplaceI6PersonSaIS0_ELN9__gnu_cxx12_Lock_policyE2EE5_Impl8_M_allocEv, .-_ZNSt23_Sp_counted_ptr_inplaceI6PersonSaIS0_ELN9__gnu_cxx12_Lock_policyE2EE5_Impl8_M_allocEv
	.section	.text._ZNSt16allocator_traitsISaI6PersonEE7destroyIS0_EEvRS1_PT_,"axG",@progbits,_ZNSt16allocator_traitsISaI6PersonEE7destroyIS0_EEvRS1_PT_,comdat
	.weak	_ZNSt16allocator_traitsISaI6PersonEE7destroyIS0_EEvRS1_PT_
	.type	_ZNSt16allocator_traitsISaI6PersonEE7destroyIS0_EEvRS1_PT_, @function
_ZNSt16allocator_traitsISaI6PersonEE7destroyIS0_EEvRS1_PT_:
.LFB4762:
	.cfi_startproc
	endbr64
	pushq	%rbp
	.cfi_def_cfa_offset 16
	.cfi_offset 6, -16
	movq	%rsp, %rbp
	.cfi_def_cfa_register 6
	subq	$16, %rsp
	movq	%rdi, -8(%rbp)
	movq	%rsi, -16(%rbp)
	movq	-16(%rbp), %rdx
	movq	-8(%rbp), %rax
	movq	%rdx, %rsi
	movq	%rax, %rdi
	call	_ZN9__gnu_cxx13new_allocatorI6PersonE7destroyIS1_EEvPT_
	nop
	leave
	.cfi_def_cfa 7, 8
	ret
	.cfi_endproc
```
希望人类写出这样的程序是完全不可能的。同时，在编写上述C++程序时，我不需要了解任何玩弄寄存器的背景知识，只需要take everything as a blackbox，不求甚解的创建智能指针和调用对象就行了。从这一刻起，大量的寄存器操作可以被抽象成“函数”这个概念，你只需要告诉计算机我希望这个函数输入某个数据、进行什么运算和得到什么结果即可，而不需要理会寄存器发生了什么操作。

> 这一段内容应该会有不少错误？

当然，C/C++作为和计算机紧密结合的语言，仍然有着操作底层硬件的能力--如果你在未来学习单片机你会对这一件事会有更深刻的了解。然而在操作系统下运行的程序被限制了这些功能。

> 这一段也有一些不严谨的部分，理解意思即可。

__但是对于很多应用场景而言，我们根本不需要了解计算机的底层到底发生了什么！__ 而C/C++对于语法、数据结构、数据类型的创建、调用和修改有着极为严格的限制，这使得很多使用者学习了大量无用功，同时增加了开发周期和难度。在这一背景下，无需编译、且语法相对宽松和简单的 __脚本语言__ 诞生了。譬如对一个变量的定义，C/C++需要声明变量类型，同时也要注意调用格式--假设一段1byte的内存为11110000，使用uint_8t和int8_t的类型表示，分别会得到240和-16这两种结果--而若是考虑在不同平台的大小端问题，则又会产生更多的麻烦。而在脚本语言当中，很多情况下，数据类型几乎不是一个十分值得考虑的问题。使用者只需要使用类似```var a = 1```甚至```a = 1```的代码就可以完成赋值。内存发生了什么？它的指针指向哪里？这并不重要。

__以一言蔽之，对于未来职业和学习规划当中需要深入了解计算机系统本身的同学应当将C/C++作为自己学习的第一门语言，而若是需要定制化的程序作为一种工具以完成某种目标，你应当选择Python/Matlab。__

 #### 我需要安装什么？

 首先从Matlab讲起。请访问[MathWorks官网](https://www.mathworks.com/)下载Matlab。请注意，它是一个付费软件，但是最晚从大二开始你的老师会给你这个软件的激活方式。Matlab是开箱即用的，你不需要进行大量前期工作。

 对于C/C++而言，你需要安装 __编译器__ 将代码编译成机器码组成的可执行文件以运行，同时你需要一个 __编辑器__ 来编写你的代码。例如，Windows上的记事本（是的！它是一个编辑器）就是一个最简单的编辑器。同时，或许你希望了解你的程序在运行时具体是怎么执行的，那么这时候，你需要一个 __调试器__。当然，对于入门而言调试器并不是必须的工具。
 > Word不是这里所指的编辑器！即使很多文件（.txt .c .cpp .py .json等等等等）有着不同的后缀，但是由于它们使用相同的编码规则，任何编辑器都可以打开它们，同时对于编译程序或者执行脚本而言，后缀在很多情况下不会产生影响，很多时候只是为了作为一种标识符。

一个 __集成开发环境（IDE）__ 则会包括以上所有的内容。编译器和调试器的使用需要一些学习，但在现代IDE下，这些工具的使用则较为简便。个人推荐[Clion](https://www.jetbrains.com/clion/)作为你的集成开发环境，你可以在bilibili上寻找“Clion C++环境”一类的教程。在不同的教程中你或许会看到不同的配置方式，例如编译器的选择上，一些教程会选择MinGW（GCC/G++的Windows移植版），或clang，它们都是正确的，并且并不会影响你的入门学习。对于学习C/C++语言本身，可以观看 _The Cherno_ 或 _黑马程序员_ 的教程，尤其推荐前者。

除了Clion以外，或许你们还听说过了例如Visual Studio和Visual Studio Code之类的IDE。VS Code也是一个不错的选择，有着众多的扩展，支持各种语言（而JetBrains则是一个萝卜一个坑，Clion专精C/C++，PyCharm针对Python）；Visual Studio虽然配置简单开箱即用，但是会占用巨量的C盘空间（基础20G+），建议不要使用。

> _The Cherno_ 的视频在YouTube上，Bilibili有搬运，而_黑马程序员_则是Bilibili的UP主。个人很不喜欢黑马程序员废话一箩筐的风格。

> 请不要在这种基础问题上询问他人应该怎么做。使用搜索引擎自行解决问题和仔细阅读教程是一种美德。

而对于Python而言你需要安装一个 __Python解释器__ 以运行脚本。类似的，请参考B站教程，搜索类似“Python开发环境搭建”一类的关键词可以得到答案。在这一过程中，你或许会遇上和Python相关的一些其他软件，例如Conda、pip。这是因为不同版本的解释器对同一会有不同的效果，而一台电脑需要运行多个时期的代码，这时Conda就可以配置出不同版本解释器和模块的Python执行代码。pip则是Python的一个包管理软件，在一个Python环境下，可以安装或删除不同的模块扩展或精简功能。

同样，这里推荐JetBrains的[PyCharm](https://www.jetbrains.com/pycharm/)作为你的PythonIDE。关于VSCode/Visual Studio的内容请参考C++环境部分。Python的教程请搜索Bilibili，个人不做任何推荐（因为我没有看过任何视频教程，完全参考[Runoob](https://www.runoob.com/)的文档学习）。

> 由于本人并不了解Python，关于Python环境的内容若有大佬和我相左，请以他为准。

## 一些不太重要的内容

#### 你需要GNU/Linux吗？
很推荐，可以从Ubuntu开始，Linux的学习成本较高，但它更合适开发者，配置环境也极为简单。GNU/Linux的大量功能是为开发者而生的。

>我的Github上有[关于Linux的简易教程](https://github.com/Animex77/linux-tutorial)，可以进行一些参考

#### C/C++的区别是什么？
从编译器的角度而言两者有着巨大的差异，但是从语法上C++可以看作是C的扩展包。C++提供了类和对象、泛式编程、模板和容器等功能，而C则是面向过程编程。这一部分内容在你进行进一步的学习后你就会明白了。