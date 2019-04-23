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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840883"
---
# <a name="migrating-roles-and-features-in-windows-server"></a>Windows Server の役割と機能を移行する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このページでは、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012 への役割と機能の移行に役立つ情報やツールへのリンクを示します。 役割と機能の多くは、Windows Server 移行ツールを使用して移行できます。このツールは、役割と機能の要素やデータを簡単に移行できるように、Windows Server 2008 R2 で導入された 5 つの Windows PowerShell コマンドレットのセットです。

移行ガイドは、2 台のサーバー間で、指定した役割や機能を移行する作業について記載されています (インプレース アップグレードは対象外です)。 ガイドの中で特に断りのない限り、移行は物理コンピューターと仮想コンピューターの間において、完全なインストール オプションの Windows Server と Server Core インストール オプションを実行しているサーバー間でサポートされます。  

## <a name="before-you-begin"></a>始める前に

役割と機能の移行を開始する前に、移行元と移行先の両方のサーバーが、それぞれのオペレーティング システムで利用可能な最新のサービス パックを実行していることを確認します。
Windows Server 2012 R2 と Windows Server 2012 の移行ガイドは、電子書籍版が提供されています。 詳細および電子書籍のダウンロードについては、「[E-Book Gallery for Microsoft Technologies (マイクロソフト テクノロジ電子書籍ギャラリー)](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#MigrateRoles)をご覧ください。 

>[!NOTE]
>Windows Server のどのバージョンに移行またはアップグレードする場合も、[サポート ライフサイクル ポリシー](https://support.microsoft.com/lifecycle)および対象バージョンのサポート期間を確認し把握したうえで、それに応じて計画を立てる必要があります。 特定の Windows Server リリースのライフサイクルについては、[こちらでご検索ください](https://support.microsoft.com/lifecycle)。
 
## <a name="windows-server-2016"></a>Windows Server 2016

### <a name="migration-guides"></a>移行ガイド
Windows Server 2016 用の新しい移行ガイドは、現在開発中です。 定期的にこのページにアクセスして、新しい移行ガイドに関する最新情報をご確認ください。 多くの場合、Windows Server 2012 R2 の移行ガイドの手順は、Windows Server 2016 にも当てはまります。

- [リモート デスクトップ サービス](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/migrate-rds-role-services)
- [Web サーバー (IIS)](https://www.iis.net/downloads/microsoft/web-deploy)
- [Windows Server Update Services](https://technet.microsoft.com/library/hh852339.aspx)
- [MultiPoint Services](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/multipoint-services/multipoint-services-migrate)
 
## <a name="windows-server-2012-r2"></a>Windows Server 2012 R2

### <a name="migration-guides"></a>移行ガイド
Windows Server 2003、Windows Server 2008、Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2 のいずれかを実行しているサーバーの役割と機能を Windows Server 2012 R2 に移行する場合は、以下のガイドの手順に従ってください。 Windows Server 2012 R2 の Windows Server 移行ツールでは、クロス サブネットの移行がサポートされています。

- [インストール、使用、および Windows Server 移行ツールを削除します。](https://technet.microsoft.com/library/jj134202.aspx)
- [Windows Server 2012 R2 の active Directory 証明書サービス移行ガイド](https://technet.microsoft.com/library/dn486797.aspx)
- [Windows Server 2012 R2 に Active Directory フェデレーション サービス役割サービスを移行します。](https://technet.microsoft.com/library/dn486815.aspx)
- [Active Directory Rights Management サービスの移行とアップグレード ガイド](https://technet.microsoft.com/library/cc754277.aspx)
- [Windows Server 2012 R2 へのファイル サービスおよび記憶域サービスを移行します。](https://technet.microsoft.com/library/dn479292.aspx)
- [Windows Server 2012 から Windows Server 2012 R2 への Hyper-V の移行](https://technet.microsoft.com/library/dn486799.aspx)
- [Windows Server 2012 へのネットワーク ポリシー サーバーを移行します。](https://technet.microsoft.com/library/hh831652)
- [Windows Server 2012 R2 へのリモート デスクトップ サービスを移行します。](https://technet.microsoft.com/library/dn479239.aspx)
- [Windows Server 2012 R2 への Windows Server Update Services を移行します。](https://technet.microsoft.com/library/hh852339.aspx)
- [Windows Server 2012 R2 へのクラスターの役割を移行します。](https://technet.microsoft.com/library/dn530779.aspx)
- [Windows Server 2012 R2 への DHCP サーバーを移行します。](https://technet.microsoft.com/library/dn495425.aspx)
 
## <a name="windows-server-2012"></a>Windows Server 2012

### <a name="migration-guides"></a>移行ガイド
Windows Server 2003、Windows Server 2008、Windows Server 2008 R2、Windows Server 2012 のいずれかを実行しているサーバーの役割と機能を Windows Server 2012 に移行する場合は、以下のガイドの手順に従ってください。 Windows Server 2012 の Windows Server 移行ツールでは、クロス サブネットの移行がサポートされています。

- [インストール、使用、および Windows Server 移行ツールを削除します。](https://technet.microsoft.com/library/jj134202)
- [Windows Server 2012 への Active Directory フェデレーション サービス役割サービスを移行します。](https://technet.microsoft.com/library/jj647765)
- [Windows Server 2012 への正常性登録機関を移行します。](https://technet.microsoft.com/library/hh831513)
- [Windows Server 2008 R2 から Windows Server 2012 への HYPER-V の移行します。](https://technet.microsoft.com/library/jj574113)
- [Windows Server 2012 への IP 構成を移行します。](https://technet.microsoft.com/library/jj574133)
- [Windows Server 2012 へのネットワーク ポリシー サーバーを移行します。](https://technet.microsoft.com/library/hh831652)
- [移行の印刷とドキュメント Windows Server 2012 へのサービス](https://technet.microsoft.com/library/jj134150)
- [Windows Server 2012 へのリモート アクセスを移行します。](https://technet.microsoft.com/library/hh831423)
- [Windows Server 2012 への Windows Server Update Services を移行します。](https://technet.microsoft.com/library/hh852339)
- [Active Directory ドメイン コント ローラーを Windows Server 2012 にアップグレードします。](https://technet.microsoft.com/library/hh994618.aspx)
- [クラスター化されたサービスとアプリケーションを Windows Server 2012 に移行します。](https://technet.microsoft.com/library/dn486790.aspx)
 

移行に関するその他の資料については、「[Windows Server への役割と機能の移行](https://technet.microsoft.com/library/jj134039)」をご覧ください。

## <a name="windows-server-2008-r2"></a>Windows Server 2008 R2

### <a name="migration-guides"></a>移行ガイド
Windows Server 2003、Windows Server 2008、Windows Server 2008 R2 のいずれかを実行しているサーバーの役割と機能を Windows Server 2008 R2 に移行する場合は、以下のガイドの手順に従ってください。 Windows Server 2008 R2 の Windows Server 移行ツールでは、クロス サブネットの移行はサポートされていません。

- [Windows Server 移行ツールのインストール、アクセス、および削除](https://technet.microsoft.com/library/dd379545)
- [Active Directory 証明書サービス移行ガイド](https://technet.microsoft.com/library/ee126170)
- [Active Directory Domain Services とドメイン名システム (DNS) サーバーの移行ガイド](https://technet.microsoft.com/library/dd379558)
- [BranchCache 移行ガイド](https://technet.microsoft.com/library/dd548365)
- [動的ホスト構成プロトコル (DHCP) サーバーの移行ガイド](https://technet.microsoft.com/library/dd379535)
- [ファイル サービスの移行ガイド](https://technet.microsoft.com/library/dd379487)
- [HRA 移行ガイド](https://technet.microsoft.com/library/ee791829)
- [HYPER-V 移行ガイド](https://technet.microsoft.com/library/ee849855)
- [IP Configuration Migration Guide](https://technet.microsoft.com/library/dd379537)
- [ローカル ユーザーとグループの移行ガイド](https://technet.microsoft.com/library/dd379531)
- [NPS 移行ガイド](https://technet.microsoft.com/library/ee791849)
- [印刷サービス移行ガイド](https://technet.microsoft.com/library/dd379488)
- [リモート デスクトップ サービス移行ガイド](https://technet.microsoft.com/library/ff849223)
- [RRAS の移行ガイド](https://technet.microsoft.com/library/ee822825)
- [Windows Server 移行の一般的なタスクと情報](https://technet.microsoft.com/library/ff400258)
- [Windows Server Update Services 3.0 SP2 移行ガイド](https://technet.microsoft.com/library/ee822826)  
移行に関するその他の資料については、「[Migrate Roles and Features to Windows Server 2008 R2 (Windows Server 2008 R2 への役割と機能の移行)](https://technet.microsoft.com/library/dd365353)」をご覧ください。
