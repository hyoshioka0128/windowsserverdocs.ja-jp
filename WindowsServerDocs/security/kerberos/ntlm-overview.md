---
title: NTLM Overview
description: Windows Server のセキュリティ
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890643"
---
# <a name="ntlm-overview"></a>NTLM Overview

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

IT プロフェッショナルは、このトピックでは、NTLM、機能のすべての変更点について説明し、Windows 認証と Windows Server 2012 の NTLM と以前のバージョンに技術的なリソースへのリンクを提供します。

## <a name="BKMK_OVER"></a>機能の説明
NTLM 認証は Windows Msv1 に含まれる認証プロトコルのファミリです。\_0.dll します。 NTLM 認証プロトコルには、LAN Manager Version 1 および 2、NTLM Version 1 および 2 が含まれます。 NTLM 認証プロトコルには、認証のユーザーとコンピューターをチャレンジに基づく\/サーバーまたはユーザー アカウントに関連付けられているパスワードを認識しているドメイン コント ローラー証明応答メカニズム。 NTLM プロトコルを使用した場合、リソース サーバーは、新しいアクセス トークンが必要になったら、次のいずれかの処理でコンピューターまたはユーザーの ID を検証する必要があります。

-   ドメイン コントローラーのドメイン認証サービスにコンピューターまたはユーザーのアカウント ドメインを問い合わせる (アカウントがドメイン アカウントである場合)。

-   コンピューターまたはユーザーのアカウントをローカル アカウント データベースに照会する (アカウントがローカル アカウントである場合)。

## <a name="BKMK_APP"></a>現在のアプリケーション
NTLM 認証はこれまでどおりサポートされており、ワークグループのメンバーとして構成されているシステムに対する Windows 認証で使用する必要があります。 NTLM 認証がローカルのログオン認証以外にも使用\-ドメイン コント ローラー。 Kerberos version 5 認証は Active Directory 環境では非推奨される認証方法\-Microsoft または Microsoft アプリケーションでは NTLM が使用も可能性があります。

IT 環境で NTLM プロトコルの使用を減らすには、デプロイされるアプリケーションの NTLM に関する要件に加え、コンピューティング環境を他のプロトコルを使用するように構成するための戦略と手順に関する知識が必要です。 NTLM トラフィックを選択的に制限するために NTLM を使用する方法を見つけるために役立つ新しいツールと設定が追加されています。 お使いの環境での NTLM の使用状況の分析とその使用制限に関する情報については、「 [NTLM 認証の制限の概要](https://technet.microsoft.com/library/dd560653(v=ws.10).aspx) 」の NTLM の使用の監査と制限についての説明を参照してください。

## <a name="BKMK_NEW"></a>新規または変更された機能
Windows Server 2012 の NTLM の機能の変更はありません。

## <a name="BKMK_DEP"></a>削除または非推奨の機能
Windows Server 2012 の NTLM の削除または非推奨の機能はありません。

## <a name="BKMK_INSTALL"></a>サーバー マネージャーの情報
NTLM をサーバー マネージャーから構成することはできません。 コンピューター システム間の NTLM 認証の使用を管理するには、セキュリティ ポリシー設定かグループ ポリシーを使います。 ドメインでは、Kerberos が既定の認証プロトコルです。

## <a name="BKMK_LINKS"></a>参照してください。
次の表に、NTLM とその他の Windows 認証テクノロジに関係するリソースをまとめます。

|コンテンツの種類|参考資料|
|--------|-------|
|**製品評価**|[NTLM 認証の制限の概要](https://technet.microsoft.com/library/dd560653.aspx)<br /><br />[NTLM 認証の変更点](https://technet.microsoft.com/library/dd566199.aspx)|
|**計画**|[IT インフラストラクチャの脅威モデリング ガイド](https://technet.microsoft.com/library/dd941826.aspx)<br /><br />[脅威と対策:Windows Server 2003 と Windows XP のセキュリティ設定](https://technet.microsoft.com/library/dd162275.aspx)<br /><br />[脅威と対策ガイド:Windows Server 2008 および Windows Vista のセキュリティ設定](https://technet.microsoft.com/library/dd349791.aspx)<br /><br />[脅威と対策ガイド:Windows Server 2008 R2 と Windows 7 のセキュリティ設定](https://technet.microsoft.com/library/hh125921.aspx)|
|**展開**|[認証の拡張保護](https://support.microsoft.com/kb/968389)<br /><br />[監査と NTLM の使用に関するガイドを制限します。](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)<br /><br />[Ask the Directory Services Team:NTLM Blocking and You:アプリケーションの分析と Windows 7 での方法論の監査](https://blogs.technet.com/askds/archive/2009/10/08/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7.aspx)<br /><br />[Windows 認証ブログ](https://blogs.technet.com/authentication/)<br /><br />[MaxConcurrentAPI を NTLM パスの構成\-認証を使用](https://social.technet.microsoft.com/wiki/contents/articles/9759.configuring-maxconcurrentapi-for-ntlm-pass-through-authentication.aspx)|
|**開発**|[Microsoft NTLM \(Windows\)](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)<br /><br />[\[MS\-NLMP\]:NT LAN Manager \(NTLM\)認証プロトコルの仕様](https://msdn.microsoft.com/library/cc236621(PROT.10).aspx)<br /><br />[\[MS\-NNTP\]:NT LAN Manager \(NTLM\)認証。ネットワーク ニュース転送プロトコル\(NNTP\)拡張機能](https://msdn.microsoft.com/library/cc236774(PROT.10).aspx)<br /><br />[\[MS\-NTHT\]:HTTP プロトコルの仕様経由の NTLM](https://msdn.microsoft.com/library/cc237488(PROT.10).aspx)|
|**トラブルシューティング**|現在は入手不能|
|**コミュニティ リソース**|[この木馬を配信不能まだは。NTLM のボトルネックと RPC ランタイム](http://blogs.technet.com/b/askds/archive/2011/09/15/is-this-horse-dead-yet-ntlm-bottlenecks-and-the-rpc-runtime.aspx)|



