<h1>aws lambda layer追加</h1>

2025/03/18

手動でlayerを追加

![alt text](images/image-8.png)

[AWS lambda Node\.jsの追加モジュールを使って他のAPIを実行してみる（requestモジュール使用 現在は非推奨） – ANTEKU CREATIVE BLOG](https://anteku.jp/blog/develop/aws-lambda-node-js%E3%81%AE%E8%BF%BD%E5%8A%A0%E3%83%A2%E3%82%B8%E3%83%A5%E3%83%BC%E3%83%AB%E3%82%92%E4%BD%BF%E3%81%A3%E3%81%A6%E4%BB%96%E3%81%AEapi%E3%82%92%E5%AE%9F%E8%A1%8C%E3%81%97%E3%81%A6/)

[Lambdaレイヤーにnode\_modulesを登録してみた](https://zenn.dev/mn87/articles/c421ebaea55f8b)

lambda作成

![alt text](images/image.png)

テストイベント作成
![alt text](images/image-1.png)

lambda関数

index.mjs

```js
import request from 'request';
const url = 'https://qiita.com/api/v2/users/miriwo';

const method = 'GET';
const options = {
    url: url,
    method: method,
};

export const handler = (event) => {
    request(options, function (error, response, body) {
        console.log(body);
    });  
};
```

追加モジュールの準備

nodejsフォルダを作成する。かならず,nodejsというフォルダ名にすること。
npm initは必要ない。

```
practice-aws-lambda-manual-layer $ mkdir nodejs
nodejs $  mkdir node_modules
nodejs $  npm install request
:::::::::
practice-aws-lambda-manual-layer $ zip -r nodejs.zip nodejs/
```

レイヤーの作成

先に作成したnodejs.zipを使ってレイヤーを作成。

レイヤー
![alt text](images/image-2.png)
レイヤーの作成
![alt text](images/image-3.png)
レイヤーの設定
![alt text](images/image-4.png)
レイヤーの追加
![alt text](images/image-5.png)
追加
![alt text](images/image-6.png)

テスト実行
![alt text](images/image-7.png)


モジュールを追加したい場合は、ローカルでnpm installしてからバージョンを作成することでバージョンアップできます。