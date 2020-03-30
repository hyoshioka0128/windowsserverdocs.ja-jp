---
title: Windows デスクトップ クライアントの新機能
description: Microsoft デスクトップのリモート デスクトップ クライアントに対する最近の変更について説明します
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: heidilohr
manager: lizross
ms.author: helohr
ms.date: 03/24/2020
ms.localizationpriority: medium
ms.openlocfilehash: 38b779b12b841e276d8f807af6f6332469c20817
ms.sourcegitcommit: 9e8fddf683c9a36aad330ebef9b80d57f75ffb43
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2020
ms.locfileid: "80233304"
---
# <a name="whats-new-in-the-windows-desktop-client"></a>Windows デスクトップ クライアントの新機能

Windows デスクトップ クライアントの詳細については、「[Windows デスクトップ クライアントの概要](windowsdesktop.md)」で確認できます。 クライアントの最新の更新プログラムは以下で確認できます。

## <a name="latest-client-versions"></a>最新のクライアント バージョン

クライアントは、さまざまな[ユーザー グループ](windowsdesktop-admin.md#configure-user-groups)に対して構成できます。 次の表に、各ユーザー グループで使用できる現在のバージョンを示します。

|ユーザー グループ |バージョン  |
|-----------|---------|
|パブリック     |1.2.790  |
|Insider    |1.2.790  |

## <a name="updates-for-version-12790"></a>バージョン 1.2.790 の更新内容

*公開日:2020 年 3 月 24 日*

ダウンロード:[Windows 64 ビット](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4siSh)、[Windows 32 ビット](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4siSi)、[Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4sllb)

- 他のリモート デスクトップ クライアントとの一貫性を保つために、ワークスペースの "更新" アクションの名前を "最新の情報に更新" に変更しました。
- コンテキスト メニューからワークスペースを直接更新できるようになりました。
- 手動でワークスペースを更新すると、すべてのローカル コンテンツが確実に更新されるようになります。
- アプリをアンインストールすることなく、[バージョン情報] ページからクライアントのユーザー データをリセットできるようになりました。
- また、msrdcw.exe /reset をオプションの /f パラメーターと共に使用してプロンプトをスキップし、クライアントのユーザー データをリセットすることもできます。
- [バージョン情報] ページに移動すると、クライアントの更新プログラムが自動的に検索されるようになりました。
- ボタンの色が一貫性のために更新されました。

## <a name="updates-for-version-12675"></a>バージョン 1.2.675 の更新内容

*公開日:2020 年 2 月 25 日*

ダウンロード:[Windows 64 ビット](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4qeak)、[Windows 32 ビット](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4qm7h)、[Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4qm7g)

- RDP ファイルに署名がない場合、または signscope プロパティのいずれかが変更されている場合、Windows Virtual Desktop への接続がブロックされるようになりました。
- ワークスペースが空であるか削除されている場合は、接続センターが空ではないように見えます。
- トラブルシューティングを改善するために、切断メッセージにアクティビティ ID とエラー コードを追加しました。 **Ctrl + C** でダイアログ メッセージをコピーできます。
- デスクトップ接続の設定でディスプレイが検出されない原因となった問題を修正しました。
- クライアントの更新プログラムによって PC が自動的に再起動されることはなくなりました。
- ウィンドウなしのアイコンは、タスクバーに表示されなくなります。

## <a name="updates-for-version-12605"></a>バージョン 1.2.605 の更新内容

*公開日:2020 年 1 月 29 日*

ダウンロード:[Windows 64 ビット](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4oHrD)、[Windows 32 ビット](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4oJZs)、[Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4oXhD)

- デスクトップ接続に使用する表示内容を選択できるようになりました。 この設定を変更するには、デスクトップ接続のアイコンを右クリックして、 **[設定]** を選択します。
- 接続設定に使用可能な適正なスケール ファクターが表示されなかった問題が修正されました。
- 接続が開始されたときに表示されるダイアログをナレーターが読み取れない問題が修正されました。
- Azure Active Directory と Active Directory の名前が一致しなかった場合に、間違ったユーザー名が表示される問題が修正されました。
- ネットワークに接続していない状態で接続を開始したときに、クライアントからの応答が停止される問題が修正されました。
- ヘッドセットの接続時にクライアントが応答を停止する原因となった問題が修正されました。

## <a name="updates-for-version-12535"></a>バージョン 1.2.535 の更新内容

*公開日:2019/12/04*

ダウンロード:[Windows 64 ビット](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4k7jH)、[Windows 32 ビット](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4k7jL)、[Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE4k27O)

- クライアントの上部にあるコマンド バーの [その他のオプション] ボタンを使用して、更新プログラムに関する情報に直接アクセスできるようになりました。
- クライアントのコマンド バーからフィードバックを報告できるようになりました。
- [フィードバック] オプションは、フィードバック ハブを使用できる場合にのみ表示されるようになりました。
- ポリシーで通知が無効な場合、更新通知が表示されないようになりました。
- 一部の RDP ファイルを起動できない問題を修正しました。
- 一部の永続的な設定の破損が原因で発生するクライアントの起動時のクラッシュを修正しました。

## <a name="updates-for-version-12431"></a>バージョン 1.2.431 の更新内容

*公開日:2019 年 11 月 12 日*

ダウンロード:[Windows 64 ビット](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE48kow)、[Windows 32 ビット](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE48koA)、[Windows ARM64](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE48zYj)

- 32 ビットおよび ARM64 バージョンのクライアントが利用可能になりました。
- クライアントでは、接続バーに対して行ったすべての変更 (その位置、サイズ、固定状態など) が保存され、これらの変更がセッション間に適用されます。
- ゲートウェイ情報と接続状態のダイアログが更新されました。
- Azure Active Directory トークンの有効期限が切れた後に接続しようとすると、2 つの資格情報が同時に要求される問題に対処しました。
- Windows 7 では、サーバーで許可されていない資格情報を保存した場合に、ユーザーに資格情報の入力を求めるメッセージが正しく表示されるようになりました。
- Azure Active Directory プロンプトが、再接続時に接続ウィンドウの前面に表示されるようになりました。
- タスクバーにピン留めされた項目が、フィードの更新時に更新されるようになりました。
- タッチ使用時の接続センターでのスクロールが向上しました。
- [Resolution]\(解像度\) ドロップダウン メニューから空の行を削除しました。
- Windows Credential Manager の不要なエントリを削除しました。
- 全画面表示の終了時に、デスクトップ セッションが適切にサイズ変更されるようになりました。
- スリープ モードに入った後にセッションを再開すると、RemoteApp の切断のダイアログが前景に表示されるようになりました。
- キーボード ナビゲーションなどアクセシビリティの問題に対処しました。

## <a name="updates-for-version-12247"></a>バージョン 1.2.247 の更新内容

*公開日:2019 年 9 月 17 日*

ダウンロード:[Windows 64 ビット](https://query.prod.cms.rt.microsoft.com/cms/api/am/binary/RE3LkSa)

- ローカライズされたバージョンのフォールバック言語が強化されました (たとえば、FR-CA は英語ではなくフランス語で正しく表示されます)。
- サブスクリプションを削除すると、クライアントでは、保存された資格情報が Credential Manager から適切に削除されるようになりました。
- クライアントの更新プロセスは、開始後は無人で実行され、完了すると、クライアントは再起動されます。
- クライアントを Windows 10 の S モードで使用できるようになりました。
- ユーザー名にスペースが含まれるユーザーの更新プロセスが失敗する原因となっていた問題を修正しました。
- 接続中に認証を行うときに発生するクラッシュを修正しました。
- クライアントを閉じるときに発生するクラッシュを修正しました。
