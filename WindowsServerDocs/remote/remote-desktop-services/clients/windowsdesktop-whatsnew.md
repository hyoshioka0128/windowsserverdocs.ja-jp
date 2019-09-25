---
title: Windows デスクトップ クライアントの新機能
description: Microsoft デスクトップのリモート デスクトップ クライアントに対する最近の変更について説明します
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: heidilohr
manager: daveba
ms.author: helohr
ms.date: 09/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 587ad44509451497b253689238c3aef233a37153
ms.sourcegitcommit: e210fce039452a9855353520c7f8698acd76ffce
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71071289"
---
# <a name="whats-new-in-the-windows-desktop-client"></a>Windows デスクトップ クライアントの新機能

Windows デスクトップ クライアントの詳細については、「[Windows デスクトップ クライアントの概要](windowsdesktop.md)」で確認できます。 クライアントの最新の更新プログラムは以下で確認できます。

## <a name="latest-client-versions"></a>最新のクライアント バージョン

クライアントは、さまざまな[ユーザー グループ](windowsdesktop-admin.md#configure-user-groups)に対して構成できます。 次の表に、各ユーザー グループで使用できる現在のバージョンを示します。

|ユーザー グループ |バージョン  |
|-----------|---------|
|パブリック     |1.2.246  |
|Insider    |1.2.247  |

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
