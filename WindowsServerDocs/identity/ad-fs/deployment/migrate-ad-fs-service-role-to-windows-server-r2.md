---
title: Windows Server 2012 R2 への Active Directory フェデレーション サービス (AD FS) 役割サービスの移行
description: AD FS サービスを Windows Server 2012 R2 に移行する手順について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.openlocfilehash: 49c75fadcbc1284f23b490eb6ee48813ef40f781
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970909"
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012-r2"></a>Windows Server 2012 R2 への Active Directory フェデレーション サービス (AD FS) 役割サービスの移行
 このドキュメントでは、Windows Server 2012 R2 と共にインストールされる Active Directory フェデレーションサービス (AD FS) (AD FS) に次の役割サービスを移行する手順について説明します。

-   Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーション サーバー

-   Windows Server 2012 にインストールされている AD FS フェデレーション サーバー

## <a name="supported-migration-scenarios"></a>サポートされる移行シナリオ
 このガイドで説明する移行手順は次のタスクで構成されています。

- Windows Server 2008、Windows Server 2008 R2、または Windows Server 2012 を実行しているサーバーから AD FS 2.0 の構成データをエクスポートする

- Windows Server 2008、Windows Server 2008 R2、または Windows Server 2012 から Windows Server 2012 R2 への、このサーバーのオペレーティングシステムの一括アップグレードを実行します。

- 元の AD FS 構成を再作成し、このサーバーの残りの AD FS サービス設定を復元します。これで、Windows Server 2012 R2 と共にインストールされる AD FS サーバーロールが実行されます。

  このガイドでは、複数の役割を実行しているサーバーを移行する手順は取り上げません。 サーバーで複数の役割が実行されている場合は、他の役割の移行ガイドで説明されている情報に基づいて、サーバー環境に合わせたカスタムの移行プロセスを設計することをお勧めします。 他の役割に関する移行ガイドは、「[Windows Server の移行に関するポータル](https://go.microsoft.com/fwlink/?LinkId=247608)」を参照してください。

### <a name="supported-operating-systems"></a>サポートされるオペレーティング システム
 移行先サーバーのオペレーティングシステム:

 Windows Server 2012 R2 (Server Core およびフルインストールオプション)

 移行先サーバーのプロセッサ:

 x64 ベース

|移行元サーバーのプロセッサ|移行元サーバーのオペレーティング システム|
|-----------------------------|------------------------------------|
|x86 または x64 ベース| Windows Server 2008 (フルインストールオプションと Server Core インストールオプションの両方)|
|x64 ベース|Windows Server 2008 R2|
|x64 ベース|Windows Server 2008 R2 の Server Core インストール オプション|
|x64 ベース|Windows Server 2012 の server Core およびフルインストールオプション|

> [!NOTE]
> - 上の表で示したオペレーティング システムのバージョンは、サポートされている最も古い組み合わせでのオペレーティング システムとサービス パックについてのものです。
>   -   Windows Server オペレーティング システムの Foundation、Standard、Enterprise、Datacenter の各エディションは、移行元または移行先のサーバーとしてサポートされています。
>   -   物理的なオペレーティング システムと仮想化されたオペレーティング システム間での移行はサポートされています。

### <a name="supported-ad-fs-role-services-and-features"></a>サポートされている AD FS 役割サービスと機能
 次の表では、このガイドで説明している AD FS 役割サービスとそれらの各設定の移行シナリオについて説明します。

|From|Windows Server 2012 R2 と共にインストール AD FS には|
|----------|----------------------------------------------------------------------------------------------|
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーション サーバー|同じサーバーでの移行がサポートされています。 詳細については次を参照してください:<p> [AD FS フェデレーション サーバーの移行準備](prepare-migrate-ad-fs-server-r2.md)<p> [AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)|
|Windows Server 2012 にインストールされている AD FS フェデレーション サーバー|同じサーバーでの移行がサポートされています。  詳細情報<p> [AD FS フェデレーション サーバーの移行準備](prepare-migrate-ad-fs-server-r2.md)<p> [AD FS フェデレーション サーバーの移行](migrate-ad-fs-fed-server-r2.md)|

## <a name="next-steps"></a>次の手順
 [AD FS フェデレーションサーバーの移行の準備](prepare-migrate-ad-fs-server-r2.md) [AD FS フェデレーションサーバーの](migrate-ad-fs-fed-server-r2.md)移行[AD FS フェデレーションサーバープロキシの移行](migrate-fed-server-proxy-r2.md) [Windows Server 2012 R2 への AD FS の移行の検証](verify-ad-fs-migration.md)