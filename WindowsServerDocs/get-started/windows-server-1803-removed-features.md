---
title: Windows Server バージョン 1803 - 削除された機能
description: Windows Server バージョン 1803 または今後のリリースで削除または推奨されなくなる機能について説明します
ms.prod: windows-server
ms.mktglfcycl: plan
ms.localizationpriority: medium
ms.sitesec: library
author: jasongerend
ms.author: jgerend
ms.date: 10/22/2019
ms.openlocfilehash: c3c948e447d060d1ce733778c3362d83ad116708
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "75948201"
---
# <a name="features-removed-or-planned-for-replacement-starting-with-windows-server-version-1803"></a>Windows Server バージョン 1803 以降で削除された機能と置換が計画されている機能

> 適用先:Windows Server バージョン 1803

Windows Server の各リリースでは新機能が追加されます。また、機能が削除される場合もあります。これは、通常、より優れたオプションが追加されたためです。 Windows Server バージョン 1803 で削除された機能の詳細を次に示します。   

> [!TIP]
> - [Windows Insider プログラム](https://insider.windows.com)に参加することで Windows Server ビルドにいち早くアクセスできます。これは、機能の変更をテストするための最適な方法です。
> - その他のリリースに関する質問がある場合 「[Windows Server で削除された機能と置換が計画されている機能](../get-started-19/removed-features.md)」をご覧ください。

**この一覧は変更される可能性があります。また、影響を受ける機能でこの一覧に含まれていないものもあります。** 

## <a name="features-we-removed-in-this-release"></a>このリリースで削除された機能

Windows Server バージョン 1803 でインストールされている製品イメージから次の機能を削除しました。 これらの機能に依存するアプリケーションまたはコードは、別の方法を使用しない限りこのリリースでは機能しません。   

| 機能    | 代わりに使用できる機能 |
| ----------- | -------------------- |
| [ファイル レプリケーション サービス](https://support.microsoft.com/help/4025991/windows-server-version-1709-no-longer-supports-frs)|Windows Server 2003 R2 で導入されたファイル レプリケーション サービスは、DFS レプリケーションに置き換えられました。 [FRS を使用するドメイン コントローラーを SYSVOL による DFS レプリケーションに移行する](https://blogs.technet.microsoft.com/filecab/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol/)必要があります。 |
| Hyper-V ネットワーク仮想化 (HNV)|[ネットワークの仮想化](../networking/sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md)は、[ソフトウェア定義ネットワーク](../networking/sdn/software-defined-networking.md) (SDN) ソリューションの一部として Windows Server に含まれるようになりました。ソリューションには、ネットワーク コントローラー、ソフトウェア負荷分散、ユーザー定義ルーティング、アクセス制御リストも含まれます。 |

## <a name="features-were-no-longer-developing"></a>開発を行っていない機能

次の機能の開発は積極的には行われなくなりました。今後の更新プログラムから削除される可能性があります。 他の機能に置き換えられた機能と、現在さまざまなソースから利用可能な機能があります。 

>[!NOTE]
> 次に説明する一部の機能と役割は、Windows Server バージョン 1803 で提供される、Server Core のインストール オプションには含まれていません。 デスクトップ エクスペリエンス搭載サーバーのインストール オプションには "*含まれています*"。これは、Windows Server 2016 で最後にリリースされ、Windows Server 2019 で再リリースされる予定です。

提案されているこれらの機能の置換についてフィードバックがある場合は、[フィードバック Hub アプリ](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)を使用できます。 

| 機能または役割    | 代わりに使用できる機能 |
| ----------- | --------------------- |
| ビジネス スキャン (分散スキャン管理 (DSM) とも呼ばれます)|[スキャン管理機能](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd759124\(v%3dws.11\))は Windows Server 2008 R2 で導入され、セキュリティで保護されたスキャンおよびエンタープライズ内のスキャナーの管理が可能になりました。 この機能への投資は行われなくなっており、サポートするデバイスは提供されていません。 |
| IPv4/6 移行テクノロジ (6to4、ISATAP、および Direct Tunnels)|Windows 10 バージョン 1607 (Anniversary Update) 以降、6to4 は既定で無効になり、Windows 10 バージョン 1703 (Creators Update) 以降、ISATAP は既定で無効になり、Direct Tunnels は常に既定で無効になっています。 代わりに、ネイティブ IPv6 サポートを使用してください。 |
| [MultiPoint Services](../remote/multipoint-services/multipoint-services.md)|現在、Windows Server の一部として MultiPoint Services の役割の開発は行われなくなりました。 MultiPoint Connector サービスは、[オンデマンド機能](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities)によって Windows Server と Windows 10 の両方で利用可能です。 [リモート デスクトップ サービス](../remote/remote-desktop-services/welcome-to-rds.md) (特に、リモート デスクトップ サービス セッション ホスト) を使用して RDP 接続を提供できます。 |
| [オフラインのシンボル パッケージ](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-symbols) (デバッグ シンボル MSI)|シンボル パッケージをダウンロード可能な MSI として利用できなくなりました。 代わりに、[Microsoft シンボル サーバーは Azure ベースのシンボル ストアに移行しています](https://blogs.msdn.microsoft.com/windbg/2017/10/18/update-on-microsofts-symbol-server/)。 Windows シンボルが必要な場合は、Microsoft シンボル サーバーに接続してシンボルをローカルにキャッシュするか、またはインターネットにアクセスできるコンピューター上で SymChk.exe によりマニフェスト ファイルを使用します。 |
| Server Core インストールでの[リモート デスクトップ接続ブローカーおよびリモート デスクトップ仮想化ホスト](../remote/remote-desktop-services/desktop-hosting-service.md)|ほとんどのリモート デスクトップ サービスの展開には、リモート デスクトップ セッション ホスト (RDSH) と共存するこれらの役割があり、RDSH にはデスクトップ エクスペリエンス搭載サーバーが必要になります。RDSH との一貫性が保たれるように、これらの役割でもデスクトップ エクスペリエンス搭載サーバーを必要とするように変更を行っています。 [Server Core インストール](../administration/server-core/what-is-server-core.md)で使用するためのこれらの RDS 役割の開発は行われなくなりました。 [リモート デスクトップ インフラストラクチャの一部としてこれらの役割を展開する](../remote/remote-desktop-services/rds-deploy-infrastructure.md)必要がある場合は、[デスクトップ エクスペリエンスを搭載した Windows Server 2016 に役割をインストールする](getting-started-with-server-with-desktop-experience.md)ことができます。 <br/><br/>これらの役割は、Windows Server 2019 のデスクトップ エクスペリエンスのインストール オプションにも含まれています。 [Windows Server 2019 の Windows Insider ビルド](https://docs.microsoft.com/windows-insider/at-work/)上でテストすることもできます。必ず LTSC イメージを選択してください。 |
| [RemoteFX 3D ビデオ アダプター (vGPU)](../remote/remote-desktop-services/rds-remotefx-vgpu.md)|仮想化環境のための新しいグラフィック アクセラレータ オプションを開発しています。 [個別のデバイスの割り当て (DDA)](../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md) を代わりに使用することもできます。 |
| グループ ポリシーの[ソフトウェア制限ポリシー](../identity/software-restriction-policies/software-restriction-policies.md)|グループ ポリシーを介してソフトウェア制限ポリシーを使用する代わりに、[AppLocker](https://docs.microsoft.com/windows/security/threat-protection/applocker/applocker-overview) または [Windows Defender アプリケーション制御](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control)を使用してユーザーがアクセスできるアプリ、およびカーネルで実行できるコードを制御することができます。 |
| SAS ファブリックを使用した共有構成での記憶域スペース|代わりに、[記憶域スペース ダイレクト](../storage/storage-spaces/storage-spaces-direct-overview.md)を展開してください。 「[記憶域スペース ダイレクトのハードウェア要件](../storage/storage-spaces/storage-spaces-direct-hardware-requirements.md)」に説明されているように、記憶域スペース ダイレクトは、HLK で認定された SAS エンクロージャの使用を非共有の構成でサポートしています。 |
| Windows Server Essentials Experience|Windows Server Standard または Windows Server Datacenter SKU 用の Essentials エクスペリエンス役割の開発は行われなくなりました。 小/中規模の企業向けの使いやすいサーバー ソリューションが必要な場合は、新しい[ビジネス向け Microsoft 365](https://www.microsoft.com/microsoft-365/business) ソリューションを検討するか、[Windows Server 2016 Essentials](https://docs.microsoft.com/windows-server-essentials/get-started/get-started) を使用してください。 |

