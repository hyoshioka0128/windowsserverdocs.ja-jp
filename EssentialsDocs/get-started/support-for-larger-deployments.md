---
title: "大規模展開のサポート"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.openlocfilehash: c60e5f73c88a225fbd1067992894f9d20da745ad
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
#<a name="support-for-larger-deployments"></a>大規模展開のサポート

>Windows Server 2016 Essentials の適用対象:

> [!IMPORTANT]  
> Essentials Experience 役割が有効になっている、および Windows Server 2016 Essentials SKU ではなく、このトピックで説明する機能は Windows Server 2016 上でのみ動作します。


Windows Server Essentials には、大規模な展開で今すぐサポートしています。

- 複数のドメイン
- 複数のドメイン コントローラー
- 指定されたドメイン コントローラーを指定する機能
- 最大 500 のユーザーとデバイスの 500 のサポート

##<a name="support-for-multiple-domains"></a>複数のドメインのサポート

Windows server 2012 R2 Essentials をサポートする必要がある、サーバーあたり 1 つのドメインと、Essentials サーバーは、フォレストのルートである必要があります。 ドメインとフォレストがまだ必要なときに、Windows Server 2016 Essentials Experience 役割は Windows Server 2016 Standard または Datacenter 複数ドメインをサポートするようになりました展開できます。

## <a name="support-for-multiple-domain-controllers"></a>複数のドメイン コントローラーのサポート

 Windows Server Essentials 2012 R2 では、1 つ以上のドメイン コントローラーが展開されている、Office 365 などの Azure Active Directory を利用しているすべてのサービスをブロックします。 理由は、する間、ローカル ドメイン コントローラーと Azure Active Directory アカウントとパスワードの同期につながる可能性がアカウントの資格情報の同期はパスワードを使用します。 このような制限は、Windows Server 2016 Essentials で削除されました。

##<a name="ability-to-specify-a-designated-domain-controller"></a>指定されたドメイン コントローラーを指定する機能

今すぐは Active Directory ドメインのオブジェクトの検索時間を向上だけでなく、ドメイン内の他のドメイン コントローラー アカウントの変更の同期を調整する指定されたドメイン コントローラーを選択できます。

ドメイン コントローラーが指定されている既定は、Windows Server Essentials Experience サーバーの役割を実行しているのと同じサーバーになります。 そのサーバーがメンバーサーバーの場合、つまり、ドメイン コントローラーではありませんし、既定値が指定されたドメイン コントローラーは自動的にに基づいて決定するドメイン コントローラーをドメインでテストが、ネットワーク待ち時間、Windows Server のエクスペリエンスのサーバーの役割を実行しているサーバーにします。 どのサーバーが、指定されたドメイン コントローラーを手動で変更する場合を行うために**設定**で、**Windows Server Essentials ダッシュ ボード**次のようにします。

![設定を示すスクリーン ショットは、パネルで、フォア グラウンドとバック グラウンドで Windows Server Essentials ダッシュ ボードを制御します。 コントロール パネルの [設定のドメイン コントローラーの指定] ページは、現在選択されています。](media/larger-deployments-1.PNG)

##<a name="support-for-500-users-and-500-devices"></a>ユーザー数が 500 および 500 のデバイスのサポート
-------------------------------------

Windows Server 2012 R2 Essentials でサポートされているユーザーとデバイスの最大数、25 50、それぞれします。 Windows Server Essentials Experience サーバーの役割の導入により、制限が 100 人のユーザーと 200 台のデバイスに拡大されました。

Windows Server 2016 Essentials は、ユーザー数が 500 および 500 のデバイスをサポートします。 これを行う可能なプロバイダー フレームワークの更新は、オブジェクトのリスト コントロールをキャッシュし、すぐに大規模なユーザーとデバイス オブジェクトのリストをレンダリングします。 さらに、ユーザーまたはデバイスが必要な場合 (図 5-2 を参照してください) をすばやく検索検索とフィルター機能が追加されました。 検索とフィルター機能が表示されます、**Windows Server Essentials ダッシュ ボード**、**リモート Web アクセス**、および Windows および Windows Phone ストア**My Server**アプリケーション。

![文字列"d5c"を検索する、Windows Server Essentials ダッシュ ボードの検索機能の使用方法を示すスクリーン ショット この検索の結果には、2 つのファイルおよびフォルダーと 2 人のユーザーが含まれます。](media/larger-deployments-2.PNG)

文字列"d5c"を検索する、Windows Server Essentials ダッシュ ボードの検索機能の使用方法を示すスクリーン ショット。 この検索の結果には、2 つのファイルおよびフォルダーと 2 人のユーザーが含まれます。

> [!NOTE]  
> サポートされているユーザーとデバイスの上限が Windows Server Essentials サーバーの役割、75 でクライアント バックアップはサポートされている制限の拡張中にします。

<a name="see-also"></a>参照してください。
--------
[Windows Server Essentials を使ってみる](get-started.md)