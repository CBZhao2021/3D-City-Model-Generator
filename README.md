# 3D都市モデル生成シミュレータ

![image](res_examples/fig01.png)

## 1. 概要

本リポジトリでは、Project PLATEAUの令和5年度のユースケース開発業務の一環として行われた「dt24-05 3D都市モデル生成シミュレータ」の成果物である「3D都市モデル生成ツール」のソースコードを公開しています。

「3D都市モデル生成ツール」は、建物フットプリントデータやユーザーが指定するパラメータに基づき、3D都市モデル（建築物、道路、植生、都市設備）を自動で生成するWebオーサリングツールです。このツールは、衛星画像や沿道画像の範囲の3D都市モデルの作成に対応しており、詳細レベル（LOD）の向上機能（LOD1-3）を備えています。

## 2. 「3D都市モデル生成ツール」について

「3D都市モデル生成シミュレータ」プロジェクトは、3D都市モデルのアクセシビリティとスケーラビリティを高め、都市デジタルツインの作成コストを大幅に削減することを目指しています。この目標達成のために、最新の自動生成技術を核とする3D都市モデル生成シミュレータが開発されました。

このシミュレータは、建築物、道路、都市設備、植生を含む主要なモデルを網羅し、LOD（詳細レベル）、形状、高さ、種別などのパラメータをユーザーが自由に設定できる設計になっています。また、生成された3D都市モデルをCityGML形式で出力し、ツール上での視覚化も可能です。

## 3. 利用手順

本システムの構築手順及び利用手順については利用チュートリアルを参照してください。

## 4. システム概要

### 【3D都市モデル生成】

1. **衛星画像リファレンス機能**  
   - 衛星画像に基に、建物輪郭・屋根形状・道路・植生を抽出するとともに、それらの空間分布に基づいて3D都市モデルを生成します。
   - インスタンスセグメンテーションやセマンティックセグメンテーション等を用いたアルゴリズムを採用しています。

2. **沿道映像リファレンス機能 (LOD3のみ)**  
   - 沿道映像からLOD3に必要な開口部情報に関するパラメータを抽出します。  
   - 三次元再構築、セグメンテーション、点群ラベリングを用いたアルゴリズムを採用しています。

3. **パラメータ設定機能**  
   - LOD、スケール、対象地物、乱数シードなどの汎用的なパラメータを設定可能です。  
   - 各地物特有のパラメータ設定も可能です。

4. **実際の都市における仮想3D建築物モデル生成機能**  
   - パラメータ(LOD, 建物輪郭、屋根形状，高さ)に基づいて、3D建築物を生成し、CityGML(PLATEAU v4)形式で出力します。  
   - PLATEAUの3D建築物モデルを学習して、衛星画像と沿道画像（LOD３の場合）から3D建築物モデルを生成します。

5. **道路モデル生成機能**  
   - ユーザが設定したパラメータ (LOD, 道路種別, 幅員) に基づいて、道路モデルを生成し配置します。  
   - CityGML (PLATEAU v4) 形式で出力されます。

6. **植生モデル生成機能**  
   - ユーザが設定したパラメータ (LOD, 種別) に基づいて、植生モデルを生成し配置します。  
   - CityGML (PLATEAU v4) 形式で出力されます。

7. **都市設備モデル生成機能**  
   - ユーザが設定した入力パラメータ (LOD, 種別) に基づいて、都市設備モデルを生成し配置します。  
   - CityGML (PLATEAU v4) 形式で出力されます。

8. **可視化機能**  
   - 生成した3D都市モデルはツール上で可視化されます。

## 5. 利用技術

| ID | 名称 | 内容 |
| --- | --- | --- |
| 1 | PyCharm Community | Pythonで開発する際に使用するソフトウェア |
| 2 | Visual Studio Code | C++で開発する際に使用するソフトウェア |
| 3 | Feature Manipulation Engine (FME) | 建物GMLファイルをOBJに変換する際に使用するソフトウェア |
| 4 | Computational Geometry Algorithms Library (CGAL) | メッシュを生成、最適化する際に使用するライブラリ |
| 5 | OpenCV | 二次元画像データに関する処理に効果的なライブラリ |
| 6 | Point Cloud Library (PCL) | 三次元点群データに関する処理に効果的なライブラリ |
| 7 | CCCoreLib | 建物OBJファイルを点群にサンプリングする際に使用するライブラリ |
| 8 | PyTorch | 生成的モデルの実行に必要となり、基本的な深層学習モジュールも提供されるライブラリ |
| 9 | torchvision | ツールと方法を提供し、画像の読み込み、前処理、モデル訓練、評価などのタスクを簡素化するライブラリ |
| 10 | cudatoolkit | GPU高速計算をサポートし、CUDAプログラミングを行い、複数のGPUでの並列アルゴリズムとデータ構造を実現するためのライブラリ |
| 11 | conda-forge | Conda環境において、バージョン管理、環境隔離、クロスプラットフォーム互換性、統合開発環境を実現するライブラリ |
| 12 | yacs | コンピュータビジョンプロジェクトにおいて、設定ファイルを定義し管理するためのライブラリ |
| 13 | pyyaml | YAML形式のデータを読み込み、修正し、書き込むために使用されるライブラリ |
| 14 | scipy | numpyに基づくオープンソースの科学計算ライブラリで、科学、技術、工学分野に多くの数学アルゴリズムを提供している。例として、線形代数、積分と微分方程式、信号処理などが含まれる |
| 15 | numpy | 大量の次元配列と行列演算をサポートするために使用される |
| 16 | openmim | OpenMMLab コミュニティによって開発されたコマンドラインツール、機械学習モデルやアルゴリズムライブラリの管理と使用プロセスを簡素化することを目的としている |
| 17 | mmcv-full | OpenMMLabプロジェクトを統合するため、コンピュータビジョン研究と深層学習プロジェクトのための一連の基本機能とツールを提供し、CUDA操作をサポートするライブラリ |
| 18 | mmsegmentation | OpenMMLabコミュニティによって開発されたオープンソースのセグメンテーションライブラリ、深層学習による画像分割モデルの訓練と推論フレームワークの提供に特化している |
| 19 | mmdet | OpenMMLabコミュニティによって開発されたオープンソースの目標検出ライブラリで、深層学習による画像分割モデルの訓練と推論フレームワークの提供に特化している |
| 20 | timm | PyTorchに基づく深層学習画像モデルライブラリで、多数の現代の画像認識・分類モデルの実装が含まれており、最新の研究成果を含めて継続的に更新されている |
| 21 | gdal | 多様な空間データ形式を読み書きするために使用されるライブラリ |
| 22 | ogr | GDALのサブセットで、ベクターデータの処理に特化している |
| 23 | pandas | 高性能で使いやすいデータ構造とデータ分析ツールを提供し、DataFrameやSeriesなどをサポートし、CSV、Excel、JSON、HTMLなどのデータの処理が可能なライブラリ |
| 24 | geopandas | pandasに基づく拡張で、地理空間データの処理に特化しているライブラリ |
| 25 | shapely | 平面オブジェクト（Points、Lines、Polygonなど）の処理に使用され、平面オブジェクトの作成、空間分析、トポロジー分析機能を含むライブラリ |
| 26 | argparse | プログラム実行時のオプションとパラメータをユーザーが指定できるようにするPythonの標準ライブラリ |
| 27 | albumentations | 深層学習および機械学習における画像の前処理とデータ拡張のために設計されたライブラリ |
| 28 | pytorch-lightning | PyTorchの複雑さを簡素化することを目指す高度な深層学習フレームワーク |
| 29 | omegaconf | 軽量な設定ライブラリ、YAMLやJSONなどの設定ファイルを扱い、強力なマージ、補間、および型チェック機能を提供し、設定管理を簡単かつ柔軟にする |
| 30 | test-tube | 機械学習の実験結果を追跡、整理、分析するためのライブラリ、ハイパーパラメータの最適化と実験のバージョン管理をサポートする |
| 31 | einops | テンソル操作とリシェイプをより直感的で柔軟に行うためのPythonライブラリ。多次元データの再配置、次元変換、スケーリングを処理するための簡潔な表現方法を提供する |
| 32 | transformers | オープンソースの自然言語処理（NLP）ライブラリ。BERT、GPT、RoBERTaなどの多数の事前訓練済みモデルの実装を提供し、テキスト分類、生成、翻訳などの多様なNLPタスクに使用され、迅速なデプロイと使いやすいAPIをサポートする |
| 33 | kornia | PyTorchに基づくオープンソースのコンピュータビジョンライブラリ。一連の微分可能な視覚変換関数を提供し、画像処理、強化、特徴抽出などの操作を実現し、GPU加速と自動微分をサポートする |
| 34 | open_clip_torch | PyTorchに基づくオープンソースライブラリ。OpenAI CLIPに似た機能を提供し、自然言語のプロンプトを通じて画像を検索・理解できるようにすることを目的としており、多様な事前訓練モデルとカスタマイズ可能な訓練プロセスをサポートする |
| 35 | torchmetrics | PyTorchに基づく機械学習の指標ライブラリ。モデル評価用の標準指標（正確性、精度、再現率など）を一連提供し、モデル性能評価プロセスを簡素化し統一することを目的としている |
| 36 | addict | Pythonのdictを拡張したライブラリ。属性アクセスを通じて動的にネストされたdictを作成およびアクセスできる使いやすいインターフェースを提供し、dict操作の複雑さを簡素化する |
| 37 | yapf | Pythonコードフォーマットツール。PEP 8スタイルガイドに準拠するようにPythonコードを自動的に再フォーマットし、コードの可読性と一貫性を向上させることを目的とする |
| 38 | trimesh | 三次元メッシュの読み込み、処理、表示、分析を行うためのライブラリ。多様なファイル形式に対応し、三次元幾何データを扱うためのシンプルなインターフェースを提供する |
| 39 | random | 擬似乱数を生成するためのライブラリ。整数、浮動小数点数、シーケンスからの要素の選択、ランダムな文字の生成など、さまざまな乱数生成器を提供する |
| 40 | lxml | XMLおよびHTMLドキュメントを解析するために使用されるライブラリ。XMLおよびHTMLコンテンツに迅速にアクセス、修正、作成するためのシンプルで使いやすいAPIを提供する |
| 41 | earcut | 軽量な多角形三角形分割ツール。複雑な多角形を三角形メッシュに変換するために使用され、グラフィックレンダリングや地理情報システム（GIS）データ処理によく使用される |
| 42 | math | 一連の数学関数と定数を提供し、浮動小数点数の数学演算を実行するために使用されるライブラリ。これには、三角関数、対数関数、指数関数などが含まれる |
| 43 | detectron2 | 画像認識や物体検出モデルの構築に使用するライブラリ |
| 44 | onnx | 深層学習モデルの相互運用性を実現するために使用するオープンフォーマット |
| 45 | onnxruntime | ONNX形式の深層学習モデルの高速推論に使用するランタイム |
| 46 | xgboost | 勾配ブースティングを用いた機械学習モデルの構築に使用するライブラリ |
| 47 | transformers | 自然言語処理におけるTransformerモデルの活用に使用するライブラリ |
| 48 | classifier_free_guidance_pytorch | 生成モデルのガイダンスにおいてクラス分類を使用しない手法を実装するためのPyTorchライブラリ |
| 49 | open3d | 3次元データの処理や可視化に使用するライブラリ |
| 50 | sentencepiece | 自然言語処理におけるサブワード単位のトークン化を実現するライブラリ |
| 51 | optimum | Transformerモデルなどの機械学習モデルの推論最適化に使用するライブラリ |
| 52 | triangle | 2次元メッシュ生成および最適な三角分割を実現するために使用するソフトウェア |


## 6. 動作環境

| 項目   | 最小動作環境     | 推奨動作環境      |
| ------ | ---------------- | ----------------- |
| OS     | Ubuntu 20.08     | 同左              |
| GPU    | メモリ16GB以上   | NVIDIA A100推奨   |
| Python | Anaconda       | 同左              |
| CUDA   | CUDA>=11.3     | CUDA==12.4       |


## 7. 本リポジトリのフォルダ構成

| フォルダ名                          | 詳細                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| bg_extract                         | 衛星画像から植生・道路自動抽出機能                            |
| Building_Generation_Opening        | 街路画像から建物開口部と窓口位置情報推定及びメッシュ単位LOD3建物モデル生成機能 |
| data_src                           | Plateauテンプレートデータ                                    |
| Para_calc                          | 建物高さを推定する機能                                        |
| Roof_classification_inference      | 建物フォトプリント自動抽出及び屋根タイプ自動判別機能            |
| res_example                        | 結果図例                                                     |
| util                               | データ中間処理で使うツール                                    |

## 8. ライセンス

- ソースコード及び関連ドキュメントの著作権は国土交通省に帰属します。
- 本ドキュメントは Project PLATEAU のサイトポリシー（CCBY4.0 及び政府標準利用規約2.0）に従い提供されています。

## 9. 注意事項

- 本リポジトリは参考資料として提供しているものです。動作保証は行っていません。
- 本リポジトリについては予告なく変更又は削除をする可能性があります。
- 本リポジトリの利用により生じた損失及び損害等について、国土交通省はいかなる責任も負わないものとします。

## 10. 参考資料

- PLATEAU Webサイトの Use Case ページ「3D都市モデル生成シミュレータ」: [http://gen3d.sekilab.global/](https://www.mlit.go.jp/plateau/use-case/dt23-06/)
