#区块链(blockchain)
****

###区块链的本质:用一句话概括，它是一种特殊的分布式数据库。

****

* 任何人都可以架设服务器，加入区块链网络，成为一个节点。区块链的世界里面，没有中心节点，每个节点都是平等的，都保存着整个数据库。你可以向任何一个节点，写入/读取数据，因为所有节点最后都会同步，保证区块链一致。
		
* 区块链由一个个区块（block）组成。区块很像数据库的记录，每次写入数据，就是创建一个区块。
	* 区块头（Head）：记录当前区块的元信息,区块头包含了当前区块的多项元信息
		* 生成时间
		* 实际数据（即区块体）的 Hash
		* 上一个区块的 Hash
		* ...
	* 区块体（Body）：实际数据
		* 每个区块的 Hash 都是不一样的，可以通过 Hash 标识区块。
		* 如果区块的内容变了，它的 Hash 一定会改变。
	![Markdown Screenshot](http://www.ruanyifeng.com/blogimg/asset/2017/bg2017122703.png)
	
* LayerDrawable
		
* StateListDrawable
* LevelListDrawable
* TransitionDrawable
* InsetDrawable
* ScaleDrawable
* ClipDrawable

#...
不想一一列举了，在写就吐了，这种字典类型的功能，个人觉得还是随用随看比较好，不需操之过急。

