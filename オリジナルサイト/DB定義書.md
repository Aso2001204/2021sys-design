# DB定義書

## ER図
[ER図はこちらです](https://github.com/Aso2001204/2021sys-design/blob/main/%E3%82%AA%E3%83%AA%E3%82%B8%E3%83%8A%E3%83%AB%E3%82%B5%E3%82%A4%E3%83%88/ER%E5%9B%B3.md)
*****
*****

## DBテーブル詳細一覧
AUTO_INCREMENT 自動採番を表す
*****
### 顧客情報マスタ(m_customers)
|   和名   |      属性名    | 型(カラム名)  | PK | FK | NN |      備考      |
|----------|:--------------|:--------------|-----|----|----|----------------|
|顧客ID    |customer_id    |int(10)        |〇   |-   |〇  |AUTO_INCRIMENT  |
|氏名      |customer_name  |varchar(30)    |-    |-   |〇  |-               |
|電話番号  |customer_tel   |int(25)        |-    |-   |〇  |-               |
|メールアドレス|customer_email|varchar(100)|-    |    |〇  |-               |
|住所      |customer_adress|varchar(100)   |-    |-   |〇  |-               |
|商品ID    |item_id        |int(10)        |-    |〇  |〇  |商品テーブル参照 |
|最終購入日|f_reg_date     |date           |-    |-   |〇  |-               |

*****
### ログインテーブル
|   和名   |      属性名    | 型(カラム名)  | PK | FK | NN |      備考      |
|----------|:--------------|:--------------|-----|----|----|----------------|
|ログインID|rogin_id       |int(10)         |〇  |-    |〇  |AUTO_INCLEMENT |
|パスワード|password       |varchar(20)     |-   |-    |〇  |-              |
|メールアドレス|email      |varchar(100)    |-   |-    |〇  |-              |

*****
### 商品テーブル（M_items）
|   和名   |      属性名    | 型(カラム名)  | PK | FK | NN |      備考      |
|----------|:--------------|:--------------|-----|----|----|----------------|
|アイテムID|item_id        |int(10)        |〇    |-   |〇 |AUTO＿INCLEMENT |
|商品名    |item_name      |varchar(20)    |-     |-   |〇 |-               |
|価格      |price          |int(6)         |-     |-   |〇 |-               |
|仕入ID    |supplier_id    |int(10)        |-     |〇  |〇 |仕入先マスタ参照 |
|画像ファイル|image        |varchar(250)   |-     |-   |〇 |-               |
|商品詳細  |detail         |varchar(500)   |-     |-   |-  |デフォルト値:null|
|削除フラグ|del_flag       |int(11)        |-     |-   |-  |デフォルト値:null|
|登録日    |reg_date       |date           |-     |-   |〇 |-                |

*****
### 仕入先テーブル（d_supplier）
|   和名   |      属性名    | 型(カラム名)  | PK | FK | NN |      備考      |
|----------|:---------------|:-------------|-----|----|----|----------------|
|仕入先ID  |supplier_id     |int(10)       |〇   |-   |〇  |AUTO_INCLEMENT  |
|商品ID    |item_id         |int(10)       |〇   |〇  |〇  |商品テーブル参照|
|仕入先名  |supplier        |varchar(100)  |-    |-   |〇  |-　　 　　　　　|
|住所      |adress          |varchar(200)  |-    |-   |〇  |-              |
|電話番号  |tel             |int(15)       |-    |-   |〇  |-              |
|メールアドレス|email       |varchar(100)  |-    |-   |〇  |-              |
|登録日    |reg_date        |date          |-    |-   |〇  |-              |

*****
### 購入テーブル(d_order)
|   和名   |      属性名    | 型(カラム名)  | PK | FK | NN |      備考      |
|----------|:---------------|:-------------|-----|----|----|----------------|
|オーダーID|order_id        |int(10)       |〇    |-   |〇  |AUTO＿INCLEMENT |
|顧客ID    |customer_id     |int(10)       |-    |〇   |〇  |顧客テーブル参照|
|購入日    |purchase_date   |date          |-    |-    |〇  |-               |
|総計      |total_price     |int(15)       |-    |-    |〇  |-               |
*****

### 購入詳細テーブル（d_purchase_detail)
|   和名   |      属性名    | 型(カラム名)  | PK | FK | NN |      備考      |
|----------|:---------------|:-------------|-----|----|----|----------------|
|購入ID    |detail_id       |int(10)        |〇  |-   |〇  |AUTO_INCREMENT  |
|オーダーID|order_id        |int(10)        |〇  |-   |〇  |デフォルト値:0 購入テーブル参照|
|商品コード|item_code       |int(10)        |-   |-   |〇  |商品テーブル参照|
|価格      |price           |int(6)         |-   |-   |〇  |-               |
|数量      |num             |int(10)        |-   |-   |〇  |デフォルト値:0   |
