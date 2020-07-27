---
title: サービス チャネル
description: Windows Server サービス チャネルの説明 - LTSC と SAC
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.localizationpriority: high
ms.date: 05/21/2019
ms.openlocfilehash: 1823816d2218c09c84e5eb61bf8af6bd3411a0d7
ms.sourcegitcommit: 78b59522234825c43b00c271a04c35f3fd9d65e3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86946596"
---
# <a name="windows-server-servicing-channels-ltsc-and-sac"></a>Windows Server サービス チャネル: LTSC と SAC

> 適用先:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)

Windows Server のユーザーは、長期サービス チャネルと半期チャネルの 2 つのリリース チャネルを利用できます。

ユーザーはニーズに最も適した方法を選択できます。サーバーを長期サービス チャネル (LTSC) のままにすることも、半期チャネルに移行することも、一部のサーバーをいずれかのトラックで利用することも可能です。

## <a name="long-term-servicing-channel-ltsc"></a>長期サービス チャネル (LTSC)

以前から使用されているリリース モデルです (旧称、“Long-Term Servicing *Branch*”)。このモデルでは、Windows Server の新しいメジャー バージョンが、2 ～ 3 年ごとにリリースされます。 ユーザーは、5 年間のメインストリーム サポートとそれに続く 5 年間の延長サポートを受けることができます。 このチャネルは、さらに長期のサービス オプションと機能安定性を必要とするシステムに適しています。 Windows Server 2019 およびそれ以前のバージョンの Windows Server の展開環境に対する、新しい半期チャネルのリリースによる影響はありません。 長期的なサービス チャネルでは、引き続きセキュリティ更新プログラムとセキュリティ以外の更新プログラムが提供されますが、新機能は提供されません。

> [!Note]
> **現在の LTSC 製品は Windows Server 2019 です**。 このチャネルを維持する場合は、Windows Server 2019 をインストールする (または使用を継続する) 必要があります。この場合、Server Core インストール オプションまたはデスクトップ エクスペリエンス搭載サーバーのインストール オプションでインストールすることができます。

## <a name="semi-annual-channel"></a>半期チャネル

半期チャネルは、迅速なイノベーションを行っているお客様にとって最適です。オペレーティング システムの新機能を、特にコンテナーとマイクロサービスにフォーカスして、より速いペースで活用することができます。 半期チャネルの Windows Server 製品は、年に 2 回、春と秋に新しいリリースが公開されます。 このチャネルの各リリースは、最初のリリースから 18 か月サポートされます。

半期チャネルで提供される機能のほとんどは、Windows Server の次回の長期サービス チャネル リリースに含まれます。 各リリースのエディション、機能、およびサポート コンテンツは、ユーザーのフィードバックに応じて変わる場合があります。

半期チャネルは、[ソフトウェア アシュアランス](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default.aspx) をご利用のボリューム ライセンスのお客様以外にも、Azure Marketplace やその他のクラウド/ホスティング サービス プロバイダー、Visual Studio サブスクリプションなどのロイヤルティ プログラム経由で入手できます。

> [!Note]  
> **半期チャネルの現在のリリースは、Windows Server バージョン 1909 です**。 サーバーをこのチャネルで利用する場合は、Windows Server バージョン 1909 をインストールする必要があります。この場合、Server Core モードで、またはコンテナー内で実行される Nano Server としてインストールすることができます。 長期サービス チャネル リリースからの一括アップグレードは、**異なるリリース チャネル**にあるためサポートされていません。 半期チャネルのリリースは更新プログラムではありません。これは、半期チャネルにおける Windows Server の次のリリースです。

このモデルでは、Windows Server のリリースが、リリースの年と月によって識別されます。たとえば、2017 年の 9 番目の月 (9 月) のリリースは、**バージョン 1709** となります。 半期チャネルでは、Windows Server の新しいリリースが毎年 2 回提供されます。 各リリースのサポート ライフサイクルは、18 か月です。

## <a name="should-you-keep-servers-on-the-ltsc-or-move-them-to-the-semi-annual-channel"></a>サーバーは LTSC のまま利用すべきでしょうか、それとも半期チャネルに移行すべきでしょうか。

決定にあたっては、次の重要な相違点を考慮する必要があります。

- Devops、コンテナー、マイクロサービスの新しいテクノロジをステップアップする必要がありますか。 そうであれば、**Windows Server バージョン 1909** をインストールして、**半期チャネルに参加**することを検討してください。 その場合、このトピックで説明したように、年に 2 回新しいバージョンを受け取り、各リリースのメインストリームの運用サポートは 18 か月になります。 これは、ボリューム ライセンス、Azure、または Visual Studio サブスクリプション サービスを通じて提供されます。 現時点では、製品を運用環境で実行する場合に、半期チャネルのリリースを利用するには、ボリューム ライセンスとソフトウェア アシュアランスが必要です。
- 安定性と予測可能性を確保する必要がありますか。 物理サーバー上の仮想マシンと従来のワークロードを実行する必要がありますか。 そうであれば、**それらのサーバーを長期サービス チャネルのまま**利用します。 現在の LTSC リリースは、**Windows Server 2019** です。 その場合、このトピックで説明したように、2 から 3 年ごとに新しいバージョンが提供されます。各リリースのメインストリームの運用サポートは 5 年間で、その後 5 年間サポートを延長することができます。 LTSC リリースは、すべてのリリース メカニズムで利用できます。 LTSC のリリースは、使用しているライセンス モデルに関係なく、すべてのユーザーが利用できます。 

次の表は、チャネル間の主な違いをまとめたものです。


|                       |                                                              長期サービス チャネル (Windows Server 2019)                                                               |                                   半期チャネル (Windows Server)                                   |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| 推奨されるシナリオ | 汎用ファイル サーバー、Microsoft と Microsoft 以外のワークロード、従来のアプリ、インフラストラクチャの役割、ソフトウェア定義データセンター、ハイパーコンバージド インフラストラクチャ | コンテナー化されたアプリケーション、コンテナー ホスト、および迅速なイノベーションを活用するアプリケーション シナリオ |
|     新しいリリース      |                                                                               2 から 3 年ごと                                                                                |                                              6 か月ごと                                              |
|        サポート        |                                                       5 年間のメインストリーム サポートとそれに続く 5 年間の延長サポート                                                        |                                                18 か月                                                 |
|       エディション        |                                                                    利用可能なすべての Windows Server エディション                                                                     |                                     Standard エディションと Datacenter エディション                                     |
|      利用できるユーザー      |                                                                      すべてのチャネルのすべてのユーザー                                                                      |                               ソフトウェア アシュアランスとクラウドのユーザーのみ                                |
| インストール オプション  |                                                                Server Core とデスクトップ エクスペリエンス搭載サーバー                                                                |                 コンテナー ホストとコンテナー イメージの Server Core および Nano Server コンテナー イメージ                 |

## <a name="device-compatibility"></a>デバイスの互換性

特に断りのない限り、半期チャネルのリリースを実行するための最小ハードウェア要件は、Windows Server の最新の長期サービス チャネルのリリースと同じです。 たとえば、**長期サービス チャネルの現行リリースは、Windows Server 2019 です**。 ほとんどのハードウェア ドライバーは、引き続きこれらのリリースで機能します。

## <a name="servicing"></a>サービス

セキュリティ更新プログラムとセキュリティ以外の更新プログラムで、長期サービス チャネルと半期チャネルの両方のリリースがサポートされます。 ただし、前述のように、サポート期間の長さはリリースによって異なります。

### <a name="servicing-tools"></a>サービス ツール

IT 担当者が Windows Server を操作するためのツールは数多く存在します。 機能や制御からシンプルさや管理要件の低さまで、各オプションにはそれぞれ長所と短所があります。 以下に、サービス更新プログラムを管理するために使用できるサービス ツールの例を示します。

- **Windows Update (スタンドアロン)** : このオプションは、インターネットに接続されていて、Windows Update が有効にされているサーバーでのみ利用できます。
- **Windows Server Update Services (WSUS)** は、Windows 10 と Windows Server の更新プログラムを詳細に管理することができ、Windows Server オペレーティング システムでネイティブに利用できます。 更新プログラムを延期できることに加えて、更新プログラムの承認層を追加し、準備できるたびに特定のコンピューターまたはコンピューターのグループに展開することを選択できます。
- **Microsoft Endpoint Configuration Manager** では、サービスを最も制御できます。 IT 担当者は、更新プログラムを延期、承認することができ、展開のターゲットを設定し、帯域幅の使用と展開回数を管理するための複数のオプションを選択できます。

リソース、スタッフ、および専門知識に基づいて、既に、これらのオプションのいずれか 1 つまたは複数を使用している場合、 半期チャネルのリリースでも、同じプロセスを引き続き使用できます。たとえば、既に更新プログラムの管理に Configuration Manager を使用している場合は、それを使い続けることができます。 同様に、WSUS を使っている場合は、引き続きそれを使うことができます。

## <a name="where-to-obtain-semi-annual-channel-releases"></a>半期チャネルのリリースを入手する場所

半期チャネルのリリースは、クリーン インストールでインストールする必要があります。

- ボリューム ライセンス サービス センター (VLSC): [ソフトウェア アシュアランス](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default.aspx)をご利用になっているボリューム ライセンスのお客様は、[ボリューム ライセンス サービス センター](https://www.microsoft.com/Licensing/servicecenter/default.aspx)に移動して、 **[サインイン]** をクリックすることによって、このリリースを入手できます。 次に、 **[Downloads and Keys]** (ダウンロードとキー) をクリックし、このリリースを検索します。

- 半期チャネルのリリースは [Microsoft Azure](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.WindowsServer?tab=Overview) でも入手できます。

- Visual Studio サブスクリプション: Visual Studio サブスクライバーが半期チャネルのリリースを入手するには、[Visual Studio サブスクライバー ダウンロード ページ](https://my.visualstudio.com/downloads?pid=2347)からダウンロードします。 まだサブスクライバーではない場合は、[Visual Studio サブスクリプション](https://www.visualstudio.com/subscriptions/)にサインアップしてから、上記のように [Visual Studio サブスクライバーのダウンロード ページ](https://my.visualstudio.com/downloads?pid=2347)にアクセスします。 Visual Studio サブスクリプション経由で入手したリリースは、開発とテストにのみ利用できます。

- Windows Insider Program を通じてプレビュー リリースを入手します。Windows Server の初期ビルドのテストは、問題点をリリース前に発見できる可能性があるため、マイクロソフトとお客様の両方に役立ちます。 またお客様にとっては、製品の機能に直接影響を与える貴重な機会となります。
ユーザーからのフィードバックは、全開発プロセスを通じて重要な役割を果たしており、マイクロソフトはこれによってできる限り迅速に製品を調整することができます。 事前テストとフィードバックは、迅速なリリース モデルに不可欠です。 Windows Insider Program に参加する場合は、「[Windows Insider Program for Server docs](/windows-insider/at-work/)」 (Windows Insider Program for Server のドキュメント) をご覧ください。

## <a name="activating-semi-annual-channel-releases"></a>半期チャネルのリリースのライセンス認証

- Microsoft Azure を使用している場合、このリリースは自動的にライセンス認証されます。
- ボリューム ライセンス サービス センターまたは Visual Studio サブスクリプションからこのリリースを入手した場合、そのライセンス認証を行うには、ご利用のキー管理システム (KMS) 環境で Windows Server 2019 CSVLK を使用します。 詳細については、「[KMS クライアント セットアップ キー](../get-started/kmsclientkeys.md)」を参照してください。

Windows Server 2019 の前にリリースされた半期チャネルのリリースでは、Windows Server 2016 CSVLK が使用されます。

## <a name="why-do-semi-annual-channel-releases-offer-only-the-server-core-installation-option"></a>半期チャネルのリリースで Server Core インストール オプションしか提供されていないのはどうしてですか?

Windows Server の各リリースの計画で最も重要な手順の 1 つは、お客様からのフィードバック、つまりお客様がどのように Windows Server を使用しているかについて情報を収集することです。 どのような新機能が、Windows Server の展開、言い換えれば、お客様の日常的なビジネスに大きな影響を与えるでしょうか。 お客様からのフィードバックは、新しい技術革新をできるだけ迅速かつ効率的に提供することが最優先であることを示しています。 同時に、最も迅速に技術革新を進めているお客様からは、主に PowerShell でコマンド ライン スクリプトを使用してデータ センターを管理しているため、デスクトップ エクスペリエンス モードでインストールされた Windows Server で利用可能なデスクトップ GUI の必要性は高くないというご意見をいただいています。特に、ご利用のサーバーをリモートで管理するために、[Windows Admin Center](../manage/windows-admin-center/overview.md) を使用できるようになりました。

Server Core インストール オプションに重点を置くことによって、従来の Windows Server プラットフォームの機能やアプリケーションとの互換性を維持しながら、新しい技術革新により多くのリソースを割り当てることができます。 Windows Server と今後のリリースに関して、この問題を含むさまざまな問題に関するフィードバックがある場合は、[フィードバック Hub](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) を通じてご意見やご提案をお寄せください。

## <a name="what-about-nano-server"></a>Nano Server について

Nano Server は、半期チャネルでのコンテナー オペレーティング システムとして使用できます。 詳細については、「[Windows Server 半期チャネルで Nano Server に加えられる変更](../get-started/nano-in-semi-annual-channel.md)」を参照してください。

## <a name="how-to-tell-whether-a-server-is-running-an-ltsc-or-sac-release"></a>LTSC または SAC のいずれのリリースがサーバーで実行されているかを確認する方法

一般的に言って、長期サービス チャネルのリリース (Windows Server 2019 など) は、半期チャネルの新しいバージョン (Windows Server バージョン 1809 など) と同時にリリースされます。 このため、半期チャネルのリリースがサーバーで実行されているかどうかを判断するのが少し面倒になる場合があります。 ビルド番号を調べるのでなく、製品名を調べる必要があります。半期チャネルのリリースでは Windows Server Standard または Windows Server Datacenter といった製品名がバージョン番号なしで使用されます。一方、長期サービス チャネルのリリースには Windows Server 2019 Datacenter のようにバージョン番号が含まれます。

> [!Note]
> 以下のガイダンスは、ライフサイクルと一般的なインベントリのみを目的として LTSC と SAC を見分け、区別するためのものです。  アプリケーションの互換性や、特定の API サーフェスを表現することは意図していません。  システムの使用期間中コンポーネント、API、機能が追加されることもあれば追加されないこともあるため、アプリ開発者は別のガイダンスを使って互換性を適切に確保してください。 アプリ開発者は[オペレーティング システムのバージョン](/windows/desktop/sysinfo/operating-system-version)から開始することをお勧めします。

PowerShell を開き、Get-ItemProperty コマンドレットまたは Get-ComputerInfo コマンドレットを使って、レジストリでこれらのプロパティを確認します。  ビルド番号と共にブランド年 (つまり 2019) があるかどうかによって、LTSC か SAC かがわかります。  LTSC にはこれがあり、SAC にはありません。  これは、ReleaseId または WindowsVersion (つまり 1809) によってリリースのタイミングと、インストールが Server Core であるかデスクトップ エクスペリエンス搭載サーバーであるかも返します。

**Windows Server 2019 Datacenter Edition (LTSC) (デスクトップ エクスペリエンスあり) の例:**

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

**Windows Server Version 1809 (SAC) Standard Edition Server Core の例:**

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

**Windows Server 2019 Standard Edition (LTSC) Server Core の例:**


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

新しい [Server Core アプリ互換性 FOD](./install-fod-19.md) がサーバーに存在するかどうかを照会するには、[Get-WindowsCapability](/powershell/module/dism/get-windowscapability?view=win10-ps) コマンドレットを使って以下を調べます。
````
Name    :     ServerCore.AppCompatibility~~~~0.0.1.0
State   :     Installed
````

## <a name="additional-references"></a>その他の参照情報

[Windows Server 半期チャネルで Nano Server に加えられる変更](../get-started/nano-in-semi-annual-channel.md)

[Windows Server のサポート ライフサイクル](https://support.microsoft.com/lifecycle)

[Server Core が実行されているかどうかを調べる](/previous-versions/windows/desktop/legacy/hh846315(v=vs.85)?f=255&MSPPError=-2147217396)

[GetProductInfo 関数](/windows/desktop/api/sysinfoapi/nf-sysinfoapi-getproductinfo)

[ソフトウェア インベントリ ログ コマンドレット](/powershell/module/softwareinventorylogging/?view=winserver2012R2-ps)
