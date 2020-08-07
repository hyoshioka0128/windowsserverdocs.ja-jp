---
ms.assetid: 2bac7744-9de3-491a-b0a2-4e843cec7344
title: ヘルプ デスク リンクの追加
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 53580f58636f7cb2af0d8b37944a717664ba0f19
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87947274"
---
# <a name="add-help-desk-link"></a>ヘルプ デスク リンクの追加


## <a name="to-add-a-help-desk-link"></a>ヘルプデスクのリンクを追加するには
サインインページに表示されるヘルプデスクリンクを追加するには、 \- 次の Windows PowerShell コマンドレットと構文を使用します。

![ヘルプデスクの追加](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)


`Set-AdfsGlobalWebContent -HelpDeskLink https://fs1.contoso.com/help/ -HelpDeskLinkText Help`


> [!IMPORTANT]
> このコマンドレットの `linkText` パラメーターは、既定値である *Help* を使用する場合は必要ありません。 既定値には、すべてのクライアント ロケールでローカライズ済みであるという利点があります。 ページをカスタマイズすると、カスタマイズ設定が優先されるため、サポートするすべての言語でページをカスタマイズする必要があります。


## <a name="additional-references"></a>その他の参照情報
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)
