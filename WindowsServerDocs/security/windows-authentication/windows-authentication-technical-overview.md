---
title: Windows 認証の技術概要
description: Windows Server のセキュリティ
ms.topic: article
ms.assetid: 286d3e41-434f-4703-9320-706d06ebda51
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: c2ac43da06d6df177523b389eac90f02e6e26b93
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87989971"
---
# <a name="windows-authentication-technical-overview"></a>Windows 認証の技術概要

>適用先:Windows Server (半期チャネル)、Windows Server 2016

IT 担当者向けのこのトピックでは、Windows 認証の技術概要に関するトピックへのリンクを提供します。 Windows 認証は、Windows へのアクセスを試みているユーザーまたはサービスの信頼性を証明するためのプロセスです。

この一連のトピックでは、Windows 認証アーキテクチャとそのコンポーネントについて説明します。

このライブラリからページをデジタル保存または印刷するには、[**エクスポート**] (ページの右上隅にある) をクリックして、表示される指示に従います。

-   [Windows オペレーティングシステム間での Windows 認証の相違点](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dn169017(v=ws.10))

    認証アーキテクチャとプロセスの重要な違いについて説明します。

-   [Windows 認証の概念](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dn169018(v=ws.10))

    Windows 認証の基盤となる概念について説明します。

-   [Windows ログオン認証のシナリオ](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dn169020(v=ws.10))

    さまざまなログオンシナリオの概要を示します。

-   [Windows 認証のアーキテクチャ](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dn169024(v=ws.10))

    Windows オペレーティングシステムの認証アーキテクチャとプロセスの重要な違いについて説明します。

    -   [セキュリティ サポート プロバイダー インターフェイスのアーキテクチャ](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dn169026(v=ws.10))

        SSPI アーキテクチャについて説明します。

    -   [Windows 認証での資格情報の処理](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dn169014(v=ws.10))

        さまざまな資格情報管理プロセスについて説明します。

-   [Windows 認証で使用されるグループポリシー](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dn169021(v=ws.10))

    認証プロセスにおけるグループポリシーの使用および影響について説明します。

## <a name="what-is-not-covered"></a>本記事の対象外
この一連のトピックでは、Windows 環境内で認証テクノロジを設計、実装、または監視する手順については説明しません。

-   Windows の承認方法の設計については、「[リソースの承認方法の設計](/previous-versions/windows/it-pro/windows-server-2003/cc783368(v=ws.10))」を参照してください。

-   Windows 認証方法の設計については、「[認証方法の設計](/previous-versions/windows/it-pro/windows-server-2003/cc758124(v=ws.10))」を参照してください。

-   Windows 公開キー基盤の実装戦略の設計情報については、「[公開キー基盤の設計](/previous-versions/windows/it-pro/windows-server-2003/cc773138(v=ws.10))」を参照してください。

-   Windows 環境での認証を含むセキュリティの構成と監視については、以下を参照してください。

    -   [Windows XP セキュリティガイド](https://www.microsoft.com/download/details.aspx?id=962)

    -   [Windows Vista のセキュリティベースライン](/previous-versions/tn-archive/dd450978(v=technet.10))

    -   [Windows Server 2003 のセキュリティベースライン](/previous-versions/tn-archive/cc163140(v=technet.10))と[脅威と対策ガイド](/previous-versions/tn-archive/dd162275(v=technet.10))

    -   [Windows Server 2008 セキュリティガイド](https://www.microsoft.com/download/details.aspx?id=17606)

    -   [Windows Server 2008 R2 のセキュリティベースライン](/previous-versions/tn-archive/gg236605(v=technet.10))

-   Windows でのログオンイベントと認証イベントの監査の詳細については、「[セキュリティイベントの監査](/previous-versions/windows/it-pro/windows-server-2003/cc776394(v=ws.10))」を参照してください。