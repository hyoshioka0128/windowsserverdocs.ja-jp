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
manager: daveba
ms.author: helohr
ms.date: 10/31/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6a8e66398bc61a69250b84101a3cb66f2c8f3548
ms.sourcegitcommit: 1da993bbb7d578a542e224dde07f93adfcd2f489
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73567065"
---
# <a name="whats-new-in-the-windows-desktop-client"></a>Windows デスクトップ クライアントの新機能

Windows デスクトップ クライアントの詳細については、「[Windows デスクトップ クライアントの概要](windowsdesktop.md)」で確認できます。 クライアントの最新の更新プログラムは以下で確認できます。

## <a name="latest-client-versions"></a>最新のクライアント バージョン

クライアントは、さまざまな[ユーザー グループ](windowsdesktop-admin.md#configure-user-groups)に対して構成できます。 次の表に、各ユーザー グループで使用できる現在のバージョンを示します。

|ユーザー グループ |バージョン  |
|-----------|---------|
|パブリック     |1.2.247  |
|Insider    |1.2.428  |

## <a name="updates-for-version-12428"></a>バージョン 1.2.428 の更新内容

*公開日:2019 年 10 月 31 日*

- 32 ビットおよび ARM64 バージョンのクライアントのプレビューが利用可能になりました。
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

- 接続中に認証を行うときに発生するクラッシュを修正しました。
- クライアントを閉じるときに発生するクラッシュを修正しました。

## <a name="updates-for-version-12246"></a>バージョン 1.2.246 の更新内容

*公開日:2019 年 8 月 28 日*

- ローカライズされたバージョンのフォールバック言語が強化されました (たとえば、FR-CA は英語ではなくフランス語で正しく表示されます)。
- サブスクリプションを削除すると、クライアントでは、保存された資格情報が Credential Manager から適切に削除されるようになりました。
- クライアントの更新プロセスは、開始後は無人で実行され、完了すると、クライアントは再起動されます。
- クライアントを Windows 10 の S モードで使用できるようになりました。
- ユーザー名にスペースが含まれるユーザーの更新プロセスが失敗する原因となっていた問題を修正しました。
