---
title: Windows 認証の技術概要
description: Windows Server のセキュリティ
ms.prod: windows-server
ms.technology: security-windows-auth
ms.topic: article
ms.assetid: 286d3e41-434f-4703-9320-706d06ebda51
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 7a19230e0fc1fb96700785fd83e70d501d59b76a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861695"
---
# <a name="windows-authentication-technical-overview"></a>Windows 認証の技術概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

IT 担当者向けのこのトピックでは、Windows 認証の技術概要に関するトピックへのリンクを提供します。 Windows 認証は、Windows へのアクセスを試みているユーザーまたはサービスの信頼性を証明するためのプロセスです。

この一連のトピックでは、Windows 認証アーキテクチャとそのコンポーネントについて説明します。

このライブラリからページをデジタル保存または印刷するには、 **[エクスポート]** (ページの右上隅にある) をクリックして、表示される指示に従います。

-   [Windows オペレーティングシステム間での Windows 認証の相違点](https://technet.microsoft.com/library/dn169017.aspx)

    認証アーキテクチャとプロセスの重要な違いについて説明します。

-   [Windows 認証の概念](https://technet.microsoft.com/library/dn169018.aspx)

    Windows 認証の基盤となる概念について説明します。

-   [Windows ログオン認証のシナリオ](https://technet.microsoft.com/library/dn169020.aspx)

    さまざまなログオンシナリオの概要を示します。

-   [Windows 認証のアーキテクチャ](https://technet.microsoft.com/library/dn169024.aspx)

    Windows オペレーティングシステムの認証アーキテクチャとプロセスの重要な違いについて説明します。

    -   [セキュリティ サポート プロバイダー インターフェイスのアーキテクチャ](https://technet.microsoft.com/library/dn169026.aspx)

        SSPI アーキテクチャについて説明します。

    -   [Windows 認証での資格情報の処理](https://technet.microsoft.com/library/dn169014.aspx)

        さまざまな資格情報管理プロセスについて説明します。

-   [Windows 認証で使用されるグループポリシー](https://technet.microsoft.com/library/dn169021.aspx)

    認証プロセスにおけるグループポリシーの使用および影響について説明します。

## <a name="what-is-not-covered"></a>カバーされていないもの
この一連のトピックでは、Windows 環境内で認証テクノロジを設計、実装、または監視する手順については説明しません。

-   Windows の承認方法の設計については、「[リソースの承認方法の設計](https://technet.microsoft.com/library/cc783368.aspx)」を参照してください。

-   Windows 認証方法の設計については、「[認証方法の設計](https://technet.microsoft.com/library/cc758124.aspx)」を参照してください。

-   Windows 公開キー基盤の実装戦略の設計情報については、「[公開キー基盤の設計](https://technet.microsoft.com/library/cc773138.aspx)」を参照してください。

-   Windows 環境での認証を含むセキュリティの構成と監視については、以下を参照してください。

    -   [Windows XP セキュリティガイド](https://www.microsoft.com/download/details.aspx?id=962)

    -   [Windows Vista のセキュリティベースライン](https://technet.microsoft.com/library/dd450978.aspx)

    -   [Windows Server 2003 のセキュリティベースライン](https://technet.microsoft.com/library/cc163140.aspx)と[脅威と対策ガイド](https://technet.microsoft.com/library/dd162275.aspx)

    -   [Windows Server 2008 セキュリティガイド](https://www.microsoft.com/download/details.aspx?id=17606)

    -   [Windows Server 2008 R2 のセキュリティベースライン](https://technet.microsoft.com/library/gg236605.aspx)

-   Windows でのログオンイベントと認証イベントの監査の詳細については、「[セキュリティイベントの監査](https://technet.microsoft.com/library/cc776394.aspx)」を参照してください。


