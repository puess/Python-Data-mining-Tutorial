# Day15 : 序列标注

> **作者**：长行
>
> **时间**：2020.05.08

序列标注指的是给定一个序列，找出序列中每个元素对应标签的问题。其中，标签的所有可能的取值集合称为标注集。

举一个最简单的例子：输入自然数序列，输出它们是否是质数，若是质数则标注为1，若不是则标注为0，并按顺序排列为另一个序列。

```
原始: 1  2  3  4  5  6  7  8
标注: 0  1  1  0  1  0  1  0
```

此时每个数字的判断只取决于当前的元素，而不用考虑前后其他因素的情况。但是在自然语言处理领域的绝大部分序列标注则都是需要综合考虑当前元素以及其前后元素的标签才能决定当前标签。

求解序列标注问题的模型一般称为**序列标注器**，通常由模型从一个标注数据集中学习后，再用学习的结果进行预测。

下面我们主要讨论序列标注在自然语言处理领域的应用：

## 中文分词

最简单的一种将中文分词转换为序列标注的方法，是将中文分词视作对句子的一次次切割，只有切或不切两种选择，即标注集为{切,不切}。

```
桃 花 帘 外 东 风 软 ， 桃 花 帘 内 晨 妆 懒
不 切 切 切 不 切 切 ， 不 切 切 切 不 切 切
```

这样的序列标注方法相对简单，并不能有效区分一个词语的结尾和单字成词的区别。而且很多词语的开始词也有着共性，例如“桃花”、“桃树”、“桃核”等。

基于此，就有了当前最流行的{B,M,E,S}标注集。其中B为词语开头、M为词语中部、E为词语结尾，S为单字成词。

```
桃 花 帘 外 东 风 软 ， 桃 花 帘 内 晨 妆 懒
B  E  S  S  B  E  S ， B  E  S  S  B  E  S
```

## 词性标注
词性标注就是输入句子中的词语序列，输出它们对应的词性序列。

```
桃花  帘  外  东风  软  ， 桃花  帘  内  晨妆  懒
名词 名词 介词 名词 形容 ， 名词 名词 介词 名词 形容
```

词性标注集也不是唯一的，常见的有863标注集和北大标注集。同样，词性标注也需要综合考虑当前词前后词语的词性才能决定当前词语的词性。

## 命名实体识别

命名实体识别，就是识别句子中包含的人名、地名和机构名。

命名实体识别可以在中文分词的基础上，使用BMES标注集再次标注已经分好的词语，由此来识别由多个不同词语组成的命名实体。

>学习参考文献：《自然语言处理入门》(何晗)：4.1