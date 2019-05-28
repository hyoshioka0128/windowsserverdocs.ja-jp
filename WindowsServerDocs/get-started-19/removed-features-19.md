---
title: 削除された機能または Windows Server 2019 で削除される予定
description: 削除または Windows Server 2019 以降削除予定の機能、機能について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
author: jasongerend
ms.author: jgerend
manager: jasgro
ms.date: 05/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: 820dfed8a0a58d3ccc64023325c373b761461ba8
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/27/2019
ms.locfileid: "65976518"
---
# <a name="features-removed-or-planned-for-replacement-starting-windows-server-2019"></a>削除された機能または開始 Windows サーバー 2019 交換の計画

>適用対象:Windows Server 2019

Windows Server の各リリースでは新機能が追加されています。同時に、機能が削除される場合もあります。これは、通常、より優れたオプションが追加されたためです。 機能と Windows Server 2019 で削除できる機能について詳細を次に示します。

> [!TIP]
> - [Windows Insider プログラム](https://insider.windows.com)に参加することで Windows Server ビルドにいち早くアクセスできます。これは、機能の変更をテストするための最適な方法です。
> - その他のリリースに関する質問がある場合 情報を確認[新機能については Windows Server](../get-started/whats-new-in-windows-server.md)します。

**一覧は変更される可能性し、すべての影響を受ける機能または機能が含まれません。** 

## <a name="features-we-removed-in-this-release"></a>このリリースで削除された機能

次の機能と機能を削除する、Windows Server 2019 にインストールされている製品イメージから予定しています。 これらの機能に依存するアプリケーションまたはコードは、別の方法を使用しない限りこのリリースでは機能しません。

|機能    |代わりに使用できる機能|
|-----------|--------------------
|ビジネス スキャン (分散スキャン管理 (DSM) とも呼ばれます)|このセキュリティで保護されたスキャンとスキャナーの管理機能を削除しました - この機能をサポートするデバイスはありません。|
|Server Core インストールのようになりましたオプション コンポーネントのコンポーネントを印刷します。|印刷コンポーネントにされた Windows Server の以前のリリースで*無効になっている*既定では、Server Core インストール オプションでします。 既定で有効にして、Windows Server 2016 で変更します。 Windows Server 2019、これらの印刷コンポーネントは既定では Server Core のもう一度無効です。 印刷のコンポーネントを有効にする場合は、これを行うを実行して、 **Install-windowsfeature のプリント サーバー**コマンドレット。|
|Server Core インストールでの[リモート デスクトップ接続ブローカーおよびリモート デスクトップ仮想化ホスト](../remote/remote-desktop-services/desktop-hosting-service.md)|ほとんどのリモート デスクトップ サービス展開には、リモート デスクトップ セッション ホスト (RDSH) と共存するこれらの役割があり、RDSH にはデスクトップ エクスペリエンス搭載サーバーが必要になります。RDSH との一貫性が保たれるように、これらの役割でもデスクトップ エクスペリエンス搭載サーバーを必要とするように変更を行っています。 これらの RDS の役割はで使用するため利用できなく、 [Server Core インストール](../administration/server-core/what-is-server-core.md)します。 必要がある場合[、リモート デスクトップ インフラストラクチャの一部としてこれらのロールをデプロイ](../remote/remote-desktop-services/rds-deploy-infrastructure.md)を実行できます[デスクトップ エクスペリエンス搭載の Windows サーバーにインストール](../get-started/getting-started-with-server-with-desktop-experience.md)します。 <br/><br/>これらの役割は、Windows Server 2019 のデスクトップ エクスペリエンスのインストール オプションにも含まれています。 |

## <a name="features-were-no-longer-developing"></a>開発を行っていない機能

これらの機能を不要になった現に開発中お今後の更新プログラムからを削除することがあります。 他の機能に置き換えられた機能と、現在さまざまなソースから利用可能な機能があります。 

提案されているこれらの機能の置換についてフィードバックがある場合は、[フィードバック Hub アプリ](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)を使用できます。 

| 機能   | 代わりに使用できる機能 |
|-----------|---------------------|
| HYPER-V でのキー記憶域ドライブ|HYPER-V のキー記憶域ドライブ機能に取り組んでいるところなくなりました。 第 1 世代の Vm を使用している場合はチェック アウト[Generation 1 VM の仮想化セキュリティ](https://docs.microsoft.com/windows-server/virtualization/hyper-v/learn-more/generation-1-virtual-machine-security-settings-for-hyper-v)今後オプションについてです。 作成する場合、新しい Vm より安全なソリューションの TPM デバイスの第 2 世代仮想マシンを使用します。 |
| 信頼されたプラットフォーム モジュール (TPM) 管理コンソール|TPM 管理コンソールで以前に使用できる情報が追加されました、 [**デバイスのセキュリティ**](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/wdsc-device-security)ページで、 [Windows Defender セキュリティ センター](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/windows-defender-security-center)します。 |
| ホスト ガーディアン サービスの Active Directory の構成証明モード|ホスト ガーディアン サービスの Active Directory の構成証明モードを不要になった開発中、代わりに、新しい構成証明モードが追加されました -[ホスト キーの構成証明](../security/guarded-fabric-shielded-vm/guarded-fabric-create-host-key.md)、はるかに簡単で Active Directory ベース均等の互換性構成証明書。  この新しいモードでは、セットアップ エクスペリエンスを簡単に管理 Active Directory の構成証明書よりも少ないインフラストラクチャの依存関係と同等の機能を提供します。 既存のすべてのシステムは新しいモードと互換性を保つために、ホスト キーの構成証明は必要に応じて、どのような Active Directory の構成証明を超えた追加のハードウェア要件がありません。 参照してください[保護されたホストの展開](../security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)詳細については、構成証明書オプション。 |
| OneSync サービス|OneSync サービスは、メール、カレンダー、およびユーザーのアプリのデータを同期します。 同期エンジンが同じ同期を提供する Outlook アプリに追加されました。 |
| リモートの差分圧縮 API サポート|リモートの差分圧縮 API サポートは、圧縮テクノロジは、ネットワーク経由で送信されるデータ量を最小化を使用してリモート ソースとデータの同期を有効になります。 このサポートは、任意の Microsoft 製品で現在使用されていません。 |
| WFP ライトウェイト フィルター スイッチ拡張機能|WFP ライトウェイト フィルターのスイッチ拡張機能を構築する開発者は[単純なネットワーク パケットが HYPER-V 仮想スイッチ拡張機能をフィルタ リング](https://docs.microsoft.com/en-us/windows-hardware/drivers/network/using-virtual-switch-filtering)します。 完全なフィルター拡張機能を作成して、同じ機能を実現できます。 そのため、私たちを削除するこの拡張機能、将来。 |