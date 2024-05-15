# UnityでMMDモデルを使ってMVを作成する時の忘備録 Unity編

## 1. Unityと各種ツールの導入
[Unity](https://unity.com/ja)をまずインストールしなきゃいけないのですが、Blenderとは違い登録などが必要なので具体的なインストール方法はさすがに冗長なんでここには書きません。あと、Unityは有料プランなどもあるのですが無料版のUnity Personalで大丈夫です。とりあえず登録を済ませてUnity Hubが立ち上がるようになったらInstall EditorからLTSのバージョンをインストールしてください。ちなみにこれを書いてる時に使用しているエディタのバージョンは**Unity*(20233.17f1)LTS**でした。



エディタをインストールしたら次に**Unity Hub**の右上にある**New Project**を選び3D(**Built-In Render Pipeline**)を選択してください。Project Nameは好きなものでかまいません。
<br>
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=1hpbThQ-E80lfxt4rEJBF9QrDmRurZF7l&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:404px; height:253px;"
    frameborder="0">
</iframe>
<br>
<br>


 **Unity Editor**が起動したら次にNoraさんが開発された[MMD4Mecanim (Beta)](https://stereoarts.jp/) を導入します。これはMMDのデータをUnityの形式に変換してくれる大変便利なツールです。ダウンロードした**MMD4Mecanim_Beta_20201105.zip**を解凍したら中に入っている**MMD4Mecanim.unitypackage**を開くとエディタにこのようなダイアログが表示されると思うので**import**または**Yes**を選択しインストールしてください。
<br>
<TABLE BORDER="2" WIDTH="100%" CELLSPACING="0" CELLPADDING="0">
<TR>
<TD>
<iframe
    src="https://drive.google.com/viewer?srcid=1hs0waVOTFx7wpuNSFoMHUndYEp-LxVVP&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:116px; height:191px;"
    frameborder="0">
</iframe>
</TD>
<TD>
<iframe
    src="https://drive.google.com/viewer?srcid=1hr4u-itlCtrXgl2HD83RsZ62eElc_tpO&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:116px; height:191px;"
    frameborder="0">
</iframe>
</TABLE>
<br>
<br>

時々インストールされたものがうまく認識されなかったりするのでここでUnityのエディタを再起動しておくといいかもしれません。

次に左下のAssetsの中に**Blender**で作成していた**KarinMMD**フォルダをドラッグ&ドロップで入れておきます。フォルダの中身は下記の画像といっしょになっていれば間違ってない思います。もし足りないファイルがあるとしたら**Blenderのエクスポート**で手順の間違いがあると思うのでもう一度確かめて見てください。


<iframe
    src="https://drive.google.com/viewer?srcid=1hqEBNZ-2h5cGpsofzOyWtf_vpxTfwr-R&usp&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:960px; height:589px;"
    frameborder="0">
</iframe>

<br>
<br>

次に先ほどドラッグ&ドロップで入れた**KarinMMD**フォルダ内のKarinMMD.pmxを選択すると画面右のインスペクタに規約の同意を求められるのでチェックし同意します。
<br>
<br>

 <iframe
    src="https://drive.google.com/viewer?srcid=1ht6m1tgFWVXLzGM5ISUsgJsEn_0j1WiZ&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:420px; height:234px;"
    frameborder="0">
</iframe>
<br>
<br>

同意したら次の画面のように**VMD**欄の**None**(**Object**)となっている右側の白い円をクリックし、虫眼鏡マークのサーチ欄にriseと入力し絞られた結果から**RiseHand.vmd**(**KairnMMD**フォルダ内にあるBlenderでエクスポートしたファイル)を指定します。

ここでVMDファイルを指定することでMMDのpmxファイルをUnityが扱えるfbxファイルに変換する時にMMD用のアニメーションデータも一緒に変換されるので、新しいアニメーションを追加する場合などはこのVMDファイルをその都度指定する作業が必要です。指定したら右下の**Process**を押してください。変換が始まります。
<br>
<br>

<iframe
    src="https://drive.google.com/viewer?srcid=1htVklxGLzCymRxVikO49x43AXkZ0V7g7&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:616px; height:611px;"
    frameborder="0">
</iframe>

<br>
<br>

無事変換が終わったら**KarinMMD**フォルダ内の**KarinMMD.fbx**(右に矢印が出ているアイコン)を画面左側の**Hierarchy**タブ内のSampleSceneにドラッグ&ドッロップして配置してください。

無事に変換が成功していれば画面に夏色花梨3Dモデルが表示されるので拡大して確認してみます。
<br>
<br>

<iframe
    src="https://drive.google.com/viewer?srcid=1huQpGRlBhyMqeSbT3eH1fixVXUpUsJTD&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:960px; height:589px;"
    frameborder="0">
</iframe>
<br>
<br>


### 〜ここでもしテクスチャが自動で貼られないで真っ白だった場合〜
この解説で使っているtokyo6公式で配布している夏色花梨のMMD3Dモデルは確認したところ大丈夫なのですが、他のMMDモデルだとこの時点で画面上の3Dモデルが表示はされているんだけどテクスチャがなくて白い物体だった場合、手動でテクスチャを貼り付けるちょっと面倒な手順が必要です。

Unityエディタ画面下中央の配置した3Dモデルが入っていたフォルダには**Material**というフォルダが作られていると思うのですが、その中に入ってるマテリアルに手動で一つずつテクスチャを貼るわりと面倒な作業が必要になってきます。
どのマテリアルにどのテクスチャをつけるのかは[極北Pさんが開発されているPMX Editor](https://kkhk22.seesaa.net/category/14045227-1.html)で**材質タブ**から確認するか**Blender**で確認しながらの一つづつテクスチャを指定していく作業になります。

<br>
<br>
<iframe
src="https://drive.google.com/viewer?srcid=13gJ6j1Kj5zNyxtUGr-NrGmUb9hX8Vjue&usp=drive_fs&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:648px; height:397px;"
    frameborder="0">
</iframe>
<br>
<br>
<iframe
src="https://drive.google.com/viewer?srcid=13_ojD4fQn86Dr8xkAntkORZCnGcR24N1&usp=drive_fs&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:220px; height:680px;"
    frameborder="0">
</iframe>

<br>
<br>

テクスチャを入れたいマテリアルを選んで該当するテクスチャをアタッチしていく

<iframe
    src="https://drive.google.com/viewer?srcid=13h0I6Dwea_kavSJSbjZJwYfiJw2UBLNH&usp=drive_fs&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:216px; height:671px;"
    frameborder="0">
</iframe>
<br>
<br>

このテクスチャの割当はモデルによっても変わるのとシェーダーというどう3Dを表現するかの選択も絡んで大変ややこしいので自動変換されない場合はモデルに合わせて試行錯誤するしかないみたいです。


では、無事にテクスチャが貼られたと仮定して次に見やすいようにカメラ位置を移動します。まず**SampleScene**内の**Main Camera**をクリックして右の**Inspector**から**Position**の**Z**を-1.2に設定。次に同じく**SampleScene**内の**KarinMMD**を選択して右の**Inspector**から**Rotation**の**Y**を-180に設定します。
この-180度の回転はBlenderとUnityでそれぞれ座標系が違うためです。

設定したら画面上部のタブを**Scene**から**Game**に切り替えてください。すると画面中央に夏色花梨3Dモデルが表示されると思います。
<br>

<iframe
    src="https://drive.google.com/viewer?srcid=1hu_23tcsxlmPh99NOIAts12bDVMu99_X&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:960px; height:589px;"
    frameborder="0">
</iframe>
<br>
<br>



次にインポートしたアニメーションを確認します。場所はどこでもいいのですがとりあえず**KarinMMD**フォルダ内で右クリックをして**Create > Animator Controller**を作成します。名前は適当でいいですがわかりやすく**KarinAnimation**などの名前にしておくと良いと思います。


<iframe
    src="https://drive.google.com/viewer?srcid=1hvBHC35SgUtgjROg7z50lP2FQswvsvmt&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:297px; height:521px;"
    frameborder="0">
</iframe>

<br>
<br>

作成した**Animator Controller**をダブルクリックで開いたら**KarinMMD**フォルダの中にある右に矢印が出ているアイコンの**KarinMMD.fbx**の矢印をクリックし中身を展開します。その中の**RiseHand**がアニメーションコントロール用のファイルなので先ほど開いた**Animator Controller**にドラッグ&ドロップすると自動的に**Entry**と線でつながると思います。

<iframe
    src="https://drive.google.com/viewer?srcid=1hvJ5qXNk7y-2nJ7SbajFTVLDD20w2KFq&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:960px; height:589px;"
    frameborder="0">
</iframe>
<br>
<br>



次に**SampleScene**内の**KarinMMD**を選択して右の**Inspector**から**Add Component**で**Animator**を追加します。
自動的に**MMD 4 Mecanim Model**(**Script**)も追加されます。

<br>
<br>

<iframe
    src="https://drive.google.com/viewer?srcid=1hvSj-MiVljn2_k3J__GOfN4oofFw0fOV&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:960px; height:589px;"
    frameborder="0">
</iframe>
<br>
<br>

追加した**Animator**の**Controller**欄から先ほど**RiseHand**を入れた**Animator Controller**の**KarinAnimation**を選択してください。

<br>

<iframe
    src="https://drive.google.com/viewer?srcid=1hys2F-TU7NjGkUmA2Pzb7AmZBOcPMsvX&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:960px; height:589px;"
    frameborder="0">
</iframe>

<br>
これでエディター上部の再生ボタンを押してBlenderで作った**RiseHand**のアニメーションが再現出来たらMMDモデルのUnityへのインポートはほぼ完了です。

<br>

<iframe
    src="https://drive.google.com/viewer?srcid=12LYQwMnT4BBy7rqkQOZRPWnP8rBR-tI_&usp=drive_fs&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:300px; height:364px;"
    frameborder="0">
</iframe>

Unityのアニメーションの遷移はこの**Animator Controller**で各種アニメーションのパターンを用意して線でつなげたりスクリプトから制御するようになっています。



## #リップシンク(口パク)させる

次に[凹みさん](https://tips.hecomi.com/entry/2023/04/28/230437)の[uLipSync](https://github.com/hecomi/uLipSync)という3Dモデルにリップシンク(口パク)をつけるプラグインを導入します。

[uLipSyncのReleaseページ](https://github.com/hecomi/uLipSync/releases)から2024年5月時点での最新版**v3.1.1** **uLipSync-v3.1.1-with-samples.unitypackage**をダウンロードして開いてください。
**import**したら下の方で赤い文字でエラーが表示されていると思いますがこれは**Burst**というパッケージがインストールされていないためです。

メニューの**Window** > **Package Manager**を開き左上の**Packages: In Project**をクリックして**Unity Registry**に変更します。次に右上の虫眼鏡マークのサーチ欄に**Burst**といれ絞られた結果からBurstをインストールします。これでuLipSync導入の下準備が出来ました。
<br>
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=12J7u7iRSHtkmu8r-X8RLRRCn5V3qjjJg&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:960px; height:589px;"
    frameborder="0">
</iframe>
<br>
<br>

次にエディタ左側の**Hierarchy**タブの**Sample Scene**から**KarinMMD**を選択しエディタ右側の**Inspector**から**Add Component**を押しサーチ欄に**ulipsync**と入力、絞られた結果の中の**U Lip Sync(uLipSync)**を選択します。

もう一度**Add Component**を押して次は**U Lip Sync Blend Shape(uLipSync)**を選択しアタッチします。

最後にまた**Add Component**を押して次はサーチ欄に**audio**と入力**Audio Source**を選択しアタッチします。
<br>
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=136vtTktGxwBp2XAF9KJnjjAe4yAOIAsu&usp=drive_fs&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:394px; height:951px;"
    frameborder="0">
</iframe>
<br>
<br>

このように3つ**Audio Source**, **u Lip Sync**, **U Lip Sync Blend Shape** がアタッチされています。表示されている順番は特に関係ありません。
<br>


このアタッチしたうちの一つ**Audio Source**はオーディオファイルのプレーヤーです。この**KarinMMD**にアタッチしてある**Audio Source**に**歌**や**トーク**の声のみが入ったオーディオファイルを読み込ませて、それをuLipSyncで解析して3Dモデルの表情を操作することで自動的にリップシンク(口パク)するという仕組みになっています。

口パク確認用として[Synthesizer Vで夏色花梨の「あいうえお」を出力したもの](https://drive.google.com/open?id=12VwDdQtt7YEva-Od1t0J4TBkqMPSA_fu&usp=drive_fs)を置いておきます。
これをダウンロードしたら**KarinMMD**フォルダにでもドラッグ&ドロップしてください。

先ほど**uLipSync**といっしょにアタッチした**AudioSource**の**AudioClip**欄から先ほどダウンロードした「あいうえお」の**karin_voice_MixDown.wav**を指定します。
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=138uhnB_gQ9PhUNsvO9uTJoBT0ixY5-Sb&usp=drive_fs&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:311px; height:160px;"
    frameborder="0">
</iframe>
<br>
<br>
次に**U Lip Sync Blend Shape**の設定を下の画像を画像を参考にしながら設定してください。具体的な変更点としては**Skinned Mesh Renderer**がデフォルトでは**U_Char_0**なのを**U_Char_1**に変更します。

これは3Dモデルもいくつかのパーツに分かれていたりして統一されてはいないのですが**口**を含んだパーツを指定してあげていると考えると良いと思います。なので違うモデルだと**U_Char_XX**のXXは変わると思ってください。

もう一つの変更点は**Blend Shapes**の**Phoneme - BlendShape Table**です。

*Phoneme(音素)*と**MMD**の表情などをコントロールする**ブレンドシェイプ**を指定してあげます。
要はuLipSyncが検出したA I U E O -(無音)とMMDの「あいうえお ん(無音)」の口の変化をそれぞれ対応させてる箇所です。

<br>
<iframe
    src="https://drive.google.com/viewer?srcid=13Bv0me_4yFuXvYYjD-MK_azAd-m55C-t&usp=drive_fs&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:394px; height:522px;"
    frameborder="0">
</iframe>
<br>
<br>

次に**U Lip Sync**の設定をします。

**U Lip Sync**の**On Lip Sync Update(LipSyncInfo)の**List is Empty**となっている箇所の右側の＋ボタンを押し、現れた**None** (**Object**)となっている箇所をクリック**Assets**と**Scene**というタブの**Scene**を選択してサーチ欄に**Karin**と入力して絞られた**KarinMMD**を選択します。

<br>
<iframe
    src="https://drive.google.com/viewer?srcid=13DRd9WVG3nC6UjrgeqQ2NLMMSbSCYCsD&usp=drive_fs&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:440px; height:764px;"
    frameborder="0">
</iframe>
<br>
<br>
次に**Runtime Only**の右側**No Function**になっている箇所をクリックし**uLipSyncBlendShape > OnLipSyncUpdate**を選択します。

<br>
<br>


<iframe
    src="https://drive.google.com/viewer?srcid=13I9Un9v2ER9qtssUXpEmRF2mgcAGkf2M&usp=drive_fs&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:428px; height:620px;"
    frameborder="0">
</iframe>
<br>
<br>

もう一箇所**Profile**欄を選択して**uLipSync-Profile-Sample-Female**を選択しておきます。これは音声を解析する時の元データのようなもので、キャリブレーションして自作することも出来るのですがとりあえずサンプルのものを利用します。
<br>
<br>
<iframe
    src="https://drive.google.com/viewer?srcid=13E7UqDnVXqN7PR671xssFAMOrEiV5M_p&usp=drive_fs&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:397px; height:805px;"
    frameborder="0">
</iframe>
<br>
<br>

これで**uLipSync**の設定が終わったので画面上部の再生ボタンを押してみて「あいうえお」とリップシンクしてくれたらOKです。uLipSyncはキャリブレーションといって声の特徴を解析してさらに検出の精度を上げる方法もあるので詳しくは[uLipSync](https://github.com/hecomi/uLipSync)を参考にしてみてください。

<br>
<iframe
    src="https://drive.google.com/viewer?srcid=13EJ49EkLX__dBwl1IEpDFNM1pBf_xAcL&usp=drive_fs&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:225px; height:273px;"
    frameborder="0">
</iframe>
<br>

## #まばたきさせる
これでやりたい事出来た感がある感じですけど、もう一つやっぱりまばたきは生理的なものなのでないとなんか不自然な感じがします。そこで[udasanのMMD4MFace](https://github.com/udasan/unity-mmd4mface)を利用して自動でまばたきさせてみます。
[MMD4MFaceのページ](https://github.com/udasan/unity-mmd4mface)に行き右上にある**Code**というとこをクリックして**Download Zip**でZipファイルをダウンロードしたら解凍して**KarinMMD**フォルダと同じようにUnityエディタのAssetsに解凍したフォルダごとドラッグ&ドロップしてください。

次にエディタ左側の**Hierarchy**タブの**SampeScene**から**KarinMMD**を選択しエディタ右側の**Inspector**欄に先ほどAssetsに入れた**MMD4MFace**のフォルダに入っている**MMD4MFaceController.cs**と**MMD4MFaceBlink.cs**をそれぞれドラッグ&ドロップしてアタッチしてあげます。

アタッチしたら**MMD4M Face Blink(Script)**の**Blink Params**のMorph Nameに**まばたき**と入れてください。これでまばたきの設定は終わりです。
<br>
再生ボタンを押してみると自動的にまばたきするようになってると思います。

<iframe
    src="https://drive.google.com/viewer?srcid=13HXjvkwBgi2VGUxjPcyoLCfFpTDw-E1w&usp=drive_fs&pid=explorer&efh=false&a=v&chrome=false&embedded=true"
    style="width:284px; height:384px;"
    frameborder="0">
</iframe>
<br>


## #これを土台にしたMVの作り方

これで基本的なMMDのモデルの導入とリップシンクが出来ました。

MVを作る時はもう一つ**AudioSource**を用意してそこにボーカル以外の音が入ったトラック(要はカラオケ)で、uLipSyncがアタッチされている**Audio Source**には逆にボーカルのみが入ったトラックをそれぞれDAWで曲の頭から終わりまで同じ長さで書き出してあげて読ませるとUnity内で同時再生されバーチャルカラオケ的な事になります。

それを**Unity**の[**Recorder**](https://docs.unity3d.com/ja/Packages/com.unity.recorder@2.6/manual/index.html)で画面を録画して、それを動画編集ソフトなどで音源をマスタリングしたものに差し替えてあげて歌詞のテキストをつけたりしてMVにするというような方法で作ってます。

Unityはゲームを作成するソフトなのでいろいろなエフェクトだったりもあるし、それを例えば同じように**Audio Source**に読ませたトラックの音量を検出して花火を打ち上げたりとか演出に使う事が出来るので興味がある人はやってみると楽しそうです。


