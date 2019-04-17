---
title: "Cfg.ini ファイルを作成します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 93a73556-22ef-402d-b8d4-582b74c22bcf
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 967db5f36ea27fb04eab9a6682a106ba0072d45d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="create-the-cfgini-file"></a>Cfg.ini ファイルを作成します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

Cfg.ini ファイルを使用して、次のシナリオでは、オペレーティング システムのインストールを自動化します。  
  
-   プレインストールされたイメージをターゲット コンピューター上でエンド ユーザーのエクスペリエンスをテストするには、初期構成セクションが有人または無人モードでインストールをウォークスルー使用されます。 これを行うには、次を参照してください。[初期構成セクションを作成する](Create-the-Cfg.ini-File.md#BKMK_CreateInit2)します。  
  
##  <a name="BKMK_CreateInit2"></a>初期構成セクションを作成します。  
 Cfg.ini ファイルの初期構成セクションを使用して、有人または無人モードでインストールをウォークスルーします。  
  
#### <a name="to-define-the-initial-configuration-section"></a>初期構成セクションを定義するには  
  
1.  存在する場合は、メモ帳で cfg.ini ファイルを開くそれ以外の場合、新しいファイルを作成します。  
  
2.  InitialConfiguration セクションを作成するのには、次のテキストを追加します。  
  
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
    >  初期構成中に別の言語を選択するオプションが指定されていません。 システムをリセットすると、オペレーティング システムの言語がインストールされていたものになります。  
  
    |パラメーター名|パラメーターの説明|  
    |--------------------|---------------------------|  
    |*AcceptEula*|ユーザーがマイクロソフト ソフトウェア ライセンス条項を受け入れることを示します。 値を True または False を指定できますが、これを True に設定されている場合にのみ、インストールの進行します。|  
    |*AcceptOEMEula*|(省略可能)ユーザーがパートナーのライセンス契約を受け入れることを示します。 値は True または False と等しいことができます。 サーバーを別のライセンス契約を提供しているパートナーから購入した場合にのみ、このフィールドが必要です。|  
    |*CompanyName*|(省略可能)会社の名前です。 サーバーを会社に関連付けると、会社の報告をカスタマイズするのには、会社名が使用されます。 最大 254 文字を使用することができます。|  
    |*国*|(省略可能)目的の国/地域を表す文字列。 例: マイクロソフト米国の場合。|  
    |*サーバー名*|サーバー名は、ネットワーク上のサーバーを一意に識別します。 サーバー名は、次の条件を満たす必要があります。<br /><br /> -最大 15 文字を使用ことができます。<br /><br /> の文字、数字、ハイフン (-) を含めることができます。<br /><br /> -ハイフンで始まらない必要があります。<br /><br /> -含めないでスペースを含めないでください。<br /><br /> -数字だけが含まれていない必要があります。<br /><br /> 例: ContosoServer。|  
    |*DNSName*|内部ドメインでは、サーバーとクライアント コンピューターのユーザー名、パスワード、およびその他の一般的な情報の共通データベースを共有するには、一緒にグループ化します。 ユーザーは、自分のコンピューターにログオンするが、のみ、内部使用し、は、インターネット ドメイン名と同じときに、この名前を表示します。 内部ドメイン名が指定されているのと同じ条件を満たす必要があります、*ServerName*します。<br /><br /> 例: contoso.local。|  
    |*NetbiosName*|NetBIOS 名がサーバーで実行されているリソースを識別するために使用します。 最大 15 文字まで使用できます。 例: Contoso。|  
    |*言語*|(省略可能)表示言語を指定します。 のみインストールされている言語のいずれかを指定できます。 例: en-米国で使用されている英語の場合。|  
    |*ロケール*|(省略可能)使用して、時刻と通貨の形式を指定します、*LocaleID*形式です。 例: en-通貨と時刻の場合は英語で表示され、米国で使用されている標準に従って形式化します。|  
    |*キーボード*|キーボードは、次の 2 つの形式の使用できます。<br /><br /> - **入力言語: キーボード レイアウトです。** たとえば 0409:00000409、0409 する前に**:**は入力言語と**00000409**キーボード レイアウトです。 レジストリ キーの下のキーボード レイアウトの一覧を検索する**HKEY_LOCAL_MACHINE \system\controlset001\control\keyboard Layouts**します。<br /><br /> - **入力言語: IME 識別子。** 以下に IME 識別子の完全な一覧を示します。<br /><br /> -{E429b25a-e5d3-4d1f-9be3-0c608477e3a1} {8f96574e-c86c-4bd6-9666-3f7327d4cbe8} アムハラ語入力方式<br /><br /> -{81d4e9c9-1d3b-41bc-9e6c-4b40bf79e35e} {fa550b04-5ad7-411f-a5ac-ca038ec515d7} Microsoft Pinyin - Simple Fast (簡体字中国語)<br /><br /> -{531fdebf-9b4c-4a43-a2aa-960e8fcdc732} {b2f9c502-1742-11d4-9790-0080c882687e} 中国語 (繁体字) - New Phonetic<br /><br /> -{531fdebf-9b4c-4a43-a2aa-960e8fcdc732} {4bdf9f03-c7d3-11d4-b2ab-0080c882687e} 中国語 (繁体字) - ChangJie<br /><br /> -{531fdebf-9b4c-4a43-a2aa-960e8fcdc732} {6024b45f-5c54-11d4-b921-0080c882687e} 中国語 (繁体字) - Quick<br /><br /> -{E429b25a-e5d3-4d1f-9be3-0c608477e3a1} {d38eff65-aa46-4fd5-91a7-67845fb02f5b} 中国語従来の配列<br /><br /> -{E429b25a-e5d3-4d1f-9be3-0c608477e3a1} {037b2c25-480c-4d7f-b027-d6ca6b69788a} 中国語従来 DaYi<br /><br /> -{03b5835f-f03c-411b-9ce2-aa23e1171e36} {a76c93d9-5523-4e90-aafa-4db112f9ac76} Microsoft IME (日本語)<br /><br /> -{A028ae76-01b1-46c2-99c4-acd9858ae02f} {b5fe1f02-d5f2-4445-9c03-c568f23c99a1} Microsoft IME (韓国語)<br /><br /> -{A1e2b86b-924a-4d43-80f6-8a820df7190f} {b60af051-257a-46bc-b9d3-84dad819bafb} Old Hangul IME (韓国語)<br /><br /> -{E429b25a-e5d3-4d1f-9be3-0c608477e3a1} {409c8376-007b-4357-ae8e-26316ee3fb0d} Yi 入力方式<br /><br /> -{E429b25a-e5d3-4d1f-9be3-0c608477e3a1} {3cab88b7-cc3e-46a6-9765-b772ad7761ff} ティグリニア語入力方式|  
    |*設定*|更新プログラムのユーザーの選択内容を設定します。 次の値のいずれかを使用します。<br /><br /> **-All**等しい推奨設定を使用します。<br /><br /> **-更新**は重要な更新プログラムをインストールします。 のみ<br /><br /> **-なし**equals が更新プログラムを確認しません。|  
    |*ユーザー名*|セットアップ中に作成された新しい管理者アカウントの名前。 管理者アカウント名と標準ユーザー アカウント名は、次の条件を満たす必要があります。<br /><br /> -最大 19 文字までできます。<br /><br /> -ことはできませんが含まれている/\ & #124;< > + =;, ? *<br /><br /> -起動したり、ピリオドで終了必要があります。<br /><br /> -連続する 2 つのピリオドにはが含まれていない必要があります。<br /><br /> にサーバー名または内部ドメイン名と同じする必要がありますできません。<br /><br /> に管理者またはゲストなどの定義済みのユーザー名と同じする必要がありますできません。|  
    |*PlainTextPassword*|これは、セットアップ中に作成された新しい管理者アカウントのパスワードです。<br /><br /> -少なくとも 8 文字を使用必要があります。<br /><br /> -次の 4 つのカテゴリから少なくとも 3 つを含める必要があります。<br /><br /> -大文字文字です。<br /><br /> -小文字に変換します。<br /><br /> -番号。<br /><br /> 記号。|  
    |*StdUserName*|セットアップ中に作成された新しい標準ユーザー アカウントの名前。 参照してください、*UserName*要件のパラメーターです。|  
    |*StdUserPlainTextPassword*|セットアップ中に作成される標準のユーザー アカウントのパスワード。|  
    |WebDomainName|(省略可能)サーバーのインターネット ドメイン名を構成します。 このファイルには、ドメイン名のセットアップ ウィザードで手動で構成に使用される方法と同様のドメイン名を構成することができます。|  
    |TrustedCertFileName|(省略可能)ドメイン名の信頼された証明書を構成します。 これにより、配置、します。PFX 証明書は、秘密キーが含まれています。|  
    |TrustedCertPassword|(省略可能)インポート用のパスワード、します。PFX です。|  
    |EnableVPN|(省略可能)既定で VPN を有効にします。|  
    |VpnIPv4StartAddress|(省略可能)VPN の開始アドレスを設定します。|  
    |VpnIPv4EndAddress|(省略可能)VPN の終了アドレスを設定します。|  
    |VpnBaseIPv6Address|(省略可能)VPN のベース IPV6 アドレスを設定します。|  
    |VpnIPv6PrefixLength|(省略可能)VPN IPv6 アドレスのプレフィックスの長さを設定します。|  
    |IsHosted|(省略可能)既定値が指定されていない場合は false です。 ホスト側環境でこれを設定する場合は、この値を設定します。 これは、ルーターの構成を無効になります。|  
    |StaticIPv4Address|(省略可能)動的アドレスの代わりに静的 IP アドレスを構成する場合は、静的 IP アドレスを指定します。|  
    |StaticIPv4Gateway|(省略可能)動的アドレスの代わりに静的 IP アドレスを構成する場合は、デフォルト ゲートウェイ アドレスを指定します。|  
    |StaticIPv4SubnetMask|(省略可能)動的アドレスの代わりに静的 IP アドレスを構成する場合は、サブネット マスクを指定します。|  
    |StaticIPv6Address|(省略可能)動的アドレスの代わりに静的 IP アドレスを構成する場合は、既定の IP アドレスを指定します。|  
    |StaticIPv6SubnetPrefixLength|(省略可能)動的アドレスの代わりに静的 IP アドレスを構成する場合は、既定の IPV6 サブネット プレフィックスの長さを指定します。|  
    |StaticIPv6Gateway|(省略可能)動的な 1 つの代わりに静的 IP アドレスを構成する場合は、デフォルト ゲートウェイ アドレスを指定します。|  
    |ClientBackupOn|(省略可能)オフにするクライアント バックアップ既定で新しいクライアントには、サーバーが参加しているときにします。|  
    |FileHistoryOn|(省略可能)オフにファイル履歴バックアップ既定で Windows 8 Consumer Preview を実行する新しいクライアントには、サーバーが参加しているときにします。|  
    |EnableRWA|Windows Server Essentials をインストールするときにリモート Web アクセスが有効になりますが、ルーター構成はスキップされます。 これは、製品のクリーン インストールでのみサポートされます。 既定値は false です。|  
    |IPv4DNSForwarder|IPv4 DNS フォワーダーを設定します。|  
    |IPv6DNSForwarder|IPv6 DNS フォワーダーを設定します。|  
    |LaunchPadHiddenTasks|-バックアップ エントリを非表示にすることができます (オプション) または/とスタート パッドの管理ダッシュ ボード エントリ。<br /><br /> -ダッシュ ボードを無効にするには: LaunchPadHiddenTasks=Microsoft.LaunchPad.AdminDashboard<br /><br /> -バックアップを無効にするには: LaunchPadHiddenTasks=Microsoft.LaunchPad.Backup<br /><br /> -バックアップとダッシュ ボードの両方を無効にするには: launchpadhiddentasks=microsoft.launchpad.backup, Microsoft.launchpad.admindashboard|  
  
3.  ファイルを保存します。 Cfg.ini、cfg.ini.txt ではないファイルを保存することを確認します。  
  
    > [!NOTE]
    >  特定の段階のインストールの使用できる、USB フラッシュ ドライブにファイルを保存することができますか cfg.ini ファイルは、ターゲット サーバー上の任意のハード ドライブのルートに配置することができます。 ファイルのエンコードは ANSI または Unicode に設定、UTF-8 エンコードはサポートされていないことを確認する必要があります。  
  
> [!IMPORTANT]
>  Cfg.ini の初期構成セクションは、サーバーをカスタマイズするには、エンド ユーザーまたは無人応答ファイルを使用して、サーバーのユーザー エクスペリエンスをテストするパートナーにのみ使用する必要があります。 ファイルのこのセクションでは、イメージを作成するために使用するものではありません。  
  
## <a name="see-also"></a>参照してください。  

 [Windows Server Essentials ADK の概要](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [作成して、イメージをカスタマイズします。](Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](Additional-Customizations.md)   
 [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)

 [Windows Server Essentials ADK の概要](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [作成して、イメージをカスタマイズします。](../install/Creating-and-Customizing-the-Image.md)   
 [追加のカスタマイズ](../install/Additional-Customizations.md)   
 [イメージの展開の準備](../install/Preparing-the-Image-for-Deployment.md)   
 [カスタマー エクスペリエンスのテスト](../install/Testing-the-Customer-Experience.md)

