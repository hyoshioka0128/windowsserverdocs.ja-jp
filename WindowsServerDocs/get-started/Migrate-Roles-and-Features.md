---
title: 役割と機能の移行
description: ''
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.date: 04/03/2017
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0f78ef4c-dd12-4b1b-8c6e-251dd803c5d1
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 7469171005164d9ff823dad7de230d877c874dc9
ms.sourcegitcommit: 07ac08dea2b8f2763c2614a999dc7967018aa0b4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2018
ms.locfileid: "6121361"
---
# Windows Server の役割と機能を移行する

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このページでは、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012 への役割と機能の移行に役立つ情報やツールへのリンクを示します。 役割と機能の多くは、Windows Server 移行ツールを使用して移行できます。このツールは、役割と機能の要素やデータを簡単に移行できるように、Windows Server 2008 R2 で導入された 5 つの Windows PowerShell コマンドレットのセットです。

移行ガイドは、2 台のサーバー間で、指定した役割や機能を移行する作業について記載されています (インプレース アップグレードは対象外です)。 ガイドの中で特に断りのない限り、移行は物理コンピューターと仮想コンピューターの間において、完全なインストール オプションの Windows Server と Server Core インストール オプションを実行しているサーバー間でサポートされます。  

## 開始する前に

役割と機能の移行を開始する前に、移行元と移行先の両方のサーバーが、それぞれのオペレーティング システムで利用可能な最新のサービス パックを実行していることを確認します。
Windows Server 2012 R2 と Windows Server 2012 の移行ガイドは、電子書籍版が提供されています。 詳細および電子書籍のダウンロードについては、「[E-Book Gallery for Microsoft Technologies (マイクロソフト テクノロジ電子書籍ギャラリー)](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#MigrateRoles)をご覧ください。 

>[!NOTE]
>Windows Server のどのバージョンに移行またはアップグレードする場合も、[サポート ライフサイクル ポリシー](https://support.microsoft.com/lifecycle)および対象バージョンのサポート期間を確認し把握したうえで、それに応じて計画を立てる必要があります。 特定の Windows Server リリースのライフサイクルについては、[こちらでご検索ください](https://support.microsoft.com/lifecycle)。
 
## Windows Server 2016

### 移行ガイド
Windows Server 2016 用の新しい移行ガイドは、現在開発中です。 定期的にこのページにアクセスして、新しい移行ガイドに関する最新情報をご確認ください。 多くの場合、Windows Server 2012 R2 の移行ガイドの手順は、Windows Server 2016 にも当てはまります。

- [リモート デスクトップ サービス](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/migrate-rds-role-services)
- [Web サーバー (IIS)](https://www.iis.net/downloads/microsoft/web-deploy)
- [Windows Server Update Services](https://technet.microsoft.com/library/hh852339.aspx)
- [MultiPoint Services](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/multipoint-services/multipoint-services-migrate)
 
## Windows Server 2012 R2

### 移行ガイド
Windows Server 2003、Windows Server 2008、Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2 のいずれかを実行しているサーバーの役割と機能を Windows Server 2012 R2 に移行する場合は、以下のガイドの手順に従ってください。 Windows Server 2012 R2 の Windows Server 移行ツールでは、クロス サブネットの移行がサポートされています。

- [Windows Server 移行ツールのインストール、使用、および削除](https://technet.microsoft.com/library/jj134202.aspx)
- [Windows Server 2012 R2 用 Active Directory 証明書サービス移行ガイド](https://technet.microsoft.com/library/dn486797.aspx)
- [Windows Server 2012 R2 への Active Directory フェデレーション サービス (AD FS) 役割サービスの移行](https://technet.microsoft.com/library/dn486815.aspx)
- [Active Directory Rights Management Services Migration and Upgrade Guide (Active Directory Rights Management サービス移行およびアップグレード ガイド)](https://technet.microsoft.com/library/cc754277.aspx)
- [Windows Server 2012 R2 へのファイル サービスおよび記憶域サービスの移行](https://technet.microsoft.com/library/dn479292.aspx)
- [Windows Server 2012 から Windows Server 2012 R2 への Hyper-V の移行](https://technet.microsoft.com/library/dn486799.aspx)
- [Windows Server 2012 へのネットワーク ポリシー サーバーの移行](https://technet.microsoft.com/library/hh831652)
- [Windows Server 2012 R2 へのリモート デスクトップ サービスの移行](https://technet.microsoft.com/library/dn479239.aspx)
- [Windows Server 2012 への Windows Server Update Services の移行](https://technet.microsoft.com/library/hh852339.aspx)
- [Windows Server 2012 R2 へのクラスターの役割の移行](https://technet.microsoft.com/library/dn530779.aspx)
- [Windows Server 2012 R2 への DHCP サーバーの役割の移行](https://technet.microsoft.com/library/dn495425.aspx)
 
## Windows Server 2012

### 移行ガイド
Windows Server 2003、Windows Server 2008、Windows Server 2008 R2、Windows Server 2012 のいずれかを実行しているサーバーの役割と機能を Windows Server 2012 に移行する場合は、以下のガイドの手順に従ってください。 Windows Server 2012 の Windows Server 移行ツールでは、クロス サブネットの移行がサポートされています。

- [Windows Server 移行ツールのインストール、使用、および削除](https://technet.microsoft.com/library/jj134202)
- [Windows Server 2012 への Active Directory フェデレーション サービス (AD FS) 役割サービスの移行](https://technet.microsoft.com/library/jj647765)
- [Windows Server "8" Beta への正常性登録機関の移行](https://technet.microsoft.com/library/hh831513)
- [Windows 2008 R2 から Windows Server 2012 への Hyper-V の移行](https://technet.microsoft.com/library/jj574113)
- [Windows Server 2012 への IP 構成の移行](https://technet.microsoft.com/library/jj574133)
- [Windows Server 2012 へのネットワーク ポリシー サーバーの移行](https://technet.microsoft.com/library/hh831652)
- [WindowsServer2012 への印刷とドキュメント サービスの移行](https://technet.microsoft.com/library/jj134150)
- [Windows Server 2012 へのリモート アクセスの移行](https://technet.microsoft.com/library/hh831423)
- [Windows Server 2012 への Windows Server Update Services の移行](https://technet.microsoft.com/library/hh852339)
- [ドメイン コントローラーを Windows Server 2012 R2 または Windows Server 2012 にアップグレードする](https://technet.microsoft.com/library/hh994618.aspx)
- [クラスター化されたサービスとアプリケーションの Windows Server 2012 への移行](https://technet.microsoft.com/library/dn486790.aspx)
 

移行に関するその他の資料については、「[Windows Server への役割と機能の移行](https://technet.microsoft.com/library/jj134039)」をご覧ください。

## Windows Server 2008 R2

### 移行ガイド
Windows Server 2003、Windows Server 2008、Windows Server 2008 R2 のいずれかを実行しているサーバーの役割と機能を Windows Server 2008 R2 に移行する場合は、以下のガイドの手順に従ってください。 Windows Server 2008 R2 の Windows Server 移行ツールでは、クロス サブネットの移行はサポートされていません。

- [Windows Server Migration Tools Installation, Access, and Removal (Windows Server 移行ツールのインストール、アクセス、削除)](https://technet.microsoft.com/library/dd379545)
- [Active Directory Certificate Services Migration Guide (Active Directory 証明書サービス移行ガイド)](https://technet.microsoft.com/library/ee126170)
- [Active Directory Domain Services and Domain Name System (DNS) Server Migration Guide (Active Directory Domain Servicesおよびドメイン ネーム システム (DNS) サーバー移行ガイド)](https://technet.microsoft.com/library/dd379558)
- [BranchCache Migration Guide (BranchCache 移行ガイド)](https://technet.microsoft.com/library/dd548365)
- [Dynamic Host Configuration Protocol (DHCP) Server Migration Guide (動的ホスト構成プロトコル (DHCP) サーバー移行ガイド)](https://technet.microsoft.com/library/dd379535)
- [File Services Migration Guide (ファイル サービス移行ガイド)](https://technet.microsoft.com/library/dd379487)
- [HRA Migration Guide (HRA 移行ガイド)](https://technet.microsoft.com/library/ee791829)
- [Hyper-V Migration Guide (Hyper-V 移行ガイド)](https://technet.microsoft.com/library/ee849855)
- [IP Configuration Migration Guide (IP 構成移行ガイド)](https://technet.microsoft.com/library/dd379537)
- [Local User and Group Migration Guide (ローカル ユーザーとグループ移行ガイド)](https://technet.microsoft.com/library/dd379531)
- [NPS Migration Guide (NPS 移行ガイド)](https://technet.microsoft.com/library/ee791849)
- [Print Services Migration Guide (印刷サービス移行ガイド)](https://technet.microsoft.com/library/dd379488)
- [Remote Desktop Services Migration Guide (リモート デスクトップ サービス移行ガイド)](https://technet.microsoft.com/library/ff849223)
- [RRAS Migration Guide (RRAS 移行ガイド)](https://technet.microsoft.com/library/ee822825)
- [Windows Server Migration Common Tasks and Information (Windows Server の移行に関する一般的なタスクと情報)](https://technet.microsoft.com/library/ff400258)
- [Windows Server Update Services 3.0 SP2 Migration Guide (Windows Server Update Services 3.0 SP2 移行ガイド)](https://technet.microsoft.com/library/ee822826)
 
移行に関するその他の資料については、「[Migrate Roles and Features to Windows Server 2008 R2 (Windows Server 2008 R2 への役割と機能の移行)](https://technet.microsoft.com/library/dd365353)」をご覧ください。
