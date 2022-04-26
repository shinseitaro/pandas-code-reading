# test_parse_dates を読む

- [pandas/test_parse_dates.py at main · pandas-dev/pandas](https://github.com/pandas-dev/pandas/blob/main/pandas/tests/io/parser/test_parse_dates.py)

## たろうの進め方

- 作業時間は一時間以内（メモ下記含めて）
- 今後のCode Readingも効率的にやっていく方法を探りながら読む

## メモ

- test を実行する
    - 方法がわからず、速攻隣の人にきく
        1. pandas を build する時にテストを回せる。それを使って実行。setup.py
        1. pandas のソースコードをローカルに持って、テストを直接実行してエディタでデバグをしていく（←これをやってみよう）
    - pandas 仮想環境にインストール。ファイルをぶち壊す気持ちで望む。
        - .venv/lib/python3.9/site-packages/pandas/tests/io/parser/test_parse_dates.py
        - 開いてデバグ実行
            - dateutil でインポートエラー
        - hypothesis と pytest はもうわからんかったんで、pip でライブラリ突っ込む
    - ファイルをデバグ→ブレイクポイントで止まらない→あ、ここは関数群だ。
    - test の実行方法がわからないことがわかった
- たぶん Contributing 方法について書いてあるハズ。それをみたらテスト方法も書いてあるはず。
    - あった→[Creating a development environment — pandas 1.4.2 documentation](https://pandas.pydata.org/pandas-docs/stable/development/contributing_environment.html#creating-a-development-environment)
    - Using a Docker container に従う
        - 手動で開発環境を整える代わりに、Docker使って構築する方法あるよ
        - pandasが DockerFile を用意してるから、それ使ってね
        ```bash
        $ git clone git@github.com:pandas-dev/pandas.git
        $ cd pandas
        $ ls
            AUTHORS.md  LICENSES     README.md   azure-pipelines.yml  doc              pyproject.toml        setup.cfg      test_fast.sh   web
            Dockerfile  MANIFEST.in  RELEASE.md  ci                   environment.yml  requirements-dev.txt  setup.py       typings
            LICENSE     Makefile     asv_bench   codecov.yml          pandas           scripts               test_fast.bat  versioneer.py
        ```
        - たしかにあった
        ```bash
        # イメージビルド。tag 名は、ドキュメントに従ってみました。
        $ docker build --tag pandas-shinseitaro-dev . 
        # ログがわらわらいっぱいでてくる ... けっこう時間かかります
        Successfully built 45c2f1e1123c
        Successfully tagged pandas-shinseitaro-dev:latest


        # 実行
        $ docker run -it --rm -v $pwd:/home/pandas-shinseitaro pandas-shinseitaro-dev
        root@68475d448b6e:/

        ```
        - (この作業中に時間切れしたが、さすがにここで終わるとダメなので30分くらい延長)
        - docment の見落としそうなところに `Note that you might need to rebuild the C extensions if/when you merge with upstream/master using:` って書いてあるので、やるべきなのかよくわからんけど実行

        ```
        $ root@68475d448b6e:/# cd home/pandas/
        $ python setup.py build_ext -j 4
        ```
        - で？
        ```
        $ root@68475d448b6e:/home/pandas# python setup.py test
        ```

         






## 参照
- [VSCodeで自作モジュールのimportエラーを解消してみた | DevelopersIO](https://dev.classmethod.jp/articles/vscode_python_import_error/)

