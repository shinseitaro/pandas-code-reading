# 


## テスト環境

- 前回悩んでたコンテナ内でデバグが、Remote-Containers` でサクッとできた
    1. git clone 
        ```bash
        $ git clone git@github.com:pandas-dev/pandas.git
        $ cd pandas
        ```
    1. VSCode の `Remote-Containers` をインストール
        - `Remote Development` でもOK。この場合は、Remote – SSH / Remote – Containers / Remote – WSL の3つまとめてインストールされる
    1. 表示 > コマンドパレット で `Open Folder in Container…` を選んで、さっきクローンしてきた `pandas` ディレクトリを選ぶ
    1. image build と container が自動作成されるので待ってる 
    1. 表示 > コマンドパレット > `Selected Interpreter ` > python 3.8.13 /opt/conda/bin/python を選択
    1. 表示 > コマンドパレット > `config test ` > pytest framework を選択 > pytest コードが入っているディレクトリ (`pandas`) を選択

- 参照
    - [【VS Code】Dockerコンテナの環境でリモート開発【Win/Mac】](https://chigusa-web.com/blog/vs-code%E3%81%A7docker%E3%81%AEpython%E7%92%B0%E5%A2%83%E3%81%A7%E3%83%AA%E3%83%A2%E3%83%BC%E3%83%88%E9%96%8B%E7%99%BA/)
    - [VSCodeとpytestでPythonコードをテスト&デバッグする｜CO-WRITE](https://gri.jp/media/entry/358)
