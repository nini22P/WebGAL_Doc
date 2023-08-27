# 场景与分支

在 视觉小说 中，跳转章节、场景与分支选择是不可或缺的，因此，WebGAL 也支持场景跳转与分支选择。

你可以将你的剧本拆分成多个 txt 文档，并使用一个简单的语句来切换当前运行的剧本。

::: warning
在跳转场景、分支选择或调用场景后，舞台并不会被清除。这也就意味着上一个场景应用的背景音乐、立绘、背景图片等效果会被继承到下一场景。

如果你使用 WebGAL Terre 可视化编辑器，你应该格外注意，因为编辑器在预览单独的一个场景的时候并不关心上一个场景会带来什么效果。因此，预览效果和实际游戏运行效果可能会有所差别，你应该考虑妥善处理场景跳转前的舞台清理工作。
:::

## 场景跳转

假如你现在写了两个章节的剧本，分别是 `Chapter-1.txt` 与 `Chapter-2.txt` 。在 `Chapter-1.txt` 运行结束后，你希望跳转到 `Chapter-2.txt` 对应的场景，请使用以下语句：

``` ws
changeScene:Chapter-2.txt;
```

示例：

``` ws
(Chapter-1.txt)
......
......
; // 接下来执行的就是Chapter-2.txt的内容了
changeScene:Chapter-2.txt;
......
......
(Chapter-2.txt)
......
```

通过执行这条命令，你将切换游戏场景，并使接下来的剧情发展按照新的场景剧本运行。新的剧本会在下一次鼠标点击后运行。

## 场景调用

如果你需要在一个场景中调用另一段场景，你可以使用 `callScene`，在调用的场景运行完毕后会回到原场景。

语句：

``` ws
callScene:Chapter-2.txt;
```

示例：

``` ws
(Chapter-1.txt)
......
......
callScene:Chapter-2.txt;
; // 接下来执行的就是Chapter-2.txt的内容了
......
......
(Chapter-2.txt)
......
......
(Chapter-2.txt执行完毕)
; // 回父场景，继续执行父场景语句
......
```

## 分支选择

如果你的剧本存在分支选项，你希望通过选择不同的选项进入不同的章节，请使用 `choose`。
使用 `选择项文本:章节文件名` 定义一个选择项。使用 `|` 来分隔不同选择项。示例如下：

``` ws
choose:叫住她:Chapter-2.txt|回家:Chapter-3.txt;
```

你只需要将选项的文本与选择选项后要进入的剧本名称一一对应起来，就可以实现分支选择的功能了。

## 标签跳转

如果你想要创建一个分支，但是却觉得为此新建一个 TXT 文件太麻烦，你可以尝试使用以下方式在同一文件内实现创建分支和跳转语句。

::: warning
如果你的分支很长，我不建议你使用这种方式，因为一个 TXT 的行数不适宜太长，否则可能会导致加载慢、响应迟钝等性能问题。
:::

### 创建标签（`label`）

``` ws
......
jumpLabel:label_1; // 跳转到 label_1
......
......
label:label_1; // 创建名为 label_1 的 label
......
```

简而言之， `jumpLabel` 类似于 `goto` 语句，能够立刻让你的剧本跳到场景（TXT 文件）中的任意一个位置，而这个位置需要你用 `label` 创建。

如果把 `jumpLabel` 比作任意门，那么这个任意门的终点就是 `label` 所在的位置。

### 添加选择项

有了上面的基础，你就可以通过 `choose` 来实现用分支来跳转到 `label` 所在的位置了：

``` ws
......
choose:分支 1:label_1|分支 2:label_2;
label:label_1; // 创建名为 label_1 的 label
......
......
jumpLabel:end; // 跳转到 end
label:label_2; // 创建名为 label_2 的 label
......
......
jumpLabel:end; // 跳转到 end
label:end; // 创建名为 end 的 label
......
```

注意，在每个分支的结尾，你应该用 `jumpLabel` 来跳转到你希望的位置。由于程序是线性执行的，所以如果你没有在分支的结束跳转，那么程序会继续往下运行，比如说：

``` ws
......
choose:分支 1:label_1|分支 2:label_2;
label:label_1; // 创建名为 label_1 的 label
......
......
label:label_2; // 创建名为 label_2 的 label
......
```

在这个剧本中，如果你选择了 `分支 2`，那么一切看起来好像没有问题。但是如果你选择了 `分支 1`，你会惊讶地发现，在 `分支 1` 执行完后，会继续执行 `分支 2`。那是因为程序按顺序继续执行下一行了，而你没有指定在分支结束后跳到哪里。