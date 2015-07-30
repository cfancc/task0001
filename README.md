##index.html
1. `img`元素的特性：  
	- `img`会保持图片的宽高比例，`weight=100%`的情况下，`height`也会自动跟着调整，并且会在图片最下方预留`3px`的空隙。  
	**原因：**  
		`img`是一种特殊的内联元素（`replaced inline element`）,因为是内联元素，它某些地方会表现的像一个文本字符，我们知道，文本字符和外围元素边界是有一定的空隙的。大多数元素默认有一个属性`vertical-align: baseline`,这个属性表明应该预留一定的空间。  
	**解决方案:**
		- `vertical-align`属性的其它值也会保留这个空间，但是`top`,`text-top`,`middle`,`bottom`,`text-bottom`不会,`sub`看起来也不会。
		- 如果你的image尺寸小于你的字体尺寸，这时候采用`display: block`比较好。
		- 将`img`外层的`div`容器的`line-height: 0`或者`font-size: 0`都可以解决这个问题（如果`div`内还有其它文本元素，不建议使用这种方案）
2. 负边距的问题:
	- 使用负边距调整后一个元素(`B`)覆盖前一个元素(`A`)时，从上到下依次是 `B的文本-A的文本-B的背景-A的背景`。使用`position:relative`，并调整`B`的`top`为负值时，产生的覆盖效果从上到下为`B的全部-A的全部`  
[http://css-discuss.incutio.com/wiki/Overlapping_And_ZIndex](http://css-discuss.incutio.com/wiki/Overlapping_And_ZIndex " ")
3. `margin`的重叠
	- 同一`BFC`下，两个相邻Box的`margin`会发生重叠，如果一个元素无缘无故多了上下边距，检查它的子元素看看
	- 如果中间隔着`padding`，就不会出现重叠现象
4. `padding:10000px`和`margin:-10000px`，和父元素的`overflow:hidden`
	
	当两列不同高的元素需要底部对齐时，上面的三点就可以起到作用。但是`overflow:hidden`也会造成`position:absolute`和`margin`负边距移出父元素范围的子元素被隐藏。
5. `media query`中的`max-width=900px`指的是当宽度小于980px时，其下的样式生效。
##blog.html
1. `outline`不占文档空间，不会因元素受其挤压变形导致错位
2. `font-weight`变粗会导致`td`变形，暂无解决方案
##gallery.html
1. 一个元素绝对定位，脱离文档流，无论它高度如何变化都不会影响文档高度。但是这个元素的子元素可以撑开该元素，怎么样能让文档的高度随着子元素个数的增加而增加呢？
2. `line-height`设置在`inline`元素上是无效的，`inline`元素的高度只受文字大小影响，也就是说受`font-size`的影响
3. `inline-block`之间有空隙，如果你的`html`节点中存在空格，换行等字符。

	>      <p>one</p>
	>      <p>two</p>
	>      <p>three</p>

	`<p>one</p><p>two</p><p>three</p>`或者
	>      <p>one</p><p>
	>		two</p><p>
	>		three</p>

	可以解决问题。

4. `inline-block`高度不一致的几个元素排列在意思，它们是底边对齐的。想要它们向上对齐需要调整他们的`vetical-align:top`，这个属性的用法还有些疑惑，先挖个坑，研究研究再来填。

5. 有时候`margin`实现不了的效果可以调节`padding`尝试。尤其是对两个子块元素进行压缩时，不用把它们再放到一个嵌套元素中。
##about
1. 最后一个页面用的`dl`,`dt`,`dd`来实现的，觉得不是很合适，虽然有较强的联系性，但是多个`dd`布局不方便
2. 浮动能清就要尽量清

##总结
CSS类名不能只写一个，最好写一串，但不重复的。单一CSS文件作用到多个HTML页面上可能会有重名的类，这时候一个类名无法区分。