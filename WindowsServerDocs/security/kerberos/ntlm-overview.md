---
title: NTLM Overview
description: Windows Server のセキュリティ
ms.topic: article
ms.assetid: 773909fd-c0bc-498a-95fc-bb452ec04d90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: b81d59a350f5549cdb83af7299b8636fb917cc24
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996088"
---
# <a name="ntlm-overview"></a>NTLM Overview

>適用先:Windows Server (半期チャネル)、Windows Server 2016

IT 担当者向けのこのトピックでは、NTLM とその機能の変更点について説明します。また、windows Server 2012 およびそれ以前のバージョンの Windows 認証と NTLM の技術情報へのリンクを提供します。

## <a name="feature-description"></a><a name="BKMK_OVER"></a>機能の説明
NTLM 認証は、Windows Msv10.dll に含まれている認証プロトコルのファミリです \_ 。 NTLM 認証プロトコルには、LAN Manager Version 1 および 2、NTLM Version 1 および 2 が含まれます。 NTLM 認証プロトコルは、ユーザーとコンピューターをチャレンジ応答メカニズムに基づいて認証し、 \/ ユーザーがアカウントに関連付けられているパスワードを知っていることをサーバーまたはドメインコントローラーに証明します。 NTLM プロトコルを使用した場合、リソース サーバーは、新しいアクセス トークンが必要になったら、次のいずれかの処理でコンピューターまたはユーザーの ID を検証する必要があります。

-   ドメイン コントローラーのドメイン認証サービスにコンピューターまたはユーザーのアカウント ドメインを問い合わせる (アカウントがドメイン アカウントである場合)。

-   コンピューターまたはユーザーのアカウントをローカル アカウント データベースに照会する (アカウントがローカル アカウントである場合)。

## <a name="current-applications"></a><a name="BKMK_APP"></a>現在のアプリケーション
NTLM 認証はこれまでどおりサポートされており、ワークグループのメンバーとして構成されているシステムに対する Windows 認証で使用する必要があります。 NTLM 認証は、ドメインコントローラー以外でのローカルログオン認証にも使用され \- ます。 Active Directory 環境では Kerberos version 5 認証を使用することをお勧めし \- ますが、microsoft または microsoft 以外のアプリケーションでも NTLM が使用される場合があります。

IT 環境で NTLM プロトコルの使用を減らすには、デプロイされるアプリケーションの NTLM に関する要件に加え、コンピューティング環境を他のプロトコルを使用するように構成するための戦略と手順に関する知識が必要です。 NTLM トラフィックを選択的に制限するために NTLM を使用する方法を見つけるために役立つ新しいツールと設定が追加されています。 お使いの環境での NTLM の使用状況の分析とその使用制限に関する情報については、「 [NTLM 認証の制限の概要](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd560653(v=ws.10)) 」の NTLM の使用の監査と制限についての説明を参照してください。

## <a name="new-and-changed-functionality"></a><a name="BKMK_NEW"></a>新機能と変更された機能
Windows Server 2012 では、NTLM の機能に変更はありません。

## <a name="removed-or-deprecated-functionality"></a><a name="BKMK_DEP"></a>削除された機能または非推奨の機能
Windows Server 2012 の NTLM では、削除された機能や非推奨の機能はありません。

## <a name="server-manager-information"></a><a name="BKMK_INSTALL"></a>サーバー マネージャー情報
NTLM をサーバー マネージャーから構成することはできません。 コンピューター システム間の NTLM 認証の使用を管理するには、セキュリティ ポリシー設定かグループ ポリシーを使います。 ドメインでは、Kerberos が既定の認証プロトコルです。

## <a name="see-also"></a><a name="BKMK_LINKS"></a>関連項目
次の表に、NTLM とその他の Windows 認証テクノロジに関係するリソースをまとめます。

|コンテンツ タイプ|参考資料|
|--------|-------|
|**製品評価**|[NTLM 認証の制限の概要](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd560653(v=ws.10))<p>[NTLM 認証の変更点](/previous-versions/windows/it-pro/windows-7/dd566199(v=ws.10))|
|**計画**|[IT Infrastructure Threat Modeling Guide (IT インフラストラクチャの脅威モデリング ガイド)](/previous-versions/tn-archive/dd941826(v=technet.10))<p>[Threats and Countermeasures:Security Settings in Windows Server 2003 and Windows XP (脅威と対策: Windows Server 2003 と Windows XP でのセキュリティ設定)](/previous-versions/tn-archive/dd162275(v=technet.10))<p>[Threats and Countermeasures Guide:Security Settings in Windows Server 2008 and Windows Vista (脅威と対策ガイド: Windows Server 2008 と Windows Vista でのセキュリティ設定)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd349791(v=ws.10))<p>[Threats and Countermeasures Guide: Security Settings in Windows Server 2008 R2 and Windows 7 (脅威とその対策ガイド: Windows Server 2008 R2 および Windows 7 でのセキュリティ設定)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/hh125921(v=ws.10))|
|**デプロイ**|[認証の拡張保護 (Extended Protection for Authentication)](https://support.microsoft.com/kb/968389)<p>[Auditing and restricting NTLM usage guide (NTLM の使用の監査と制限を行うためのガイド)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/jj865674(v=ws.10))<p>[ディレクトリ サービス チームへの質問:NTLM Blocking and You:Application Analysis and Auditing Methodologies in Windows 7 (NTLM のブロック: Windows 7 でのアプリケーションの分セ手法と監査手法)](https://blogs.technet.com/askds/archive/2009/10/08/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7.aspx)<p>[Windows 認証ブログ](https://blogs.technet.com/authentication/)<p>[Configuring for NTLM pass-through authentication (NTLM パススルー認証用の MaxConcurrentAPI の構成)](https://support.microsoft.com/help/2688798/how-to-do-performance-tuning-for-ntlm-authentication-by-using-the-maxc)|
|**開発**|[Microsoft NTLM \( Windows\)](/windows/win32/secauthn/microsoft-ntlm)<p>[\[MS \- nlmp \] : NT LAN Manager \( NTLM \) 認証プロトコル仕様](https://msdn.microsoft.com/library/cc236621(PROT.10).aspx)<p>[\[MS \- NNTP \] : NT LAN Manager \( NTLM \) 認証: ネットワークニュース転送プロトコルの \( NNTP \) 拡張機能](https://msdn.microsoft.com/library/cc236774(PROT.10).aspx)<p>[\[MS \- ntht \] : NTLM Over HTTP プロトコル仕様](https://msdn.microsoft.com/library/cc237488(PROT.10).aspx)|
|**トラブルシューティング**|まだ使用できません|
|**コミュニティ リソース**|[Is this horse dead yet:NTLM Bottlenecks and the RPC runtime (まだ役に立つのか: NTML のボトルネックと RPC ランタイム)](https://blogs.technet.com/b/askds/archive/2011/09/15/is-this-horse-dead-yet-ntlm-bottlenecks-and-the-rpc-runtime.aspx)|