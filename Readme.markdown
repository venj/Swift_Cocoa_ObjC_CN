# Using Swift with Cocoa and Objective-C (Swift 2.1) 中文版（初稿）

## 说明

经过几天的不懈努力，翻译的初稿已经完成。今天开始进行较对工作。预计本人自己只进行一次较对工作。

**暂时请不要提交勘误的PR。** 在我对初稿较对完成后，我就可以接受PR了。谢谢配合。

## 生成HTML文档

*注意：文档尚未较对*

``` bash
# 安装工具
$ brew install node
$ npm install -g markdown-styles

# 生成文档
$ (可选) rm -rf doc # 如果当前文件夹存在doc文件夹，先删除它
$ generate-md --layout github --input . --output doc
```

### 提示

- 因为开始本书翻译的时候，是基于Swift 2.1预发行版的。后来正式版发布，已经翻译的部分仅根据Revision History简单修改过一次，可能有部分新增或修改的内容没有及时更新，望知悉。
- 本人语法不及格，翻译多语句不通顺，也没人给我校稿，我只希望我的翻译能把意思传到到，请勿深究细节。

### 进度

- 翻译初稿完成。
- 开始校对 (0%)

### 版权

版权所有©️Venj (venj[AT]me[dot]com) 2015。 

本翻译项目以[The MIT License](http://opensource.org/licenses/MIT)开源。

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
