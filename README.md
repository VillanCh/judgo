# judgo
Golang 判断 Web 页面相似度（XML/Json/HTML/RawText）

## 定义相同与相似

* 相同：指的是所有数据相同，XML/HTML 应该指节点，包括节点参数节点数据都相同；Json 指的是字段以及字段值相同，RawText 可以所有文本内容相同
* 相似：同样的类型文本，但是不相同；经过泛化之后，在一定程度（阈值）上保持相同/相似的特性。

## 何谓泛化？

如果 HTML 页面中存在动态内容（例如时间/日期等），通过一定的替换与文本处理，把这些动态内容移除，或者替换成相同的文本，以增大文本相似度，这种做法叫做泛化

### 通用泛化思路

1. 日期格式泛化，例如 YYYY/MM/DD, YYYY-MM-DD 等格式
2. UUID 泛化 (MD5)
3. Unix 时间戳泛化
4. 动态内容移除（参见 SQLmap 对相似页面的处理）

## 不同的数据应该有不同的页面相似度算法与泛化算法

### Json

Json 有如下数据类型

1. number
2. bool
3. null
4. string
5. array
6. object

主要针对 Json Value 的部分进行泛化

### XML/HTML/RawText

可以暴力全局泛化，泛化后进行相似度比较，计算 simhash 或者其他操作