---
title: "Active Directory Domain Services コンポーネントの更新"
description: "このドキュメントでは、Windows Server 2012 R2 の AD DS のコンポーネントの更新がについて説明します"
author: billmath
ms.author: billmath
manager: femila
ms.date: 09/08/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: a3a91034-a4da-4ad7-93f8-0cd2ec3e7824
ms.technology: identity-adds
ms.openlocfilehash: 52d3dab542b4250670067e927f42ddf1597fc852
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="active-directory-domain-services-component-updates"></a>Active Directory Domain Services コンポーネントの更新

>適用対象: Windows Server 2016、Windows Server 2012 R2

このモジュールは、ディレクトリ サービスと Id スペースにマイナーな更新プログラムを受信するコンポーネントを紹介します。  
  
|作成者について|  
|--------------------|  
|**作成者:**|Justin チューナー|  
|**紹介を保存します。**|Justin は、米国テキサス州アービング州に基づく、ディレクトリ サービス チームのシニア サポート エスカレーション エンジニアです。  彼は作成または過去 12 年間、Microsoft サポート技術情報の多くのトレーニング コースやサポート技術情報の記事に寄与します。 Microsoft の従業員と顧客新製品のアーキテクチャを教えてチャーター マイクロソフト認定マスター (MCM)、マイクロソフト認定トレーナー (MCT) であり、理学を保持 コンピューター教育と認識システムで程度です。|  
|**協力者の氏名**|このトレーニング モジュールにから*Michiko Short*、 *Dean Wells*、 *Alan Jowett*、 *Manu Pushpendran*、 *Yashar Bahman*、 *Anoosh Saboori*、 *Rashmi Jha*、 *Justin Hall*と*Herbert Mauerer*|  
|**レビュー担当者**|独自の時間を確認およびフィードバックを提供する費やされた時間を感謝します: *Joey Seifert*、 *Justin Hall*|  
  
> [!NOTE]  
> このコンテンツが、Microsoft カスタマー サポート エンジニアによって書き込まれるあり、経験豊富な管理者と TechNet の通常のトピックよりも機能と Windows Server 2012 R2 で解決策の詳細な技術的説明を求めているシステム アーキテクトです。 ただし、実施されていません、同様の編集過程のため、TechNet の「新機能が見つかった通常より洗練されて、言語によってように見える場合があります。  
  
### <a name="what-you-will-learn"></a>学習する内容  
このモジュールを完了した後することができます。  
  
-   Windows Server 2012 R2 でのディレクトリ サービスと Id の技術領域内で行われたコンポーネントの更新プログラムを説明します。  
  
    -   [SPN と UPN の一意性](../../../ad-ds/manage/component-updates/SPN-and-UPN-uniqueness.md)  
  
    -   [Winlogon 自動再起動サインオン (&) #40 です。ARSO & #41 です。](../../../ad-ds/manage/component-updates/Winlogon-Automatic-Restart-Sign-On--ARSO-.md)  
  
    -   [TPM キーの構成証明](../../../ad-ds/manage/component-updates/TPM-Key-Attestation.md)  
  
    -   [CA のバックアップと復元の Windows PowerShell のコマンドレット](../../../ad-ds/manage/component-updates/CA-Backup-and-Restore-Windows-PowerShell-cmdlets.md)  
  
    -   [コマンド ライン プロセスの監査](../../../ad-ds/manage/component-updates/Command-line-process-auditing.md)  
  
    -   [資格情報の保護と管理](https://technet.microsoft.com/library/dn408190.aspx)  
  
    -   [ディレクトリ サービス コンポーネントの更新](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md)  
  
        -   [ドメインとフォレストの機能レベル](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_FL)  
  
        -   [NTFRS の廃止](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_NTFRS)  
  
        -   [LDAP クエリ オプティマイザーの変更点](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_LDAPQuery)  
  
        -   [1644 イベントの改善](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_1644)  
  
        -   [Active Directory レプリケーション スループットの向上](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_ADRepl)  
  


