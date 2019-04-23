---
title: Windows Server のハイブリッド クラウド印刷の概要
description: BYOD またはドメインの印刷の要件をサポートする IT プロフェッショナルは、ハイブリッド クラウドの印刷デバイスを参加させます。
ms.prod: w10
ms.mktglfcycl: manage
ms.sitesec: library
ms.pagetype: store
ms.technology: server-general
author: TrudyHa
ms.author: TrudyHa
ms.date: 10/16/2017
ms.openlocfilehash: faa9fde857a9a4ee3f7c03f682b3dbced0340417
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878833"
---
# <a name="windows-server-hybrid-cloud-print-overview"></a>Windows Server のハイブリッド クラウド印刷の概要

**適用対象**
-   Windows Server 2016

## <a name="what-is-hybrid-cloud-print"></a>ハイブリッド クラウドの印刷とは何ですか。
**ハイブリッド クラウドの印刷**を Windows Server 2016 の新機能を利用**オンデマンド機能**します。 これにより、自分のデバイス、または Azure Active Directory に参加しているデバイスを使用して、ユーザーの印刷の要件をサポートする IT プロフェッショナルができます。 これには、Windows Phone、ラップトップ、または Windows 10 または Windows Mobile を実行するタブレットなどのモバイル デバイスが含まれます。 印刷のサポートを提供人どこからでもインターネットへのアクセスがあります。

IT 管理者は、の**Hybrid Cloud Print**ユーザー アクセスを検証する Azure の multi-factor authentication を使用して、オンプレミスでプリンターへのユーザーのセキュリティで保護されたアクセスを提供します。 シングル サインオン (SSO) 機能は、ユーザー エクスペリエンスを簡略化します。 **ハイブリッド クラウドの印刷**は Windows 上に構築**プリント サーバー**ロール、IT プロフェッショナルと同じように、プリンターとユーザー アクセス セキュリティの管理エクスペリエンスを提供します。

**ハイブリッド クラウドの印刷**デスクや職場から離れている場合でも、作業が完了するように使用されるデバイスから印刷する、組織内のユーザーを許可します。

**ハイブリッド クラウドの印刷**Windows 10 Creators Update および Windows 10 s. でサポートされます
 
## <a name="feature-summary"></a>機能の概要
**ハイブリッド クラウドの印刷**の 2 つの主要なサーバー側コンポーネントで構成されます。**探索**サービス、および**Windows 印刷**サービス。
- **探索**クラウド プリンター検出 Mopria Alliance の業界標準をサポートしている IIS サービスで実行されているサービス エンドポイント。
- **Windows 印刷**業界をサポートしている IIS サービスで実行されているサービス エンドポイント標準インターネット印刷プロトコル (IPP) させる最も広範なクライアント OS をサポートします。

## <a name="deployment"></a>展開
**ハイブリッド クラウドの印刷**いくつかの組織がユーザー認証を必要に応じてさまざまな展開オプションをサポートしています。 どのような展開ようになります。 次に示します。

![クラウド印刷のハイブリッド ソリューションのグラフィック描写を示す図](../media/hybrid-cloud-print/wshcp-deployment-options.png)

*ハイブリッド クラウド印刷のソリューションの図*

図を示しています。
- **ハイブリッド クラウドの印刷**ユーザーの id プロバイダーとして Azure Active Directory を使用します。 
- **Windows 印刷**サービスと**検出**サービス エンドポイントは、これらのサービスに対して使用する必要なユーザーの認証トークンを取得するクライアント デバイスを有効にする Azure Active Directory に登録されています。 
- MDM サービスなど**Microsoft Intune**、Azure Active Directory を接続に必要なポリシーをクライアント デバイスをプロビジョニング**Windows 印刷**サービスと**検出**サービス。

このテーブルでは、ダイアグラム内の要素の詳細があります。  

| 要素 | 説明 |
| ------- | ----------- |
| Azure Active Directory  | 提供し、ユーザー id と承認の機能を制御 |
| Active Directory        | 提供し、ユーザー id と承認の機能を制御 |
| Azure AD Connect  | Azure AD の間でユーザーの資格情報を同期して、オンプレミスの AD。 |
| MDM サービス (Intune) | 企業のポリシーに準拠しているクライアント デバイス (BYOD デバイス) を確認するデバイス ポリシーのプロビジョニング機能を提供します。 |
| Azure AD プロキシ | Azure に企業ネットワークに、インターネットから構成されている特定のアプリケーションのトラフィックを許可するファイアウォールの背後から確立されている有効期間が長い接続を提供します。 |
| Azure Web アプリ | クラウド印刷のハイブリッド ソリューションの中核です。 プリンターを検出して非ドメイン参加済みデバイスの印刷内容の送信に必要な web エンドポイントを提供します。 |
| BYOD デバイス]、[Windows 印刷スプーラーのサーバー/プリンター | これらとして-は。 展開内の機能の変更はありません。 |

インストールする 2 つの方法がある**Hybrid Cloud Print**:
- **オンデマンド機能**-を参照してください[Windows Server でのオンデマンド機能の構成](https://docs.microsoft.com/windows-server/administration/server-manager/configure-features-on-demand-in-windows-server)詳細の追加と削除の役割と機能のファイルについてはします。 
- **Windows Server 2016 設定**-管理者に移動して**設定** -> **アプリ** -> **省略可能な機能を管理する** -> **機能を追加**と必要に応じてパッケージの機能の検索 
- PowerShell コマンド - 管理者ウィンドウで、PowerShell で、これらのコマンドを実行します。

```PowerShell
    Install-Module -Name PublishCloudPrinter
    Import-Module PublishCloudPrinter
    ```
