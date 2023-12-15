# til

**エラーの内容が表示できないとき**  
renderでエラー内容を表示するための部分テンプレートを呼び出す。  
その際下記のように記述するが、「model: f.object」の f は、form_with内で使用できる変数のこと。

~~~
<%= render 'shared/error_messages', model: f.object %>
~~~

そのため form_with の前に上記の内容を記しても変数が定義されておらず、nameerrorが発生する！
