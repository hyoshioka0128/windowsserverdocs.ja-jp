---
title: Windows Server 2012 への Active Directory フェデレーション サービス役割サービスの移行
description: AD FS サービスを Windows Server 2012 に移行する手順について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.openlocfilehash: abbd51daea374eb4684f5416bed45fb0aaf315d4
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938212"
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012"></a>Windows Server 2012 への Active Directory フェデレーション サービス役割サービスの移行

以下では、Windows Server 2012 の Active Directory フェデレーションサービス (AD FS) (AD FS) に次の役割サービスを移行する手順について説明します。

-   Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 1.1 Windows トークン ベースのエージェントおよび AD FS 1.1 要求に対応するエージェント

-   Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーション サーバーおよび AD FS 2.0 フェデレーション サーバー プロキシから移行する

## <a name="supported-migration-scenarios"></a>サポートされる移行シナリオ
 移行手順には、次のタスクが含まれています。

- Windows Server 2008 または Windows Server 2008 R2 を実行しているサーバーから AD FS 2.0 の構成データをエクスポートする

- Windows Server 2008 または Windows Server 2008 R2 から Windows Server 2012 への、このサーバーのオペレーティングシステムの一括アップグレードを実行します。

- 元の AD FS 構成を再作成し、このサーバーの残りの AD FS サービス設定を復元します。これで、Windows Server 2012 と共にインストールされる AD FS サーバーロールが実行されます。

  このガイドでは、複数の役割を実行しているサーバーを移行する手順は取り上げません。 サーバーで複数の役割が実行されている場合は、他の役割の移行ガイドで説明されている情報に基づいて、サーバー環境に合わせたカスタムの移行プロセスを設計することをお勧めします。 他の役割に関する移行ガイドは、「[Windows Server の移行に関するポータル](https://go.microsoft.com/fwlink/?LinkId=247608)」を参照してください。

## <a name="supported-operating-systems"></a>サポートされるオペレーティング システム
 **移行先サーバーのオペレーティングシステム:**


- Windows Server 2012 または Windows Server 2008 R2 (Server Core およびフルインストールオプション)

  **移行先サーバーのプロセッサ:**


- x64 ベース

|移行元サーバーのプロセッサ|移行元サーバーのオペレーティング システム|
|-----|-----|
|x86 または x64 ベース|Windows Server 2003 Service Pack 2|
|x86 または x64 ベース|Windows Server 2003 R2|
|x86 または x64 ベース|Windows Server 2008 (フルインストールオプションと Server Core インストールオプションの両方)|
|x64 ベース|Windows Server 2008 R2|
|x64 ベース|Windows Server 2008 R2 の Server Core インストール オプション|
|x64 ベース|Windows Server 2012 の server Core およびフルインストールオプション|

> [!NOTE]
> - 上の表で示したオペレーティング システムのバージョンは、サポートされている最も古い組み合わせでのオペレーティング システムとサービス パックについてのものです。
>   -   Windows Server オペレーティング システムの Foundation、Standard、Enterprise、Datacenter の各エディションは、移行元または移行先のサーバーとしてサポートされています。
>   -   物理的なオペレーティング システムと仮想化されたオペレーティング システム間での移行はサポートされています。

### <a name="supported-ad-fs-role-services-and-features"></a>サポートされている AD FS 役割サービスと機能
 次の表では、このガイドで説明している AD FS 役割サービスとそれらの各設定の移行シナリオについて説明します。

|From|Windows Server 2012 でインストールされた AD FS するには|
|----------|-----|
|Windows Server 2003 R2 にインストールされている AD FS 1.0 フェデレーション サーバー|移行はサポートされていません|
|Windows Server 2003 R2 にインストールされている AD FS 1.0 フェデレーション サーバー プロキシ|移行はサポートされていません|
|Windows Server 2003 R2 にインストールされている AD FS 1.0 Windows トークン ベースのエージェント|移行はサポートされていません|
|Windows Server 2003 R2 にインストールされている AD FS 1.0 要求に対応するエージェント|移行はサポートされていません|
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 1.1 フェデレーション サーバー|移行はサポートされていません|
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 1.1 フェデレーション サーバー プロキシ|移行はサポートされていません|
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 1.1 Windows トークン ベースのエージェント|同じサーバーでの移行はサポートされていませんが、移行された AD FS Windows トークン ベースのエージェントは、Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 1.1 フェデレーション サービスでのみ機能します。 詳細については次を参照してください:<p> [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)<p> [AD FS 1.x との相互運用](Interoperating-with-AD-FS-1.x.md)|
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 1.1 要求に対応するエージェント|同じサーバーでの移行がサポートされています。 移行された AD FS 1.1 要求に対応する Web エージェントは、次のサービスで機能します。<p> Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 1.1 フェデレーション サービス<p> Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーション サービス<p> Windows Server 2012 にインストールされている AD FS フェデレーションサービス<p> 詳細については次を参照してください:<p> [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)<p> [AD FS 1.x との相互運用](Interoperating-with-AD-FS-1.x.md)|
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーション サーバー|同じサーバーでの移行がサポートされています。 詳細については次を参照してください:<p> [AD FS 2.0 フェデレーション サーバーの移行の準備](prepare-to-migrate-ad-fs-fed-server.md)<p> [AD FS 2.0 フェデレーション サーバーの移行](migrate-the-ad-fs-fed-server.md)|
|Windows Server 2008 または Windows Server 2008 R2 にインストールされている AD FS 2.0 フェデレーション サーバー プロキシ|同じサーバーでの移行がサポートされています。  詳細情報<p> [AD FS 2.0 フェデレーション サーバー プロキシの移行の準備](prepare-to-migrate-ad-fs-fed-proxy.md)<p> [AD FS 2.0 フェデレーション サーバー プロキシの移行](migrate-the-ad-fs-2-fed-server-proxy.md)|

## <a name="see-also"></a>参照
 [AD FS 2.0 フェデレーションサーバーの移行の準備](prepare-to-migrate-ad-fs-fed-server.md) [AD FS 2.0 フェデレーションサーバープロキシ](prepare-to-migrate-ad-fs-fed-proxy.md)の移行の準備[AD FS 2.0 フェデレーションサーバー](migrate-the-ad-fs-fed-server.md) [AD FS 2.0 フェデレーションサーバープロキシの](migrate-the-ad-fs-2-fed-server-proxy.md)移行[AD FS 1.1 Web エージェントの](migrate-the-ad-fs-web-agent.md)移行