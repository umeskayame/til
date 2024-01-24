# til

**◎エラーの内容が表示できないとき**  
renderでエラー内容を表示するための部分テンプレートを呼び出す。  
その際下記のように記述するが、「model: f.object」の f は、form_with内で使用できる変数のこと。

~~~
<%= render 'shared/error_messages', model: f.object %>
~~~

そのため form_with の前に上記の内容を記しても変数が定義されておらず、nameerrorが発生する！  

  
    
**◎ログイン画面にエラー内容を表示するとき**  
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

**◎cssが一部分適用されないとき**  
1. cssファイルを適切に読み込んでいるか設定を見直す。
2. 検証モードでどの部分の影響を受けているか調べる。（他のスタイルに上書きされていないかどうか）
3. （上書きされている場合）例えばリセットcssが影響している場合、cssを適用したいクラスには特定のクラスを追加して記述する。
   リセットcssで a要素 を指定しているのであれば、「.親要素のクラス a {プロパティ;}」 のようにクラスを追加する。
   ※もしくは　「.クラス名　a {プロパティ;}」 の形にし、"クラス名"のa要素にスタイルが新たに適用されるよう上書きする。


**◎ストロングパラメーターについて**  
例えばコメントの投稿や商品の登録など新たなデータを作成する時は、プライベートメソッドにストロングパラメーターを設置して、  
どの情報を取得するかを記述する。  
※プライベートメソッドに記述していても、createアクションでストロングパラメーターを引数に指定し忘れた場合、  
エラー（~ for nil:NilClass）が起きるので注意する。  

**◎form_withメソッドにcssを適用する方法**  
(例)
~~~
<%= form_with(model: [@item, @comment], local: true) do |form| %>
 <%= form.text_area :content, placeholder: "コメントする", rows: "2" %>
 <%= form.submit "送信する" %>
<% end %>
~~~

上記のコメント記入欄と「送信」ボタンにcssを適用させたい場合、このようにcssを指定する。 
form input, form （ヘルパーメソッドの種類）  

・コメント欄  
form input, form textarea  

・送信ボタン  
form input, form submit  

※全てのform_withに設定されてしまうため、個別に設定する場合はヘルパーメソッドと一緒に ,class:"○○" という記述を追加する。

**◎cssのborder-radiusプロパティ**  
border-radiusプロパティはborderの角を丸めることができるもの。  
>https://developer.mozilla.org/ja/docs/Web/CSS/border-radius

