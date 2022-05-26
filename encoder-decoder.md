## Encoder-Decoder

## 简介

Encoder-Decoder框架顾名思义也就是编码-解码框架，目前大部分attention模型都是依附于Encoder-Decoder框架进行实现，在NLP中Encoder-Decoder框架主要被用来处理序列-序列问题。也就是输入一个序列，生成一个序列的问题。这两个序列可以分别是任意长度。具体到NLP中的任务比如：
文本摘要，输入一篇文章(序列数据)，生成文章的摘要(序列数据)
文本翻译，输入一句或一篇英文(序列数据)，生成翻译后的中文(序列数据)
问答系统，输入一个question（序列数据），生成一个answer（序列数据）
基于Encoder-Decoder框架具体使用什么模型实现，由大家自己决定~用的较多的应该就是seq2seq模型和Transformer了。
![图1](https://img-blog.csdnimg.cn/20200321173021798.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RpbmsxOTk1,size_16,color_FFFFFF,t_70)

**结构图**

