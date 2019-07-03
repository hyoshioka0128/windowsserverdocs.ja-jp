---
title: Windows Server 2019 で削除される、または削除が計画されている機能
description: Windows Server 2019 以降で削除される、または削除が計画されている機能について説明します。
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
ms.openlocfilehash: a27fb6bfa0d96d7d3cdd0b9b5bc4912b12b4462b
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280359"
---
# <a name="features-removed-or-planned-for-replacement-starting-windows-server-2019"></a>Windows Server 2019 以降で削除される、または置換が計画されている機能

>適用対象:Windows Server 2019

Windows Server の各リリースでは新機能が追加されています。同時に、機能が削除される場合もあります。これは、通常、より優れたオプションが追加されたためです。 Windows Server 2019 で削除した機能の詳細を次に示します。

> [!TIP]
> - [Windows Insider プログラム](https://insider.windows.com)に参加することで Windows Server ビルドにいち早くアクセスできます。これは、機能の変更をテストするための最適な方法です。
> - その他のリリースに関する質問がある場合 [Windows Server の新機能](../get-started/whats-new-in-windows-server.md)の情報をご覧ください。

**この一覧は変更される可能性があります。また、影響を受ける機能でこの一覧に含まれていないものもあります。** 

## <a name="features-we-removed-in-this-release"></a>このリリースで削除された機能

Windows Server 2019 でインストールされている製品イメージから次の機能を削除しています。 これらの機能に依存するアプリケーションまたはコードは、別の方法を使用しない限りこのリリースでは機能しません。

|機能    |代わりに使用できる機能|
|-----------|--------------------
|ビジネス スキャン (分散スキャン管理 (DSM) とも呼ばれます)|このセキュリティで保護されたスキャンおよびスキャナー管理機能を削除しています。この機能をサポートするデバイスはありません。|
|印刷コンポーネント - 現在はコア インストールのためのオプションのコンポーネント|Windows Server の以前のリリースでは、印刷コンポーネントは Server Core インストール オプションで、既定で*無効になっていました*。 Windows Server 2016 ではこれを変更し、既定で有効にしました。 Windows Server 2019 で、この印刷コンポーネントを Server Core でもう一度既定で無効にしました。 印刷コンポーネントを有効にする必要がある場合は、**Install-WindowsFeature Print-Server** コマンドレットを実行します。|
|Server Core インストールでの[リモート デスクトップ接続ブローカーおよびリモート デスクトップ仮想化ホスト](../remote/remote-desktop-services/desktop-hosting-service.md)|ほとんどのリモート デスクトップ サービス展開には、リモート デスクトップ セッション ホスト (RDSH) と共存するこれらの役割があり、RDSH にはデスクトップ エクスペリエンス搭載サーバーが必要になります。RDSH との一貫性が保たれるように、これらの役割でもデスクトップ エクスペリエンス搭載サーバーを必要とするように変更を行っています。 これらの RDS の役割は、[コア インストール](../administration/server-core/what-is-server-core.md)で使用できなくなりました。 [リモート デスクトップ インフラストラクチャの一部としてこれらの役割を展開する](../remote/remote-desktop-services/rds-deploy-infrastructure.md)必要がある場合は、[デスクトップ エクスペリエンスがインストールされている Windows Server に役割をインストールする](../get-started/getting-started-with-server-with-desktop-experience.md)ことができます。 <br/><br/>これらの役割は、Windows Server 2019 のデスクトップ エクスペリエンスのインストール オプションにも含まれています。 |

## <a name="features-were-no-longer-developing"></a>開発を行っていない機能

次の機能の開発は積極的には行われなくなりました。今後の更新プログラムから削除される可能性があります。 他の機能に置き換えられた機能と、現在さまざまなソースから利用可能な機能があります。 

提案されているこれらの機能の置換についてフィードバックがある場合は、[フィードバック Hub アプリ](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)を使用できます。 

| 機能   | 代わりに使用できる機能 |
|-----------|---------------------|
| Hyper-V のキー記憶域ドライブ|Hyper-V のキー記憶域ドライブ機能に対する取り組みはなくなりました。 第 1 世代の VM を使用している場合は、「[第 1 世代 VM の仮想化セキュリティ](https://docs.microsoft.com/windows-server/virtualization/hyper-v/learn-more/generation-1-virtual-machine-security-settings-for-hyper-v)」で今後のオプションの情報をご覧ください。 新しい VM を作成している場合は、より安全なソリューションのため TPM デバイスで第 2 世代仮想マシンを使用してください。 |
| トラステッド プラットフォーム モジュール (TPM) 管理コンソール|以前、TPM 管理コンソールから入手できた情報は、[Windows Defender セキュリティ センター](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/windows-defender-security-center)に関するページ「[**デバイス セキュリティ**](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-security-center/wdsc-device-security)」のページにあります。 |
| ホスト ガーディアン サービスの Active Directory 構成証明モード|ホスト ガーディアン サービスの Active Directory 構成証明モードは開発されなくなりました。代わりに、はるかにシンプルで、Active Directory ベースの構成証明と同等の互換性がある新しい構成証明モード、[ホスト キーの構成証明](../security/guarded-fabric-shielded-vm/guarded-fabric-create-host-key.md)を追加しました。  この新しいモードでは、セットアップ エクスペリエンスで同等の機能を提供し、Active Directory 構成証明よりも管理がシンプルで、インフラストラクチャの依存関係が少なくなっています。 ホスト キーの構成証明では Active Directory 構成証明で必要とされる以上のハードウェア要件がないため、既存のすべてのシステムと新しいモードとの互換性が保たれます。 構成証明オプションの詳細については、「[保護されたホストの展開](../security/guarded-fabric-shielded-vm/guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)」を参照してください。 |
| OneSync サービス|OneSync サービスは、メール、予定表、連絡先のアプリのデータを同期します。 同じ同期を提供する Outlook アプリに対し、同期エンジンを追加しました。 |
| Remote Differential Compression の API のサポート|Remote Differential Compression の API のサポートにより圧縮テクノロジを使用したリモート ソースとのデータの同期が可能になり、ネットワーク間で送信されるデータ量が最小になりました。 |
| WFP ライトウェイト フィルター スイッチ拡張機能|WFP ライトウェイト フィルター スイッチ拡張機能により、開発者が [Hyper-V 仮想スイッチ向けのシンプルなネットワーク パケット フィルター拡張機能](https://docs.microsoft.com/windows-hardware/drivers/network/using-virtual-switch-filtering)を構築できるようになりました。 同じ機能は、完全なフィルター拡張機能を作成することで実現できます。 そのため、この拡張機能は将来的に削除されます。 |
