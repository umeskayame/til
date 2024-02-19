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

**◎button要素について**  
button要素を使用するとページにボタンを作ることができる。  
~~~
<button type="属性" name="名前" value="値">
  <font>ボタンに入れたい文字</font>
</button>
~~~

type属性はボタンの種類を指定でき、下記がある。  
・submit（初期値）  
フォームに入力した内容を送信する  

・reset  
フォームに入力した内容をリセットする  

・button  
何もしない汎用的なボタン  

**◎JacaScriptの document.addEventListener("DOMContentLoaded", function() {} について**  
JavaScriptの記述で1行目に **document.addEventListener("DOMContentLoaded", function() {}** を記述すると、  
HTMLが完全に読み込まれてからJavaScriptのコードが実行される。  

**◎再読み込みをしないとJavaScriptが動作しない時の対処**  
JavaScriptを設置したページに初めて遷移した時は動作するのに、その後は画面をリロードしないとJavaScriptが動作しない場合、  
ターボリンクス（画面の遷移を速くするもの）が影響している可能性がある。  
リロードしなくてもJavaScriptを読み込むためには、JavaScriptを設置したページへ到達するまでにクリックするボタンの全てに、  
ターボを無効化する **data: { turbo: false }** を追加する。  

**◎Rubyで作成したデータベースを修正する方法**  
マイグレーションファイルは修正ができないため下記の流れで作業する。  
1. rails db:migrate:status でデータベースの状況を確認。
2. 「up」の状態であれば「down」に変更する必要があるため、rails db:rollback を行う。
3. 再度データベースの状況を確認し、「down」になっていることを確かめてから修正を行う。
4. rails db:migrate でデータベースを実行する。

※rails db:rollback を行うと最新のマイグレーションファイルのみdownになるため、最新のファイルでない場合は  
複数回rails db:rollbackを行なっていく。  

**◎Rubyのany?メソッド**  
配列に対して使えるメソッドで、要素の中に一つでも真であるものがあればtrueを返す。全ての要素が偽であればflseを返す。  
使用方法は3つ。  

1. 単独で使用
   配列.any?  
2. 各要素にパターンが含まれているかを確認
   配列.any?(パターン)
   (例)
   ~~~
   colors = [ 'black', 'gray', 'lightgray' ]
   puts.any?(/light/)
   ~~~
   ⇨true
3. 各要素に対して判定を行う
   配列.any?{|変数| 変数を使った判定条件}
   (例)
   ~~~
   animals = [ dog, cat, rabbit ]
   nnimals.any? { |animal| animal == dog }
   ~~~
   ⇨true

HappyTradeで使用したのは要素の判定を行う3。  
~~~
<% @comments.any? { |comment| comment.is_exchange_proposal? } %>
~~~
@commentsには複数のコメント情報が入っているため、変数を使用し、独自で作成したis_exchange_proposal?メソッドが各要素に当てはまるか調べている。  

**◎ビジネスロジックについて**  
ビジネスロジック（データに対する処理）は、コントローラーではなくモデルに記載する。  
(例)
~~~
class Comment < ApplicationRecord
  belongs_to :user
  belongs_to :item

  def is_exchange_proposal?
    content.present? && content.include?("交換を希望しています。こちらのアイテムと交換いただくことは可能でしょうか。")
  end

end

~~~
この例では、コメントの内容は存在しているか、かつ特定のフレーズは含まれているかを確認するメソッド。  
このメソッドをビューで ~.is_exchange_proposal? の形で使用している。  

**◎ログイン中のユーザーIDとコメント者のユーザーIDの一致確認**  
~~~
<% if current_user.id == @comment.user_id %>
~~~
上記ではエラーが発生する。原因は、コメントを表示するitemコントローラーで @comment = Comment.new と定義しており  
これだと空のインスタンスを生成しただけでuserとは紐づいていないから。  
また  @comments = @item.comments.includes(:user) より、 @comennts ではエラーが起きないように思えるが  
複数のコメント情報が入っているため引き続きエラーが発生してしまう。  
これを回避するために、まずは繰り返し処理の記述を行いコメントを一つずつ確認していく流れを作る。  
（例）  
~~~
<% @comments.each do |comment| %>
  <% if current_user.id == comment.user_id %>
    <%= "コメントした人のテスト表示" %>
  <% end %>
<% end %>
~~~

**◎マイグレーションで外部キー制約をかける時**  
外部キー制約をかけるとき、すでに作成したテーブルの主キーをカラム名に指定するのであれば、 t.references :カラム名,  foreign_key: true でOK。  
しかし作成したテーブルの主キー名を一部変更するのであれば、 t.references :カラム名, foreign_key:  { to_table: :参照先のテーブル名 } にする。  
（例）  
 t.references :buyer_user,         null: false, foreign_key: { to_table: :user }  

**◎attr_accessorについて**  
attr_accessor とは、モデルやコントローラーにおいてゲッター（値の取得をする）とセッター（値の更新をする）を記述してくれるもの。  
こうすることで、指定した値がform_withメソッドの引数に指定できるようになる。  

（モデルでのイメージ例）  
attr_accessors使用前
~~~
class Order
  def price #ゲッター
    @price
  end

  def price=(price) #セッター
    @price = price
  end
end
~~~
attr_accessors使用後  
~~~
class Order
  attr_accessor :price
end
~~~

**◎Formオブジェクトについて**  
Formオブジェクトを利用するパターンは2つある。  
  
* **一つのビューで**複数の異なる情報を入力するフォーム（例えばメモの内容を入力するフォームとカテゴリを入力するフォーム）があり、  
それぞれのテーブルを同時に更新したいとき。  

* モデルは存在しないがバリデーションを設定したいとき。（例えば検索フォームに入力されたものが正しいかどうかなどの確認。）  

一つ目のパターンは、通常通りターミナルでそれぞれのモデルを作成し、アソシエーションはそのモデルに記載する。  
バリデーションは作成したFormオブジェクトに記載する。  

**◎form_withメソッドのurlオプション**  
下記のようにurlオプションをつけると、データが送信される先のコントローラーのアクションを指定できる。  
併せてurlをハードコードする（URLを直接コード内に書き込む）必要がなくなるため、何らかの理由でurlが変更されても逐一変更する必要がない。
~~~
<%= form_with model: @trade_delivery, url: item_trades_path, data: { turbo: false } %>
~~~

**◎"モデル名.new"をした時のカラムとインスタンス変数の紐付け**  
独自で作成したインスタンス変数とdbのカラムを一致させたい時、 モデル名.new（） と記述し  
()内にカラム名と紐づけるインスタンス変数を記述する。  

（例）  
~~~
@trade_delivery = TradeDelivery.new(
      user_id: @seller.id,
      item_id: @seller_item.id,
      buyer_user_id: @buyer.id,
      buyer_item_id: @item.id
    )
~~~
   
