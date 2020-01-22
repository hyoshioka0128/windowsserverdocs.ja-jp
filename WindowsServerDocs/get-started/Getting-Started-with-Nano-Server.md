---
title: Nano Server のインストール
description: Nano Server のクリーン インストール、アップグレード、移行、および評価
ms.prod: windows-server
ms.service: na
manager: dougkim
ms.technology: server-nano
ms.date: 09/06/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2c2fa45b-6f3b-4663-b421-2da6ecc463bf
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: f94e2c083f0bc05231543c15120818481afbabb0
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75947853"
---
# <a name="install-nano-server"></a>Nano Server のインストール

>適用先:Windows Server 2016

> [!IMPORTANT]
> Windows Server バージョン 1709 以降では、Nano Server は[コンテナーの基本 OS イメージ](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)としてのみ提供されます。 その意味については、[Nano Server に加えられる変更](nano-in-semi-annual-channel.md)に関する記事をご覧ください。 

Windows Server 2016 では、新しいインストール オプションであるNano Server が提供されています。 Nano Server は、プライベート クラウドとデータセンター向けに最適化されたリモート管理サーバー オペレーティング システムです。 Nano Server は Server Core モードの Windows Server に似ていますが、サイズが大幅に小さく、ローカル ログオン機能がありません。さらに、64 ビットのアプリケーション、ツール、およびエージェントのみがサポートされます。 Windows Server と比べて Nano Server の場合は、使用されるディスク領域がかなり小さくなり、セットアップが大幅に速くなり、必要とされる更新と再起動の回数がずっと少なくなります。 再起動も非常に高速化されています。 Nano Server インストール オプションは、Windows Server 2016 の Standard Edition および Datacenter Edition で提供されます。  

Nano Server は、次のようなさまざまなシナリオに適しています。  
  
-   Hyper-V 仮想マシンの "コンピューティング" ホストとして (クラスター化されているかどうかに関係なく)  
  
-   スケールアウト ファイル サーバーの記憶域ホストとして  
  
-   DNS サーバーとして  
  
-   インターネット インフォメーション サービス (IIS) を実行する Web サーバーとして  
  
-   クラウド アプリケーション パターンを使って開発され、コンテナーまたは仮想マシン ゲスト オペレーティング システムで実行されるアプリケーションのホストとして  
  
## <a name="important-differences-in-nano-server"></a>Nano Server における重要な相違点

Nano Server は、コンテナーおよびマイクロサービスに基づく "クラウド ネイティブ" アプリケーションを実行するための軽量なオペレーティング システムとして、またはフットプリントが大幅に削減された機敏性とコスト効果の高いデータ センター ホストとして最適化されています。このため、Nano Server と、デスクトップ エクスペリエンスのインストールを使用した Server Core または Server との間には重要な違いがあります。

- Nano Server は "ヘッドレス" 型であり、ローカル ログオン機能やグラフィカル ユーザー インターフェイスはありません。
- 64 ビットのアプリケーション、ツール、およびエージェントのみがサポートされています。
- Nano Server は、Active Directory ドメイン コントローラーとして使用することはできません。
- グループ ポリシーはサポートされていません。 ただし、[必要な状態の構成 (DSC)](https://msdn.microsoft.com/powershell/dsc/nanoDsc) を使用することで、設定を大規模に適用できます。
- プロキシ サーバーを使用してインターネットにアクセスするように、Nano Server を構成することはできません。
- NIC チーミング (具体的には、LBFO (Load Balancing and Failover: 負荷分散とフェールオーバー)) はサポートされていません。 代わりに、スイッチ埋め込みチーミング (SET) がサポートされています。
- System Center Configuration Manager と System Center Data Protection Manager はサポートされていません。
- ベスト プラクティス アナライザー (BPA) のコマンドレットおよび BPA とサーバー マネージャーの統合はサポートされていません。
- Nano Server では仮想ホスト バス アダプター (HBA) はサポートされません。
- Nano Server は、プロダクト キーを使ってライセンス認証する必要はありません。 Hyper-V ホストとして機能する場合、Nano Server では[仮想マシンの自動ライセンス認証](https://technet.microsoft.com/library/dn303421%28v=ws.11%29.aspx) (AVMA) はサポートされません。 Nano Server ホストで実行される仮想マシンは、[キー管理サービス](https://technet.microsoft.com/library/jj612867(v=ws.11).aspx) (KMS) と汎用ボリューム ライセンス キーを使うか、[Active Directory によるライセンス認証](https://technet.microsoft.com/library/dn502534(v=ws.11).aspx)を使ってライセンス認証できます。
- Nano Server に提供される Windows PowerShell のバージョンには、重要な相違点があります。 詳細については、「[PowerShell on Nano Server](PowerShell-on-Nano-Server.md)」 (Nano Server 上の PowerShell) を参照してください。
- Nano Server は、Current Branch for Business (CBB) モデルでのみサポートされています。現時点で、Nano Server 用の Long-Term Servicing Branch (LTSB) リリースはありません。 詳細については、次のサブセクションを参照してください。

### <a name="current-branch-for-business"></a>Current Branch for Business
Nano Server は、開発サイクルが短い "クラウド歩調" で事業を進めているお客様をサポートするために、Current Branch for Business (CBB) と呼ばれる、よりアクティブなモデルで処理されます。 このモデルでは、Nano Server の機能更新のリリースが年に 2 回～ 3 回発生すると予想されます。 このモデルでは、Nano Server を運用環境に展開し運用する場合、[ソフトウェア アシュアランス](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default.aspx)が必要です。 サポートを維持するために、管理者は、2 つ後の CBB リリース以内に留まる必要があります。 ただし、これらのリリースで既存の展開の自動更新は行われません。管理者は、必要に応じて、新しい CBB リリースを手動でインストールします。 詳細については、「[Windows Server 2016 new Current Branch for Business servicing option](https://blogs.technet.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/)」 (Windows Server 2016 の新しい Current Branch for Business サービス オプション) を参照してください。

デスクトップ エクスペリエンスを使用する Server Core および Server インストール オプションは、5 年間のメインストリーム サポートと 5 年間の延長サポートで構成される [Long-Term Servicing Branch (LTSB) モデル](https://support.microsoft.com/lifecycle#gp%2Fgp_msl_policy)で処理されます。

## <a name="installation-scenarios"></a>インストールのシナリオ

### <a name="evaluation"></a>評価
「[Windows Server 評価版ソフトウェア](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016)」で 180 日間ライセンスが有効な Windows Server の評価版を入手できます。 Nano Server を試用するには、 **[Nano Server | 64-bit EXE option]** (Nano Server | 64 ビット EXE オプション) を選択し、「[Nano Server のクイック スタート](Nano-Server-Quick-Start.md)」または「[Nano Server の展開](Deploy-Nano-Server.md)」に戻って作業を開始します。

### <a name="clean-installation"></a>クリーン インストール
VHD を構成して Nano Server をインストールするため、クリーン インストールは、最も迅速かつ最も簡単な展開方法です。

- DHCP を使用して IP アドレスを取得する Nano Server の基本的な展開をすばやく開始するには、「[Nano Server のクイック スタート](Nano-Server-Quick-Start.md)」を参照してください。 
- Nano Server の基礎を理解している方向けに、「[Nano Server の展開](Deploy-Nano-Server.md)」で始まる一連の詳細なトピックで、イメージのカスタマイズ、ドメインの操作、オンラインとオフラインの両方でパッケージをインストールしてサーバーの役割とその他の機能を設定する方法などについて説明しています。

> [!IMPORTANT]  
> セットアップが完了し、必要なサーバーの役割と機能をすべてインストールしたら、Windows Server 2016 に適用可能な更新プログラムがあるかどうかをすぐに確認し、ある場合はインストールします。 Nano Server については、「[Nano Server の管理](Manage-Nano-Server.md)」の「Nano Server の更新を管理する」を参照してください。

### <a name="upgrade"></a>アップグレード パッケージ、アップグレード
Nano Server は Windows Server 2016 の新機能であるため、以前のバージョンのオペレーティング システムから Nano Server へのアップグレード パスはありません。

### <a name="migration"></a>移行
Nano Server は Windows Server 2016 の新機能であるため、以前のバージョンのオペレーティング システムから Nano Server への移行パスはありません。
  
-------------------------------------
別のインストール オプションが必要な場合は、[Windows Server 2016 のメイン ページ](windows-server-2016.md)に戻ってください。 

  


 
