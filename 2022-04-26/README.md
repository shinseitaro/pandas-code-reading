# test_parse_dates を読む

- [pandas/test_parse_dates.py at main · pandas-dev/pandas](https://github.com/pandas-dev/pandas/blob/main/pandas/tests/io/parser/test_parse_dates.py)

## メモ

- test を実行する
    - そもそも今回初めて test を実行するので全くわからず。
    - contribute 方法にテストの方法があるはずと思って探したらあった
        - [Creating a development environment — pandas 1.4.2 documentation](https://pandas.pydata.org/pandas-docs/stable/development/contributing_environment.html#creating-a-development-environment)
        - `Creating an environment using Docker` に従う
    - 開発環境構築
    1. git clone 
        ```bash
        $ git clone git@github.com:pandas-dev/pandas.git
        $ cd pandas
        ```
    1. イメージビルド。tag 名は、ドキュメントに従ってみました。
        ```bash
        $ docker build --tag pandas-shinseitaro-env .
        # ログがわらわらいっぱいでてくる ... けっこう時間かかります
        :
        :
        Successfully built f721882369e7
        Successfully tagged pandas-shinseitaro-env:latest
        ```
        ```
        # コンテナ実行
        $ docker run -it -w /home/pandas --rm -v $PWD:/home/pandas pandas-shinseitaro-env
        root@edafc8dc68fb:/home/pandas# 
        ```
    1. pytest でテスト回してみる（←？
        ```
        root@edafc8dc68fb:/home/pandas# pytest pandas/tests/io/parser/test_parse_dates.py 
        ImportError while loading conftest '/home/pandas/pandas/conftest.py'.
        pandas/__init__.py:22: in <module>
            from pandas.compat import is_numpy_dev as _is_numpy_dev
        pandas/compat/__init__.py:15: in <module>
            from pandas.compat.numpy import (
        pandas/compat/numpy/__init__.py:4: in <module>
            from pandas.util.version import Version
        pandas/util/__init__.py:1: in <module>
            from pandas.util._decorators import (  # noqa:F401
        pandas/util/_decorators.py:14: in <module>
            from pandas._libs.properties import cache_readonly  # noqa:F401
        pandas/_libs/__init__.py:13: in <module>
            from pandas._libs.interval import Interval
        E   ModuleNotFoundError: No module named 'pandas._libs.interval'
        ```
    1. C拡張をビルドする必要がある、ってかいてあったの飛ばしてた。よく分かってないけど。 `python setup.py build_ext -j 4` をやってみる
        ```
        root@edafc8dc68fb:/home/pandas# python setup.py build_ext -j 4
        ``` 
    1. もう一回テストトライ
        ```
        root@edafc8dc68fb:/home/pandas# pytest pandas/tests/io/parser/test_parse_dates.py 
        :
        :
        ==== 17 failed, 359 passed, 29 skipped, 56 xfailed, 1 warning in 16.57s ===
        ```
    1. なにやってるのかさっぱりわからない
        - やりたいことは `test_parse_dates.py` を ブレイクポイントを入れて実行したかっただけ。でもやり方わからないので、`test_read_csv_with_custom_date_parser` だけ分解して理解してみる
        - [2022-04-26/test_read_csv_with_custom_date_parser.ipynb](./test_read_csv_with_custom_date_parser.ipynb)

