---
title: リモート デスクトップ サービスにおいてサポートされる構成
description: Windows Server 2016 の RDS においてサポートされる構成に関する情報を示します。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 12/20/2018
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c925c7eb-6880-411f-8e59-bd0f57cc5fc3
author: lizap
manager: dongill
ms.openlocfilehash: 7363fe3eee33a5345a25c8df9e4216b9eda7e3b2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403810"
---
# <a name="supported-configurations-for-remote-desktop-services-in-windows-server-2016"></a>Windows Server 2016 のリモート デスクトップ サービスにおいてサポートされる構成

> 適用先:Windows Server 2016

リモート デスクトップ サービス環境においてサポートされる構成に関しては、最大の懸念事項がバージョンの相互運用性になる傾向があります。 ほとんどの環境には、複数のバージョンの Windows Server が含まれます。たとえば、既存の Windows Server 2012 R2 の RDS を展開しているが、Windows Server 2016 にアップグレードして新しい機能 (OpenGL\OpenCL、個別のデバイス割り当て、記憶域スペース ダイレクトのサポートなど) を活用したい場合があります。 ここで、問題になるのは、どの RDS コンポーネントによってさまざまなバージョンを操作できるのか、また、同一でなければならないのはどれか、という点です。

そのことを念頭に置いて、ここでは Windows Server 2016 でサポートされるリモート デスクトップ サービスの構成に関する基本のガイドラインを示します。

> [!NOTE]
> [Windows Server 2016 のシステム要件](../../get-started/system-requirements.md)を必ず確認してください。

## <a name="best-practices"></a>ベスト プラクティス
- リモート デスクトップのインフラストラクチャ (Web アクセス、ゲートウェイ、接続ブローカー、およびライセンス サーバー) に Windows Server 2016 を使用します。 Windows Server 2016 は、これらのコンポーネントに対する下位互換性を備えています。そのため、2012 R2 RD セッション ホストから 2016 RD 接続ブローカーに接続することはできますが、逆はできません。

- RD セッション ホストの場合、1 つのコレクション内にあるすべてのセッション ホストが同一レベルになっている必要がありますが、コレクションを複数保持することが可能です。 Windows Server 2012 R2 のセッション ホストによる 1 つのコレクションと、Windows Server 2016 のセッション ホストによるもう 1 つを保持することができます。

- RD セッション ホストを Windows Server 2016 にアップグレードする場合は、ライセンス サーバーもアップグレードしてください。 2016 ライセンス サーバーでは、Windows Server 2003 に遡るまで、以前のすべての Windows Server バージョンからの CAL を処理できることを覚えておいてください。

- [リモート デスクトップ サービス環境のアップグレード](upgrade-to-rds.md#flow-for-deployment-upgrades)に関する記事で推奨されているアップグレード順序に従ってください。 

- 高可用性環境を構築している場合、すべての接続ブローカーが同一の OS レベルになっている必要があります。

## <a name="rd-connection-brokers"></a>RD 接続ブローカー

Windows Server 2016 も実行しているリモート デスクトップ セッション ホスト (RDSH) およびリモート デスクトップ仮想化ホスト (RDVH) を使用している場合、Windows Server 2016 では、展開に含めることができる接続ブローカー数の制限を取り外しています。 次の表は、3 つ以上の接続ブローカーを備えた高可用性の展開において、どのバージョンの RDS コンポーネントによって 2016 および 2012 R2 バージョンの接続ブローカーを利用できるかを示しています。

| HA における 3 つ以上の接続ブローカー              | RDSH 2016 | RDVH 2016 | RDSH 2012 R2  | RDVH 2012 R2  |
|------------------------------------------|-----------|-----------|---------------|---------------|
| Windows Server 2016 の接続ブローカー    | サポート対象 | サポート対象 | サポート対象     | サポート対象     |
| Windows Server 2012 R2 の接続ブローカー | 該当なし       | 該当なし       | サポート対象     | サポート対象     |

## <a name="support-for-gpu-acceleration-with-hyper-v"></a>Hyper-V による GPU アクセラレーションのサポート
次の表は、仮想マシン上での GPU アクセラレーションのサポートに関する詳細を示しています。 何が必要かを明確にするには、「[Which graphics virtualization technology is right for you? (どのグラフィックス仮想化技術が適切か)](rds-graphics-virtualization.md)」をご覧ください。 DDA に関する特定の情報については、[個別のデバイス割り当てを展開する計画](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md)に関するページを参照してください。

|VM ゲスト OS  |Windows Server 2012 R2 または Windows Server 2016<br> HYPER-V の RemoteFX vGPU (Gen 1 VM) |  Windows Server 2016 HYPER-V の RemoteFX vGPU (Gen 2 VM) |  Windows Server 2016 Hyper-V の個別のデバイス割り当て (Gen 2 VM) |
|-----------------------------|------------------------------------------------------------|--------------------------------------------------------|---------------------------------------------------------------------|
| Windows 7 SP1               | 〇                                                        | X                                                     | X                                                                  |
| Windows 8.1                 | 〇                                                        | X                                                     | X                                                                  |
| Windows 10 1511 Update      | 〇                                                        | 〇                                                    | 〇                                                                 |
| Windows Server 2012 R2      | 〇                                                        | X                                                     | はい (KB 3133690 が必要)                                           |
| Windows Server 2016         | 〇                                                        | 〇                                                    | 〇                                                                 |
| Windows Server 2012 R2 RDSH | X                                                         | X                                                     | はい (KB 3133690 が必要)                                           |
| Windows Server 2016 RDSH    | X                                                         | X                                                     | 〇                                                                 |
## <a name="vdi-deployment--supported-guest-oss"></a>VDI の展開 – サポートされているゲスト OS 
Windows Server 2016 RD 仮想化ホスト サーバーでは、次のゲスト OS がサポートされます。

- Windows 10 Enterprise
- Windows 8.1 Enterprise 
- Windows 8 Enterprise 
- Windows 7 SP1 Enterprise 

次の表に、サポートされている RD 仮想化ホスト オペレーティング システムとゲスト オペレーティング システムの組み合わせを示します。

| RDVH OS バージョン        | ゲスト OS バージョン           |
| ------------- |-------------|
| Windows Server 2016      | Windows 7 SP1、Windows 8、Windows 8.1、Windows 10 |
| Windows Server 2012 R2   | Windows 7 SP1、Windows 8、Windows 8.1、Windows 10 |
| Windows Server 2012      | Windows 7 SP1、Windows 8、Windows 8.1 |

> [!NOTE]  
> - Windows Server 2016 リモート デスクトップ サービスでは、異種コレクションをサポートしていません。 1 つのコレクション内にあるすべての VM は、同じ OS バージョンになっている必要があります。 
> - 同じホスト上でさまざまなゲスト OS バージョンを利用して、別個の同種コレクションを保持することができます。 
> - VM テンプレートは、Windows Server 2016 Hyper-V ホスト上でゲスト OS として使用するために、Windows Server 2016 Hyper-V ホスト上に作成される必要があります。

## <a name="single-sign-on-sso"></a>シングル サインオン (SSO)
Windows Server 2016 の RDS では、2 つの主要な SSO エクスペリエンスがサポートされています。

 - アプリ内 (Windows、iOS、Android、および Mac 上のリモート デスクトップ アプリケーション)
 - Web SSO
 
リモート デスクトップ アプリケーションを使用して、各 OS に固有のメカニズムを通じて接続情報の一部 ([Mac](clients/remote-desktop-mac.md)) またはマネージド アカウントの一部 ([iOS](clients/remote-desktop-ios.md#manage-your-user-accounts)、[Android](clients/remote-desktop-android.md#manage-your-user-accounts)、Windows) として、安全に資格情報を格納できます。

Windows 上でインボックス リモート デスクトップ接続クライアントを通じて、SSO によってデスクトップおよび RemoteApps に接続するには、Internet Explorer から RD Web ページに接続する必要があります。 サーバー側では、次の構成オプションが必要になります。 Web SSO では、他の構成はサポートされていません。

 - フォーム ベース認証 (既定値) に設定された RD Web
 - パスワード認証 (既定値) に設定された RD ゲートウェイ
 - RD ゲートウェイのプロパティに [リモート コンピューター用の RD ゲートウェイ資格情報を使用する] (既定値) が設定された RDS の展開

> [!NOTE]
> 必須の構成オプションが原因で、スマートカードでは Web SSO はサポートされていません。 スマートカード経由でログインするユーザーには、ログインのために複数のプロンプトが表示される場合があります。

リモート デスクトップ サービスの VDI の展開の作成について詳しくは、「[リモート デスクトップ サービスの VDI でサポートされる Windows 10 のセキュリティ構成](rds-vdi-supported-config.md)」を確認してください。

## <a name="using-remote-desktop-services-with-application-proxy-services"></a>アプリケーション プロキシ サービスによってリモート デスクトップ サービスを使用する

Web クライアント以外では、[Azure AD のアプリケーション プロキシ](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-remote-desktop)を利用して、リモート デスクトップ サービスを使用できます。 リモート デスクトップ サービスでは、Windows Server 2016 および以前のバージョンに含まれる [Web アプリケーション プロキシ](https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server)の使用は、サポートされません。
