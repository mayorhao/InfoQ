# 让Angular组件通信
源文章:[Getting Components to Communicate in Angular](https://www.infoq.com/articles/angular-component-communication)
### 本文要点
* Angular应用是基于组件的，在组件之间传递数据是完全可能的。
* 可以通过`@Input()`向子组件传递数据。
* 可以通过`@Output()`捕获由子组件传递的数据。
* 可以使用外部的数据存储，像ngrx，来组织大型应用

组件就像Angular的积木，在angular应用中，每个可见的元素都是由组件构成的。基于组件的架构的优势在于：就像JavaScript函数，如果一段代码变得过于复杂，并承担过多的职责，那么你就可以把它拆分掉，这样每段代码都专注于一个功能。
也就是说，当我们着手于把组件拆分为更小的组件时，我们需要保证这些组件能够向上和向下的传递数据。为了保证能够同步我们应用中的数据，合理的组件通信很有必要的。

![图片1](https://cdn.infoq.com/statics_s1_20170530-0600u1/resource/articles/angular-component-communication/en/resources/3Picture1.jpg)

<sup>我们可以在AppComponent下构建我们整个应用，但是该组件会承担过多的职责，在基于组件的架构中，公认更好的做法是：将组件拆分，这样每个组件只承担一个职责，<sub>

### 向组件传递数据
在Angular中，当父组件需要传递数据给子组件时，我们使用`@Input`，打个比方，比如我们正在开发一个应用程序来展示某页的评论。 AppComponent会负责把含评论的数组加载进来，我们会把每条评论的数据分发给评论组件。
通过`@Input`,子组件会接收一个评论参数，以下是整个组件的代码：

```javascript
    @Component({
    selector: 'comment',
    templateUrl: './comment.component.html',
    styleUrls: ['./comment.component.css']
    })
    export class CommentComponent {
    @Input() comment;
    }
```
现在我们可以在别处调用该组件了,代码为：
```html
    <comment [comment]="comment"></comment>
```

### 语法解析
首先，是组件选择器`<comment></comment>`,如果你之前使用过Angular，对它因通过该不会陌生
第二，是属性绑定：`[comment]`，用方括号包裹这元素属性，起初看起来会有些奇怪，事实上，
