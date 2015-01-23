- [Chinese-pyim README](#sec-1)
  - [简介](#sec-1-1)
  - [背景](#sec-1-2)
  - [目标](#sec-1-3)
  - [特点](#sec-1-4)
  - [安装](#sec-1-5)
  - [配置](#sec-1-6)
    - [添加词库文件](#sec-1-6-1)
    - [激活 Chinese-pyim](#sec-1-6-2)
  - [使用](#sec-1-7)
    - [常用快捷键](#sec-1-7-1)
    - [设置模糊音](#sec-1-7-2)
    - [切换全角标点与半角标点](#sec-1-7-3)
    - [手动加词和删词](#sec-1-7-4)
    - [快速切换词库](#sec-1-7-5)
    - [[实验特性] 词语联想](#sec-1-7-6)
  - [Tips](#sec-1-8)
    - [Chinese-pyim 重要变量介绍](#sec-1-8-1)
    - [如何添加自定义拼音词库](#sec-1-8-2)
    - [如何手动安装和管理词库](#sec-1-8-3)
    - [将汉字字符串转换为拼音字符串](#sec-1-8-4)


# Chinese-pyim README<a id="sec-1"></a>

## 简介<a id="sec-1-1"></a>

Chinese-pyim 是 Chinese Pinyin Input Method 的缩写。是emacs环境下的一个中文拼音输入法。

## 背景<a id="sec-1-2"></a>

Chinese-pyim 的代码源自 emacs-eim。emacs-eim是一个emacs中文输入法框架，使用这个框架可以自定义输入法，emacs-eim 软件包本身就包含许多不同的中文输入法，比如：五笔输入法，仓颉输入法以及二笔输入法等等。

虽然 emacs-eim 很优秀。但遗憾的是，emacs-eim 并没有发展起来，因为：中文输入法的发展(尤其是拼音输入法)特别依赖庞大的用户群体直接或者间接的提供优化输入法的信息。
emacs 中文用户群体很难达到这种要求。另外各种平台下的中文输入法的高速发展，比如：
Window平台下的搜狗输入法，baidu输入法以及QQ输入法，linux平台下的fcitx，ibus等等。也间接的抹杀了 emacs-eim 的开发动力，最终的结果就是：emacs-eim 在 2008 年之后几乎停止了开发。

但是，外部的输入法与emacs配合不够默契，不断的切换输入法极大的损害了emacs那种
**行云流水** 的体验。而本人在使用（或者叫折腾） emacs-eim 的过程中发现：

1.  **当 emacs-eim 拼音词库词条超过100万时，选词频率大大降低。**
2.  **当 emacs-eim 拼音词库词条超过100万时，中文输入体验可以达到搜狗输入法的80%。**
3.  **随着使用时间的延长，emacs-eim会越来越好用（个人词库的积累）。**

所以，本人认为将 emacs-eim 作为一个 **备用** 中文输入法是非常合适的，于是我 fork 了
emacs-eim, 简化代码并更改名称为：chinese-pyim。

## 目标<a id="sec-1-3"></a>

Chinese-pyim 的目标是： **尽最大的努力成为一个好用的 emacs 备用中文拼音输入法** 。具体可表现为三个方面：

1.  Fallback:     当外部输入法不能使用时（比如：console，cygwin等），尽最大可能让 emacs 用户不必为输入中文而烦恼。
2.  Integration:  尽最大可能减少输入法切换频率，让中文输入不影响 emacs 的体验。
3.  Exchange:     尽最大可能简化 Chinese-pyim 使用其他优秀输入法的词库的难度和复杂度。

## 特点<a id="sec-1-4"></a>

1.  Chinese-pyim 只是一个拼音输入法，安装配置方便快捷，默认只通过添加词库的方式优化输入法。
2.  Chinese-pyim 只使用最简单的文本词库格式，可以快速方便的利用其他输入法的词库。

## 安装<a id="sec-1-5"></a>

1.  配置melpa源，参考：<http://melpa.org/#/getting-started>
2.  M-x package-install RET chinese-pyim RET
3.  在emacs配置文件中（比如: ~/.emacs）添加如下代码：

```emacs-lisp
(require 'chinese-pyim)
```

## 配置<a id="sec-1-6"></a>

### 添加词库文件<a id="sec-1-6-1"></a>

可以使用三种方法为 Chinese-pyim 添加词库，具体方式请参考 1.8.2 小结。

注意：每一个词库文件必须按行排序（准确的说，是按每一行的拼音code排序），因为\`Chinese-pyim' 寻找词条时，使用二分法来优化速度，而二分法工作的前提就是对文件按行排序。具体细节请参考：\`pyim-bisearch-word' 。所以，当词库排序不正确时（比如：用户手动调整词库文件后），记得运行函数
\`pyim-update-dict-file' 重新对文件排序。

### 激活 Chinese-pyim<a id="sec-1-6-2"></a>

```emacs-lisp
(setq default-input-method "chinese-pyim")
(global-set-key (kbd "C-<SPC>") 'toggle-input-method)
;; (global-set-key (kbd "C-;") 'pyim-toggle-full-width-punctuation)
;; (global-set-key (kbd "C-;") 'pyim-punctuation-translate-at-point)
```

## 使用<a id="sec-1-7"></a>

### 常用快捷键<a id="sec-1-7-1"></a>

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="left" />

<col  class="left" />
</colgroup>
<thead>
<tr>
<th scope="col" class="left">按键</th>
<th scope="col" class="left">功能</th>
</tr>
</thead>

<tbody>
<tr>
<td class="left">C-n</td>
<td class="left">向下翻页</td>
</tr>


<tr>
<td class="left">C-p</td>
<td class="left">向上翻页</td>
</tr>


<tr>
<td class="left">C-c</td>
<td class="left">取消输入</td>
</tr>


<tr>
<td class="left">SPC</td>
<td class="left">确定输入</td>
</tr>


<tr>
<td class="left">RET</td>
<td class="left">字母上屏</td>
</tr>
</tbody>
</table>

### 设置模糊音<a id="sec-1-7-2"></a>

Chinese-pyim 使用一个比较 **粗糙** 的方法处理 **模糊音** ，要了解具体细节，请运行：

    C-h v pyim-fuzzy-pinyin-adjust-function

### 切换全角标点与半角标点<a id="sec-1-7-3"></a>

1.  第一种方法：使用命令 \`pyim-toggle-full-width-punctuation'，全局切换。
2.  第二种方法：使用命令 \`pyim-punctuation-translate-at-point' 只切换光标处标点的样式。
3.  第三种方法：设置变量 \`pyim-translate-trigger-char'。输入变量设定的字符会切换光标处标点的样式。

### 手动加词和删词<a id="sec-1-7-4"></a>

1.  \`pyim-create-word-without-pinyin' 直接将一个中文词条加入个人词库的函数，用于编程环境。
2.  \`pyim-create-word-at-point:<N>char' 这是一组命令，从光标前提取N个汉字字符组成字符串，并将其加入个人词库。
3.  \`pyim-translate-trigger-char' 以默认设置为例：在“我爱吃红烧肉”后输入“5v” 可以将“爱吃红烧肉”这个词条保存到用户个人词频文件。
4.  \`pyim-delete-word-from-personal-buffer' 从个人词频文件对应的 buffer 中删除当前高亮选择的词条。

### 快速切换词库<a id="sec-1-7-5"></a>

用户可以自定义类似的命令来实现快速切换拼音词库。

```emacs-lisp
(defun pyim-use-dict:bigdict ()
  (interactive)
  (setq pyim-dicts
        '((:name "BigDict"
                 :file "/path/to/pyim-bigdict.txt"
                 :coding utf-8-unix)))
  (pyim-restart-1 t))
```

### [实验特性] 词语联想<a id="sec-1-7-6"></a>

\`Chinese-pyim' 增加了两个 \`company-mode' 补全后端来实现 **联想词** 输入功能：

1.  \`pyim-company-dabbrev' 是 \`company-dabbrev' 的中文优化版，适用于补全其它 buffer 中的中文词语。
2.  \`pyim-company-predict-words' 可以从 Chinese-pyim 词库中搜索与当前中文词条相近的词条。

安装和使用方式：

1.  安装 \`company-mode' 扩展包。
2.  在 emacs 配置中添加如下几行代码：

```emacs-lisp
(require 'chinese-pyim-company)
```

可以通过 pyim-company-predict-words-number 来设置联想词的数量，比如：从词库中搜索10个联想词可以设置为：

```emacs-lisp
(setq pyim-company-predict-words-number 10)
```

## Tips<a id="sec-1-8"></a>

### Chinese-pyim 重要变量介绍<a id="sec-1-8-1"></a>

1.  \`pyim-personal-file' Chinese-pyim 个人词频文件设置变量。
2.  \`pyim-dicts'  Chinese-pyim 词库设置变量。

### 如何添加自定义拼音词库<a id="sec-1-8-2"></a>

Chinese-pyim 默认没有携带任何拼音词库，如果不配置拼音词库，Chinese-pyim将不能正常工作。这样做的原因有两个：

1.  防止侵犯其他输入法的版权。
2.  防止自带词库质量太差，影响用户体验。

用户可以使用下面两种方式，简单的获取质量比较好的词库：

1.  第一种方式

    获取其他 Chinese-pyim 用户的拼音词库，比如，某个同学测试 Chinese-pyim 时创建了一个中文拼音词库，词条数量大约60万，文件大约20M，(注意：请使用另存为，不要直接点击链接)。

    <https://github.com/tumashu/chinese-pyim-bigdict/blob/master/pyim-bigdict.txt?raw=true>

    其他同学可以下载上述词库来体验一下超大词库为 Chinese-pyim 带来的巨大变化。

    下载上述词库后，运行 \`pyim-add-dict' ，按照命令提示，将下载得到的词库文件信息添加到 \`pyim-dicts' 中，最后运行命令 \`pyim-restart' 或者重启emacs。

2.  第二种方式

    使用词库转换工具将其他输入法的词库转化为Chinese-pyim使用的词库：这里只介绍windows平台下的一个词库转换软件：

    1.  软件名称： "imewlconverter"
    2.  中文名称：“深蓝词库转换”。
    3.  下载地址：<http://code.google.com/p/imewlconverter/>
    4.  依赖平台:  "Microsoft .NET Framework 2.0"

    首先从其他拼音输入法网站上获取所需词库，使用下述自定义输出格式转换词库文件，然后将转换得到的内容保存到文件中。

        shen,lan,ci,ku 深蓝词库

    将文件中所有","替换为"-"，得到的文件每一行都类似：

        shen-lan-ci-ku 深蓝词库

    最后，使用命令 \`pyim-add-dict' ，将转换得到的词库文件的信息添加到 \`pyim-dicts' 中，完成后运行命令 \`pyim-restart' 或者重启emacs。

3.  第三种方式

    获取中文词条，然后添加拼音code。中文词条的获取途径很多，比如：

    1.  从其它输入法中导出。
    2.  获取中文文章，通过分词系统分词得到。
    3.  中文处理工具自带的dict。
    4.  其它。

    Chinese-pyim 下面两个命令可以为中文词条添加拼音Code，从而生成可用词库：

    1.  \`pyim-article2dict-chars' 将文章中游离汉字字符转换为拼音词库。
    2.  \`pyim-article2dict-words' 将文章中中文词语转换为拼音词库。
    3.  \`pyim-article2dict-misspell-words' 将文章中连续的游离词组成字符串后，转换为拼音词库。

    注意：在运行上述两个命令之前，必须确保待转换的文章中，中文词汇已经使用 **空格** 强制隔开。

    最后将生成的词库按上述方法添加到 Chinese-pyim 中就可以了。

### 如何手动安装和管理词库<a id="sec-1-8-3"></a>

这里假设有两个词库文件：

1.  /path/to/pyim-dict1.txt
2.  /path/to/pyim-dict2.txt

在~/.emacs文件中添加如下一行配置。

```emacs-lisp
(setq pyim-dicts
      '((:name "dict1" :file "/path/to/pyim-dict1.txt" :coding gbk-dos)
        (:name "dict2" :file "/path/to/pyim-dict2.txt" :coding gbk-dos)))
```

### 将汉字字符串转换为拼音字符串<a id="sec-1-8-4"></a>

下面两个函数可以将中文字符串转换的拼音字符串或者列表，用于 emacs-lisp 编程。

1.  \`pyim-hanzi2pinyin' （考虑多音字）
2.  \`pyim-hanzi2pinyin-simple'  （不考虑多音字）
