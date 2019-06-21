---
title: AD FS の SSL や TLS プロトコルおよび暗号スイートを管理します。
description: AD FS 2016 のよく寄せられる質問
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c1153cd81185dcfe83d291161a85481e5a7d0700
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280546"
---
# <a name="managing-ssltls-protocols-and-cipher-suites-for-ad-fs"></a>AD FS の SSL や TLS プロトコルおよび暗号スイートを管理します。
次のドキュメントと AD FS によって使用される暗号を無効にして特定の TLS/SSL プロトコルを有効にする方法に関する情報を提供します

## <a name="tlsssl-schannel-and-cipher-suites-in-ad-fs"></a>TLS と SSL、SChannel および AD FS での暗号スイート

トランスポート層セキュリティ (TLS) とセキュリティで保護されたソケット レイヤー (SSL) は、セキュリティ保護された通信を提供するプロトコルです。  Active Directory フェデレーション サービスでは、これらのプロトコルを使用して通信します。  今日、これらのプロトコルのいくつかのバージョンが存在します。

Schannel は、SSL、TLS、および DTLS という標準的なインターネット認証プロトコルを実装するセキュリティ サポート プロバイダー (SSP) です。 セキュリティ サポート プロバイダー インターフェイス (SSPI) は、認証など、セキュリティ関係の機能を実行するために Windows システムで用いられる API の 1 種です。 SSPI は、Schannel SSP をはじめとする数種類のセキュリティ サポート プロバイダー (SSP) に共通のインターフェイスとして機能します。

暗号スイートは、暗号化アルゴリズムのセットです。 TLS と SSL プロトコルの schannel SSP の実装では、暗号スイートからアルゴリズムを使用して、キーを作成し、情報を暗号化します。 暗号スイートでは、次のタスクごとに 1 つのアルゴリズムが指定されています。

- キーの交換
- 一括暗号化
- メッセージ認証

AD FS では、Schannel.dll を使用して、セキュリティで保護された通信と、対話を行います。  現在 AD FS には、すべてのプロトコルと Schannel.dll でサポートされている暗号スイートがサポートしています。

## <a name="managing-the-tlsssl-protocols-and-cipher-suites"></a>TLS/SSL プロトコルおよび暗号スイートを管理します。
> [!IMPORTANT]
> このセクションには、レジストリを変更する方法を説明する手順が含まれています。 ただし、レジストリを正しく変更していない場合、重大な問題が発生する可能性があります。 そのため、手順は確認の上、注意して行ってください。 
> 
> 特定のクライアントとサーバー間の通信を防止または中断 SCHANNEL では、既定のセキュリティ設定を変更することがあります。  これは、ような状況が、セキュリティで保護された通信が必要ですとの通信をネゴシエートするプロトコルがない場合に発生します。
> 
> これらの変更を適用する場合は、すべての AD FS サーバー ファーム内に適用する必要があります。  これらの変更を適用した後、再起動が必要です。

今日 1 日と有効期間、サーバーのセキュリティ強化と古い削除または脆弱な暗号スイートが、多くの組織の主要な優先度が高まっています。  ソフトウェアのスイートが使用可能なサーバーをテストし、これらのプロトコルとスイートの詳細情報を提供するがします。  準拠性を維持したり、セキュリティで保護された評価を達成したりするには、するには削除または暗号強度の低いプロトコルを無効になりました必要があります。  このドキュメントの残りの部分と暗号スイートを有効にするか、特定のプロトコルを無効にする方法のガイダンスが提供されます。

次のレジストリ キーは、同じ場所に配置されます。Hkey_local_machine \system\currentcontrolset\control\securityproviders\schannel\protocols します。  暗号スイートを有効にするか、これらのプロトコルを無効にするには、regedit または PowerShell を使用します。

![レジストリの場所](media/Managing-SSL-Protocols-in-AD-FS/registry.png)

## <a name="enable-and-disable-ssl-20"></a>有効にして、SSL 2.0 を無効にします。
SSL 2.0 を無効にするには、次のレジストリ キーおよび値を使用します。

### <a name="enable-ssl-20"></a>Enable SSL 2.0
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server]"Enabled"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server]"DisabledByDefault"dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client]"Enabled"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client]"DisabledByDefault"dword:00000000 を = 

### <a name="disable-ssl-20"></a>SSL 2.0 を無効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SL 2.0\Server]"Enabled"dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server]"DisabledByDefault"= dword:00000001 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client]"Enabled"dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client]"DisabledByDefault"= dword:00000001

### <a name="using-powershell-to-disable-ssl-20"></a>PowerShell を使用して、SSL 2.0 を無効にするには

``` powershell
New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -Force | Out-Null
    
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
            
New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
Write-Host 'SSL 2.0 has been disabled.'
```

## <a name="enable-and-disable-ssl-30"></a>有効にして、SSL 3.0 を無効にします。
SSL 3.0 を無効にするには、次のレジストリ キーおよび値を使用します。

### <a name="enable-ssl-30"></a>SSL 3.0 の有効化
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server]"Enabled"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server]"DisabledByDefault"dword:00000000 を = 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client]"Enabled"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client]"DisabledByDefault"dword:00000000 を = 

### <a name="disable-ssl-30"></a>SSL 3.0 を無効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server]"Enabled"dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server]"DisabledByDefault"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client]"Enabled"dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client]"DisabledByDefault"= dword:00000001 

### <a name="using-powershell-to-disable-ssl-30"></a>PowerShell を使用して、SSL 3.0 を無効にするには

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'SSL 3.0 has been disabled.'
```

## <a name="enable-and-disable-tls-10"></a>有効にして、TLS 1.0 を無効にします。
TLS 1.0 を無効にするには、次のレジストリ キーおよび値を使用します。

> [!IMPORTANT]
> TLS 1.0 を無効にすると、AD FS を信頼する、WAP が中断されます。  TLS 1.0 を無効にした場合、アプリケーションの強力な認証を有効にする必要があります。  参照してください[強力な認証を有効にします。](#enabling-strong-authentication-for-net-applications) 



### <a name="enable-tls-10"></a>TLS 1.0 を有効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \server]"Enabled"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \server]"DisabledByDefault"dword:00000000 を = 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS サブキー]"Enabled"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS サブキー]"DisabledByDefault"dword:00000000 を = 

### <a name="disable-tls-10"></a>TLS 1.0 を無効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \server]"Enabled"dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \server]"DisabledByDefault"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS サブキー]"Enabled"dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS サブキー]"DisabledByDefault"= dword:00000001 

### <a name="using-powershell-to-disable-tls-10"></a>PowerShell を使用して、TLS 1.0 を無効にするには

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.0 has been disabled.'
```


## <a name="enable-and-disable-tls-11"></a>有効にして、TLS 1.1 を無効にします。
TLS 1.1 を無効にするには、次のレジストリ キーおよび値を使用します。

### <a name="enable-tls-11"></a>TLS 1.1 を有効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server]"Enabled"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server]"DisabledByDefault"dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client]"Enabled"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client]"DisabledByDefault"dword:00000000 を =

### <a name="disable-tls-11"></a>TLS 1.1 を無効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server]"Enabled"dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server]"DisabledByDefault"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client]"Enabled"dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client]"DisabledByDefault"= dword:00000001 

### <a name="using-powershell-to-disable-tls-11"></a>PowerShell を使用して、TLS 1.1 を無効にするには

``` powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.1 has been disabled.'
```

## <a name="enable-and-disable-tls-12"></a>有効にして、TLS 1.2 を無効にします。

TLS 1.2 を無効にするには、次のレジストリ キーおよび値を使用します。

### <a name="enable-tls-12"></a>TLS 1.2 を有効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \server]"Enabled"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \server]"DisabledByDefault"dword:00000000 を = 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \client]"Enabled"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \client]"DisabledByDefault"dword:00000000 を =

### <a name="disable-tls-12"></a>TLS 1.2 を無効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \server]"Enabled"dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \server]"DisabledByDefault"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \client]"Enabled"dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \client]"DisabledByDefault"= dword:00000001

### <a name="using-powershell-to-disable-tls-12"></a>PowerShell を使用して、TLS 1.2 を無効にするには

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.2 has been disabled.'
```

## <a name="enable-and-disable-rc4"></a>有効にして、RC4 を無効にします。 

RC4 を無効にするには、次のレジストリ キーおよび値を使用します。  この暗号スイートのレジストリ キーはここに。

- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\

![レジストリの場所](media/Managing-SSL-Protocols-in-AD-FS/cipher.png)



### <a name="enable-rc4"></a>Enable RC4

- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128] "Enabled"=dword:00000001 

### <a name="disable-rc4"></a>RC4 を無効にします。

- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128] "Enabled"=dword:00000000 

### <a name="using-powershell"></a>PowerShell を使用する

```powershell
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
```

## <a name="enabling-or-disabling-additional-cipher-suites"></a>有効化またはその他の暗号スイートを無効にします。

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Cryptography\Configuration\Local\SSL\00010002 からそれらを削除することで特定の特定の暗号を無効にすることができます。 

![レジストリの場所](media/Managing-SSL-Protocols-in-AD-FS/suites.png)

暗号スイートを有効にするには、関数の複数行文字列値のキーに文字列値を追加します。  たとえば、TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P521 を有効にする場合しは追加文字列にします。

スイートをサポートされている暗号の一覧を参照してください[in TLS/SSL (Schannel SSP) 暗号スイート](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)します。  このドキュメントでは、既定でサポートされますが、既定で無効になっていると有効になっているスイートのテーブルを提供します。  暗号スイートを参照してください優先順位を付ける[Schannel 暗号スイートの優先順位を付ける](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx)します。

## <a name="enabling-strong-authentication-for-net-applications"></a>.NET アプリケーションの強力な認証を有効にします。
.NET Framework の 3.5/4.0/4.5.x アプリケーションは、SchUseStrongCrypto のレジストリ キーを有効にすると、TLS 1.2 に既定のプロトコルを切り替えることができます。  このレジストリ キーには、TLS 1.2 を使用する .NET アプリケーションが強制されます。

> [!IMPORTANT]
> Windows Server 2016 および Windows Server 2012 R2 で AD FS の .NET Framework 4.0/4.5.x キーを使用する必要があります。HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\v4.0.30319


.NET Framework 3.5 用には、次のレジストリ キーを使用します。

[Hkey_local_machine \software\wow6432node\microsoft\\します。NETFramework\v2.0.50727]"SchUseStrongCrypto"= dword:00000001

.NET Framework 4.0/4.5.x は次のレジストリ キーを使用します。Hkey_local_machine \software\microsoft\\します。NETFramework\v4.0.30319"SchUseStrongCrypto"= dword:00000001

![強力な認証](media/Managing-SSL-Protocols-in-AD-FS/strongauth.png)

```powershell
    
    New-ItemProperty -path 'HKLM:\SOFTWARE\Microsoft\.NetFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value '1' -PropertyType 'DWord' -Force | Out-Null
```

## <a name="additional-information"></a>追加情報

- [TLS/SSL (Schannel SSP) の暗号スイート](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)
- [Windows 8.1 での TLS 暗号スイート](https://msdn.microsoft.com/library/windows/desktop/mt767781.aspx)
- [優先順位を付ける Schannel 暗号スイート](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx)
- [暗号およびその他の謎めいた語で言うと](https://blogs.technet.microsoft.com/askds/2015/12/08/speaking-in-ciphers-and-other-enigmatic-tonguesupdate/)
