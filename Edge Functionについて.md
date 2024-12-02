# Supabase Edge Function 概要と使い方
SupabaseのEdge Functionについて現時点での理解をまとめました。
## Edge Functionとは
- Edge Functionは、Supabaseで提供される軽量なサーバーレス関数。ユーザーのリクエストに即座に反応し、インターネットの近くで処理を実行する。このプログラムを使用することで、特定のアクション（例えば、ボタンを押す/フォームに入力するなど）に即座に反応して処理を行うことができる。

- Edge Functionは、データベースの更新や計算、特定の処理を実行するために利用される。このプログラムはインターネット上のサーバーで動作するため、どこからでも高速に実行されるという特徴がある。

## Edge Functionの特徴
- 即時実行：Edge Functionは、指定されたアクションに素早く反応して実行される。これにより、ユーザーが操作をした後、即座に結果を受け取ることができる。
- 拡張性：多くのユーザーが同時に利用しても、問題なく動作する。
- 高いパフォーマンス：ユーザの近くで処理が行われるため、遅延が少なく非常に速い。

## Edge Functionの使い方
### Supabaseプロジェクトの作成
- まず、Supabaseのアカウントを作成し、新しいプロジェクトを作成する。プロジェクトを作成した後、Edge Functionを使用できるようになる。

### Edge Functionの作成
1. Supabase CLI（コマンドラインインターフェース）のインストール
- Edge Functionを作成するためには、まずSupabase CLIをインストールする必要がある。CLIをインストールすることで、コマンドラインから直接Edge Functionを操作できる。

~~~
yarn global add supabase
~~~

2. Supabase CLIでログイン
- Supabaseアカウントにログインし、CLIを使用してプロジェクトの管理や操作をする。
~~~
supabase login
~~~

3. Supabaseプロジェクトとリンク
- プロジェクトIDを指定してローカル環境とSupabaseプロジェクトを繋げる
~~~
supabase link --project-ref <project-id>
~~~

4. Edge Functionの作成
- コマンドラインで、以下のコマンドを使用してEdge Functionを作成する。これによりローカル環境で編集できるようになる。
- 以下では、hello-functionという関数を作成している。

~~~
supabase functions new hello-function
~~~

5. 関数の実装
- 作成されたファイルを開き、関数の内容を記述する。例えば、特定のデータを処理したり、ユーザへのレスポンスを返したりする処理を実装することでEdge Functionの機能を形にする。

6. Edge Functionのデプロイ
- 関数を書いた後、その関数をSupabaseにデプロイ（アップロード）する。

~~~
supabase functions deploy hello-function
~~~

- これにより、Edge Functionが実際に動作を始める。

### Edge Functionを呼び出す ★修正する★
- Supabaseで作成したEdge Functionは、HTTPリクエストを介してAPIとして呼び出すことができる。これにより、特定のイベント（ボタンのクリック、フォームの送信など）が発生した際に、その関数を実行させることができる。
~~~

~~~

## ローカルでの動作確認をせずにデプロイをする場合のリスク
1. 予期せぬエラーが本番環境に影響を与える
- ローカルでのテストなしにデプロイすると、予期しないエラーが本番環境で発生する可能性がある。特に、ユーザーの操作や他のシステムに影響を与えるようなバグが見逃されると、大きな問題になりかない。

2. デバッグが難しくなる
- 本番環境でエラーが発生した場合、ログを追跡して原因を特定するのが非常に困難になることがある。ローカルでの動作確認をせずに直接デプロイすると、問題発生後に対応する手間が大きくなる。

3. 無駄なデプロイ回数が増える
- ローカルで動作確認を行わないと、デプロイ後にエラーを修正して再度デプロイすることになり、無駄なデプロイ作業が増える。これにより、開発効率が低下する。

## Edge Functionの呼び出し
1. Edge FunctionのURLを確認
- まず、SupabaseにデプロイしたEdge FunctionのURLを確認する。通常、デプロイ後にSupabaseダッシュボードで関数のエンドポイントURLを確認できる。もしくは、CLIで以下のコマンドを使ってURLを確認できる。
~~~
supabase functions list
~~~
- hello-functionという関数をデプロイした場合、URLは以下のようになる
~~~
https://<project-id>.supabase.co/functions/v1/hello-function
~~~

2. curlを使ってEdge Functionを呼び出す
- 以下のコマンドを実行する。
~~~
curl https://<project-id>.supabase.co/functions/v1/hello-function
~~~
- Edge Functionが正しく設定されていれば、そのレスポンスが表示される。
