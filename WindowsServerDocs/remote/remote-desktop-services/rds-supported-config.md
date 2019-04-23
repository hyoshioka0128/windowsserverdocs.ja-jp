---
title: リモート デスクトップ サービスでサポートされる構成
description: Windows Server 2016 で RDS でサポートされる構成についてを説明します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 894ea8b134ae5b871a2978e3f72e683c12346fe5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850203"
---
# <a name="supported-configurations-for-remote-desktop-services-in-windows-server-2016"></a>Windows Server 2016 でのリモート デスクトップ サービスでサポートされる構成

> 適用先:Windows Server 2016

リモート デスクトップ サービス環境でサポートされる構成する際に最大の懸念事項は、バージョンの相互運用性のある傾向があります。 ほとんどの環境が Windows Server の複数のバージョンを含める - たとえば、既存の Windows Server 2012 R2 RDS デプロイしますが、(OpenGL\OpenCL、不連続値のサポートなどの新機能を活用するために Windows Server 2016 にアップグレードします。デバイスの割り当て、または記憶域スペース ダイレクトを使用)。 ここで問題は、RDS コンポーネントは別のバージョンで動作し、同じにする必要になるでしょうか。

これを念頭に、ここではサポートされている構成の Windows Server 2016 でのリモート デスクトップ サービスの基本的なガイドラインです。

> [!NOTE]
> 必ず確認、 [Windows Server 2016 のシステム要件](../../get-started/system-requirements.md)します。

## <a name="best-practices"></a>ベスト プラクティス
- Web アクセス、ゲートウェイ、接続ブローカー、およびライセンス サーバー、リモート デスクトップ インフラストラクチャ - Windows Server 2016 を使用します。 Windows Server 2016 では、これらのコンポーネントの旧バージョンと互換性のあるは、2012 R2 RD セッション ホストは、2016 の RD 接続ブローカーに接続できますが、逆はできませんので。

- RD セッション ホスト - コレクション内のすべてのセッション ホストを同じレベルを指定する必要がありますが、複数のコレクションがあることができます。 Windows Server 2012 R2 セッション ホストを持つコレクションと Windows Server 2016 のセッション ホストを 1 つのことができます。

- Windows Server 2016、RD セッション ホストをアップグレードする場合は、ライセンス サーバーもアップグレードします。 2016 のライセンス サーバーが Windows Server、Windows Server 2003 までのすべての以前のバージョンから Cal を処理できることに注意してください。

- 推奨されているアップグレードの順序に従う[リモート デスクトップ サービス環境のアップグレード](upgrade-to-rds.md#flow-for-deployment-upgrades)します。 

- 高可用性環境を作成する場合は、同じ OS レベルであるすべての接続ブローカーの必要があります。

## <a name="rd-connection-brokers"></a>RD 接続ブローカー

Windows Server 2016 は、リモート デスクトップ仮想化ホスト (RDVH) も Windows Server 2016 を実行しているリモート デスクトップ セッション ホスト (RDSH) の使用時に展開することが、接続ブローカーの数の制限を削除します。 次の表では、次の 3 つまたは複数の接続ブローカーの高可用性の展開で、2016 および 2012 R2 のバージョンの接続ブローカーでの RDS のコンポーネントの作業バージョンを示します。

| HA で 3 + 接続ブローカー              | RDSH 2016 | RDVH 2016 | RDSH 2012 R2  | RDVH 2012 R2  |
|------------------------------------------|-----------|-----------|---------------|---------------|
| Windows Server 2016 の接続ブローカー    | サポートされている | サポート対象 | サポート対象     | サポートされている     |
| Windows Server 2012 R2 接続ブローカー | なし       | なし       | サポートされている     | サポートされている     |

## <a name="support-for-gpu-acceleration-with-hyper-v"></a>Hyper V と GPU アクセラレーションのサポート
次の表では、仮想マシンに GPU アクセラレータのサポートについて説明します。 参照してください[グラフィックス仮想化テクノロジが適切な?](rds-graphics-virtualization.md)確認する必要がある手助けをします。 DDA の詳細については、チェック アウト[の個別のデバイスの割り当ての展開を計画](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md)します。

|VM のゲスト OS  |Windows Server 2012 R2 または Windows Server 2016<br> HYPER-V の RemoteFX vGPU (Gen 1 VM) |  Windows Server 2016 HYPER-V の RemoteFX vGPU (Gen 2 VM) |  Windows Server 2016 HYPER-V の個別のデバイスの割り当て (第 2 世代 VM) |
|-----------------------------|------------------------------------------------------------|--------------------------------------------------------|---------------------------------------------------------------------|
| Windows 7 SP1               | 〇                                                        | X                                                     | いいえ                                                                  |
| Windows 8.1                 | 〇                                                        | X                                                     | いいえ                                                                  |
| Windows 10 1511 Update      | 〇                                                        | 〇                                                    | 〇                                                                 |
| Windows Server 2012 R2      | 〇                                                        | いいえ                                                     | はい (KB 3133690 が必要)                                           |
| Windows Server 2016         | 〇                                                        | 〇                                                    | 〇                                                                 |
| Windows Server 2012 R2 の RDSH | X                                                         | X                                                     | はい (KB 3133690 が必要)                                           |
| Windows Server 2016 の RDSH    | X                                                         | X                                                     | 〇                                                                 |
## <a name="vdi-deployment--supported-guest-oss"></a>VDI 展開 – サポートされるゲスト Os 
Windows Server 2016 の RD 仮想化ホスト サーバーは、次のゲスト Os をサポートします。

- Windows 10 Enterprise
- Windows 8.1 Enterprise 
- Windows 8 Enterprise 
- Windows 7 SP1 Enterprise 

次の表は、サポートされている RD 仮想化ホスト オペレーティング システムとゲスト オペレーティング システムの組み合わせを示します。

| RDVH OS バージョン        | ゲスト OS バージョン           |
| ------------- |-------------|
| Windows Server 2016      | Windows 7 SP1、Windows 8、Windows 8.1、Windows 10 |
| Windows Server 2012 R2   | Windows 7 SP1、Windows 8、Windows 8.1、Windows 10 |
| Windows Server 2012      | Windows 7 SP1、Windows 8、Windows 8.1 |

> [!NOTE]  
> - Windows Server 2016 リモート デスクトップ サービスは、異種コレクションをサポートしていません。 コレクション内のすべての Vm は、同じ OS バージョンである必要があります。 
> - 同じホストには、さまざまなゲスト OS バージョンと同種の別個のコレクションがあります。 
> - Windows Server 2016 の HYPER-V ホスト上のゲスト OS として使用する Windows Server 2016 の HYPER-V ホストには、VM テンプレートを作成する必要があります。

## <a name="single-sign-on-sso"></a>シングル サインオン (SSO)
Windows Server 2016 の RDS は、2 つの主な SSO エクスペリエンスをサポートしています。

 - アプリ (Windows、iOS、Android、および Mac でリモート デスクトップ アプリケーション)
 - Web SSO
 
リモート デスクトップ アプリケーションを使用することができます資格情報を格納、接続情報の一部として ([Mac](clients\remote-desktop-mac.md)) または管理アカウントの一部として ([iOS](clients\remote-desktop-ios.md#manage-your-user-accounts)、 [Android](clients\remote-desktop-android.md#manage-your-user-accounts)Windows)各 OS に固有のメカニズムを通じて安全に。

Windows 上の受信トレイのリモート デスクトップ接続クライアントをデスクトップと SSO と Remoteapp に接続するには、Internet Explorer を使用して RD Web ページに接続する必要があります。 サーバー側では、次の構成オプションが必要です。 Web SSO の他の構成はサポートされていません。

 - RD Web は、フォーム ベース認証 (既定値) に設定
 - RD ゲートウェイは、パスワード認証 (既定値) に設定
 - RDS のデプロイは、「使用 RD ゲートウェイはリモート コンピューターの資格情報」に設定 (既定) では、RD ゲートウェイのプロパティ

> [!NOTE]
> 必要な構成オプションにより Web SSO はスマート カードではサポートされていません。 スマート カードを使用してログインがログインに複数のプロンプトが直面するユーザー。

リモート デスクトップ サービスの VDI の展開を作成する方法の詳細については、チェック アウト[リモート デスクトップ サービスの VDI に Windows 10 のサポートされているセキュリティ構成](rds-vdi-supported-config.md)します。

## <a name="using-remote-desktop-services-with-application-proxy-services"></a>アプリケーション プロキシ サービスでリモート デスクトップ サービスを使用します。

Web クライアントを除くリモート デスクトップ サービスを使用できる[Azure AD アプリケーション プロキシ](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-remote-desktop)します。 リモート デスクトップ サービスでは、使用はサポートしません[Web アプリケーション プロキシ](https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server)、Windows Server 2016 と以前のバージョンに含まれます。
