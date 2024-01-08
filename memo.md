# til

**エラーの内容が表示できないとき**  
renderでエラー内容を表示するための部分テンプレートを呼び出す。  
その際下記のように記述するが、「model: f.object」の f は、form_with内で使用できる変数のこと。

~~~
<%= render 'shared/error_messages', model: f.object %>
~~~

そのため form_with の前に上記の内容を記しても変数が定義されておらず、nameerrorが発生する！  

  
    
**ログイン画面にエラー内容を表示するとき**  
ビューに下記を設置する。  

~~~
 <div class='login-flash-message'>
        <%= flash[:notice] %>
        <%= flash[:alert] %>
        </div>
~~~


**cssのpositionプロパティ**  
positionプロパティを指定することで要素の位置を指定できる。  

  position: absolute;  
  要素に上記を指定するとHTMLの構造を無視して配置が可能。top,right,left,bottomと一緒に使用する。  

  position: relative;  
  基準にしたい要素に上記を指定し、動かしたい要素にposition: absolute;を指定すると、  
  基準を基に要素の位置を決めることができる。  


  **Railsの link_to ~ do について**  
  link_to に画像を指定することはできない。その際に下記の形で記述することで画像にリンク先を指定できる。  
  末尾の <% end %> を忘れないようにする！  
  
  ~~~
<%= link_to item_path(item.id) do %>
  <div class='item-img-content'>
  <%= image_tag item.image, class: "item-img" %>
  </div>
<% end %>
  ~~~
