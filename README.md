# AWS-EC2インスタンス起動・Elastic IPの設定方法

## はじめに
## ※料金について※

### 当ドキュメントはEC2インスタンスおよびElastic IPの設定方法を記述したものです。これらを無料で使用する方法を記したものではありません。通常、下記方法で設定すると無料で使用することができますが、無料であることを保証するものではありません。したがって、当ドキュメントに倣って各設定をしたことで料金が発生しても、いかなる理由においても責任をおいません。

### 必ずAWS公式ドキュメントを参照ください


無料期間中のEC2インスタンス起動は基本的に無料ですが（全て無料対象環境を選択し、起動した場合）、
利用状況によっては料金が発生するため、不要になった際は必ず削除してください。詳細は公式ドキュメントを参照してください。

Elastic IPについては料金が発生する可能性があります。
EC2インスタンス等に関連付けを行えば無料で使用できます。しかし、その後、インスタンスを削除したり、手動で関連付けを解除することによって、どのインスタンスにも関連付けが行われていない場合、料金が発生します。関連付けを解除した際は、必ずIPの「解放」を行ってください。詳細は公式ドキュメントを参照してください。
また、当ドキュメント下部に解放の方法を記述しています。
<br>
<br>


## - AWSのEC2インスタンスの起動方法とElastic IPの設定方法 -

## 0.AWSアカウントを開設する
事前にAWSのアカウントを開設してください。
<br>

## 1.EC2インスタンスの起動
### 1-1.マネジメントコンソールにログインしてEC2ダッシュボードにアクセスする
![image](https://user-images.githubusercontent.com/66664167/92108283-15c8c780-ee22-11ea-88d1-2f34b653d8e6.png)

### 1-2.「インスタンスを起動する」ボタンを押下
![image](https://user-images.githubusercontent.com/66664167/92108417-4c9edd80-ee22-11ea-9883-474054b16d48.png)

### 1-3.Amazonマシーンイメージ（AMI)：「Linux 2 AMI(無料利用枠の対象）」を選択後、「次のステップ」ボタン押下
（環境に合わせてOSを選択する。）
![image](https://user-images.githubusercontent.com/66664167/92108528-8374f380-ee22-11ea-8b50-a60c77c2c3b3.png)

### 1-4.インスタンスタイプの選択：タイプ「t2.micro（無料利用枠の対象)」を選択後、「次のステップ」ボタン押下
![image](https://user-images.githubusercontent.com/66664167/92108904-0a29d080-ee23-11ea-8142-edc28e4add7a.png)

### 1-5.インスタンスの詳細の設定：初期設定のまま、「次のステップ」ボタン押下（環境によって詳細設定を変える）
![image](https://user-images.githubusercontent.com/66664167/92109391-e74bec00-ee23-11ea-8a48-3d1cd91d6197.png)

### 1-6.ストレージの追加：初期設定のまま、「次のステップ」ボタン押下（環境によって詳細設定を変える）
![image](https://user-images.githubusercontent.com/66664167/92109483-11051300-ee24-11ea-9b22-256e3d79e4e2.png)

### 1-7.タグの追加：初期設定のまま、「次のステップ」ボタン押下（環境によってタグを追加する）
![image](https://user-images.githubusercontent.com/66664167/92109589-41e54800-ee24-11ea-8c03-83ae4155308e.png)

### 1-8.セキュリティグループの設定をする
#### 1-8-1. 「ルールの追加」ボタンを押下する
![image](https://user-images.githubusercontent.com/66664167/92109703-76f19a80-ee24-11ea-940d-2c02e7d7a85d.png)

#### 1-8-2.追加された列の「タイプ」のプルダウンから「HTTP」を選択

![image](https://user-images.githubusercontent.com/66664167/92109843-b4eebe80-ee24-11ea-9d2c-237a31b0437e.png)


![image](https://user-images.githubusercontent.com/66664167/92109875-bd46f980-ee24-11ea-8cd5-6113a7ad7c76.png)

#### 1-8-3.「確認と作成」ボタンを押下

![image](https://user-images.githubusercontent.com/66664167/92109909-c8018e80-ee24-11ea-9ee5-fb7a1def0894.png)

### 1-9.インスタンス作成の確認：「起動」ボタンを押下
![image](https://user-images.githubusercontent.com/66664167/92110145-3c3c3200-ee25-11ea-9fb7-47dd699a3acf.png)


### 1-10.キーペアを作成する
#### 1-10-1. 「新しいキーペアの作成」（既存を使用する場合は「既存のキーペア」を使用を選択)
#### 1-10-2. 「キーペア名」に任意の名前を入力する
#### 1-10-3.「キーペアのダウンロード」ボタンを押下する
#### 1-10-4.「インスタンスの作成」ボタンを押下

![image](https://user-images.githubusercontent.com/60914189/122027914-7865df80-ce06-11eb-9753-1aa4602e51c2.png)

### 1-11.「インスタンスの表示」ボタンを押下
![image](https://user-images.githubusercontent.com/66664167/92112724-33e5f600-ee29-11ea-86cf-ed16968d6d2b.png)


## 2. Elastic IPの設定
### 2-1. メニューから「Elastic IP」を選択し、「Elastic IPアドレスの割り当て」ボタンを押下
![image](https://user-images.githubusercontent.com/66664167/92112122-47dd2800-ee28-11ea-8683-4a1de647ccd3.png)

### 2-2. Elastic IP アドレスの割り当て：　初期設定（AmazonのIPv４アドレスプール）のまま、「割り当て」ボタンを押下する
![image](https://user-images.githubusercontent.com/66664167/92112345-9a1e4900-ee28-11ea-9f41-8834faa54ca9.png)

### 2-3. Elastic IP が割り振られていることを確認する
![image](https://user-images.githubusercontent.com/66664167/92112535-e5d0f280-ee28-11ea-8291-3a7acc0967fb.png)

### 2-4. 「アクション」から、「Elastic IPアドレスの関連付け」を押下する
![image](https://user-images.githubusercontent.com/66664167/92113430-41e84680-ee2a-11ea-83ff-830fd8cb43b6.png)

### 2-5. Elastic IPアドレスの関連付け：「インスタンス」を選択（テキストボックスをクリックすると、起動しているインスタンスが選択できる)、「関連付ける」ボタンを押下する
![image](https://user-images.githubusercontent.com/66664167/92117681-77902e00-ee30-11ea-81d0-f40795866971.png)

### 2-6. インスタンスが関連づけられていることを確認する
![image](https://user-images.githubusercontent.com/66664167/92114421-c4bdd100-ee2b-11ea-8216-67b5d62ecb85.png)


# ！！重要！！　<br>！！料金が発生しない方法！！　　<br>Elastic IP の関連付け解除後の解放
## Elastic IPはインスタンス等に関連付けしている場合は課金されないが、関連付けされていない状態で保持していると料金が発生するので注意！
## 関連付け解除後は「解放」することで料金の発生防ぐ

### インスタンス削除等による、Elastic IPの関連付け解除後の「開放」方法
- メニューより「Elastic IP」を押下し、「アクション」の中の「Elastic IPアドレスの解放」をクリック
![image](https://user-images.githubusercontent.com/66664167/92121104-dd7eb480-ee34-11ea-8f00-f93ec0b48307.png)

- 「解放」を押下する
![image](https://user-images.githubusercontent.com/66664167/92118659-bb376780-ee31-11ea-8944-77d92193265e.png)

- Elastic IPがないことを確認する
![image](https://user-images.githubusercontent.com/66664167/92118981-1ff2c200-ee32-11ea-93a7-bead0ec9d444.png)
