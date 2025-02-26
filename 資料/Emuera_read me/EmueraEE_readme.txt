﻿タイトル：EmueraEM+EE 最終更新日:2023/06/30
バージョン：1.824+v18+EMv17+EEv37
改変者：Enter
元となったアプリケーション：Emuera1.824+v18（妊）|дﾟ)の中の人、及びMinorShift制作）、WebP-wrapper(JosePineiro制作)、Emuera.EM（EvilMask制作）
連絡先：Twitter/@eraBEMANI Discord/https://discord.gg/p5rb5uK
eraシリーズまとめwikiのページ：https://seesaawiki.jp/eraseries/d/EmueraEM%2bEE%a4%ce%c4%c9%b2%c3%b5%a1%c7%bd
docs：https://evilmask.gitlab.io/emuera.em.doc/

※eramakerの作者様及びMinorShift様、妊の人様はEmueraEEの製作には関与していません。
　当アプリの不具合は上記連絡先にご報告ください

※同梱のEmuera-Anchor-EEは英語圏のeraコミュニティで使用されている「Emuera-Anchor」をEEに対応させたものです
　各UIやエラーメッセージ等が英語になっています。必要に応じて使い分けてください

※使用しているセキュリティソフト次第では危険なファイルとして警告・削除される場合があります
　セキュリティソフトの設定を変更して使用することはできますが、自己責任でお願いします
　virustotal(ファイルの安全性確認サイト)のリンク：https://www.virustotal.com/gui/file/8bbc88d1dfeaab25a9681ddc61e85de935c1a972e2d5ed54e7e41824dfa88471

[v12にてEmuera.EMと機能統合。上記リンクのドキュメント(docs)を参照]
[EMv8+EEv15にてhtml形式のドキュメントを同梱。追加機能などがより詳しく書かれています]

[一部のエラーについて]
System.TypeInitializationException:'MinorShift.Emuera.GameProc.Function.FunctionIdentifier' のタイプ初期化子が例外をスローしました。

上記のエラーはWindows Media Playerがインストールされてないことが原因のひとつと確認されており、インストールすることで直る場合があります

[報告]
EmueraEM+EEのVSCode用拡張機能を作りました。sasami氏のerabasic拡張機能をベースにしています
https://marketplace.visualstudio.com/items?itemName=deletedenter.erabasic-emee

[概要]
Emueraをベースに改造を施したバージョンです。追加された機能は以下の通り

・PLAYSOUND "ファイル名.拡張子"
「sound」フォルダ内にある音声ファイルを1回再生します
v12で10チャンネルに対応。最大10個のファイルを同時再生できる

・STOPSOUND
PLAYSOUNDで再生中の音声ファイルを停止します

・PLAYBGM "ファイル名.拡張子"
「sound」フォルダ内にある音声ファイルをループ再生します

・STOPBGM
PLAYBGMで再生中の音声ファイルを停止します

・EXISTSOUND "ファイル名.拡張子"
「sound」フォルダ内に指定した音声ファイルが存在するか判定します。存在すれば1が、しなければ0がRESULTに入ります

・EXISTSOUND("ファイル名.拡張子")
同名命令の式中関数版

・SETSOUNDVOLUME int
PLAYSOUNDの音量を変更します。引数には0～100を指定できます

・SETBGMVOLUME
PLAYBGMの音量を変更します。引数には0～100を指定できます

Windows Media Playerのライブラリを使っているのでWMPがインストールされてるPCであれば、
WMPで動く音声ファイルは全て動くと思います。

・INPUTMOUSEKEYでボタン使用可能に
命令実行時にRESULT:0=1(マウスクリック時)だった場合にRESULT:5にボタンの数値が入ります
また、数値型と文字列型両方の入力に対応。数値型ならRESULTに、文字列型ならRESULTSに入る。PRINTBUTTONとの併用も可能

・GDRAWTEXT gID, "テキスト", X座標, Y座標
指定したgIDにテキストを描写する 座標は省略可能
GSETBRUSH cARGBと組み合わせることで文字の濃度と色を変更できる cARGBは濃度+文字色の16進数8桁
成功すればRESULT:0に1が、RESULT:1には生成したテキスト画像の幅が、RESULT:2には高さが入る(高さはほぼGSETFONTで指定した値)
v7plusから描画フォーマットをGenericTypographicsに変更 実際のPRINT描画と同じ位置になるように

・GGETFONT gID
指定したIDの、GSETFONTで指定したフォント名を呼び出す

・GGETFONTSIZE gID
指定したIDの、GSETFONTで指定したフォントサイズを呼び出す

・OUTPUTLOGでファイル名と拡張子を指定可能に
OUTPUTLOGに引数指定することでそのファイル名.拡張子で出力できる リテラルはPRINTSとかと同じ
v5fixで親ディレクトリを指定できる脆弱性を修正 子ディレクトリは指定可能

・EXISTFUNCTION("関数名")
名前の通り関数が存在するかの式中関数 通常関数なら1を、式中関数(数値型)なら2を、式中関数(文字列型)なら3を返す
TRYC系でCALL機能を付随させたくない場合にお使いください また、システム関数やシステム組み込み式中関数は0を返す

・GSETFONTでフォントスタイルを指定できるように
第4引数にSETFONTと同じ4ビット数(1=太字 2=斜体 4=打ち消し線 8=下線)指定で装飾を付けられるように 省略可能

・GGETFONT gID
指定したIDの、GSETFONTで指定したフォントスタイルを数値で返す

・GGETTEXTSIZE "テキスト", フォント名, フォントサイズ, フォントスタイル
指定の引数でGDRAWTEXTを行った場合のサイズを取得する 第4引数(フォントスタイル)は省略可能
FONTBOLD相当のスタイルの場合、サイズが微妙に大きくなるため注意

・TRYCALLF 関数名
CALLFのTRY命令 CALLF同様に返り値は破棄されるが、関数が無くてもエラーにならない

・TRYCALLFORMF 関数名
CALLFORMFのTRY命令 CALLFORMF同様に返り値は破棄されるが、関数が無くてもエラーにならない
上記2つをTRYC～CATCH式に使う場合はEXISTFUNCTIONと併用してください

・GDRAWGWITHROTATE コピー先gID, コピー元gID, 回転させる角度(時計回り), X座標, Y座標
コピー元IDのイメージを、指定した角度回転させてコピー先IDに貼り付ける 座標は省略可能で省略すると中心点(X/2,Y/2)になる
角度はマイナスを指定すれば反時計回りになる 360を超過しても問題ない
中心点はコピー元のサイズに準拠しているが、サイズの違うgIDを扱うとズレが生じる 角度に応じてズレの度合いが違う(90°、270°で最大)ので、その際は中心点を変えてあげるとよい

左のように200*100を90°回転させて100*200のgに移す場合、太枠の100,50地点を中心に回転するため右のようにずれる
なので重なってる部分の中心点、つまり50,50地点(・)を中心点に指定すればきれいにハマる 270°回転なら全体の中心点、100,100を指定するとハマる
┏━┯━┓ ―┏━┓
┃・│―┃ ┌╂┐┃
┣━┿━┛ │┃│┃
│―│―― │┗┿┛
└─┘―― └─┘―

・QUIT_AND_RESTART
再起動命令。QUIT同様にWAIT1回相当の入力待ちがある

・FORCE_QUIT
入力待ちせずにQUITする命令

・FORCE_QUIT_AND_RESTART
入力待ちせずにQUIT_AND_RESTARTする命令 入力待ちを挟まず連続実行されるとダイアログボックスで警告が出る

・FORCE_BEGIN システム関数
BEGINの制約を受けずに強制的にBEGINを実行する。フローを意図的に壊すため、予期せぬ不具合が起こる可能性があります

・WebPに対応
がめら氏作の「src1824+v11+webp+Secure」を参考にWebP読み込み機能を追加
あくまで参考で(=完全マージではない ベースバージョンが違うため)、ファイル読み込み処理だけWebP対応にしただけなので元のWebP版には無いエラーが起こる可能性があります
WebPWrapperについては東etoマン氏、M氏が改良を行ったものを使用しています 僭越ながら同梱の「WebP版read me」に文書をまとめさせていただきました 感謝
EMv6+EEv13にてセキュリティ上の観点から別のライブラリに変更しました。同梱のlibwebp.dllをEmueraと同ディレクトリにコピーしてお使いください

・ERHで定義した変数にcsvファイルで名前を付けられるように
ERHで定義した変数名を準拠にファイルを読み込み、既存のcsv変数と同じように配列に名前を付けることができる
CSVフォルダ内で使えるものは従来どおり「変数名.csv」、ERB内で使えるものは「変数名.ERD」ファイルとなる。書式はCSV変数のファイルと同じ。これらが2つ以上存在する場合は起動時にエラー吐いて終了する
ただしABLNAMEやTRAINNAMEに相当する変数は無し。今後命令や式中関数を実装する予定
v23にて多次元配列にも対応。多次元配列に名前を付ける場合、左の次元から@1,@2,@3とファイル名の末尾に付けることで適用可能

・GETMEMORYUSAGE()
現在起動中のEmueraのメモリ使用量を返す（byte）。ワーキングセットの値なのでタスクマネージャーの数値とは差異が生じます

・CLEARMEMORY()
メモリを解放する。解放されたメモリ量（byte）を返す
DELCHARAやセーブデータのロード、RESETDATA等データ削除した際に使うと効果がありますが、それらが行われないタイミングで使用しても特に効果はありません
そこそこ重いため乱用は控えたほうが無難

・ホットキー機能拡張
Anchorからの機能移植。Ctrl+Tでタイトル画面に戻る、Ctrl+Rで再起動、Ctrl+OでERB再読み込み

・VariableSize.csvでCOUNTを使用禁止変数に設定できるように
COUNTを使用禁止変数に設定した場合は起動時にREPEAT行を警告し、実行されるとエラー落ちするように

・キーマクロをUTF-8で保存するように
英語以外の外国語も問題なく使えるようになりました

・DAY、TIME、MONEYにCSVを適用可能に
各「DAY.csv」「TIME.csv」「MONEY.csv」に対応しています。DAYNAME、TIMENAME、MONEYNAMEも実装

・GETTEXTSIZE
実行時点でテキストボックスに入力されている内容を取得する

・SETTEXTBOX
テキストボックスを任意の文字列に置き換える

・INPUTANY
数値、文字列両方の入力に対応したINPUT。数値型が入力されればRESULTに、文字列型が入力されればRESULTSに代入される

・GETNUM拡張
多次元配列ERDに対応するためGETNUMで第三引数に次元を指定できるように。左から1,2,3となる。式中関数VARSETの仕様(0,1,2)とは異なるため注意
また、オプションにて式中関数VARSETの次元指定をERDと同じく1,2,3とするオプションを追加

・ERDNAME 変数名, 要素(, 次元)
TALENTNAMEやCFLAGNAMEのように数字から要素名を逆引きできる。式中関数としても使用可。次元指定は左から1,2,3
上記GETNUMも含め、一次元配列変数で次元指定すると機能しない

・INPUT拡張
EM版の「クリックをEnterキーとみなす」の後に引数を追加
非0を指定すると右クリックでのスキップ中にRESULTもしくはRESULTSにデフォルト値を入れてスキップされる
「クリックをEnterキーとみなす」の引数が0の場合はRESULT:0,RESULTS:0に、非0の場合はRESULT:1,RESULTS:1にデフォルト値が入る

・FLOWINPUT デフォルト値(, 左クリックをEnterキーとみなすか, 右クリックでスキップ可能か)
SHOW_SHOP内などフロー上で行われるINPUTにデフォルト値、クリックをEnterキーとみなすオプション、右クリックでスキップ可能のオプションを設定できる

・MOUSEB
現在マウスオーバー中のボタン内容を取得する。MOUSEX,MOUSEYと同様にAWAITと組み合わせて使う
実行時点でINPUTかINPUTSか確定していないため文字列型として返される点に注意

・SPRITEDISPOSEALL
スプライトをすべて破棄する。引数に0を指定するとERB上で作成したものだけ、非0を指定するとresourceフォルダ内のCSVで定義したものも含めて全部破棄する
返り値はそれぞれ破棄されたスプライト数を返す

・SKIPLOG
引数に非0を渡すと右クリック等でスキップしてる状態にする。0を渡すとスキップ状態を強制解除する

・BINPUT、BINPUTS
実行時点でボタン化されている値のみを受け付けるINPUT(INPUTS)。「ボタン入力のみを受け付ける」ではなく「ボタン化されてる値のみを受け付ける」ため、マウス操作とキーボード操作を両立させつつ、マウス操作では入力し得ない値を弾く
ボタンが一つも無い状態で実行された場合は、デフォルト値が設定されていれば入力待ちをせずにRESULT(S)にデフォルト値を入れる。デフォルト値も無ければゲームが進行不可になるのでエラーになる

・GDRAWLINE gID, fromX, fromY, forX, forY
指定したgIDのfromX,fromY座標からforX,forY座標に線を引く。線の色と太さはGSETPENで指定したものを使用。式中関数としても使える

・GETDISPLAYLINE
PRINT、もしくはHTML_PRINTで表示済みの行の内容を取得する。HTML_PRINTのほうはタグ付きなので、表示文字だけ取得したいのならHTML_TOPLAINTEXTなどと組み合わせるとよい
表示行の内容は配列で保存されているため、0からのスタートとなる(=GETDISPLAYLINE(LINECOUNT)は常に空文字)。LINECOUNTでループ回すとちょうど全行取得できる

・GCREATEFROMFILE拡張
第三引数に非0を渡すことで、Emueraからの相対パスで画像ファイルを指定できる。これによりERBやCSVフォルダ、独自に作成したフォルダも画像用フォルダとして使用可能になる
本家の時点で親ディレクトリが指定できちゃったのは内緒。一応この仕様は残してある

・GDASHSTYLE gID, DashStyle, DashCap
GDRAWLINEの線のスタイルを指定する。DashStyle、DashCapそれぞれC#のDashStyle、DashCap列挙型の数値で指定可能
DashStyle 0=普通の線 1=ダッシュで構成された線 2=ドットで構成された線 3=ダッシュとドットで構成された線 4=ダッシュとドット2個で構成された線
DashCap(線の端の形) 0=普通の形(直角) 2=丸めた形 3=三角形の形 1は欠番。文句はMicrosoftに言ってください

・多言語化対応
詳しくは下記リンク
https://evilmask.gitlab.io/emuera.em.doc/i18n/
オプション→表示 から言語を変更可能。現在は日本語、英語、中国語に対応

・Emuera-AnchorからClipboard機能を移植
設定→クリップボードから設定可能。百聞は一見にしかず

・ツールチップ機能拡張
詳しくは→https://evilmask.gitlab.io/emuera.em.doc/Reference/TOOLTIP_EXTENSION/

・日本語→英語の翻訳辞書機能を実装
JukesBouver99氏のパッチにて実装。辞書ファイルは同梱済み
コンフィグでオンオフ切替可能。不要な場合は辞書ファイルも削除可能

・ttfファイルとotfファイルに対応
Emueraと同じディレクトリに「font」フォルダを作成してttfファイルかotfファイルを置くと、コンフィグ→フォントからそのフォントが使用可能になる
GSETFONTとTOOLTIP_SETFONTにも対応
サンプルとしてたぬきフォント様の「たぬゴ」「全児童フォント」を同梱。以下はたぬきフォント様のサイトのリンク
https://tanukifont.com/

・.NET 7に正式対応
CRER氏のお陰で対応できました。感謝
一部UIが現代的に変わっています

・UPDATECHECK
アップデートチェック命令を追加。以下使い方
1,GameBase.csvに「バージョン名」「バージョン情報URL」を追加
　バージョン名には文字列型で任意のバージョン名、URLにはバージョン確認用のURLを記載する
2,上記のURLにバージョン情報と最新版リンクを記載したテキストをアップロードする
　1行目に最新のバージョン名を書き、2行目にはリンクを書く 3行目以降はコメント等自由に書いてOK
　オープンなGitを使うならリポジトリにプッシュしてrawで参照するのもあり
3,UPDATECHECK実行時にGameBase.csvに記載したURLにアクセスし、現バージョンと最新バージョンが違えばダイアログボックス経由でサーバー側のリンクを開くかどうかプレイヤーに尋ねる
　最新版の場合はRESULTに0が入って終了する
4,「はい」が選ばれればブラウザを開きRESULTに2が入る 「いいえ」が選ばれれば何もせずRESULTに1が入る リンク先が見つからない、リンク先にバージョン情報や最新版リンクが書いてない等、何らかの理由で失敗した場合はRESULTには3が入る
　また、コンフィグに「UPDATECHECKを許可しない」の項目を追加、これがオンになってるときにUPDATECHECKを実行した場合は何もしないが、RESULTに4が入る
11fixにてネットワークに接続されていない場合はRESULTに5が入るように

※※※※※※※※※※※※※※※※※※※※※※
製作者の方々へ 上記の機能を利用して悪意あるリンク等を記載しユーザーを騙す行為は不正アクセス禁止法に抵触し、厳重な処罰を受ける場合があります 良識を持った使い方を心がけましょう
ユーザーの方々へ リンクを開く際はそれが安全で信頼できるアドレスかを確認し、慎重に開くようにしましょう
※※※※※※※※※※※※※※※※※※※※※※


[使用方法]
Emueraが正常に動作するeraバリアントのディレクトリにてEmueraと同様の方法でお使いください

[ライセンス]
同フォルダ内のEmuera_readme.txtの[ライセンス]の項に準じます
私、Enterは一切の権利を主張しません
また、当Emueraを使用、同梱及び配布したバリアントについて生じた問題には責任を負いかねます

[Special Thanks]
lackbfun docsの中国語翻訳

