---
title: サービス チャネル
description: Windows Server サービスのチャネルの説明:LTSC と SAC
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
ms.localizationpriority: high
ms.openlocfilehash: c4329339e37acbb0b589e767a570073f4ae1363f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848733"
---
# <a name="windows-server-servicing-channels-ltsc-and-sac"></a>Windows Server がチャネルをサービス:LTSC と SAC

>適用先:Windows Server 2019、Windows Server 2016


**2 つの主なリリース チャネルは Windows Server ユーザー、長期的なサービス チャネルと半期チャネルに使用できます。** 

ユーザーはニーズに最も適した方法を選択できます。サーバーを長期サービス チャネル (LTSC) のままにすることも、半期チャネルに移行することも、一部のサーバーをいずれかのトラックで利用することも可能です。


## <a name="long-term-servicing-channel-ltsc"></a>長期的なサービス チャネル (LTSC)
以前から使用されているリリース モデルです (旧称、“Long-Term Servicing *Branch*”)。このモデルでは、Windows Server の新しいメジャー バージョンが、2 ～ 3 年ごとにリリースされます。 ユーザーは、5 年間のメインストリーム サポートとそれに続く 5 年間の延長サポートを受けることができます。 このチャネルは、長期のサービス オプションと機能安定性を必要とするシステムに適しています。 Windows Server 2016 およびそれ以前のバージョンの Windows Server の展開環境に対する、新しい半期チャネルのリリースによる影響はありません。 長期的なサービス チャネルでは、引き続きセキュリティ更新プログラムとセキュリティ以外の更新プログラムが提供されますが、新機能は提供されません。

> [!Note]  
> **現在の LTSC 製品は Windows Server 2019 です**。 このチャネルを維持する場合は、Windows Server 2019 をインストールする (または使用を継続する) 必要があります。この場合、Server Core インストール オプションまたはデスクトップ エクスペリエンス インストール オプションでインストールすることができます。

## <a name="semi-annual-channel"></a>半期チャネル 
半期チャネルは迅速に活用するために新しいオペレーティング システムの機能の両方のアプリケーションで高速のペースで特にのコンテナーとマイクロ サービス、およびソフトウェア定義でビルドされた革新はお客様に最適です。ハイブリッド データ センターです。 半期チャネルの Windows Server 製品は、年に 2 回、春と秋に新しいリリースが公開されます。 このチャネルの各リリースは、最初のリリースから 18 か月サポートされます。

半期チャネルで提供される機能のほとんどは、Windows Server の次回の長期的なサービス チャネル リリースに含まれます。 各リリースのエディション、機能、およびサポート コンテンツは、ユーザーのフィードバックに応じて異なる場合があります。

半期チャネルは、[ソフトウェア アシュアランス](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx) をご利用のボリューム ライセンスのお客様以外にも、Azure Marketplace やその他のクラウド/ホスティング サービス プロバイダー、Visual Studio サブスクリプションなどのロイヤルティ プログラム経由で入手できます。

> [!Note]  
> **半年チャネルの現在のリリースは、Windows Server Version 1809 です**。 サーバーをこのチャネルで利用する場合は、Windows Server Version 1809 をインストールする必要があります。この場合、Server Core モードで、またはコンテナー内で実行される Nano Server としてインストールすることができます。 Windows Server 2016 から Windows Server Version 1809 への一括アップグレードはサポートされていません。これら 2 つの**リリース チャネルが異なる**ためです。 Windows Server Version 1809 は、Windows Server 2016 に対する更新プログラムではなく、半期チャネルの次の Windows Server リリースです。



このモデルでは、Windows Server のリリースが、リリースの年と月によって識別されます。たとえば、2017 年の 9 番目の月 (9 月) のリリースは、**バージョン 1709** となります。 半期チャネルでは、Windows Serverの新しいリリースが毎年 2 回提供されます。 各リリースのサポート ライフサイクルは、18 か月です。

## <a name="should-you-keep-servers-on-the-ltsc-or-move-them-to-the-semi-annual-channel"></a>サーバーを LTSC のまま利用するべきか、半期チャネルに移行すべきか
決定にあたっては、次の重要な相違点を考慮する必要があります。

- 革新的な機能を迅速に取り入れる必要がありますか。 Windows Server の最新機能への早期アクセスが必要ですか。 頻繁に更新されるハイブリッド アプリケーション、DevOps、および Hyper-V ファブリックをサポートする必要がありますか。 そうであれば、**Windows Server Version 1809** をインストールして、**半期チャネルに参加**することを検討してください。 その場合、このトピックで説明したように、年に 2 回新しいバージョンを受け取り、各リリースのメインストリームの運用サポートは 18 か月になります。 これは、ボリューム ライセンス、Azure、または Visual Studio サブスクリプション サービスを通じて提供されます。 現時点では、製品を運用環境で実行する場合に、半期チャネルのリリースを利用するには、ボリューム ライセンスとソフトウェア アシュアランスが必要です。
- 安定性と予測可能性を確保する必要がありますか。 物理サーバー上の仮想マシンと従来のワークロードを実行する必要がありますか。 そうであれば、**それらのサーバーを長期的なサービス チャネルのまま**利用します。 現在の LTSC リリースは、**Windows Server 2019** です。 その場合、このトピックで説明したように、2 ～ 3 年ごとに新しいバージョンが提供されます。各リリースのメインストリームの運用サポートは 5 年間で、その後 5 年間サポートを延長することができます。 LTSC リリースは、すべてのリリース メカニズムで利用できます。 LTSC のリリースは、使用しているライセンス モデルに関係なく、すべてのユーザーが利用できます。 

次の表は、チャネル間の主な違いをまとめたものです。

|  | 長期サービス チャネル (Windows Server 2019) |半期チャネル (Windows Server) |
| ------------------- | ------------------------------------ | ------------------------------------------------- |
|推奨されるシナリオ | 汎用ファイル サーバー、Microsoft と Microsoft 以外のワークロード、従来のアプリ、インフラストラクチャの役割、ソフトウェア定義データセンター、ハイパーコンバージド インフラストラクチャ | コンテナー化されたアプリケーション、コンテナー ホスト、および迅速なイノベーションを活用するアプリケーション シナリオ |
| 新しいリリース | 2 ～ 3 年ごと |6 か月ごと |
| サポート |5 年間のメインストリーム サポートとそれに続く 5 年間の延長サポート | 18 か月 |
| エディション | 利用可能なすべての Windows Server エディション | Standard エディションと Datacenter エディション |
| 利用できるユーザー | すべてのチャネルのすべてのユーザー | ソフトウェア アシュアランスとクラウドのユーザーのみ |
| インストール オプション | Server Core とデスクトップ エクスペリエンス搭載サーバー | コンテナー ホストとコンテナー イメージの Server Core および Nano Server コンテナー イメージ |                |


## <a name="device-compatibility"></a>デバイスの互換性
特に断りのない限り、半期チャネルのリリースを実行するための最小ハードウェア要件は、Windows Server の最新の長期的なサービス チャネルのリリースと同じです。 たとえば、**長期的なサービス チャネルの現行リリースは、Windows Server 2019 です**。 ほとんどのハードウェア ドライバーは、引き続きこれらのリリースで機能します。

## <a name="servicing"></a>サービス
セキュリティ更新プログラムとセキュリティ以外の更新プログラムで、長期的なサービス チャネルと半期チャネルの両方のリリースがサポートされます。 ただし、前述のように、サポート期間の長さはリリースによって異なります。

### <a name="servicing-tools"></a>サービス ツール
IT 担当者が Windows Server を操作するためのツールは数多く存在します。 機能や制御からシンプルさや管理要件の低さまで、各オプションにはそれぞれ長所と短所があります。 以下に、サービス更新プログラムを管理するために使用できるサービス ツールの例を示します。

- **Windows Update (スタンドアロン)**:このオプションでは、インターネットに接続されていて、Windows Update を有効になっているサーバーで利用できるのみです。
- **Windows Server Update Services (WSUS)** は、Windows 10 と Windows Server の更新プログラムを詳細に管理することができ、Windows Server オペレーティング システムでネイティブに利用できます。 更新プログラムを延期できることに加えて、更新プログラムの承認層を追加し、準備できるたびに特定のコンピューターまたはコンピューターのグループに展開することを選択できます。
- **System Center Configuration Manager** では、サービスをきめ細かく制御できます。 IT 担当者は、更新プログラムを延期、承認することができ、展開のターゲットを設定し、帯域幅の使用と展開回数を管理するための複数のオプションを選択できます。

リソース、スタッフ、および専門知識に基づいて、既に、これらのオプションのいずれか 1 つまたは複数を使用している場合、 半期チャネルのリリースでも、同じプロセスを引き続き使用できます。たとえば、既に更新プログラムの管理に System Center Configuration Manager を使用している場合は、それを使い続けることができます。 同様に、WSUS を使っている場合は、引き続きそれを使うことができます。

## <a name="obtain-preview-releases-through-the-windows-insider-program"></a>Windows Insider Program を通じてプレビュー リリースを入手します。
Windows Server の初期ビルドのテストは、問題点をリリース前に発見できる可能性があるため、マイクロソフトとお客様の両方に役立ちます。 またお客様にとっては、製品の機能に直接影響を与える貴重な機会となります。 

ユーザーからのフィードバックは、全開発プロセスを通じて重要な役割を果たしており、マイクロソフトはこれによってできる限り迅速に製品を調整することができます。 事前テストとフィードバックは、迅速なリリース モデルに不可欠です。

Windows Insider Program に参加する方法について詳しくは、「[Windows Insider Program for Server docs (Windows Insider Program for Server のドキュメント)](https://docs.microsoft.com/windows-insider/at-work/)」をご覧ください。

## <a name="to-identify-windows-server-2019-and-windows-server-version-1809"></a>Windows Server 2019 と Windows Server Version 1809 を見分けるには

>[!Note]  
> 以下のガイダンスは、ライフサイクルと一般的なインベントリのみを目的として LTSC と SAC を見分け、区別するためのものです。  アプリケーションの互換性や、特定の API サーフェスを表現することは意図していません。  システムの使用期間中コンポーネント、API、機能が追加されることもあれば追加されないこともあるため、アプリ開発者は別のガイダンスを使って互換性を適切に確保してください。 [オペレーティング システムのバージョン](https://docs.microsoft.com/windows/desktop/SysInfo/operating-system-version)の方がアプリ開発者にとって適切な出発点です。

Powershell を開き、Get ItemProperty コマンドレットまたは Get ComputerInfo コマンドレットを使って、レジストリでこれらのプロパティを確認します。  ビルド番号と共にブランド年 (つまり 2019) があるかどうかによって、LTSC か SAC かがわかります。  LTSC にはこれがあり、SAC にはありません。  これは、ReleaseId または WindowsVersion (つまり 1809) によってリリースのタイミングと、インストールが Server Core であるかデスクトップ エクスペリエンス搭載サーバーであるかも返します。 

**Windows Server 2019 Datacenter Edition (LTSC) とデスクトップ エクスペリエンスの例:**

````PowerShell
Get-ItemProperty -Path "HKLM:\Software\Microsoft\Windows NT\CurrentVersion" | Select ProductName, ReleaseId, InstallationType, CurrentMajorVersionNumber,CurrentMinorVersionNumber,CurrentBuild
````

````
ProductName               : Windows Server 2019 Datacenter
ReleaseId                 : 1809
InstallationType          : Server
CurrentMajorVersionNumber : 10
CurrentMinorVersionNumber : 0
CurrentBuild              : 17763
````

**Windows Server、バージョン 1809 (SAC) Standard Edition サーバー コアの使用例:**

````PowerShell
Get-ItemProperty -Path "HKLM:\Software\Microsoft\Windows NT\CurrentVersion" | Select ProductName, ReleaseId, InstallationType, CurrentMajorVersionNumber,CurrentMinorVersionNumber,CurrentBuild
````

````
ProductName               : Windows Server Standard
ReleaseId                 : 1809
InstallationType          : Server Core
CurrentMajorVersionNumber : 10
CurrentMinorVersionNumber : 0
CurrentBuild              : 17763
````

**Windows Server 2019 Standard Edition (LTSC) サーバー コアの使用例:**


````PowerShell
Get-ComputerInfo | Select WindowsProductName, WindowsVersion, WindowsInstallationType, OsServerLevel, OsVersion, OsHardwareAbstractionLayer
````

````
WindowsProductName            : Windows Server 2019 Standard
WindowsVersion                : 1809
WindowsInstallationType       : Server Core
OsServerLevel                 : ServerCore
OsVersion                     : 10.0.17763
OsHardwareAbstractionLayer    : 10.0.17763.107
````

新しい [Server Core アプリ互換性 FOD](https://docs.microsoft.com/windows-server/get-started-19/install-fod-19) がサーバーに存在するかどうかを照会するには、[Get-WindowsCapability](https://docs.microsoft.com/powershell/module/dism/get-windowscapability?view=win10-ps) コマンドレットを使って以下を調べます。
````
Name    :     ServerCore.AppCompatibility~~~~0.0.1.0
State   :     Installed
````

# <a name="related-topics"></a>関連トピック
[Windows Server 半期チャネルでの Nano Server への変更](../get-started/nano-in-semi-annual-channel.md)

[Windows Server のサポート ライフ サイクル](https://support.microsoft.com/lifecycle)

[Server Core が実行されているかどうかを決定します。](https://msdn.microsoft.com/library/hh846315%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396)

[GetProductInfo 関数](https://docs.microsoft.com/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getproductinfo)

[ソフトウェア インベントリ ログ コマンドレット](https://docs.microsoft.com/powershell/module/softwareinventorylogging/?view=winserver2012R2-ps)
