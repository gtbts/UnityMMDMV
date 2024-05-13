# UnityでMMDモデルを使ってMVを作成する時の忘備録 Blender編

## \-- やりたい事

興味があったSynthesizer Vという歌声合成のソフトを購入して曲は作ってみたけど、音だけだとSNSとかにUPしづらかったり動画サイトにUPするのも静止画だと寂しいし、もう少し簡単にできないかな〜と思ってこれも興味があったUnityを使ってMV的な物が作れないかと思って試行錯誤したベーシックな手順をまとめてみます。

## \-- 手順

手順としては
- **blenderでMMDのモデルを読み込みアニメーションやポーズをつける -> Unityで読み込みUnityで扱えるよう**MMD4Mecanim**変換する -> uLipSyncやMMD4MFaceで口パクや表情をコントロールする**

です。
想定してるのはMMDも3Dソフトも触ったことなかったくらいのなんもわからん自分みたいな人なので、ちょっと冗長な感じでまとめておきます。


## 1. blenderとMMD Toolsの導入
まず3D制作ソフトの[Blender](https://www.blender.org/)をインストールします。 2024年5月時点での最新版は4.1なのですが、後述するMMD Toolsが現時点では対応していないため バージョン3.6.11 https://www.blender.org/download/lts/3-20
をダウンロードしてインストールしてください。

インストールしたらとりあえず起動します。こんな画面が出ると思います。
<iframe
    src="https://drive.google.com/viewer?srcid=1--VBNGJuZIwy9RgtNlIUQn8hGLviXWSV&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:960px; height:540px;"
    frameborder="0">
</iframe>
<br>
<br>

次に[MMD tools](https://mmd-blender.fandom.com/ja/wiki/MMD_Tools) を導入します。MMD ToolsはBlenderでMMDの各種モデルやモーションデータをやり取りするアドオンです。

まずMMD Toolsの[GitHub Release page](https://github.com/UuuNyaa/blender_mmd_tools/releases)
からRelease v2.10.2の **mmd_tools-v2.10.2.zip**をダウンロードします。最新のバージョンはBlender4x用でまだ実験リリースなので使えません。

ダウンロードしたら解凍せず**Zip**ファイルのままで大丈夫です。メニューの**編集** > **プリファレンス**を開き**アドオン**から**インストール**を選び先ほどダウンロードしたMMD Toolsの**Zip**ファイルを選択してインストールします。
<br>
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=1--VYTeNuIXdlyStkiTKgCD7SO9OxAPh4&usp&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:778px; height:604px;"
    frameborder="0">
</iframe>
<br>
<br>

ここで**オブジェクト:mmd_tools**の**チェックボックスをチェック**したらBlenderを再起動してください。

再起動したらMMD Toolsのインストールは完了です。

次にMMDモデルを読み込んでいきます。まず右上のシーンコレクションにCamera Light Cubeの3つのオブジェクトがありますがこれはとりあえず使わないし邪魔なので右クリックで削除して大丈夫です。
<br>
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=1DB0euBUzp-k2KvqdOPF7y-iggjuQypvs&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:440px; height:422px;"
    frameborder="0">
</iframe>
<br>
<br>



もう一つ地味に重要な点なのですが、メニューの**ファイル** > **外部データ**にある**リソースの自動パック**にチェックを入れておいてください
<br>
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=1--H6LZHcpcVNCShutj0NLV_mQiFDqD-r&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:761px; height:574px;"
    frameborder="0">
</iframe>
<br>
<br>

このリソースの自動パックは3Dモデルには**テクスチャ**といって3Dモデルの表面に貼り付ける画像があるのですが、Blenderの初期設定ではテクスチャのような外部ファイルは一緒に保存されません。なのでBlenderファイルを他のPCで編集したり読み込んだファイルの場所を移動した時にテクスチャが見つからずピンク色の物体になったりするのを防ぐためこの**リソースの自動パックをチェック**しておきます。


次に[tokyo6公式が配布している夏色花梨のMMDモデル](https://note.com/tokyo6/n/n10fdd7d3e146)をダウンロードします。後でBlenderで読み込むのでダウンロードしたら適当なところに解凍してください。

これでMMDモデルを読み込む準備ができました。画面はこのようになにもオブジェクトがない状態です。
<iframe
    src="https://drive.google.com/viewer?srcid=1--8EWKoEck1uRl3iuLlPcxqBlV3PzMmR&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:960px; height:540px;"
    frameborder="0">
</iframe>

<br>
<br>

メニューの**ファイル** > **インポート** > **MikuMikuDance Model(.pmd, .pmx)** を選び、先ほどダウンロードして解凍した夏色花梨3Dモデルのフォルダに入っている**夏色花梨.pmx**を選択し読み込みます。
<iframe
    src="https://drive.google.com/viewer?srcid=1-9g4HkMLZPIDHIfcyJ4VmYarxGh6xpD3&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:960px; height:540px;"
    frameborder="0">
</iframe>
<br>
<br>


読み込んだものを
*  **マウスのホイールでズーム**
*   **マウスの中ボタンを押しながらドラッグで視点の回転**
*  **Shiftキーを押しながらマウスのホイールを動かすと視点の移動**

を使って夏色花梨3Dモデルの正面に視点を移動します。
<br>
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=1-KTZmsjSwMaHX7mbo7_nmAnJiN65y93d&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:960px; height:540px;"
    frameborder="0">
</iframe>
<br>
<br>

でも、せっかくの3Dモデルが灰色のままです。これを変更するには画面右上の4つ円形のアイコンが並んでいる**3Dビューのシェーディング**を下記の画像のように右から2番目の円形アイコンの**マテリアルプレビュー**を選択します。
<iframe
    src="https://drive.google.com/viewer?srcid=1-LfLPk1dadCjY6SWtClvRELeWo3XOlO4&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:253px; height30px;"
    frameborder="0">
</iframe>
<br>
<br>
するとモデルにテクスチャが貼られて色がついた状態で表示されます。
<br>
<br>


<iframe
    src="https://drive.google.com/viewer?srcid=1-NfL39I_hFR6JcoVTqDpq-MDCg6CbMnR&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:960px; height:540px;"
    frameborder="0">
</iframe>
<br>
<br>

ここで一旦ファイルを保存しておきます。ファイル名はなんでもいいのですが後でUnityにモデルを読み込んだりする時にファイル名がデフォルトで選択されるのでとりあえず**KarinMMD**としておきます。


先ほどインストールしたMMD Toolsは画面右上の十字の座標軸の右側に小さい **<** が出てるので
<br>
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=1-T8BuyOvbhwob-dBoIqSI_DnSNdecRfu&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:658px; height:525px;"
    frameborder="0">
</iframe>
<br>
<br>


ドラッグするとこのように**MMDタブ**でMMD Toolsが表示されます
<br>
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=1-YLo3kU3ql9_OfzbSMqrBqfB9fZ_QDRR&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:960px; height:540px;"
    frameborder="0">
</iframe>
<br>
<br>

ここでMMDモデルのボーンと呼ばれる骨組みのような構造体の表示形式を変えます。この作業は必要ないといえばないのですが見やすくなるので。

画面右上の**シーンコレクション**から**夏色花梨_arm**を選択します。その状態で下の人形のアイコンの**データ**タブを選択し**ビューポート表示**を選ぶと表示方法が**八面体**になっていると思います。
<iframe
    src="https://drive.google.com/viewer?srcid=1-cmWm_qPgThQZoloxlinGiHOVBHtArTL&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:447px; height:832px;"
    frameborder="0">
</iframe>
<br>
<br>

これを**ワイヤーフレーム**に変更します。するとボーンの表示が線形になりスッキリと見やすくなりました。
<br>
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=1-eqZ0NhtvziZqkk3QC69GbEyx2H0Jr2F&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:960px; height:540px;"
    frameborder="0">
</iframe>

<br>
<br>


次にMMDモデルにポーズをつけたりアニメーションをつける作業に移ります。
画面上部のタブを**アニメーション**に切り替え**オブジェクトの対話モード**を**ポーズモード**に切り替えます。

<iframe
    src="https://drive.google.com/viewer?srcid=1-m1bDZrSMEbzNz4BtbrWkIEC3oGLIIWN&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:504px; height:176px;"
    frameborder="0">
</iframe>
<br>
<br>

次に画面左下の**ドープシート**を**アクション**に切り替えます。
<br>
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=1-oaYo34-Ad4MlOkOoZZ3M_-v-Rh1g1ey&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:625px; height:426px;"
    frameborder="0">
</iframe>
<br>
<br>

ここで左下の**再生**という箇所をクリックし**シンク**を**毎フレーム再生**から**コマ落とし**に変えておきます。これは必要ないといえばそうなのですがアニメーションのプレビューが軽くなります。
<br>
<br>

<iframe
    src="https://drive.google.com/viewer?srcid=100j-HDMCc_Oz2DxkYng9pgJ_jtAy04n0&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:270px; height:449px;"
    frameborder="0">
</iframe>
<br>
<br>

画面下中央の**フレーム**の**新規**を押し、アニメーションの名前をつけるのですがとりあえず今回は適当な右手を挙げるだけのアニメーションを作るので**RiseHand**にしておきます。

<iframe
    src="https://drive.google.com/viewer?srcid=1-rwXcHb_Uk_iVNFZcSNI6sjzGLbZhye0&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:306px; height:101px;"
    frameborder="0">
</iframe>
<br>
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=1-sHdXCEKUm3WjU5S5tMCBCWDRDKmysEH&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:236px; height:55px;"
    frameborder="0">
</iframe>
<br>
<br>

次に画面右上のシーンコレクションから**夏色花梨_arm** > **アニメーション**の中の先ほど作成した**RideHand**を右クリックし**アセットとしてマーク**をチェックしておきます。
これはあんま良く分かってないのですが色々再利用など便利だそうなので、新しいアニメーションを作る時はこの**アセットとしてマーク**をチェックするようにしておきます。
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=1-sdeGB16N4-cTL_dSHYo8Savx2pUABap&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:331px; height:355px;"
    frameborder="0">
</iframe>
<br>
<br>

では、早速アニメーションというかとりあえず確認するためだけなので単純なポーズですが、**画面下のフレームが1**なのを確認したら花梨MMDモデルの**右上腕**のボーンを選択しキーボードの**Rキー**を一度押しマウスでちょうど上下させて腕を下げたポーズにします。
<br>
<br>

<iframe
    src="https://drive.google.com/viewer?srcid=1-vXHqImH27AShcUBRGg_D9ziGZLnAJUs&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:217px; height:397px;"
    frameborder="0">
</iframe>

<br>
<br>

同じように**左上腕**のボーンを選択し**Rキー**を一度押してマウスで下にさげてちょうど両手を下げたポーズを作ります。
<br>
<br>

<iframe
    src="https://drive.google.com/viewer?srcid=1-yQG9ZWRNa162BAb6FMtz68qlr7EJQAg&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:163px; height:400px;"
    frameborder="0">
</iframe>
<br>
<br>

Blenderのポーズをつけるときのショートカットは
*  G が移動 (Alt-G)で移動をリセット
*  R が回転(押す回数で回転の向きが変わります) (Alt-R)で回転をリセット
*  S がスケール (Alt-S)で移動をリセット

ですが主にGの移動とRの回転をよく使います。
<br>
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=1001lp6J3u3cCkNhwae87CLVxy7-bTRvt&usp&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:387px; height:399px;"
    frameborder="0">
</iframe>
<br>
<br>

ここで1フレーム目に現在のポーズを記録します。**Aキー**を押しすべてボーンが選択されている状態で**Iキー**を押し、出てきたメニューから**位置・回転・スケール**を選びます。すると1フレーム目に各ボーンの位置などが記録されました。
<br>
<br>

<iframe
    src="https://drive.google.com/viewer?srcid=1003edosijpZ7wrTY9DiDWApHRH6WPMTw&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:274px; height:214px;"
    frameborder="0">
</iframe>
<br>
<br>

次に腕を上げたポーズを20フレームに記録します。20フレーム目にカーソルを移動して**右上腕**のボーンを選択し**Rキー**を**2回**押して右腕を挙げます。挙げたら同じように**Aキー**を押しすべてボーンが選択されている状態で**Iキー**を押し、出てきたメニューから**位置・回転・スケール**を選びます。すると20フレーム目に今の手を挙げたポーズが記録されます。
<br>
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=102GxJEHhkR3VpHVNSTpi3VXh9MNvqap5&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:960px; height:540px;"
    frameborder="0">
</iframe>

<br>

ここで画面下の再生ボタンを押すと1フレーム目と2フレーム目のポーズの間が補完され雑ですが簡単なアニメーションをつけることが出来ました。
<br>
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=102ybznW0gQIXUvBNxMNNDKUFVQ3iwHp8&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:145px; height:396px;"
    frameborder="0">
</iframe>

<br>
<br>

ここで画面右下の**手動フレーム範囲**にチェックを付け開始と終了をそれぞれ1と20に設定しておきます。もしループさせたい場合は**ループアニメーション**にチェックを入れます。
<br>
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=10KGNZEcxnjURn12kPguK1L2d0qN49UlU&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:662px; height:280px;"
    frameborder="0">
</iframe>

次にどこか適当な場所にとりあえず**KarinMMD**と名前を付けた(名前は特になんでもいいです。)フォルダを作り、その中に今回作ったアニメーションやモデルのデータを入れてUnityにインポートする準備をします。

メニューの**ファイル** > **エクスポート** > **FBX(.fbx)** を選び、下記画像を参考にして設定します。

**パスモード**は**コピー**その右のアイコンは箱に書類が入っているようなアイコンの状態にします。**内容**のオブジェクトは**アーマチュア**と**メッシュ**のみを選択します。この設定はアニメーションを追加したりする度に使うのでこの設定をオペレータープリセットでプリセットとして保存しておくと良いと思います。


設定したら先ほど作った**KarinMMD**というフォルダにファイル名をこれも**KarinMMD**(ファイル名は拡張子こみでKarinMMD.fbx)としてFBXファイルをエクスポートします。このファイル名は次にエクスポートするPMXファイルと共通にしておきます。

<iframe
    src="https://drive.google.com/viewer?srcid=109uZlGZtJfC8RHtx-jS-VAcGSpR3fIfe&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:142px; height:451px;"
    frameborder="0">
</iframe>
<br>
<br>


次にメニューの**ファイル** > **エクスポート** > **MikuMikuDance Model(.pmd, .pmx)** を選び、テクスチャをコピーを選んでおきます。これもファイル名は**KarinMMD**(ファイル名は拡張子こみでKarinMMD.pmx)として同じく**KarinMMD**フォルダにエクスポートしておきます。

<iframe
    src="https://drive.google.com/viewer?srcid=10Y0wxVhDB16ZYRd91lEig17H4f249kR4&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:250px; height:355px;"
    frameborder="0">
</iframe>
<br>
<br>

あとは先ほど作った**RiseHand**アニメーションをエクスポートします。

MMD Toolsのメニューから**モーション**の**エクスポート**を押し
<iframe
    src="https://drive.google.com/viewer?srcid=10IIDrhscSE22E7x5UB8wnvqHx-1GRS0i&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:540px; height:646px;"
    frameborder="0">
</iframe>
<br>
<br>

**フレーム範囲を使用**のチェックボックスをチェックして、ファイル名は**RiseHand**(拡張子こみでRiseHand.vmd)これも同じ**MMDKarin**フォルダに保存します。
<iframe
    src="https://drive.google.com/viewer?srcid=10UmOPTQmOhhmsjkZLom_7LfUOIH1DEY5&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:244px; height:120px;"
    frameborder="0">
</iframe>
<br>
<br>

これでBlenderでの下準備は終わりです。アニメーションを追加する時などはこのファイルを使うので保存を忘れないようにしておきます。

次はUnity編です。
