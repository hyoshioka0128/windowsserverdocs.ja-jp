---
title: "NTLM の概要"
description: "Windows Server のセキュリティ"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 773909fd-c0bc-498a-95fc-bb452ec04d90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 523fb71304ae55d17203cab4d1c5a17551bf8fdf
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="ntlm-overview"></a>NTLM の概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

IT プロフェッショナル向けのこのトピックでは、NTLM、機能、任意の変更点を説明し、Windows 認証および Windows Server 2012 の NTLM と以前のバージョンにテクニカル リソースへのリンクを示します。

## <a name="BKMK_OVER"></a>機能の説明
NTLM 認証は、Windows Msv1\_0.dll に含まれる認証プロトコルのファミリです。 NTLM 認証プロトコルには、LAN Manager version 1 および 2、および NTLM version 1 および 2 が含まれます。 NTLM 認証プロトコルは、ユーザーとコンピューターをサーバーまたはユーザーがアカウントに関連付けられているパスワードを知っているドメイン コントローラーに対して証明 challenge\/レスポンス メカニズムに基づいて認証します。 NTLM プロトコルを使用すると、新しいアクセス トークンが必要な場合は、常に、コンピューターまたはユーザーの身元を検証する次の操作のいずれかのリソース サーバーを実行する必要があります。

-   アカウントがドメイン アカウントの場合、コンピューターまたはユーザーのアカウント ドメインのドメイン コントローラーでドメイン認証サービスに問い合わせてください。

-   アカウントがローカル アカウントの場合は、ローカル アカウント データベース内のコンピューターまたはユーザーのアカウントを検索します。

## <a name="BKMK_APP"></a>現在のアプリケーション
NTLM 認証は、引き続きサポートし、ワークグループのメンバーとして構成されているシステムと Windows 認証を使用する必要があります。 NTLM 認証は以外のドメイン コントローラー上でローカル ログオン認証も使用されます。 Kerberos バージョン 5 認証は Active Directory 環境では、推奨される認証方法は以外 Microsoft または Microsoft アプリケーション可能性があります NTLM を使用して引き続きします。

IT 環境で NTLM プロトコルの使用量の削減には、NTLM と戦略とコンピューティング環境の構成に必要な手順を他のプロトコルを使用する展開したアプリケーションの要件の両方の知識が必要です。 選択的に NTLM トラフィックを制限するために NTLM を使用する方法を見つけるために、新しいツールと設定が追加されました。 分析し、使いの環境で NTLM の使用を制限する方法については、次を参照してください。[NTLM 認証の制限を導入](https://technet.microsoft.com/library/dd560653(v=ws.10).aspx)へのアクセスの監査と NTLM の使用に関するガイドを制限します。

## <a name="BKMK_NEW"></a>新機能と変更された機能
Windows Server 2012 の NTLM の機能の変更はありません。

## <a name="BKMK_DEP"></a>削除されたまたは推奨されなくなった機能
Windows Server 2012 の NTLM の削除されたまたは推奨されなくなった機能はありません。

## <a name="BKMK_INSTALL"></a>サーバー マネージャー情報
NTLM は、サーバー マネージャーから構成することはできません。 セキュリティ ポリシーの設定またはグループ ポリシーを使用して、コンピューター システム間の NTLM 認証の使用を管理することができます。 ドメインで Kerberos は、既定の認証プロトコルです。

## <a name="BKMK_LINKS"></a>参照してください。
次の表は、NTLM とその他の Windows 認証テクノロジの関連リソースを示します。

|コンテンツの種類|参照|
|--------|-------|
|**製品評価**|[NTLM 認証の制限の概要](https://technet.microsoft.com/library/dd560653.aspx)<br /><br />[NTLM 認証の変更点](https://technet.microsoft.com/library/dd566199.aspx)|
|**計画**|[IT インフラストラクチャの脅威モデリング ガイド](https://technet.microsoft.com/library/dd941826.aspx)<br /><br />[脅威と対策: Windows Server 2003 および Windows XP のセキュリティ設定](https://technet.microsoft.com/library/dd162275.aspx)<br /><br />[脅威と対策ガイド: Windows Server 2008 および Windows Vista でのセキュリティの設定](https://technet.microsoft.com/library/dd349791.aspx)<br /><br />[脅威と対策ガイド: Windows Server 2008 R2 および Windows 7 でのセキュリティの設定](https://technet.microsoft.com/library/hh125921.aspx)|
|**展開**|[認証に対する保護の強化](https://support.microsoft.com/kb/968389)<br /><br />[監査と NTLM の使用に関するガイドを制限します。](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)<br /><br />[ディレクトリ サービス チームに依頼する: NTLM のブロックとする: アプリケーションの分析と、Windows 7 で Methodologies の監査](https://blogs.technet.com/askds/archive/2009/10/08/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7.aspx)<br /><br />[Windows 認証ブログ](https://blogs.technet.com/authentication/)<br /><br />[NTLM pass\ を通じて認証用の MaxConcurrentAPI の構成](https://social.technet.microsoft.com/wiki/contents/articles/9759.configuring-maxconcurrentapi-for-ntlm-pass-through-authentication.aspx)|
|**開発**|[Microsoft NTLM \(Windows\)](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)<br /><br />[\[MS\-NLMP\]: NT LAN Manager \(NTLM\) 認証プロトコルの仕様](https://msdn.microsoft.com/library/cc236621(PROT.10).aspx)<br /><br />[\[MS\-NNTP\]: NT LAN Manager \(NTLM\) 認証: ネットワーク ニュース転送プロトコル \(NNTP\) 拡張](https://msdn.microsoft.com/library/cc236774(PROT.10).aspx)<br /><br />[\[MS\-NTHT\]: NTLM Over HTTP プロトコルの仕様](https://msdn.microsoft.com/library/cc237488(PROT.10).aspx)|
|**トラブルシューティング**|まだ利用できません。|
|**コミュニティ リソース**|[この木馬 dead なって: NTLM のボトルネックと RPC ランタイム](http://blogs.technet.com/b/askds/archive/2011/09/15/is-this-horse-dead-yet-ntlm-bottlenecks-and-the-rpc-runtime.aspx)|



