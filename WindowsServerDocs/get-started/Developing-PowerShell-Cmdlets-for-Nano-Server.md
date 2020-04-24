---
title: Nano Server 用の PowerShell コマンドレットを開発する
description: CIM の移植, .NET コマンドレット, C++
ms.prod: windows-server
manager: DonGill
ms.technology: server-nano
ms.topic: article
ms.assetid: 7b4267f0-1c91-4a40-9262-5daf4659f686
author: jaimeo
ms.author: jaimeo
ms.date: 09/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3965e453483b3515e4957ecfaba39cf9a0b8104f
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80827075"
---
# <a name="developing-powershell-cmdlets-for-nano-server"></a>Nano Server 用の PowerShell コマンドレットを開発する

>適用先:Windows Server 2016

> [!IMPORTANT]
> Windows Server バージョン 1709 以降では、Nano Server は[コンテナーの基本 OS イメージ](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)としてのみ提供されます。 その意味については、[Nano Server に加えられる変更](nano-in-semi-annual-channel.md)に関する記事をご覧ください。 
  
## <a name="overview"></a>概要  
すべての Nano Server インストールには PowerShell Core が既定で含まれます。 PowerShell Core は、.NET Core に基づいて作成された PowerShell のフットプリントが小さいエディションであり、Windows のフットプリントが小さいエディション (Nano Server、Windows IoT Core など) で動作します。 PowerShell Core は、PowerShell の他のエディション (Windows Server 2016 で実行される Windows PowerShell など) と同じように動作します。 ただし、Nano Server のフットプリントが小さいため、Nano Server 上の PowerShell Core では、Windows Server 2016 の PowerShell 機能のうち、使用できない機能があります。  
  
このトピックでは、Nano Server 上で実行したい既存の PowerShell コマンドレットがある場合や、Nano Server 上で実行する新しい PowerShell コマンドレットを開発する場合に役立つヒントと推奨事項を紹介します。  

## <a name="powershell-editions"></a>PowerShell のエディション  
  
  
PowerShell は、バージョン 5.1 以降、機能セットとプラットフォーム互換性が異なるさまざまなエディションが提供されるようになりました。  
  
- **Desktop Edition:** .NET Framework 上に構築され、Windows の完全フットプリント エディション (Server Core、Windows Desktop など) で実行される PowerShell のバージョンをターゲットとするスクリプトおよびモジュールと互換性があります。  
- **Core Edition:** .NET Core 上に構築され、Windows のフットプリントが小さいエディション (Nano Server、Windows IoT など) で実行される PowerShell のバージョンをターゲットとするスクリプトおよびモジュールと互換性があります。  
  
PowerShell の実行中のエディションは、$PSVersionTable の PSEdition プロパティに表示されます。  
```powershell  
$PSVersionTable  
  
Name                           Value  
----                           -----  
PSVersion                      5.1.14300.1000  
PSEdition                      Desktop  
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}  
CLRVersion                     4.0.30319.42000  
BuildVersion                   10.0.14300.1000  
WSManStackVersion              3.0  
PSRemotingProtocolVersion      2.3  
SerializationVersion           1.1.0.1  
```  
  
モジュールの作成者は、CompatiblePSEditions モジュール マニフェスト キーを使用して、モジュールが 1 つまたは複数の PowerShell エディションと互換性があることを宣言できます。 このキーは、PowerShell 5.1 以降でのみサポートされます。  
```powershell  
New-ModuleManifest -Path .\TestModuleWithEdition.psd1 -CompatiblePSEditions Desktop,Core -PowerShellVersion 5.1  
$moduleInfo = Test-ModuleManifest -Path \TestModuleWithEdition.psd1  
$moduleInfo.CompatiblePSEditions  
Desktop  
Core  
  
$moduleInfo | Get-Member CompatiblePSEditions  
  
   TypeName: System.Management.Automation.PSModuleInfo  
  
Name                 MemberType Definition  
----                 ---------- ----------  
CompatiblePSEditions Property   System.Collections.Generic.IEnumerable[string] CompatiblePSEditions {get;}  
  
```  
利用可能なモジュールの一覧を取得するとき、PowerShell のエディションで一覧にフィルターを適用できます。  
```powershell  
Get-Module -ListAvailable | ? CompatiblePSEditions -Contains Desktop  
  
    Directory: C:\Program Files\WindowsPowerShell\Modules  
  
  
ModuleType Version    Name                                ExportedCommands  
---------- -------    ----                                ----------------  
Manifest   1.0        ModuleWithPSEditions  
  
Get-Module -ListAvailable | ? CompatiblePSEditions -Contains Core | % CompatiblePSEditions  
Desktop  
Core  
  
```  
スクリプトの作成者は、#requires ステートメントに PSEdition パラメーターを使用することで、PowerShell の互換性のあるエディション以外でスクリプトが実行されるのを防止できます。  
```powershell  
Set-Content C:\script.ps1 -Value #requires -PSEdition Core  
Get-Process -Name PowerShell  
Get-Content C:\script.ps1  
#requires -PSEdition Core  
Get-Process -Name PowerShell  
  
C:\script.ps1  
C:\script.ps1 : The script 'script.ps1' cannot be run because it contained a #requires statement for PowerShell editions 'Core'. The edition of PowerShell that is required by the script does not match the currently running PowerShell Desktop edition.  
At line:1 char:1  
+ C:\script.ps1  
+ ~~~~~~~~~~~~~  
    + CategoryInfo          : NotSpecified: (script.ps1:String) [], RuntimeException  
    + FullyQualifiedErrorId : ScriptRequiresUnmatchedPSEdition  
```  
  
  
## <a name="installing-nano-server"></a>Nano Server のインストール  
仮想マシンまたは物理マシンに Nano Server をインストールするためのクイックスタートおよび詳細な手順については、このトピックの親トピックである「[Nano Server のインストール](Getting-Started-with-Nano-Server.md)」を参照してください。  
  
> [!NOTE]  
> Nano Server 上で開発を行うには、New-NanoServerImage の -Development パラメーターを使用して Nano Server をインストールすると便利です。 これにより、署名されていないドライバーのインストール、デバッガー バイナリのコピー、デバッグ用にポートを開く操作、テスト署名、開発者用ライセンスなしでの AppX パッケージのインストールを行うことができるようになります。 たとえば、次のように入力します。  
>  
>`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -Development`  
  
## <a name="determining-the-type-of-cmdlet-implementation"></a>コマンドレットの実装の種類の決定  
PowerShell では、コマンドレットに対していくつかの実装の種類をサポートしています。どの種類の実装を使用しているかによって、Nano Server で実行するコマンドレットの作成操作および移植操作に必要なプロセスとツールが異なります。 サポートされている実装の種類は次のとおりです。  
* CIM - CIM (WMIv2) プロバイダーの上に階層的に配置された CDXML ファイルで構成されます。   
* .NET - .NET アセンブリで構成され、管理されたコマンドレット インターフェイス (通常は C# で記述します) を実装します。   
* PowerShell スクリプト - PowerShell 言語で記述されたスクリプト モジュール (.psm1) またはスクリプト (.ps1) で構成されます。   
  
移植する既存のコマンドレットに使用されている実装の種類がわからない場合は、製品または機能をインストールし、次のいずれかの場所にある PowerShell モジュール フォルダーを探します。   
  
* %windir%\system32\WindowsPowerShell\v1.0\Modules   
* %ProgramFiles%\WindowsPowerShell\Modules   
* %UserProfile%\Documents\WindowsPowerShell\Modules   
* \<製品のインストール場所>   
    
  次のことを理解したうえでこれらの場所を確認します。  
  * CIM コマンドレットは、拡張子が .cdxml ファイルです。  
  * .NET コマンドレットは、拡張子が .dll ファイル拡張子です。または、アセンブリが、.psd1 ファイルの RootModule、ModuleToProcess、または NestedModules フィールドの下に記載されている GAC にインストールされています。  
* PowerShell スクリプトのコマンドレットは、拡張子が .psm1 または .ps1 のファイル拡張子です。   
  
## <a name="porting-cim-cmdlets"></a>CIM コマンドレットの移植  
通常、これらのコマンドレットは、変換せずに Nano Server で動作します。 ただし、基になる WMI v2 プロバイダーを Nano Server で動作するように移植していない場合は、移植する必要があります。  
  
### <a name="building-c-for-nano-server"></a>Nano Server 向けの C++ のビルド  
C++ の DLL を Nano Server で実行するには、特定のエディションではなく Nano Server を対象にコンパイルします。  
  
Nano Server 上の C++ の開発に関する前提条件とチュートリアルについては、「[Developing Native Apps on Nano Server (Nano Server でのネイティブ アプリの開発)](https://blogs.technet.com/b/nanoserver/archive/2016/04/27/developing-native-apps-on-nano-server.aspx)」を参照してください。  
  
  
## <a name="porting-net-cmdlets"></a>.NET コマンドレットの移植  
ほとんどの C# コードは Nano Server でサポートされます。 [ApiPort](https://github.com/Microsoft/dotnet-apiport) を使用すると、互換性のない API を検出できます。  
  
### <a name="powershell-core-sdk"></a>PowerShell Core SDK  
[PowerShell ギャラリー](https://www.powershellgallery.com/packages/Microsoft.PowerShell.NanoServer.SDK/)から入手できる Microsoft.PowerShell.NanoServer.SDK モジュールを使用すると、Nano Server で使用可能な CoreCLR および PowerShell Core のバージョンをターゲットとする .NET コマンドレットを Visual Studio 2015 Update 2 で簡単に開発できるようになります。 このモジュールは、PowerShellGet と次のコマンドを使用してインストールすることができます。  
  
`Find-Module Microsoft.PowerShell.NanoServer.SDK -Repository PSGallery | Install-Module -Scope <scope>`  
  
PowerShell Core SDK モジュールは、適切な CoreCLR および PowerShell Core 参照アセンブリをセットアップするためのコマンドレット、これらの参照アセンブリをターゲットとする C# プロジェクトを Visual Studio 2015 で作成するためのコマンドレット、および Nano Server コンピューター上にリモート デバッガーをセットアップするためのコマンドレットを公開します。そのため、開発者は、Visual Studio 2015 を使って、Nano Server 上で実行される .NET コマンドレットをリモートでデバッグできます。  
  
PowerShell Core SDK モジュールを使用するには、Visual Studio 2015 Update 2 が必要です。 Visual Studio 2015 がインストールされていない場合は、[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) をインストールできます。  
  
この SDK モジュールは、Visual Studio 2015 でインストールする次の機能にも依存します。  
  
- [Windows 開発と Web 開発]、[ユニバーサル Windows アプリ開発ツール]、[ツール (1.3.1) と Windows 10 SDK] の順にクリック  
  
SDK モジュールを使用する前に Visual Studio のインストールを確認して、これらの前提条件が満たされていることを確認します。 必ず Visual Studio のインストール時に上記の機能をインストールするよう選択するか、または既存の Visual Studio 2015 インストールを変更して上記の機能をインストールしてください。  
  
PowerShell Core SDK モジュールには、次のコマンドレットが含まれています。  
- New-NanoCSharpProject: Nano Server の Windows Server 2016 リリースに含まれている CoreCLR と PowerShell Core をターゲットとする新しい Visual Studio C# プロジェクトを作成します。  
- Show-SdkSetupReadMe: エクスプローラーで SDK のルート フォルダーを開き、手動セットアップ用の README.txt ファイルを開きます。  
- Install-RemoteDebugger: Nano Server コンピューターに Visual Studio リモート デバッガーをインストールし、構成します。  
- Start-RemoteDebugger: Nano Server が実行されているリモート コンピューターでリモート デバッガーを起動します。  
- Stop-RemoteDebugger: Nano Server が実行されているリモート コンピューターでリモート デバッガーを停止します。  
  
これらのコマンドレットの使い方の詳細については、モジュールをインストールしてインポートした後、次のように各コマンドレットに対して Get-Help を実行します。  
  
`Get-Command -Module Microsoft.PowerShell.NanoServer.SDK | Get-Help -Full`   
  
  
### <a name="searching-for-compatible-apis"></a>互換性のある API の検索  
  
API カタログ内で .NET Core を検索したり、Core CLR 参照アセンブリを逆アセンブルしたりできます。 .NET API のプラットフォームの移植性の詳細については、「[Platform Portability (プラットフォームの移植性)](https://github.com/Microsoft/dotnet-apiport/blob/master/docs/HowTo/PlatformPortability.md)」を参照してください。  
  
### <a name="pinvoke"></a>PInvoke  
Nano Server で使用される Core CLR では、kernel32.dll、advapi32.dll などのいくつかの基本的な DLL が多数の API セットに分割されました。そのため、PInvoke が正しい API を参照していることを確認する必要があります。 互換性がない場合は、実行時エラーが発生します。  
  
Nano Server でサポートされているネイティブ API の一覧については、「[Nano Server APIs (Nano Server の API)](https://msdn.microsoft.com/library/mt588480(v=vs.85).aspx)」を参照してください。  
  
### <a name="building-c-for-nano-server"></a>Nano Server 向けの C# のビルド  
  
Visual Studio 2015 で `New-NanoCSharpProject` を使用して作成した C# プロジェクトをビルドするには、 **[ビルド]** メニューをクリックし、 **[プロジェクトのビルド]** または **[ソリューションのビルド]** を選択します。 アセンブリは、Nano Server に付属する正しい CoreCLR および PowerShell Core をターゲットとして生成されます。そのため、Nano Server を実行しているコンピューターにコピーするだけでこのアセンブリを使用できます。  
  
### <a name="building-managed-c-cppcli-for-nano-server"></a>Nano Server 向けのマネージド C++ (CPP/CLI) のビルド  
マネージド C++ は CoreCLR ではサポートされていません。 CoreCLR に移植するには、C++ マネージド コードを C# で書き直し、すべてのネイティブ呼び出しを PInvoke 経由で行います。  
  
## <a name="porting-powershell-script-cmdlets"></a>PowerShell スクリプト コマンドレットの移植  
  
PowerShell Core は、PowerShell 言語に関して、Windows Server 2016 および Windows 10 で実行されているエディションを含む他の PowerShell エディションと完全に同等です。 ただし、PowerShell スクリプト コマンドレットを Nano Server に移植する場合は、次の点に注意してください。  
* 他のコマンドレットに対する依存関係がありますか。 依存関係がある場合、それらのコマンドレットは Nano Server で使用できますか。 使用できないコマンドレットについては、「[Nano Server の PowerShell](PowerShell-on-Nano-Server.md)」を参照してください。  
* 実行時に読み込まれるアセンブリに対する依存関係がある場合、それらは引き続き動作しますか。   
* スクリプトをどのようにリモートでデバッグしますか。   
* WMI .Net をどのように MI .Net に移植しますか。  
  
### <a name="dependency-on-built-in-cmdlets"></a>組み込みのコマンドレットに対する依存関係  
Nano Server では、Windows Server 2016 のコマンドレットを一部使用できません (「[Nano Server の PowerShell](PowerShell-on-Nano-Server.md)」を参照してください)。 最も良い方法は、Nano Server 仮想マシンをセットアップし、必要なコマンドレットを使用できるかどうか確認することです。 そのためには、`Enter-PSSession` を実行してターゲットの Nano Server に接続し、`Get-Command -CommandType Cmdlet, Function` を実行して使用可能なコマンドレットの一覧を取得します。  
  
### <a name="consider-using-powershell-classes"></a>PowerShell クラスの使用の検討  
Nano Server では、インライン C# コードをコンパイルするための Add-Type がサポートされています。 新しいコードを記述する場合や既存のコードを移植する場合は、PowerShell クラスを使ってカスタムの型を定義することを検討してください。 PowerShell クラスは、列挙型に加えてプロパティ バッグ シナリオにも使用できます。 PInvoke を実行する必要がある場合は、Add-Type を使った C# 経由または事前にコンパイルしたアセンブリ内で実行します。  
次の例に Add-Type の使い方を示します。  
  
```  
Add-Type -ReferencedAssemblies ([Microsoft.Management.Infrastructure.Ciminstance].Assembly.Location) -TypeDefinition @'  
public class TestNetConnectionResult  
{  
   // The compute name  
   public string ComputerName = null;  
   // The Remote IP address used for connectivity  
   public System.Net.IPAddress RemoteAddress = null;  
}  
'@  
# Create object and set properties  
$result = New-Object TestNetConnectionResult  
$result.ComputerName = Foo  
$result.RemoteAddress = 1.1.1.1  
  
```  
 この例は、Nano Server での PowerShell クラスの使い方を示しています。  
   
```  
class TestNetConnectionResult    
{    
   # The compute name  
  [string] $ComputerName    
  
  #The Remote IP address used for connectivity    
  [System.Net.IPAddress] $RemoteAddress  
}  
# Create object and set properties  
$result = [TestNetConnectionResult]::new()  
$result.ComputerName = Foo  
$result.RemoteAddress = 1.1.1.1  
  
```  
  
### <a name="remotely-debugging-scripts"></a>スクリプトのリモートでのデバッグ  
  
スクリプトをリモートでデバッグするには、PowerShell ISE から `Enter-PSsession` を使用してリモート コンピューターに接続します。 開いたセッションで `psedit <file_path>` を実行して、ファイルのコピーをローカルの PowerShell ISE で開きます。 次に、ブレークポイントを設定して、スクリプトをローカルで実行しているかのようにデバッグできます。 また、このファイルに加えた変更は、すべてリモートのバージョンに保存されます。   
  
### <a name="migrating-from-wmi-net-to-mi-net"></a>WMI .NET から MI .NET への移行  
  
[WMI .NET](https://msdn.microsoft.com/library/mt481551(v=vs.110).aspx) はサポートされないため、古い API を使用しているすべてコマンドレットを、サポートされている WMI API:[MI.NET](https://msdn.microsoft.com/library/dn387184(v=vs.85).aspx)) に移行する必要があります。 MI .NET には、C# から直接、または CimCmdlets モジュールのコマンドレットを通じてアクセスできます。   
  
### <a name="cimcmdlets-module"></a>CimCmdlets モジュール  
  
Nano Server では、WMI v1 コマンドレット (たとえば、Get-WmiObject) はサポートされていません。 ただし、CimCmdlets モジュールの CIM コマンドレット (たとえば、Get-CimInstance) はサポートされています。 CIM コマンドレットと WMI v1 コマンドレットはほとんど対応しています。 たとえば、Get-WmiObject は Get-CimInstance に対応し、よく似たパラメーターが使用されています。 メソッドの呼び出し構文は少し異なりますが、Invoke-CimMethod で明確に文書化されています。 パラメーターの型指定については注意が必要です。 MI .NET には、メソッド パラメーターの型に関してより厳密な要件があります。  
  
### <a name="c-api"></a>C# API  
  
WMI .NET は WMIv1 インターフェイスをラップします。これに対し、MI .NET は WMIv2 (CIM) インターフェイスをラップします。 公開されるクラスは異なる場合がありますが、基になる操作はよく似ています。 オブジェクトのインスタンスを列挙または取得し、それに対する操作を呼び出してタスクを実行します。   
  
  


