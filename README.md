# authorization-app-practice

## 概要
COACHTECH 教材 Tutorial 10-3「認可機能 ハンズオン演習」で作成した成果物です。
スターターキットを加工し、ユーザごとの認可機能（ユーザ自身の投稿した内容のみ編集、削除機能）を実装

## 使用技術
- PHP 8.x
- Laravel 10.x
- Policy / Gate（認可）
- Laravel Fortify（認証）

## ディレクトリ構成（抜粋）
```text
~/laravel-practice/
└── 9-5-5_hands-on/
    └── relation-app-practice/
        ├── app/                                # MVCのモデル（M） とコントローラー(C)
                └── Controllers                 # HTTPのコントローラー（リクエスト処理）
                    └── PostController.php      # PostController（$this->authorize('メソッド名',$post)を確認）
            └── Providers/                      #Provider（ルーティング周りをまとめるクラス）の設定
                    └── RouteServiceProvider    #ログイン後に行くページ等を設定            　　 
        ├── database/    
            ├── factories/                      # ファクトリー（テストデータの自動生成）
                └── UserFactory.php
            ├── migrations/                     # マイグレーションの定義
                ├── 2014_10_12_000000_create_users_table.php
                ├── 2014_10_12_100000_create_password_reset_tokens_table.php
                ├── 2019_08_19_000000_create_failed_jobs_table.php
                ├── 2019_12_14_000001_create_personal_access_tokens_table.php
                └── 2019_12_14_000001_create_posts_table.php
            └──Seeder 　　　　　　　　　　　　　　#シーダーの定義
                └── DatabaseSeeder.php
        ├── routes/                            #コントローラとの紐づけ（ルーティング）
            ├── api.php
            ├── channels.php
            ├── console.php
            └── web.php　　　　　　　　　　　　　　#PostControllerとのルーティング
        ├── resources/
            ├── css/
            ├── js/
            └──  views/                   　　　 # Bladeテンプレート（V）
                └── auth/ 
                    ├── login.blade.php          #ログインページ
                    └── register.blade.php       #登録ページ
                └── posts/ 
                    ├── edit.blade.php           #編集ページ
                    └── index.blade.php     　　 #投稿一覧ページ
        ├── config/
        ├── strage/
        ├── bootstrap/
        └── tests/
```


## 学んだこと
- ポリシーメソッドによる実装
    - ポリシーを活用することにより、コントローラー部分の実装を少なくすることができる。 （コントローラー側で認可を追加する必要あり）
- ポリシーメソッドに合わせて、Bladeに@can、@cannnotディテクティブを追加することで、表示を変えることができる。　※今回は@canで実装


## 動作確認
1. Githubからリポジトリをクローン
'''
git clone git@github.com:aridome-sashizume/authorization-app-practice.git
'''
2. Sailを起動
'''
./vendor/bin/sail up -d
'''
3. http://localhost にアクセス
4. ログインをクリック
5. usera@example.com / password でログイン
6. 投稿一覧が表示され、ユーザAのみ編集・削除が表示されれば成功