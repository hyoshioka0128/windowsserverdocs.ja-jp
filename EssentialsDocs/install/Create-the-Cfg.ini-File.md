---
title: Cfg.ini ファイルの作成
description: Windows Server Essentials の使用方法について説明します。
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 93a73556-22ef-402d-b8d4-582b74c22bcf
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 0702fb8616ced4e7e00de344da47995d540f074d
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312074"
---
# <a name="create-the-cfgini-file"></a>Cfg.ini ファイルの作成

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

次のシナリオでは、オペレーティング システムのインストールを自動化するために cfg.ini ファイルを使用します。  
  
-   ターゲット コンピューターのプレインストールされたイメージでエンド ユーザーのエクスペリエンスをテストする場合、初期構成セクションを使用して有人モードまたは無人モードでインストールをウォークスルーします。 これを行うには、「[初期構成セクションの作成](Create-the-Cfg.ini-File.md#BKMK_CreateInit2)」を参照してください。  
  
##  <a name="create-the-initial-configuration-section"></a><a name="BKMK_CreateInit2"></a>初期構成セクションを作成する  
 cfg.ini ファイルの初期構成セクションを使用して、有人モードまたは無人モードでインストールをウォークスルーします。  
  
#### <a name="to-define-the-initial-configuration-section"></a>初期構成セクションを定義するには  
  
1.  cfg.ini ファイルが存在する場合はメモ帳でこのファイルを開きます。存在しない場合は、新しいファイルを作成します。  
  
2.  InitialConfiguration セクションを作成するには、次のテキストを追加します。  
  
    ```  
  
    [InitialConfiguration]  
    ;Optional, display language can only be one of the installed language  
    Language=en-us  
    ;Optional, The name of a script that runs after setupComplete.cmd but before the initial configuration begins.  
    ;Optional  
    Locale=en-us  
    ;Optional  
    Country=US  
    ;Optional  
    Keyboard=0409:00000409  
    AcceptEula=true  
    ;This is only required on a server where an OEM EULA has been specified   
    ;by using the OOBE.xml file  
    AcceptOEMEula=true  
    ;Optional. Example: My Company Name  
    CompanyName=EnterCompanyName  
    ServerName=EnterServerName  
    ; Example: CONTOSO  
    NetbiosName=EnterNetbiosDomainName  
    ; Example: contoso.local  
    DNSName=EnterDNSDomain   
    ; Used to set the user name for the domain admin  
    UserName=EnterDomainAdminUserName  
    ;The password has to be strong and at least 8 characters  
    PlainTextPassword=EnterAdminPassword  
    ;. Used to set the user name for the domain standard user account. Ignored in migration mode.  
    StdUserName=EnterDomainStandardUserName  
    ;. The password for the domain standard user account has to be strong and at least 8 characters  
    StdUserPlainTextPassword=EnterStandardUserPassword  
    ;Controls the Watson and automatic update settings  
    Settings=All or Updates or None  
    WebDomainName=www.abc.com  
    TrustedCertFileName=c:\cert\a.pfx  
    TrustedCertPassword=Enteryourpassword  
    EnableVPN=true  
    EnableRWA=true  
    IPv4DNSForwarder=<IPV4Address,IPV4Address,¦>  
    IPv6DNSForwarder=<IPV6Address,IPV6Address,¦>  
    VpnIPv4StartAddress=<IPV4Address>  
    VpnIPv4EndAddress=<IPV4Address>  
    VpnBaseIPv6Address=<IPV6Address>  
    VpnIPv6PrefixLength=<number>  
    ;All these section are optional.  
     [PostOSInstall]  
    ;Optional, The name of a script that runs after setupComplete.cmd but before the initial configuration begins.  
  
    IsHosted=true  
    StaticIPv4Address=<IPV4Address>  
    StaticIPv4Gateway=<IPV4Address>  
    StaticIPv4SubnetMask=<IPV4SubnetMask>   
    StaticIPv6Address=<IPV6Address>  
    StaticIPv6SubnetPrefixLength=<number>  
    StaticIPv6Gateway=<IPV6Address>  
    ClientBackupOn=true  
    FileHistoryOn=true  
    LaunchPadHiddenTasks=<Microsoft.LaunchPad.AdminDashboard,Microsoft.LaunchPad.Backup>  
  
    ```  
  
    > [!NOTE]
    >  初期構成中に別の言語を選択することはできません。 システムがリセットされると、オペレーティング システムの言語はもともとインストールされていた言語になります。  
  
    |[パラメーター名]|パラメーターの説明|  
    |--------------------|---------------------------|  
    |*AcceptEula*|ユーザーがマイクロソフト ソフトウェア ライセンス条項を受け入れることを示します。 この値には True または False を指定できますが、True に設定されている場合にのみ、インストールが続行されます。|  
    |*AcceptOEMEula*|(省略可能) ユーザーがパートナーのライセンス契約を受け入れることを示します。 この値には True または False を指定できます。 このフィールドは、個別のライセンス契約を提供しているパートナーからサーバーを購入した場合にのみ必須です。|  
    |*CompanyName*|(省略可能) 会社名。 会社名は、サーバーを会社に関連付け、会社の報告をカスタマイズするために使用されます。 254 文字まで使用できます。|  
    |*原産*|(省略可能) 目的の国/地域を表す文字列。 例: 米国の場合、US です。|  
    |*Server*|サーバー名は、ネットワーク上のサーバーを一意に識別します。 サーバー名は、次の条件を満たしている必要があります。<br /><br /> -最大15文字まで指定できます。<br /><br /> -文字、数字、ハイフン (-) を含めることができます。<br /><br /> -先頭をハイフンにすることはできません。<br /><br /> -スペースを含めることはできません。<br /><br /> -数字のみを含めることはできません。<br /><br /> 例: ContosoServer。|  
    |*DNSName*|内部ドメインにより、サーバーとクライアント コンピューターをグループ化し、ユーザー名、パスワード、およびその他の共通情報の共通データベースを共有します。 ユーザーがコンピューターにログオンするときにはこの名前が表示されますが、この名前は内部でのみ使用されるもので、インターネット ドメイン名とは異なります。 内部ドメイン名は、*ServerName* と同じ条件を満たしている必要があります。<br /><br /> 例: contoso.local。|  
    |*NetbiosName*|NetBIOS 名は、サーバー上で実行されているリソースを識別するために使用されます。 15 文字まで使用できます。 例: Contoso。|  
    |*言語*|(省略可能) 表示言語を指定します。 インストールされている言語のうちの 1 言語のみを指定できます。 例: 米国で使用されている英語の場合、en-us。|  
    |*国*|(省略可能) *LocaleID* 形式を使用して、時刻と通貨の形式を指定します。 例: en-us の場合、英語で表示され、米国で使用されている標準に従って形式化される通貨と時刻です。|  
    |*キーボード*|キーボードには次の 2 つの形式を使用できます。<br /><br /> - **入力言語: キーボードレイアウト。** たとえば、0409:00000409 の場合、 **:** の前の 0409 は入力言語で、**00000409** はキーボード レイアウトです。 キーボード レイアウトの一覧は、レジストリ キー **HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Keyboard Layouts** の下で確認できます。<br /><br /> - **入力言語: IME 識別子。** 以下に IME 識別子の完全な一覧を示します。<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1} {8F96574E-C86C-4bd6-9666-3F7327D4CBE8} アムハラ語 Input メソッド<br /><br /> -{81d4e9c9-1d3b-41bc-9e6c-4b40bf79e35e} {FA550B04-5AD7-411F-A5AC-CA038EC515D7} Microsoft Pinyin-Simple Fast (簡体字中国語)<br /><br /> -{531FDEBF-9B4C-4A43-A2AA-960E8FCDC732} {B2F9C502-1742-11D4-9790-0080C882687E} 中国語 (繁体字)-新しい発音<br /><br /> -{531FDEBF-9B4C-4A43-A2AA-960E8FCDC732} {4BDF9F03-C7D3-11D4-B2AB-0080C882687E} 中国語 (繁体字)-ChangJie<br /><br /> -{531FDEBF-9B4C-4A43-A2AA-960E8FCDC732} {6024B45F-5C54-11D4B921-0080c882687 e} 中国語 (繁体字)-クイック<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1} {D38EFF65-AA46-4FD5-91A7-67845FB02F5B} 繁体字中国語配列<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1} {037B2C25-480C-4D7F-B027-D6CA6B69788A} 繁体字中国語 (繁体字)<br /><br /> -{03B5835F-F03C-411B-9CE2-AA23E1171E36} {A76C93D9-5523-4E90-AAFA-4DB112F9AC76} Microsoft IME (日本語)<br /><br /> -{A028AE76-01B1-46C2-99C4-ACD9858AE02F} {B5FE1F02-D5F2-4445-9C03-C568F23C99A1} Microsoft IME (韓国語)<br /><br /> -{A1E2B86B-924A-4D43-80F6-8A820DF7190F} {B60AF051-257A-46BC-B9D3-84DAD819BAFB} 古いハングル IME (韓国語)<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1} {409C8376-007B-4357-AE8E-26316EE3FB0D} イ語入力メソッド<br /><br /> -{E429B25A-E5D3-4D1F-9BE3-0C608477E3A1} {3cab88 B7-CC3E47 6A6-9765-b772ad7761ff} ティグリニア語 Input メソッド|  
    |*設定*|更新に関するユーザーの選択を設定します。 次のいずれかの値を使用します。<br /><br /> **-All は、** 推奨設定を使用します。<br /><br /> **-更新プログラムは、** 重要な更新プログラムのインストールに相当します。 のみ<br /><br /> **-None は、** 更新プログラムをチェックしません。|  
    |*UserName*|-セットアップ中に作成された新しい管理者アカウントの名前。 管理者アカウント名と標準のユーザー アカウント名は、次の条件を満たしている必要があります。<br /><br /> -最大19文字まで指定できます。<br /><br /> -/\ [] &#124; < > + =; を含めることはできません。, ? *<br /><br /> -先頭または末尾にピリオドを使用することはできません。<br /><br /> -2 つの連続するピリオドを含めることはできません。<br /><br /> -サーバー名または内部ドメイン名と同じにすることはできません。<br /><br /> -管理者やゲストなど、定義済みのユーザー名と同じにすることはできません。|  
    |*PlainTextPassword*|これは、セットアップ中に作成された新しい管理者アカウントのパスワードです。<br /><br /> -少なくとも8文字以上である必要があります。<br /><br /> -次の4つのカテゴリのうち少なくとも3つが含まれている必要があります。<br /><br /> 大文字。<br /><br /> -小文字。<br /><br /> 乱数.<br /><br /> 文字.|  
    |*StdUserName*|セットアップ中に作成された新しい標準ユーザー アカウントの名前。 要件については、*UserName* パラメーターを参照してください。|  
    |*StdUserPlainTextPassword*|セットアップ中に作成された標準ユーザー アカウントのパスワード。|  
    |WebDomainName|(省略可能) サーバーのインターネット ドメイン名を構成します。 このファイルでは、ドメイン名のセットアップ ウィザードによる手動構成で使用する方法と同じように、ドメイン名を構成できます。|  
    |TrustedCertFileName|(省略可能) ドメイン名の信頼できる証明書を構成します。 これにより、秘密キーが格納された .PFX 証明書を配置できます。|  
    |TrustedCertPassword|(省略可能) .PFX インポート用のパスワード。|  
    |EnableVPN|(省略可能) 既定で VPN を有効にします。|  
    |VpnIPv4StartAddress|(省略可能) VPN の開始アドレスを設定します。|  
    |VpnIPv4EndAddress|(省略可能) VPN の終了アドレスを設定します。|  
    |VpnBaseIPv6Address|(省略可能) VPN のベース IPV6 アドレスを設定します。|  
    |VpnIPv6PrefixLength|(省略可能) VPN IPv6 アドレスのプレフィックスの長さを設定します。|  
    |IsHosted|(省略可能) 指定しない場合の既定値は false です。 ホスト側環境でこれをセットアップする場合、この値を設定します。 これにより、ルーター構成が無効になります。|  
    |StaticIPv4Address|(省略可能) 動的アドレスの代わりに静的 IP アドレスを構成する場合、静的 IP アドレスを指定します。|  
    |StaticIPv4Gateway|(省略可能) 動的アドレスの代わりに静的 IP アドレスを構成する場合、デフォルト ゲートウェイ アドレスを指定します。|  
    |StaticIPv4SubnetMask|(省略可能) 動的アドレスの代わりに静的 IP アドレスを構成する場合、サブネット マスクを指定します。|  
    |StaticIPv6Address|(省略可能) 動的アドレスの代わりに静的 IP アドレスを構成する場合、既定の IP アドレスを指定します。|  
    |StaticIPv6SubnetPrefixLength|(省略可能) 動的アドレスの代わりに静的 IP アドレスを構成する場合、既定の IPV6 サブネット プレフィックスの長さを指定します。|  
    |StaticIPv6Gateway|(省略可能) 動的アドレスの代わりに静的 IP アドレスを構成する場合、デフォルト ゲートウェイ アドレスを指定します。|  
    |ClientBackupOn|(省略可能) 新しいクライアントをサーバーに追加した場合、既定でクライアント バックアップを無効にします。|  
    |FileHistoryOn|(省略可能) Windows 8 Consumer Preview を実行する新しいクライアントをサーバーに追加した場合、既定でファイル履歴バックアップを無効にします。|  
    |EnableRWA|これにより、Windows Server Essentials をインストールするときにリモート Web アクセスが有効になりますが、ルーターの構成はスキップされます。 これは、製品のクリーン インストールでのみサポートされます。 既定値は false です。|  
    |IPv4DNSForwarder|IPv4 DNS フォワーダーを設定します。|  
    |IPv6DNSForwarder|IPv6 DNS フォワーダーを設定します。|  
    |LaunchPadHiddenTasks|-(省略可能) スタートパッドのバックアップエントリまたは管理ダッシュボードのエントリを非表示にすることができます。<br /><br /> -ダッシュボードを無効にするには: LaunchPadHiddenTasks = Microsoft. スタートパッド. AdminDashboard<br /><br /> -バックアップを無効にするには: LaunchPadHiddenTasks = Microsoft. スタートパッド. Backup<br /><br /> -バックアップとダッシュボードの両方を無効にするには: LaunchPadHiddenTasks = Microsoft. スタートパッド. Backup, Microsoft. スタートパッド. AdminDashboard|  
  
3.  ファイルを保存します。 保存するファイルの名前は、cfg.ini.txt ではなく、cfg.ini としてください。  
  
    > [!NOTE]
    >  このファイルは USB フラッシュ ドライブに保存して、インストールの特定の段階で使用することができます。また、ターゲット サーバー上の任意のハード ドライブのルートに配置することもできます。 ファイルのエンコードは ANSI または Unicode に設定してください。UTF-8 エンコードはサポートされていません。  
  
> [!IMPORTANT]
>  cfg.ini の初期構成セクションは、エンド ユーザーがサーバーをカスタマイズする場合、またはパートナーが無人応答ファイルを使用してサーバーのユーザー エクスペリエンスをテストする場合にのみ使用します。 ファイルのこのセクションは、イメージの作成用ではありません。  
  
## <a name="see-also"></a>参照  

 [Windows Server ESSENTIALS ADK でのはじめに](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [イメージ  の作成とカスタマイズ](Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](Additional-Customizations.md)   
 [展開  のイメージの準備](Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [Windows Server ESSENTIALS ADK でのはじめに](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [イメージ  の作成とカスタマイズ](../install/Creating-and-Customizing-the-Image.md)  
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [展開  のイメージの準備](../install/Preparing-the-Image-for-Deployment.md)  
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

