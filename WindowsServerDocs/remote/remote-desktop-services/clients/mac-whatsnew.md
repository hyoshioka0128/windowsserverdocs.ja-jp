---
title: Mac でリモート デスクトップの新機能
description: Mac 用のリモート デスクトップ クライアントに対する最近の変更について説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 03/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: d0cf81f24374e81ca28c2d2cfd83a394e096706c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844793"
---
# <a name="whats-new-for-the-remote-desktop-client-on-macos"></a>MacOS 上のリモート デスクトップ クライアントの新しい何ですか。

定期的に更新、 [macOS 用のリモート デスクトップ クライアント](remote-desktop-mac.md)、新しい機能を追加および問題を修正します。 以下の最新の更新プログラムを確認します。

問題が発生した場合は、常に弊社までご連絡を使用して**ヘルプ > 問題を報告する**します。

## <a name="updates-for-version-1029"></a>バージョン 10.2.9 用更新プログラム
*公開日:3/6/2019*

- サーバーのリダイレクトがときに発生する RD ゲートウェイ接続の問題を修正しましたこのリリースでは次のように配置します。
- 10.2.8 による、RD ゲートウェイの回帰をアドレス指定も更新します。

## <a name="updates-for-version-1028"></a>バージョン 10.2.8 用更新プログラム
*公開日:3/1/2019*

- RD ゲートウェイを使用する場合に表示される接続の問題を解決します。
- 接続するときに表示されていた不適切な証明書の警告を修正しました。
- 場合によっては、メニュー バーとドッキング ステーションが不必要に非はリモート アプリを起動するときに場所のアドレスを指定します。
- アドレスのクラッシュやハングがある一部のユーザーを悩ませるされているクリップボードのリダイレクト コードを作成し直します。
- 不必要なスクロールの接続を起動するときに、接続センターを原因となったバグを修正しました。

## <a name="updates-for-version-1027"></a>10.2.7 のバージョンの更新プログラム
*公開日:2/6/2019*

- このリリースでは、AVC444 モードを使用するときに表示されるグラフィックス mispaints (サーバー エンコードのバグによって引き起こさ) に対処しました。

## <a name="updates-for-version-1026"></a>10.2.6 のバージョンの更新プログラム
*公開日:1/28/2019*

- AVC (420 および 444) コーデックでは、Windows 10 の現在のバージョンに接続するときに使用可能なサポートが追加されました。
- ウィンドウ モードに合わせる]、[ウィンドウの更新を今すぐ直後に発生して、そのコンテンツのサイズ変更は、補間の適切なレベルにレンダリングされます。
- 一部のユーザーに重複するフィードのヘッダーの原因となったレイアウトのバグを修正しました。
- アプリケーションの基本設定の UI をクリーンアップします。
- 追加/編集デスクトップ UI を洗練されました。
- 多くの調整し、しあげのデスクトップとフィードの接続センター タイルとリスト ビューの調整が行われます。

>[!NOTE]
>大量のディスク領域を使用する (~/Library フォルダー内で深く入れ子になった) macOS 10.14.0 と 10.14.1".com.microsoft.rdc.application-data_SUPPORT/_EXTERNAL_DATA"を引き起こす可能性のあるフォルダー内のバグでがあります。 この問題を解決するには、フォルダーの内容を削除し、macOS 10.14.2 にアップグレードします。 ブックマークに割り当てられているスナップショット画像が削除されることは、フォルダーの内容を削除する副作用に注意してください。 リモート PC に再接続するとき、これらのイメージを再生成されます。

## <a name="updates-for-version-1024"></a>10.2.4 のバージョンの更新プログラム
*公開日:12/18/2018*

- MacOS Mojave 10.14 のダーク モードのサポートを追加します。
- 空の場合は、接続センターで今すぐ Microsoft リモート デスクトップ 8 からインポートするオプションが表示されます。
- フォルダー リダイレクトの一部のサードパーティ製のエンタープライズ アプリケーション互換性のアドレスを指定します。
- ユーザーを受け取っているセキュリティ上の理由 0x30000069 リモート デスクトップ ゲートウェイのエラー プロトコルのフォールバックの問題の問題を解決します。
- 固定プログレッシブ レンダリングの問題で発生していた一部のユーザーに合わせてウィンドウ モードにします。
- 妨げるバグを修正しました。 ファイルをコピーし、ファイルの最新バージョンのコピーから貼り付けます。
- 小さいスクロールのデルタのスクロール マウス ベースが向上します。

## <a name="updates-for-version-1023"></a>10.2.3 用の更新プログラム
*公開日:11/06/2018*

- リモート アプリのシナリオの"remoteapplicationcmdline"RDP ファイルの設定のサポートが追加されました。
- セッション ウィンドウのタイトルが、RDP ファイル (とサーバー名) の名前が含まれています、RDP ファイルから起動するとします。
- 報告された RD ゲートウェイのパフォーマンスの問題を修正しました。
- 固定の報告された RD ゲートウェイがクラッシュします。
- 接続がハングが RD ゲートウェイ経由で接続するときに、問題を修正しました。
- メニュー バーとドッキング ステーションをインテリジェントに非表示にしてリモート アプリを全画面表示のより優れた処理します。
- 起動後リモート アプリが非表示したままのシナリオを修正しました。
- 低速のレンダリングの更新プログラムは、「ウィンドウに合わせる」を無効になっているハードウェア アクセラレータを使用する場合に対処します。
- クライアントの起動時に、不適切なアクセス許可によるデータベース作成エラーを処理します。 
- 問題を修正しましたが、クライアントである一貫して起動時にクラッシュし、一部のユーザーに起動しません。
- シナリオでの接続が正しくインポートされないとして 8 のリモート デスクトップから全画面表示を修正しました。

## <a name="updates-for-version-1022"></a>10.2.2 のバージョンの更新プログラム
*公開日:10/09/2018*

- サポートする新しい接続センターでは、ドラッグ アンド ドロップ、デスクトップ、リスト ビュー モード、列ベースの並べ替え、およびグループの管理を簡単にサイズ変更可能な列の手動の配置。
- 接続センターで、最後のアクティブなピボット (デスクトップまたはフィード) をとき記憶今すぐアプリを終了します。
- UI とフローの入力を求める資格情報が徹底的に見直されました。
- RD ゲートウェイのフィードバックは、接続の状態 UI の一部ではようになりました。
- バージョン 8 のクライアントからの設定のインポートが改善されました。
- RemoteApp のエンドポイントを指す RDP ファイルのファイルは、接続センターに今すぐインポートできます。
- リモート デスクトップ シナリオの 1 つのモニター retina ディスプレイの最適化。
- (これは、ブラーが強く影響します)、グラフィックス補間のレベルを指定するためのサポート Retina 最適化を使用しない場合。
- Windows 2000 に接続できるように 256 色のサポート。
- Windows 7、Windows Server 2008 R2 に接続するときに、画面の右および下のクリッピングとそれ以前を修正しました。
- 添付ファイルとしてファイルを追加するようになりました (リモート セッションで実行されている) Outlook にローカル ファイルをコピーします。
- ネットワーク共有からファイルが作成された場合は、クリップボード ベースのファイル転送を遅らせるが問題を修正しました。
- Excel (リモート セッションで実行されている) にリダイレクトされたフォルダーのファイルに保存するときにハングする原因となっていたバグに対処します。
- 原因では空き領域がリダイレクトされたフォルダーの報告される問題を修正しました。
- Macos 10.14 が多すぎるディスク記憶域を使用するサムネイルの原因となったバグを修正しました。
- RD ゲートウェイ デバイスのリダイレクト ポリシーを適用するためのサポートが追加されました。
- RD ゲートウェイを使用して、接続から切断すると、セッションのウィンドウを閉じるを防ぐ問題を修正しました。
- ネットワーク レベル認証 (NLA) は、サーバーによって強制されない場合がルーティングされますログイン画面に、パスワードの有効期限が切れている場合。
- 表示されるときにパフォーマンスの問題を修正しました。 ネットワーク経由で大量のデータを転送中だった。
- スマート カードのリダイレクトを修正します。
- サポート"EnableCredSspSupport"と「認証レベル」のすべての可能な値の RDP ファイルの設定 (com.microsoft.rdc.macos ドメイン) 内のユーザーの既定の ClientSettings.EnforceCredSSPSupport キーが 0 に設定されている場合。
- NLA がネゴシエートされない場合は、「プロンプト クライアント用に資格情報に」RDP ファイルの設定をサポートします。
- NLA はネゴシエートされずと Winlogon プロンプトでスマート カードのリダイレクトを使用してスマート カード ベースのログインをサポートします。
- フィードの URL にスペースが含まれるリソースのダウンロードを妨げる問題を修正しました。

## <a name="updates-for-version-1021"></a>10. 2.1. のバージョンの更新プログラム
*公開日:08/06/2018*

- 有効な接続の Azure Active Directory (AAD) に参加する Pc。 接続に、AAD に参加する PC、自分のユーザー名は、次の形式のいずれかである必要があります。"AzureAD\user"または"AzureAD\user@domain"。
- リモート セッションでのスマート カードの使用量に影響を与えるいくつかのバグに対処します。

## <a name="updates-for-version-1020"></a>バージョン 10.2.0 用更新プログラム
*公開日:07/24/2018*

- GDPR コンプライアンスの更新プログラムを結果を反映します。
- MicrosoftAccount\username@domain 有効なユーザー名として承認されたようになりました。
- クリップボードの共有が高速化およびその他の書式をサポートする書き換えられました。
- コピーしてテキスト、画像、または現在のセッションの間でファイルに貼り付けることは、ローカル コンピューターのクリップボードをバイパスします。
- ようになりました (警告プロンプトに同意する) 場合、信頼されていない証明書で、RD ゲートウェイ サーバー経由で接続することができます。
- メタル ハードウェアの高速化が使用されます (サポートされている) 場合のレンダリングを高速化し、バッテリの使用量を最適化します。
- させる不思議な力を操作するように努めてメタル ハードウェア アクセラレータを使用する場合、セッションのグラフィックスがより鮮明に表示します。
- Windows は閉じられている後に話し、いくつかのインスタンスを削除します。
- 一部のシナリオでの RemoteApp プログラムの起動エラーの原因が修正されたバグ。
- 0x204 エラーを発生させるが RD ゲートウェイ チャンネルの同期エラーを修正しました。
- マウスのカーソル更新正しくセッションまたは RemoteApp ウィンドウから移動するときに。
- データ損失の原因となっていたフォルダー リダイレクトのバグを修正しましたとコピーするフォルダーを貼り付けることです。
- フォルダーのサイズの正しくないレポートの原因となったフォルダー リダイレクトの問題を修正しました。
- ローカル アカウントを使用して、AAD に参加しているマシンにログインを妨げていたバグ再発の修正。
- セッション ウィンドウの内容をクリップするを原因となっている修正されたバグ。
- 楕円曲線の非対称キーを含む RD エンドポイント証明書のサポートが追加されました。
- 一部のシナリオでマネージ リソースのダウンロードを妨げていたバグを修正しました。
- 固定接続センターでクリッピング問題に対処します。
- 適切に共同作業する表示プロパティ シートで、チェック ボックスを修正しました。
- ダイナミック表示の変更が有効な場合は、縦横比をロックは無効になりました。
- F5 キーを押してインフラストラクチャとの互換性の問題に対処します。
- 接続時に正しいメッセージを表示することを確認するパスワードが空白の処理を更新します。
- 固定のマウス MapInfra Pro と互換性の問題をスクロールします。
- Mojave で実行されている場合は、接続センターでいくつかの配置の問題を修正しました。

## <a name="updates-for-version-1018"></a>バージョン 10.1.8 用更新プログラム
*公開日:05/04/2018*

- セッション ウィンドウのサイズを変更してリモートの解像度の変更のサポートが追加されました。
- リモート リソースがダウンロードをフィード固定のシナリオでは、極端に長い時間がかかります。
- パッチは適用されません CredSSP 暗号化 oracle 修復アップデート (CVE 2018 0886) を使用してサーバーに接続するときに発生する 0x207 エラーを解決します。

## <a name="updates-for-version-1017"></a>バージョン 10.1.7 用更新プログラム
*公開日:04/05/2018*

- CVE-2018-0886」の説明に従って、CredSSP 暗号化 oracle の修復の更新プログラムを組み込むセキュリティ修正プログラムを作成します。
- 表示が改善されました RemoteApp アイコンをマウス カーソルに報告された mispaints に対処します。
- 接続センターの背後にある windows の RemoteApp が表示されていた問題に対処します。
- リモート デスクトップ 8 からインポートした後にローカル リソースを編集するときに発生した問題を修正しました。
- デスクトップのタイルで ENTER キーを押して、接続を開始できます。
- 全画面表示の場合は、CMD キーを押しながら M キーこれで正しくマップ WIN + M します。
- 接続センター、環境設定、およびについて windows CMD キーを押しながら M キーに応答します。
- ENTER キーを押してフィードの検出を開始できます、**リモート リソースの追加**ページ。
- 更新した後、リモート リソースの新しいフィードがまで、接続センターでの空で示しました問題を修正しました。
 
## <a name="updates-for-version-1016"></a>バージョン 10.1.6 用更新プログラム
*公開日:03/26/2018*

- RemoteApp windows を並べ替えるはそれ自体問題を修正しました。
- 一部の RemoteApp ウィンドウの親ウィンドウの背後に停止の原因となったバグを解決します。
- 一部の RemoteApp プログラムの影響をマウス ポインターのオフセット問題に対処します。
- 新しいセッション ウィンドウを開くのではなく、既存のセッションにフォーカスが、新しい接続を開始した問題を修正しました。
- エラー メッセージでエラーを修正しました - 今すぐ、ゲートウェイが見つからない場合、適切なメッセージが表示されます。
- Quit ショートカット (⌘ + Q) が UI に一貫して表示されています。
- 「ウィンドウに合わせる」モードでをストレッチするときは、イメージ品質を向上します。
- リモート セッションで表示するホーム フォルダーの複数のインスタンスの原因となったバグ再発の修正。
- デスクトップのタイルの既定のアイコンを更新します。
