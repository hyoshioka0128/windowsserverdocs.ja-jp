---
title: Active Directory Domain Services コンポーネントの更新
description: このドキュメントでは、Windows Server 2012 R2 の AD DS コンポーネントの更新について説明します。
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 09/08/2017
ms.topic: article
ms.prod: windows-server
ms.assetid: a3a91034-a4da-4ad7-93f8-0cd2ec3e7824
ms.technology: identity-adds
ms.openlocfilehash: 0dfb108067bee1a5f276963116e2a72b99f6aec2
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961124"
---
# <a name="active-directory-domain-services-component-updates"></a>Active Directory Domain Services コンポーネントの更新

>適用対象: Windows Server 2016 の場合は Windows Server 2012 R2

このモジュールでは、マイナーな更新が行われたディレクトリ サービスと ID スペースのコンポーネントについて説明します。  


| 著者について |
|------------------|
|   **作成者:**    |
|     **略歴:**     |
| **寄稿者** |
|  **校閲者**   |

> [!NOTE]  
> この内容は Microsoft カスタマー サポート エンジニアによって作成され、TechNet が通常提供しているトピックよりも詳細な Windows Server 2012 R2 の機能やソリューションの技術的説明を求めている、経験豊かな管理者とシステム設計者を対象としています。 ただし、TechNet と同様の編集過程は実施されていないため、言語によっては通常より洗練されていない文章が見られる場合があります。  

### <a name="what-you-will-learn"></a>学習する内容  
このモジュールを完了すると、次のことができるようになります。  

-   Windows Server 2012 R2 のディレクトリ サービスと ID の技術領域内で行われたコンポーネントの更新についての説明  

    -   [SPN と UPN の一意性](../../../ad-ds/manage/component-updates/SPN-and-UPN-uniqueness.md)  

    -   [Winlogon の自動再起動サインオン &#40;ARSO&#41;](../../../ad-ds/manage/component-updates/Winlogon-Automatic-Restart-Sign-On--ARSO-.md)  

    -   [TPM キーの構成証明](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md)  

    -   [CA のバックアップと復元の Windows PowerShell コマンドレット](../../../ad-ds/manage/component-updates/CA-Backup-and-Restore-Windows-PowerShell-cmdlets.md)  

    -   [コマンド ライン プロセ](../../../ad-ds/manage/component-updates/Command-line-process-auditing.md)スの監査  

    -   [資格情報の保護と管理](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn408190(v=ws.11))  

    -   [ディレクトリ サービス コンポーネントの更新](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md)  

        -   [ドメインとフォレストの機能レベル](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_FL)  

        -   [NTFRS の廃止](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_NTFRS)  

        -   [LDAP クエリ オプティマイザーの変更点](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_LDAPQuery)  

        -   [1644 イベントの改善](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_1644)  

        -   [Active Directory レプリケーション スループットの向上](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_ADRepl)  
