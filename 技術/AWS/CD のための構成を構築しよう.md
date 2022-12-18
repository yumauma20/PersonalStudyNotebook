![Alt text](https://pages.awscloud.com/rs/112-TZM-766/images/Hands-On-for-Beginners_2022_code_0819_v1.png)

# 7 - 01
- AWS CodeCommit 
  - ソース管理サービス
  - サーバー管理不要
- AWS CodeBuild
  - ソースコードをコンパイルテスト実行
  - サーバー管理不要
- AWS CodeDeploy
  - コンピューティングソースに対してデプロイを行う
  - オートスケーリングする構成に対しても自動デプロイする
- AWS CodePipeline 
  - 継続的デリバリーサービス
  - ソースコードの変更をトリガにビルド、デプロイといった一連の流れを自動的に実行
  - パイプライン数で料金が決まる
- S3
  - データを格納・管理できるオブジェクトストレージサービス
  - 主にウェブサイトやアプリケーションなどのデータバックアップおよび復元、アーカイブなど、さまざまなことに利用
  - また、ファイルのバックアップ、ファイル処理の加工前、あるいは加工後のファイルの保存、動画・画像ファイルやCSSなどWebで使う静的なファイルをS3に置いて配信するなど、非常に広範囲な使い方ができる
- Amazon EC2
  - LinuxやWindowsなどの仮想サーバを作成できるサービス

# 7 - 02

- codecommitで作成したリポジトリをcloneするコマンド
  - コピーするコマンドが今存在していない？のでミスりがち

`git clone https://git-codecommit.ap-northeast-1.amazonaws.com/v1/repos/{リポジトリの名前}`

# 7 - 03

- CodeCommitにコミットした時点で自動でCodePipelineの機能でS3に反映させる

- ソースコードの変更検知方法
  - CloudWatch
    - 変更時
  - CodePipeline
    - 定期的

# 7 - 04

`wget https://aws-codedeploy-ap-northeast-1.s3.ap-northeast-1.amazonaws.com/latest/install`

- サービスが実行されているかどうか確認するには、次のコマンドを実行する。

`sudo service codedeploy-agent status`

そのファイルに CodeDeploy エージェントがインストールされて実行している場合、下のようなメッセージが表示される。
`The AWS CodeDeploy agent is running。`

# 7 - 05

- buildspec.yml
```
version: 0.2

phases:
  build:
    commands:
      - aws deploy push --application-name xxx --s3-location s3://xxx/artifact.zip --source src
artifacts:
  files:
    - '**/*'
  base-directory: src
```

# 7 - 06
- appspec.yml
```
version: 0.0
os: linux
files:
  - source: index.html
    destination: /var/www/html/
```

# 7 - 07

- CodeCommit
- CodeBuild
- CodeDeploy
の順に進んでいく

- NextStep
ELB + EC2の構成を使ってさまざまなデプロイを試す