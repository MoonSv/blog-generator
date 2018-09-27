---
title: HTML补漏梳理
date: 2018-09-23 15:49:56
tags:html
---

## HTML补漏梳理

- ul — unordered list

  - li — list item

- dl — description list

  - dt — description term
  - dd — description definition

- a标签（get请求）

  - taget:
    - _blank
    - _self
    - _parent
    - _top
  - a标签的color默认是不继承的，会使用浏览器自带的颜色，如chrome就是`color: -webkit-link;`，可以通过`color: inherit;`强制继承祖先的颜色

- form（多用于post请求）

  - 只能发送POST或者GET请求
  - form标签也有target，和a标签的target是一模一样的
  - 如果form只有一个button标签`<button></button>`，那么它会**自动升级为提交按钮**
  - `<textarea style="resize:none;"></textarea>`

- table（详细用法）

  - ```html
    <table>
    	<colgroup>
      		<col width=100></col>
        	<col bgcolor=red width=200></col>
      		<col width=100></col>
      	</colgroup>
    	<thead>
    		<tr>
          		<th>Name</th>
          		<th>class</th>
          		<th>grade</th>
          	</tr>
    	</thead>
    	<tbody>
          	<tr>
          		<td>Jack</td>
          		<td>1</td>
          		<td>93</td>
    	</tbody>
    	<tfoot>
    	</tfoot>
    </table>
      
    ```

    一些人不知道colgroup的用法，其实这个标签很好用，可以直接对应列改变样式等等。