---
title: 大規模展開のサポート
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 07d0c4c6-3e92-4969-82b8-105e46ab8d97
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d98ab8b203bc73da4129d63b5a2b7518742a3667
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181648"
---
# <a name="support-for-larger-deployments"></a>大規模展開のサポート

>適用対象: Windows Server 2016 Essentials

> [!IMPORTANT]
> このトピックで説明する機能は、windows server 2016 Essentials SKU ではなく、Essentials Experience role が有効になっている Windows Server 2016 でのみ機能します。


Windows Server Essentials で、次の機能を備えた大規模な展開をサポート

- 複数のドメイン
- 複数のドメインコントローラー
- 指定されたドメインコントローラーを指定する機能
- 最大500ユーザーおよび500デバイスのサポート

## <a name="support-for-multiple-domains"></a>複数のドメインのサポート

Windows server 2012 R2 Essentials では、サーバーごとに1つのドメイン (必須) がサポートされており、Essentials サーバーはフォレストのルートである必要があります。 ドメインとフォレストは依然として必要ですが、windows server 2016 Essentials エクスペリエンスの役割を Windows Server 2016 Standard または Datacenter に展開して、複数のドメインをサポートできるようになりました。

## <a name="support-for-multiple-domain-controllers"></a>複数のドメインコントローラーのサポート

 Windows Server Essentials 2012 R2 では、複数のドメインコントローラーが展開されている Office 365 など、Azure Active Directory を利用するすべてのサービスがブロックされます。 これは、ローカルドメインコントローラと Azure Active Directory 間のアカウントとパスワードの同期によって、同期されていないパスワードを使用してアカウントの資格情報が送信される可能性があるためです。この制限は、Windows Server 2016 Essentials では削除されています。

## <a name="ability-to-specify-a-designated-domain-controller"></a>指定されたドメインコントローラーを指定する機能

指定したドメインコントローラーを選択できるようになりました。これにより Active Directory ドメインオブジェクトの取得時間が短縮され、ドメイン内の他のドメインコントローラー間でのアカウントの変更の同期が調整されます。

既定のドメインコントローラーは、Windows Server Essentials エクスペリエンスサーバーの役割を実行しているサーバーと同じサーバーになります。 そのサーバーがメンバーサーバーである場合 (ドメインコントローラーではない場合)、ドメイン内のどのドメインコントローラーが Windows Server Experience サーバーの役割を実行しているサーバーに対して最も短いネットワーク待機時間を持つかをテストすることに基づいて、既定のドメインコントローラーが自動的に決定されます。 指定されたドメインコントローラーのサーバーを手動で変更する場合は、次に示すように、 **Windows Server Essentials ダッシュボード**の [**設定**] で変更できます。

![バックグラウンドの [コントロールパネル] の前景と Windows Server Essentials ダッシュボードに表示されるスクリーンショット。 [設定] コントロールパネルの [指定したドメインコントローラー] ページが現在選択されています。](media/larger-deployments-1.PNG)

## <a name="support-for-500-users-and-500-devices"></a>500ユーザーと500デバイスのサポート
-------------------------------------

Windows Server 2012 R2 Essentials でサポートされているユーザーとデバイスの最大数は、それぞれ25と50です。 Windows Server Essentials Experience サーバーの役割の導入により、この制限は100ユーザーと200デバイスに増加しました。

Windows Server 2016 Essentials では、500ユーザーと500デバイスがサポートされています。 これを可能にすることは、プロバイダーフレームワークおよびオブジェクトリストコントロールを更新することで、サイズの大きいユーザーおよびデバイスのオブジェクトリストをキャッシュし、すばやく表示できるようにすることです。 さらに、探しているユーザーまたはデバイスをすばやく検索するための検索とフィルター機能が追加されました (図5-2 を参照)。 検索機能とフィルター機能については、「 **Windows Server Essentials ダッシュボード**」、「**リモート Web アクセス**」、および「Windows と Windows Phone ストア**マイサーバー**アプリケーション」を参照してください。

!["D5c" という文字列を検索するための Windows Server Essentials ダッシュボードの検索機能の使用方法を示すスクリーンショット。 この検索の結果には、2つのファイルとフォルダー、および2人のユーザーが含まれます。](media/larger-deployments-2.PNG)

"D5c" という文字列を検索するための Windows Server Essentials ダッシュボードの検索機能の使用方法を示すスクリーンショット。 この検索の結果には、2つのファイルとフォルダー、および2人のユーザーが含まれます。

> [!NOTE]
> Windows Server Essentials のサーバーの役割でサポートされているユーザーとデバイスの制限が引き上げられていますが、クライアントのバックアップでサポートされる制限は75にとどまります。

<a name="see-also"></a>関連項目
--------
[Windows Server Essentials の概要](get-started.md)