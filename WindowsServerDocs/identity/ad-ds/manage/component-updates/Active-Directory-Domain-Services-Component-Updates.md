---
title: Active Directory Domain Services コンポーネントの更新
description: このドキュメントでは、Windows Server 2012 R2 の AD DS のコンポーネントの更新がについて説明します
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 09/08/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: a3a91034-a4da-4ad7-93f8-0cd2ec3e7824
ms.technology: identity-adds
ms.openlocfilehash: 300bf7dafe0ef0ede754302f2c0aa8c36a7adbfd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889883"
---
# <a name="active-directory-domain-services-component-updates"></a>Active Directory Domain Services コンポーネントの更新

>適用先:Windows Server 2016、Windows Server 2012 R2

このモジュールでは、マイナーな更新が行われたディレクトリ サービスと ID スペースのコンポーネントについて説明します。  
  
|作成者について|  
|--------------------|  
|**作成者:**|Justin Turner|  
|**略歴:**|Justin は、米国テキサス州アービングを拠点とするディレクトリ サービス チームのシニア サポート エスカレーション エンジニアです。  過去 12 年間にわたって、多くのトレーニング コースや Microsoft サポート技術情報の記事を作成し、貢献してきました。 チャーター マイクロソフト認定マスター (MCM)、マイクロソフト認定トレーナー (MCT) し、修士号を取得を保持する彼はマイクロソフトの社員と顧客新製品のアーキテクチャについて説明します。 コンピューター教育と認識システムでの角度です。|  
|**寄稿者**|このトレーニング モジュールには、 *Michiko Short*, *Dean Wells*, *Alan Jowett*, *Manu Pushpendran*, *Yashar Bahman*, *Anoosh Saboori*, *Rashmi Jha*, *Justin Hall* 、 *Herbert Mauerer*からの寄稿が掲載されています。|  
|**校閲者**|多くのレビューとフィードバックを提供する独自の時間を費やしている人物を次に協力してくれた:*Joey Seifert*、 *Justin Hall*|  
  
> [!NOTE]  
> この内容は Microsoft カスタマー サポート エンジニアによって作成され、TechNet が通常提供しているトピックよりも詳細な Windows Server 2012 R2 の機能やソリューションの技術的説明を求めている、経験豊かな管理者とシステム設計者を対象としています。 ただし、TechNet と同様の編集過程は実施されていないため、言語によっては通常より洗練されていない文章が見られる場合があります。  
  
### <a name="what-you-will-learn"></a>学習する内容  
このモジュールを完了すると、次のことができるようになります。  
  
-   Windows Server 2012 R2 のディレクトリ サービスと ID の技術領域内で行われたコンポーネントの更新についての説明  
  
    -   [SPN と UPN の一意性](../../../ad-ds/manage/component-updates/SPN-and-UPN-uniqueness.md)  
  
    -   [Winlogon 自動再起動サインオン&#40;ARSO&#41;](../../../ad-ds/manage/component-updates/Winlogon-Automatic-Restart-Sign-On--ARSO-.md)  
  
    -   [TPM キーの構成証明](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md)  
  
    -   [CA のバックアップと復元の Windows PowerShell コマンドレット](../../../ad-ds/manage/component-updates/CA-Backup-and-Restore-Windows-PowerShell-cmdlets.md)  
  
    -   [コマンド ライン プロセスの監査](../../../ad-ds/manage/component-updates/Command-line-process-auditing.md)  
  
    -   [資格情報の保護と管理](https://technet.microsoft.com/library/dn408190.aspx)  
  
    -   [ディレクトリ サービス コンポーネントの更新](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md)  
  
        -   [ドメインとフォレストの機能レベル](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_FL)  
  
        -   [NTFRS の廃止](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_NTFRS)  
  
        -   [LDAP クエリ オプティマイザーの変更点](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_LDAPQuery)  
  
        -   [1644 イベントの改善](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_1644)  
  
        -   [Active Directory レプリケーション スループットの向上](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_ADRepl)  
  


