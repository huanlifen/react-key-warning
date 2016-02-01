# react-kwy-warning

在学习react遇到这个问题，页面可以正常工作，但控制台一直出现这个警告，看着很不爽，然后研究怎么解决。

Warning: Each child in an array or iterator should have a unique "key" prop. Check the render method

1. warning01/todo.html

 在浏览器中打开后，点击“add #7”按钮会出现上面的警告，原因是数组循环时缺少unique "key" prop,意思就是要有一个不会重复的关键参数key。

2.warning02/todo.html

 那么，关键参数重复了会怎样呢？
 在浏览器中打开后，点击“add #7”按钮增加重复的对象，会出现：

 Warning: flattenChildren(...): Encountered two children with the same key, `.$1`. Child keys must be unique; when two children share a key, only the first child will be used.

 而且，添加不了重复的对象，不同的对象是可以添加的。

3. warning/todo.html

 由此，我们可以从表面上理解：在页面可以正常工作的前提下，这个key要么设置为会重复的关键参数，要么不设置。不设置，控制台会出警告，但不影响页面正常工作。完美的解决方法：就是消除警告，页面还可以正常工作。

 改写TodoList ，增加key，reactid从0开始递增，前缀：li_,由此产生不重复的key值。
 var TodoList = React.createClass({
         render: function() {
             var reactid = 0;
             var createItem = function(itemText) {
                 return <li key={'li_' + reactid++}>{itemText}</li>;
             };
             return <ul>{this.props.items.map(createItem)}</ul>;
         }
     });

 在浏览器中打开后，没有警告，页面可以正常工作。

 但是，这个key在传递数据的时候根本就没有用，设置了不是很多余吗？