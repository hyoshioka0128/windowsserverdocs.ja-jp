---
title: 削除された機能、または Windows Server 2019 で削除予定
description: 機能と削除、または Windows Server 2019 以降削除予定の機能について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: jasgro
ms.date: 03/29/2019
ms.localizationpriority: medium
ms.openlocfilehash: 470857616a9b36d238de031b4ccf80a68eff1e61
ms.sourcegitcommit: 971f6538e8d89af84ef50fc8aab2188bdf6f47cb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/02/2019
ms.locfileid: "9279133"
---
# <a name="features-removed-or-planned-for-replacement-starting-windows-server-2019"></a>削除された機能、または Windows Server 2019 の置換が計画されています。

>適用対象: Windows Server 2019

Windows Server の各リリースでは新機能が追加されています。同時に、機能が削除される場合もあります。これは、通常、より優れたオプションが追加されたためです。 機能と Windows Server 2019 で削除された機能の詳細を次に示します。   

> [!TIP]
> - [Windows Insider プログラム](https://insider.windows.com)に参加することで Windows Server ビルドにいち早くアクセスできます。これは、機能の変更をテストするための最適な方法です。
> - その他のリリースに関する質問がある場合 [Windows Server、バージョン 1803](../get-started/windows-server-1803-removed-features.md) [Windows Server version 1709](../get-started/removed-features-1709.md)、および[Windows Server 2016](../get-started/deprecated-features.md)の情報を確認します。

**この一覧は変更される可能性があります。また、影響を受ける機能でこの一覧に含まれていないものもあります。** 

## <a name="features-we-removed-in-this-release"></a>このリリースで削除された機能

Windows Server 2019 でインストールされる製品イメージから、次の機能を削除しますします。 これらの機能に依存するアプリケーションまたはコードは、別の方法を使用しない限りこのリリースでは機能しません。   

|機能    |代わりに使用できる機能または役割|
|-----------|--------------------
|ビジネス スキャン (分散スキャン管理 (DSM) とも呼ばれます)|このセキュリティで保護されたスキャンとスキャナー管理機能を削除します - この機能をサポートするデバイスはありません。|
|Server Core インストールのようになりましたオプション コンポーネントのコンポーネントを印刷します。|Windows Server の以前のリリースでは、印刷のコンポーネントは、Server Core インストール オプションで既定で*無効になっている*はでした。 既定で有効にすると、Windows Server 2016 で変更します。 Windows Server 2019 では、それらの印刷コンポーネントは既定で Server Core をもう一度無効です。 印刷のコンポーネントを有効にする必要がある場合は、[**インストール WindowsFeature のプリント サーバー**のコマンドレットを実行して実行できます。|
|Server Core インストールでの[リモート デスクトップ接続ブローカーおよびリモート デスクトップ仮想化ホスト](../remote/remote-desktop-services/desktop-hosting-service.md)|ほとんどのリモート デスクトップ サービス展開には、リモート デスクトップ セッション ホスト (RDSH) と共存するこれらの役割があり、RDSH にはデスクトップ エクスペリエンス搭載サーバーが必要になります。RDSH との一貫性が保たれるように、これらの役割でもデスクトップ エクスペリエンス搭載サーバーを必要とするように変更を行っています。 これらの RDS 役割は[Server Core インストール](../administration/server-core/what-is-server-core.md)で使用可能ではありません。 [リモート デスクトップ インフラストラクチャの一部としてこれらの役割を展開](../remote/remote-desktop-services/rds-deploy-infrastructure.md)する必要がある場合は、[デスクトップ エクスペリエンス搭載 Windows Server 上でそれらをインストール](../get-started/getting-started-with-server-with-desktop-experience.md)できます。 <br/><br/>これらの役割は、Windows Server 2019 のデスクトップ エクスペリエンスのインストール オプションにも含まれています。 |



## <a name="features-were-no-longer-developing"></a>開発を行っていない機能

これらの機能を開発しているアクティブになったし、今後の更新プログラムからを削除することがあります。 他の機能に置き換えられた機能と、現在さまざまなソースから利用可能な機能があります。 

提案されているこれらの機能の置換についてフィードバックがある場合は、[フィードバック Hub アプリ](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)を使用できます。 

|機能    |代わりに使用できる機能|
|-----------|---------------------|
|HYPER-V のキー記憶域ドライブ|不要になったに取り組んでいます HYPER-V でキー記憶域ドライブの機能です。 第 1 世代 Vm を使用している場合は、今後オプションについて[ジェネレーション 1 の VM の仮想化のセキュリティ](https://docs.microsoft.com/windows-server/virtualization/hyper-v/learn-more/generation-1-virtual-machine-security-settings-for-hyper-v)を確認します。 作成する場合、新しい Vm より安全なソリューションの TPM デバイスと第 2 世代仮想マシンを使用します。 |
|信頼されたプラットフォーム モジュール (TPM) 管理コンソール|[Windows Defender セキュリティ センター](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/windows-defender-security-center)で[**デバイスのセキュリティ**](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/wdsc-device-security)] ページで TPM 管理コンソールで利用可能であったの情報があるようになりました。|
|ホスト ガーディアン サービスの Active Directory の構成証明モード|ホスト ガーディアン サービスの Active Directory の構成証明モード開発は行っていません - 新しい構成証明モードでは、[ホスト キーの構成証明](../security/guarded-fabric-shielded-vm/guarded-fabric-create-host-key.md)、方がはるかに簡単かつ均等に互換性のある Active Directory ベースの構成証明を代わりに追加しました。  この新しいモードでは、セットアップ エクスペリエンス、シンプルな管理、Active Directory の構成証明よりも少ないインフラストラクチャの依存関係と同等の機能を提供します。 既存のすべてのシステムは新しいモードと互換性を保つために、ホスト キーの構成証明は必須ではどのような Active Directory の構成証明以外の追加のハードウェア要件はありません。 構成証明のオプションの詳細については、[保護されたホストの展開](../security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)を参照してください。|
|OneSync サービス|OneSync サービスは、メール、カレンダー、および People アプリのデータを同期します。 Outlook を提供するアプリと同じ同期する同期エンジンを追加しました。|
|リモートの差分圧縮 API のサポート|リモートの差分圧縮 API サポートでは、ネットワーク経由で送信されるデータの量を最小限になる圧縮テクノロジを使用してリモート ソースとデータの同期を有効にします。 このサポートは、Microsoft の製品で使用されていません。|
|WFP 軽量なフィルター スイッチの拡張機能|[単純なネットワーク パケット フィルタ リング拡張機能の HYPER-V 仮想スイッチ](https://docs.microsoft.com/en-us/windows-hardware/drivers/network/using-virtual-switch-filtering)を作成する開発者は WFP 軽量なフィルター スイッチ拡張できます。 完全なフィルタ リングの拡張機能を作成して、同じ機能を実現できます。 このため、します削除されますこの拡張機能、今後。|

