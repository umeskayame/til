# til

**◎エラーの内容が表示できないとき**  
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


**◎cssのpositionプロパティ**  
positionプロパティを指定することで要素の位置を指定できる。  

  position: absolute;  
  要素に上記を指定するとHTMLの構造を無視して配置が可能。top,right,left,bottomと一緒に使用する。  

  position: relative;  
  基準にしたい要素に上記を指定し、動かしたい要素にposition: absolute;を指定すると、  
  基準を基に要素の位置を決めることができる。  


  **◎Railsの link_to ~ do について**  
  link_to に画像を指定することはできない。その際に下記の形で記述することで画像にリンク先を指定できる。  
  末尾の <% end %> を忘れないようにする！  
  
  ~~~
<%= link_to item_path(item.id) do %>
  <div class='item-img-content'>
  <%= image_tag item.image, class: "item-img" %>
  </div>
<% end %>
  ~~~

**◎HTMLのtableタグについて**  
tableタグは下記のような表を作成できる。  

  
|      名前        |     番号      | 
| ------          | ------        | 
|       こん       |       1       |
|       梅        |       2       |  

表を作成する時は、th要素・tr要素・td要素を一緒に使用していく。  


th要素 → タイトル部分（名前/番号）  
tr要素 → 表の行  
td要素 → 表のデータ部分(こん,2など) 

(例)  

~~~
<table class="detail-table">
        <tr>
          <th class="detail-item">出品者</th>
          <td class="detail-value"><%= @item.user.nickname %></td>
        </tr>
        <tr>
          <th class="detail-item">カテゴリー</th>
          <td class="detail-value"><%= @item.category.name %></td>
        </tr>
        <tr>
          <th class="detail-item">商品の状態</th>
          <td class="detail-value"><%= @item.status.name %></td>
        </tr>
        <tr>
          <th class="detail-item">発送元の地域</th>
          <td class="detail-value"><%= @item.prefecture.name %></td>
        </tr>
        <tr>
          <th class="detail-item">発送日の目安</th>
          <td class="detail-value"><%= @item.shipping_day.name %></td>
        </tr>
</table>

~~~

**◎cssのobject-fitプロパティ**  
object-fitプロパティを使用すると、親要素に対してどのように画像や動画を埋め込むかを指定できる。  
値は下記がある。  
*contain  
*cover  
*fill  
*none  
*scale-down  
>https://developer.mozilla.org/ja/docs/Web/CSS/object-fit
