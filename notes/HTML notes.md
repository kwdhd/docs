# HTML notes

## form

### input

表单是一个包含表单元素的区域。
表单元素是允许用户在表单中（比如：文本域、下拉列表、单选框、复选框等等）输入信息的元素。
表单使用表单标签 `<form>` 定义。

|type 类型|含义|
|:-----:|:-----:|
|text |单行文本框|
|password|密码|
|radio|单选按钮|
|checkbox|复选按钮|
|submit|确认按钮|
|reset|重置按钮|
|button|按钮|

| 标签 | 描述 |
|:-----:|:-----:|
|`<form>` | 定义供用户输入的表单 |
| `<input>` | 定义输入域 |
| `<textarea>` | 定义文本域 (一个多行的输入控件) |
| `<label>` | 定义一个控制的标签  |
| `<fieldset>` | 定义域 |
| `<legend>` | 定义域的标题  |
| `<select>` | 定义一个选择列表  | 
| `<optgroup>` | 定义选项组  |
| `<option>` | 定义下拉列表中的选项  |
| `<button>`| 定义一个按钮  |


```
<form name="input" action="/html/html_form_action.asp" method="get">
Type your first name: 
<input type="text" name="FirstName" value="Mickey" size="20">
<br>Type your last name: 
<input type="text" name="LastName" value="Mouse" size="20">
<br>
<input type="submit" value="Submit">
</form> 
```