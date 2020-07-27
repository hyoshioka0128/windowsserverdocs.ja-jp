---
title: 役割と機能の移行
description: 役割と機能を新しいバージョンの Windows Server に移行する方法について説明します。
ms.prod: windows-server
ms.date: 08/28/2019
ms.technology: server-general
ms.topic: article
ms.assetid: 0f78ef4c-dd12-4b1b-8c6e-251dd803c5d1
author: jasongerend
ms.author: jgerend
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 538ea2d6e0f038a98b64a197bd49ed5719fe15ac
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86959574"
---
# <a name="migrating-roles-and-features-in-windows-server"></a>Windows Server の役割と機能を移行する

> 適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このページでは、新しいバージョンの Windows Server への役割と機能の移行に役立つ情報やツールへのリンクを示します。 [記憶域の移行サービス](../storage/storage-migration-service/overview.md)を使用してファイル サーバーと記憶域を移行できますが、その他の多くの役割と機能は、Windows Server 2008 R2 で役割と機能の移行のために導入された一連の PowerShell コマンドレットである Windows Server 移行ツールを使用して移行できます。

移行ガイドは、2 台のサーバー間で、指定した役割や機能を移行する作業について記載されています (インプレース アップグレードは対象外です)。 ガイドの中で特に断りのない限り、移行は物理コンピューターと仮想コンピューターの間において、完全なインストール オプションの Windows Server と Server Core インストール オプションを実行しているサーバー間でサポートされます。

## <a name="before-you-begin"></a>開始する前に

役割と機能の移行を開始する前に、移行元と移行先の両方のサーバーが、それぞれのオペレーティング システムで利用可能な最新のサービス パックを実行していることを確認します。 

> [!NOTE]
> Windows Server のどのバージョンに移行またはアップグレードする場合も、[サポート ライフサイクル ポリシー](https://support.microsoft.com/lifecycle)および対象バージョンのサポート期間を確認し把握したうえで、それに応じて計画を立てる必要があります。 特定の Windows Server リリースのライフサイクルについては、[こちらでご検索ください](https://support.microsoft.com/lifecycle)。

## <a name="windows-server-2019"></a>Windows Server 2019

ファイル サーバーと記憶域を Windows Server 2019 または Windows Server 2016 に移行するには、[記憶域の移行サービス](../storage/storage-migration-service/overview.md)を使用することをお勧めします。 他の役割を移行するには、Windows Server 2016 および Windows Server 2012 R2 のガイダンスを参照してください。

## <a name="windows-server-2016"></a>Windows Server 2016

ここでは、Windows Server 2016 の移行ガイドを示します。 多くの場合、Windows Server 2012 R2 の移行ガイドを使用することもできます。

- [リモート デスクトップ サービス](../remote/remote-desktop-services/migrate-rds-role-services.md)
- [Web サーバー (IIS)](https://www.iis.net/downloads/microsoft/web-deploy)
- [Windows Server Update Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852339(v=ws.11))
- [MultiPoint Services](../remote/multipoint-services/multipoint-services-migrate.md)

ファイル サーバーを Windows Server 2019 または Windows Server 2016 に移行するには、[記憶域の移行サービス](../storage/storage-migration-service/overview.md)を使用することをお勧めします。

## <a name="windows-server-2012-r2"></a>Windows Server 2012 R2

Windows Server 2003、Windows Server 2008、Windows Server 2008 R2、Windows Server 2012、Windows Server 2012 R2 のいずれかを実行しているサーバーの役割と機能を Windows Server 2012 R2 に移行する場合は、以下のガイドの手順に従ってください。 Windows Server 2012 R2 の Windows Server 移行ツールでは、クロス サブネットの移行がサポートされています。

- [Windows Server 移行ツールのインストール、使用、および削除](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134202(v=ws.11))
- [Windows Server 2012 R2 用 Active Directory 証明書サービス移行ガイド](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486797(v=ws.11))
- [Windows Server 2012 R2 への Active Directory フェデレーション サービス役割サービスの移行](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486815(v=ws.11))
- [Active Directory Rights Management サービスの移行およびアップグレード ガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754277(v=ws.10))
- [Windows Server 2012 R2 へのファイル サービスおよび記憶域サービスの移行](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn479292(v=ws.11))
- [Windows Server 2012 から Windows Server 2012 R2 への Hyper-V の移行](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486799(v=ws.11))
- [Windows Server 2012 へのネットワーク ポリシー サーバーの移行](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831652(v=ws.11))
- [Windows Server 2012 R2 へのリモート デスクトップ サービスの移行](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn479239(v=ws.11))
- [Windows Server 2012 R2 への Windows Server Update Services の移行](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852339(v=ws.11))
- [Windows Server 2012 R2 へのクラスターの役割の移行](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn530779(v=ws.11))
- [Windows Server 2012 R2 への DHCP サーバーの移行](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn495425(v=ws.11))

Windows Server 2012 R2 と Windows Server 2012 の移行ガイドは、電子書籍版が提供されています。 詳細および電子書籍のダウンロードについては、「[E-Book Gallery for Microsoft Technologies (マイクロソフト テクノロジ電子書籍ギャラリー)](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#MigrateRoles)をご覧ください。

## <a name="windows-server-2012"></a>Windows Server 2012

Windows Server 2003、Windows Server 2008、Windows Server 2008 R2、Windows Server 2012 のいずれかを実行しているサーバーの役割と機能を Windows Server 2012 に移行する場合は、以下のガイドの手順に従ってください。 Windows Server 2012 の Windows Server 移行ツールでは、クロス サブネットの移行がサポートされています。

- [Windows Server 移行ツールのインストール、使用、および削除](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134202(v=ws.11))
- [Windows Server 2012 への Active Directory フェデレーション サービス (AD FS) 役割サービスの移行](../identity/ad-fs/deployment/migrate-ad-fs-role-services-to-windows-server-2012.md)
- [Windows Server 2012 への正常性登録機関の移行](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831513(v=ws.11))
- [Windows 2008 R2 から Windows Server 2012 への Hyper-V の移行](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574113(v=ws.11))
- [Windows Server 2012 への IP 構成の移行](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574133(v=ws.11))
- [Windows Server 2012 へのネットワーク ポリシー サーバーの移行](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831652(v=ws.11))
- [Windows Server 2012 への印刷とドキュメント サービスの移行](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134150(v=ws.11))
- [Windows Server 2012 へのリモート アクセスの移行](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831423(v=ws.11))
- [Windows Server 2012 への Windows Server Update Services の移行](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852339(v=ws.11))
- [Active Directory ドメイン コントローラーを Windows Server 2012 にアップグレードする](../identity/ad-ds/deploy/upgrade-domain-controllers-to-windows-server-2012-r2-and-windows-server-2012.md)
- [クラスター化されたサービスとアプリケーションの Windows Server 2012 への移行](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486790(v=ws.11))
 

移行に関するその他の資料については、「[Windows Server への役割と機能の移行](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134039(v=ws.11))」をご覧ください。

## <a name="windows-server-2008-r2"></a>Windows Server 2008 R2

Windows Server 2003、Windows Server 2008、Windows Server 2008 R2 のいずれかを実行しているサーバーの役割と機能を Windows Server 2008 R2 に移行する場合は、以下のガイドの手順に従ってください。 Windows Server 2008 R2 の Windows Server 移行ツールでは、クロス サブネットの移行はサポートされていません。

- [Windows Server 移行ツールのインストール、アクセス、および削除](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379545(v=ws.10))
- [Active Directory 証明書サービス移行ガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee126170(v=ws.10))
- [Active Directory Domain Services とドメイン ネーム システム (DNS) サーバーの移行ガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379558(v=ws.10))
- [BranchCache 移行ガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd548365(v=ws.10))
- [動的ホスト構成プロトコル (DHCP) サーバーの移行ガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379535(v=ws.10))
- [ファイル サービスの移行ガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379487(v=ws.10))
- [HRA 移行ガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee791829(v=ws.10))
- [Hyper-V 移行ガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee849855(v=ws.10))
- [IP 構成移行ガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379537(v=ws.10))
- [ローカル ユーザーとグループ移行のガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379531(v=ws.10))
- [NPS 移行ガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee791849(v=ws.10))
- [印刷サービス移行ガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379488(v=ws.10))
- [リモート デスクトップ サービスの移行ガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff849223(v=ws.10))
- [RRAS 移行ガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee822825(v=ws.10))
- [Windows Server の移行に関する一般的なタスクと情報](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff400258(v=ws.10))
- [Windows Server Update Services 3.0 SP2 移行ガイド](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee822826(v=ws.10))
 
移行に関するその他の資料については、「[Migrate Roles and Features to Windows Server 2008 R2 (Windows Server 2008 R2 への役割と機能の移行)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd365353(v=ws.10))」をご覧ください。
