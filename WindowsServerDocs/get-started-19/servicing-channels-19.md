---
title: サービス チャネル
description: Windows Server サービスのチャネルの説明:LTSC と SAC
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: high
ms.date: 05/21/2019
ms.openlocfilehash: 625d71edd00ce404cee9525e06a2237d8be4cfcb
ms.sourcegitcommit: c8cc0b25ba336a2aafaabc92b19fe8faa56be32b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65976460"
---
# <a name="windows-server-servicing-channels-ltsc-and-sac"></a>Windows Server がチャネルをサービス:LTSC と SAC

>適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

Windows Server のユーザーは、長期サービス チャネルと半期チャネルの 2 つのチャネルを利用できます。

ユーザーはニーズに最も適した方法を選択できます。サーバーを長期サービス チャネル (LTSC) のままにすることも、半期チャネルに移行することも、一部のサーバーをいずれかのトラックで利用することも可能です。

## <a name="long-term-servicing-channel-ltsc"></a>長期的なサービス チャネル (LTSC)

以前から使用されているリリース モデルです (旧称、“Long-Term Servicing *Branch*”)。このモデルでは、Windows Server の新しいメジャー バージョンが、2 ～ 3 年ごとにリリースされます。 ユーザーは、5 年間のメインストリーム サポートとそれに続く 5 年間の延長サポートを受けることができます。 このチャネルは、長期のサービス オプションと機能安定性を必要とするシステムに適しています。 Windows Server 2016 およびそれ以前のバージョンの Windows Server の展開環境に対する、新しい半期チャネルのリリースによる影響はありません。 長期的なサービス チャネルでは、引き続きセキュリティ更新プログラムとセキュリティ以外の更新プログラムが提供されますが、新機能は提供されません。

> [!Note]  
> **現在の LTSC 製品は Windows Server 2019 です**。 このチャネルを維持する場合は、Windows Server 2019 をインストールする (または使用を継続する) 必要があります。この場合、Server Core インストール オプションまたはデスクトップ エクスペリエンス インストール オプションでインストールすることができます。

## <a name="semi-annual-channel"></a>半期チャネル

半期チャネルは迅速に活用するために新しいオペレーティング システムの機能の両方のアプリケーションで高速のペースで特にのコンテナーとマイクロ サービス、およびソフトウェア定義でビルドされた革新はお客様に最適です。ハイブリッド データ センターです。 半期チャネルの Windows Server 製品は、年に 2 回、春と秋に新しいリリースが公開されます。 このチャネルの各リリースは、最初のリリースから 18 か月サポートされます。

半期チャネルで提供される機能のほとんどは、Windows Server の次回の長期的なサービス チャネル リリースに含まれます。 各リリースのエディション、機能、およびサポート コンテンツは、ユーザーのフィードバックに応じて異なる場合があります。

半期チャネルは、ボリューム ライセンスのお客様は[ソフトウェア アシュアランス](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx)も、Azure Marketplace またはその他のクラウドに/ホスティングを使用してサービス プロバイダーやロイヤルティ プログラムなど、Visual Studio サブスクリプションとして。

> [!Note]  
> **現在の半期チャネル リリースは、Windows Server バージョンが 1903**します。 このチャネルでサーバーに配置する場合は、Windows Server、Server Core モードまたはコンテナーで実行する Nano Server としてインストールできるバージョン 1903 年をインストールする必要があります。 含まれているために、長期的なサービス チャネル リリースからのインプレース アップグレードはサポートされていません**別のリリース チャネル**します。 半期チャネル リリースのない更新プログラム – 半期チャネルでは、次の Windows Server リリースです。

このモデルでは、Windows Server のリリースが、リリースの年と月によって識別されます。たとえば、2017 年の 9 番目の月 (9 月) のリリースは、**バージョン 1709** となります。 半期チャネルでは、Windows Serverの新しいリリースが毎年 2 回提供されます。 各リリースのサポート ライフサイクルは、18 か月です。

## <a name="should-you-keep-servers-on-the-ltsc-or-move-them-to-the-semi-annual-channel"></a>サーバーを LTSC のまま利用するべきか、半期チャネルに移行すべきか

決定にあたっては、次の重要な相違点を考慮する必要があります。

- 革新的な機能を迅速に取り入れる必要がありますか。 Windows Server の最新機能への早期アクセスが必要ですか。 頻繁に更新されるハイブリッド アプリケーション、DevOps、および Hyper-V ファブリックをサポートする必要がありますか。 考慮する必要がありますので場合、**半期チャネルに参加する**をインストールして**Windows Server バージョンが 1903**します。 その場合、このトピックで説明したように、年に 2 回新しいバージョンを受け取り、各リリースのメインストリームの運用サポートは 18 か月になります。 これは、ボリューム ライセンス、Azure、または Visual Studio サブスクリプション サービスを通じて提供されます。 現時点では、製品を運用環境で実行する場合に、半期チャネルのリリースを利用するには、ボリューム ライセンスとソフトウェア アシュアランスが必要です。
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

- **Windows Update (スタンドアロン)** :このオプションでは、インターネットに接続されていて、Windows Update を有効になっているサーバーで利用できるのみです。
- **Windows Server Update Services (WSUS)** は、Windows 10 と Windows Server の更新プログラムを詳細に管理することができ、Windows Server オペレーティング システムでネイティブに利用できます。 更新プログラムを延期できることに加えて、更新プログラムの承認層を追加し、準備できるたびに特定のコンピューターまたはコンピューターのグループに展開することを選択できます。
- **System Center Configuration Manager** では、サービスをきめ細かく制御できます。 IT 担当者は、更新プログラムを延期、承認することができ、展開のターゲットを設定し、帯域幅の使用と展開回数を管理するための複数のオプションを選択できます。

リソース、スタッフ、および専門知識に基づいて、既に、これらのオプションのいずれか 1 つまたは複数を使用している場合、 半期チャネルのリリースでも、同じプロセスを引き続き使用できます。たとえば、既に更新プログラムの管理に System Center Configuration Manager を使用している場合は、それを使い続けることができます。 同様に、WSUS を使っている場合は、引き続きそれを使うことができます。

## <a name="where-to-obtain-semi-annual-channel-releases"></a>半期チャネルを取得する場所を解放します。

半期チャネル リリースは、クリーン インストールとしてインストールする必要があります。

- ボリューム ライセンス サービス センター (VLSC):ボリューム ライセンスのお客様[ソフトウェア アシュアランス](https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx)に移動して、このリリースを取得できます、[ボリューム ライセンス サービス センター](https://www.microsoft.com/Licensing/servicecenter/default.aspx)クリック**サインイン**します。 次に、 **[Downloads and Keys]** (ダウンロードとキー) をクリックし、このリリースを検索します。 

- 半期チャネル リリースがでも利用できる[Microsoft Azure](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.WindowsServer?tab=Overview)します。

- Visual Studio サブスクリプション:Visual Studio サブスクライバーが半期チャネル リリースをからダウンロードして取得できます、 [Visual Studio サブスクライバー ダウンロード ページ](https://my.visualstudio.com/downloads?pid=2347)します。 まだサブスクライバーではない場合は、[Visual Studio サブスクリプション](https://www.visualstudio.com/subscriptions/)にサインアップしてから、上記のように [Visual Studio サブスクライバーのダウンロード ページ](https://my.visualstudio.com/downloads?pid=2347)にアクセスします。 Visual Studio サブスクリプション経由で入手したリリースは、開発とテストにのみ利用できます。

- Windows Insider プログラムを介したプレビュー リリースを入手します。Windows Server の初期ビルドのテストは、問題点をリリース前に発見できる可能性があるため、マイクロソフトとお客様の両方に役立ちます。 またお客様にとっては、製品の機能に直接影響を与える貴重な機会となります。   
ユーザーからのフィードバックは、全開発プロセスを通じて重要な役割を果たしており、マイクロソフトはこれによってできる限り迅速に製品を調整することができます。 事前テストとフィードバックは、迅速なリリース モデルに不可欠です。 Windows Insider Program にご参加を参照してください、 [Server のドキュメントの Windows Insider Program](https://docs.microsoft.com/windows-insider/at-work/)します。

## <a name="activating-semi-annual-channel-releases"></a>半期チャネルをアクティブ化のリリースします。

- Microsoft Azure を使用している場合このリリースに自動的にアクティブにする必要があります。
- このリリースから、ボリューム ライセンス サービス センターまたは Visual Studio サブスクリプションで入手した場合は、キー管理サービス (KMS) 環境と Windows Server の 2019 CSVLK を使用してアクティブ化できます。 詳細については、次を参照してください。 [KMS クライアント セットアップ キー](../get-started/kmsclientkeys.md)します。

Windows Server 2019 する前にリリースされた場合は半期チャネル リリースでは、Windows Server 2016 の CSVLK を使用します。

## <a name="why-do-semi-annual-channel-releases-offer-only-the-server-core-installation-option"></a>半期チャネル リリースの Server Core インストール オプションのみの勧める理由

Windows Server の各リリースの計画で最も重要な手順の 1 つは、お客様からのフィードバック、つまりお客様がどのように Windows Server を使用しているかについて情報を収集することです。 どのような新機能が、Windows Server の展開、言い換えれば、お客様の日常的なビジネスに大きな影響を与えるでしょうか。 お客様からのフィードバックは、新しい技術革新をできるだけ迅速かつ効率的に提供することが最優先であることを示しています。 同時に、最も迅速に革新顧客のことが指定されました主に使用しているコマンド ラインは、PowerShell を使用したスクリプトを複数のデータ センターを管理して、そのため、強力ないないことのデスクトップの GUI のインストールで使用できる必要がありますデスクトップ エクスペリエンス搭載の Windows Server 今[Windows Admin Center](../manage/windows-admin-center/overview.md)はリモート サーバーの管理に使用できます。

Server Core インストール オプションに重点を置くことによって、従来の Windows Server プラットフォームの機能やアプリケーションとの互換性を維持しながら、新しい技術革新により多くのリソースを割り当てることができます。 Windows Server と今後のリリースに関して、この問題を含むさまざまな問題に関するフィードバックがある場合は、[フィードバック Hub](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) を通じてご意見やご提案をお寄せください。

## <a name="what-about-nano-server"></a>Nano Server について

Nano Server は半期チャネルでコンテナーのオペレーティング システムとして使用できます。 詳細については、「[Windows Server 半期チャネルでの Nano Server の変更点](../get-started/nano-in-semi-annual-channel.md)」をご覧ください。

## <a name="how-to-tell-whether-a-server-is-running-an-ltsc-or-sac-release"></a>サーバーが LTSC または SAC リリースを実行しているかどうかを確認する方法

一般に、長期的なサービス チャネルは、Windows Server 2019 が半期チャネルは、Windows Server、バージョンは 1809 などの新しいバージョンとして同時にリリースされたなどを解放します。 これは、ため、サーバーが半期チャネル リリースを実行しているかどうかを判断する、少し注意が必要になります。 ビルド番号を調べる代わりには、製品名を参照してください。半期チャネル リリースでは、"Windows Server Standard"または"Windows Server Datacenter"製品名のバージョン番号を使用して、長期的なサービス チャネル リリースの例では、"Windows Server 2019 Datacenter"、バージョン番号を含めます。

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

## <a name="see-also"></a>関連項目

[Windows Server 半期チャネルでの Nano Server への変更](../get-started/nano-in-semi-annual-channel.md)

[Windows Server のサポート ライフ サイクル](https://support.microsoft.com/lifecycle)

[Server Core が実行されているかどうかを決定します。](https://msdn.microsoft.com/library/hh846315%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396)

[GetProductInfo 関数](https://docs.microsoft.com/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getproductinfo)

[ソフトウェア インベントリ ログ コマンドレット](https://docs.microsoft.com/powershell/module/softwareinventorylogging/?view=winserver2012R2-ps)
