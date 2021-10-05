```uml
@startuml
!define MASTER_MARK_COLOR Orange 
!define TRANSACTION_MARK_COLOR DeepSkyBlue
!define MAIN_ENTITY #MintCream-MIstyRose
skinparam class {
    '図の背景
    BackgroundColor Snow
    '図の枠
    BorderColor Black
    'リレーションの色
    ArrowColor Black
}

entity "購入マスタ" as purchase <m_purchase><<M,MASTER_MARK_COLOR>>{
 + order_id [PK]
 + customer_code [PK][FK]
 --
 purcharse_date
 total_price
}

entity "購入詳細テーブル" as purchase_detail <d_purcharse_detail><<T,TRANSACTION_MARK_COLOR>> MAIN_ENTITY{
 + detail_id [PK]
 + order_id [PK][FK]
 --
 item_code
 price
 num
}

entity "ユーザ（顧客）マスタ" as customer <m_customers><<M,MASTER_MARK_COLOR>>{
 + customer_code [PK]
 --
 name
 pass
 address
 tel
 mail
 del_flag
 reg_date
}

entity "カテゴリーテーブル" as category <d_category><<T,TRANSACTION_MARK_COLOR>> MAIN_ENTITY{
 + category_id [PK]
 --
 name
 regdate
}

entity "商品マスタ" as item <M_item><<M,MASTER_MARK_COLOR>>{
 + item_code
 --
 item_name
 price
 image
 text
 detail
 del_flag
 reg_date
}
 
entity "お気に入りテーブル" as favorite <d_favorite><<T,TRANSACTION_MARK_COLOR>>MAIN_ENTITY{
 + favorite_id [PK]
 + customer_code [PK][FK]
 --
 item_name
}

entity "退会テーブル" as withdrawal <d_withdrawal><<T,TRANSACTION_MARK_COLOR>>MAIN_ENTITY{
 + with_id [PK]
 --
 customer_code
 with_date
 option
}

entity "カートテーブル" as cart <d_cart><<T,TRANSACTION_MARK_COLOR>>MAIN_ENTITY{
 + cart_id [PK]
 + customer_code [PK]
 + item_code [PK]
 --
 cart_num
}

entity "商品変更テーブル" as itemChange <d_itemChange><<T,TRANSACTION_MARK_COLOR>>MAIN_ENTITY{
 + change_id [PK]
 + item_code [PK][FK]
 --
 change_flg
 change_text
 change_index
}
 
entity "メーカーマスタ" as maker <M_maker><<M,MASTER_MARK_COLOR>>{
 + maker_id [PK]
 --
 maker_name
 adress
 tel
 reg_date
}

item      ---ri-o{   itemChange
item      }o-le---   maker
item      }o-do---   cart
item      }o-up---   category
purchase  }o-le---   customer
purchase  ---ri---   purchase_detail
customer  ---up-||   withdrawal
customer  }o-le-||   favorite


@enduml
```
