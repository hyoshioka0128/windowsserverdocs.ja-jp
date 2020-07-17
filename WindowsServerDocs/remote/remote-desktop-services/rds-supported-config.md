---
title: リモート デスクトップ サービスにおいてサポートされる構成
description: Windows Server 2016 および Windows Server 2019 の RDS においてサポートされる構成に関する情報を示します。
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 10/22/2019
ms.topic: article
ms.assetid: c925c7eb-6880-411f-8e59-bd0f57cc5fc3
author: lizap
manager: dongill
ms.openlocfilehash: dae6c00bd09e9c10e32932701095244a75f9ca7a
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80860115"
---
# <a name="supported-configurations-for-remote-desktop-services"></a>リモート デスクトップ サービスにおいてサポートされる構成

> 適用先:Windows Server 2019、Windows Server 2016

リモート デスクトップ サービス環境においてサポートされる構成に関しては、最大の懸念事項がバージョンの相互運用性になる傾向があります。 ほとんどの環境には、複数のバージョンの Windows Server が含まれます。たとえば、既存の Windows Server 2012 R2 の RDS を展開しているが、Windows Server 2016 にアップグレードして新しい機能 (OpenGL\OpenCL、個別のデバイス割り当て、記憶域スペース ダイレクトのサポートなど) を活用したい場合があります。 ここで、問題になるのは、どの RDS コンポーネントによってさまざまなバージョンを操作できるのか、また、同一でなければならないのはどれか、という点です。

そのことを念頭に置いて、ここでは Windows Server でサポートされるリモート デスクトップ サービスの構成に関する基本のガイドラインを示します。

> [!NOTE]
> [Windows Server 2016 のシステム要件](../../get-started/system-requirements.md)と [Windows Server 2019 のシステム要件](../../get-started-19/sys-reqs-19.md)を必ず確認してください。

## <a name="best-practices"></a>ベスト プラクティス

- リモート デスクトップのインフラストラクチャ (Web アクセス、ゲートウェイ、接続ブローカー、およびライセンス サーバー) に Windows Server 2019 を使用します。 Windows Server 2019 は、これらのコンポーネントと下位互換性があります。つまり、Windows Server 2016 または Windows Server 2012 R2 の RD セッション ホストは 2019 RD 接続ブローカーに接続できますが、その逆は接続できません。

- RD セッション ホストの場合、1 つのコレクション内にあるすべてのセッション ホストが同一レベルになっている必要がありますが、コレクションを複数保持することが可能です。 Windows Server 2016 のセッション ホストによる 1 つのコレクションと、Windows Server 2019 のセッション ホストによるもう 1 つを保持することができます。

- RD セッション ホストを Windows Server 2019 にアップグレードする場合は、ライセンス サーバーもアップグレードしてください。 2019 ライセンス サーバーでは、Windows Server 2003 に遡るまで、以前のすべての Windows Server バージョンからの CAL を処理できます。

- [リモート デスクトップ サービス環境のアップグレード](upgrade-to-rds.md#flow-for-deployment-upgrades)に関する記事で推奨されているアップグレード順序に従ってください。

- 高可用性環境を構築している場合、すべての接続ブローカーが同一の OS レベルになっている必要があります。

## <a name="rd-connection-brokers"></a>RD 接続ブローカー

Windows Server 2016 も実行しているリモート デスクトップ セッション ホスト (RDSH) およびリモート デスクトップ仮想化ホスト (RDVH) を使用している場合、Windows Server 2016 では、展開に含めることができる接続ブローカー数の制限を取り外しています。 次の表は、3 つ以上の接続ブローカーを備えた高可用性の展開において、どのバージョンの RDS コンポーネントによって 2016 および 2012 R2 バージョンの接続ブローカーを利用できるかを示しています。

|HA における 3 つ以上の接続ブローカー|RDSH または RDVH 2019|RDSH または RDVH 2016|RDSH または RDVH 2012 R2|
|---|---|---|---|
 |Windows Server 2019 の接続ブローカー|サポート|サポート|サポート|
 |Windows Server 2016 の接続ブローカー|なし|サポート|サポート|
 |Windows Server 2012 R2 の接続ブローカー|なし|なし|サポートしていません。|

## <a name="support-for-graphics-processing-unit-gpu-acceleration"></a>グラフィックス処理装置 (GPU) アクセラレーションのサポート

リモート デスクトップ サービスは GPU を備えたシステムをサポートします。 GPU を必要とするアプリケーションを、リモート接続を介して使用できます。 さらに、GPU でアクセラレーションされたレンダリングとエンコードを有効にして、アプリのパフォーマンスとスケーラビリティを向上させることができます。

リモート デスクトップ サービスのセッション ホストと単一セッションのクライアント オペレーティングシステム システムは、[Azure の GPU が最適化された仮想マシン サイズ](/en-us/azure/virtual-machines/windows/sizes-gpu)、物理 RDSH サーバーで利用可能な GPU、RemoteFX vGPU (Windows Server 2016 のみ)、サポートされるハイパーバイザーにより VM に提供される GPU など、オペレーティング システムに提供される物理的または仮想の GPU のメリットを活かすことができます。

何が必要かを明確にするには、「[Which graphics virtualization technology is right for you? (どのグラフィックス仮想化技術が適切か)](rds-graphics-virtualization.md)」をご覧ください。 DDA に関する特定の情報については、[個別のデバイス割り当てを展開する計画](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md)に関するページを参照してください。

GPU ベンダーによっては、RDSH シナリオ用に個別のライセンス スキームが用意されていたり、サーバー OS での GPU 使用が制限されている場合があります。対象のベンダーに要件を確認してください。

Microsoft 以外のハイパーバイザーまたはクラウド プラットフォームによって提供される GPU には、WHQL によってデジタル署名され、GPU ベンダーによって提供されるドライバーが必要です。

### <a name="remote-desktop-session-host-support-for-gpus"></a>リモート デスクトップ セッション ホストの GPU のサポート

以下の表は、RDSH ホストのさまざまなバージョンでサポートされるシナリオを示しています。

|機能|Windows Server 2008 R2|Windows Server 2012 R2|Windows Server 2016|Windows Server 2019|
|---|---|---|---|---|
|すべての RDP セッションでのハードウェア GPU の使用|いいえ|はい|はい|はい|
|H.264/AVC ハードウェア エンコード (GPU によってサポートされている場合)|いいえ|いいえ|はい|はい|
|OS に提供される複数の GPU 間の負荷分散|いいえ|いいえ|いいえ|はい|
|帯域幅の使用量を最小化するための H.264/AVC エンコードの最適化|いいえ|いいえ|いいえ|はい|
|4K 解像度のための H.264/AVC のサポート|いいえ|いいえ|いいえ|はい|

### <a name="vdi-support-for-gpus"></a>GPU の VDI サポート

次の表は、クライアント OS での GPU シナリオのサポートを示しています。

|機能|Windows 7 SP1|Windows 8.1|Windows 10|
|---|---|---|---|
|すべての RDP セッションでのハードウェア GPU の使用|いいえ|はい|はい|
|H.264/AVC ハードウェア エンコード (GPU によってサポートされている場合)|いいえ|いいえ|Windows 10 1703 以降|
|OS に提供される複数の GPU 間の負荷分散|いいえ|いいえ|Windows 10 1803 以降|
|帯域幅の使用量を最小化するための H.264/AVC エンコードの最適化|いいえ|いいえ|Windows 10 1803 以降|
|4K 解像度のための H.264/AVC のサポート|いいえ|いいえ|Windows 10 1803 以降|

### <a name="remotefx-3d-video-adapter-vgpu-support"></a>RemoteFX 3D ビデオ アダプター (vGPU) のサポート

Windows Server 2012 R2 または Windows Server 2016 で VM が Hyper-V ゲストとして実行されている場合、リモート デスクトップ サービスは RemoteFX vGPU をサポートします。 次のゲスト オペレーティング システムでは、RemoteFX vGPU がサポートされています。

- Windows 7 SP1
- Windows 8.1
- Windows 10 1703 以降
- Windows Server 2016 (シングル セッション配置の場合のみ)
- Windows Server 2019 (シングル セッション配置の場合のみ)

### <a name="discrete-device-assignment-support"></a>個別のデバイスの割り当てのサポート

リモート デスクトップ サービスは、Windows Server 2016 または Windows Server 2019 の Hyper-V ホストからの個別のデバイス割り当てで提供される物理 GPU をサポートしています。 詳細については、「[個別のデバイスの割り当て展開の計画](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md)」を参照してください。


## <a name="vdi-deployment--supported-guest-oses"></a>VDI の展開 – サポートされているゲスト OS

Windows Server 2016 および Windows 2019 の RD 仮想化ホスト サーバーでは、次のゲスト OS がサポートされます。

- Windows 10 Enterprise
- Windows 8.1 Enterprise
- Windows 7 SP1 Enterprise

> [!NOTE]
> - リモート デスクトップ サービスでは、異種セッション コレクションをサポートしていません。 1 つのコレクション内のすべての VM の OS は、同じバージョンである必要があります。
> - 同じホスト上でさまざまなゲスト OS バージョンを利用して、別個の同種コレクションを保持することができます。
> - VM の実行に使用する Hyper-V ホストは、元の VM テンプレートの作成に使用された Hyper-V ホストと同じバージョンである必要があります。

## <a name="single-sign-on"></a>シングル サインオン

Windows Server 2016 および Windows Server 2019 の RDS では、2 つの主要な SSO エクスペリエンスがサポートされています。

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
