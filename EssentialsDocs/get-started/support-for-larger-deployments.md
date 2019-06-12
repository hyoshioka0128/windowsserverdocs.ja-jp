---
title: 大規模展開のサポート
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07d0c4c6-3e92-4969-82b8-105e46ab8d97
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: a99698519524c3b5050dc534d61921560522528c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433868"
---
# <a name="support-for-larger-deployments"></a>大規模展開のサポート

>適用先:Windows Server 2016 Essentials

> [!IMPORTANT]  
> Essentials Experience 役割が有効になっている、および Windows Server 2016 Essentials SKU ではなく、このトピックで説明する機能は Windows Server 2016 でのみ機能します。


Windows Server Essentials では、大規模な展開で使用できるようになりました。

- 複数のドメイン
- 複数のドメイン コント ローラー
- 指定されたドメイン コント ローラーを指定する機能
- 最大 500 ユーザーと 500 台のデバイスのサポート

## <a name="support-for-multiple-domains"></a>複数のドメインのサポート

Windows server 2012 R2 Essentials のサポートが必要な場合、サーバーごとに 1 つのドメインと、Essentials サーバーは、フォレストのルートである必要があります。 ドメインとフォレストは引き続き必要ですが、Windows Server 2016 Essentials Experience 役割は Windows Server 2016 Standard または Datacenter 複数のドメインをサポートするために今すぐ展開できます。

## <a name="support-for-multiple-domain-controllers"></a>複数のドメイン コント ローラーのサポート

 Windows Server Essentials 2012 R2 では、1 つ以上のドメイン コント ローラーが展開されている Office 365 など、Azure Active Directory を利用するすべてのサービスをブロックします。 理由は、ローカル ドメイン コント ローラーと Azure Active Directory のアカウントとパスワードの同期は、同期されていないパスワードを持つアカウントの資格情報になることができることです。Windows Server 2016 Essentials で、この制限がなくなりました。

## <a name="ability-to-specify-a-designated-domain-controller"></a>指定されたドメイン コント ローラーを指定する機能

ここでは、Active Directory ドメインのオブジェクトの取得時間を向上だけでなく、ドメイン内の他のドメイン コント ローラー間でのアカウントの変更の同期の調整が指定されたドメイン コント ローラーを選択できます。

既定のドメイン コント ローラーを指定は、Windows Server Essentials Experience サーバーの役割を実行しているのと同じサーバーになります。 サーバーの場合は、メンバー サーバーで、ドメイン コント ローラーではありませんし、指定されたドメイン コント ローラーが自動的に決定される既定値は、テストに基づく、ドメインのドメイン コント ローラーを実行するサーバーの短いネットワーク待機時間、Windows Server エクスペリエンスの役割。 実行できますが、指定されたドメイン コント ローラーをどのサーバーを手動で変更する場合は、**設定**で、 **Windows Server Essentials ダッシュ ボード**次のようです。

![設定が表示されたスクリーン ショットでは、フォア グラウンドでパネルと、バック グラウンドで Windows Server Essentials ダッシュ ボードを制御します。 コントロール パネルの設定の指定されたドメイン コント ローラーのページは現在選択されています。](media/larger-deployments-1.PNG)

## <a name="support-for-500-users-and-500-devices"></a>500 人のユーザーと 500 台のデバイスのサポート
-------------------------------------

Windows Server 2012 R2 Essentials でサポートされているユーザーとデバイスの最大数は、それぞれ 25、50、です。 Windows Server Essentials Experience サーバーの役割の導入に伴い、制限は 100 人のユーザーと 200 台のデバイスに拡張されました。

Windows Server 2016 Essentials は、500 人のユーザーと 500 台のデバイスをサポートします。 これを行うプロバイダー framework の更新プログラムは、考えられると、オブジェクトの一覧をキャッシュし、大規模なユーザーとデバイス オブジェクトのリストをすばやく表示を制御します。 さらに、ユーザーまたはデバイスが必要な場合 (図 5-2 を参照してください) をすばやく検索する検索およびフィルター処理機能が追加されました。 検索およびフィルター機能を見つけたら、 **Windows Server Essentials ダッシュ ボード**、**リモート Web アクセス**、および、Windows および Windows Phone ストア**My Server**アプリケーション。

![文字列"d5c"を検索する Windows Server Essentials ダッシュ ボードの検索機能の使用方法を示すスクリーン ショット この検索の結果には、2 つのファイルおよびフォルダーと 2 人のユーザーが含まれます。](media/larger-deployments-2.PNG)

文字列"d5c"を検索する Windows Server Essentials ダッシュ ボードの検索機能の使用を示すスクリーン ショット。 この検索の結果には、2 つのファイルおよびフォルダーと 2 人のユーザーが含まれます。

> [!NOTE]  
> Windows Server Essentials サーバー ロールに、クライアント バックアップ順位 75 でのサポートされる上限に高めましたがサポートされているユーザーとデバイスの上限。

<a name="see-also"></a>関連項目
--------
[Windows Server Essentials の概要](get-started.md)