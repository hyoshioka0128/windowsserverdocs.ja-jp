---
ms.assetid: 638c89bd-87e6-484b-9d2e-8ae2a74227e5
title: サービス通信証明書を設定する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 7253502390db004747d3732cf3d288a51afdaaf1
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280687"
---
# <a name="set-a-service-communications-certificate"></a>サービス通信証明書を設定する


Active Directory フェデレーション サービス内のフェデレーション サーバー \(AD FS\)サービス通信証明書を使用して、Secure Sockets Layer の Web サービス トラフィックをセキュリティで保護する\(SSL\) Web との通信クライアントまたはフェデレーション サーバー プロキシ。

> [!NOTE]  
> サービス通信証明書は、SSL 証明書と同じではありません。 AD FS SSL 証明書を変更するには Powershell を使用する必要があります。 このガイダンスに従う[記事](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/manage-ssl-certificates-ad-fs-wap)します。


次の手順を使用するには、AD FS 管理スナップインでサービス通信証明書を変更する\-でします。  

> [!NOTE]  
> AD FS 管理スナップイン\-サービス通信証明書としてフェデレーション サーバーのサーバー認証証明書を参照しています。  

この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/でしょうか。LinkId\=83477\)します。   

### <a name="to-set-a-service-communications-certificate"></a>サービス通信証明書を設定するには  

1.  **開始**画面で「**AD FS 管理**、し、ENTER キーを押します。  

2.  コンソール ツリーで、二重\-クリックして**サービス**、順にクリックします**証明書**します。  

3.  **アクション**ウィンドウで、をクリックして、**設定サービス通信証明書**リンク。  

4.  **サービス通信証明書を選択します** ダイアログ ボックスで、サービス通信証明書として設定、証明書ファイルを選択し、クリックする証明書ファイルを移動**を開く。** .  

## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  

[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)  
