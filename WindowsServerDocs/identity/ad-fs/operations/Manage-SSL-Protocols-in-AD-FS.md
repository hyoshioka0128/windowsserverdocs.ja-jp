---
title: AD FS のための SSL/TLS プロトコルと暗号スイートの管理
description: AD FS 2016 に関してよく寄せられる質問
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b97a9cb50743972a85826d10aba89f9e6fffb5a6
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86954464"
---
# <a name="managing-ssltls-protocols-and-cipher-suites-for-ad-fs"></a>AD FS のための SSL/TLS プロトコルと暗号スイートの管理
次のドキュメントでは、で使用される特定の TLS/SSL プロトコルおよび暗号スイートを無効にして有効にする方法について説明し AD FS

## <a name="tlsssl-schannel-and-cipher-suites-in-ad-fs"></a>AD FS での TLS/SSL、SChannel、および暗号スイート

トランスポート層セキュリティ (TLS) と Secure Sockets Layer (SSL) は、セキュリティで保護された通信のためにを提供するプロトコルです。  Active Directory フェデレーションサービス (AD FS) は、これらのプロトコルを使用して通信を行います。  現在、これらのプロトコルにはいくつかのバージョンがあります。

Schannel は、SSL、TLS、および DTLS という標準的なインターネット認証プロトコルを実装するセキュリティ サポート プロバイダー (SSP) です。 セキュリティ サポート プロバイダー インターフェイス (SSPI) は、認証など、セキュリティ関係の機能を実行するために Windows システムで用いられる API の 1 種です。 SSPI は、Schannel SSP をはじめとする数種類のセキュリティ サポート プロバイダー (SSP) に共通のインターフェイスとして機能します。

暗号スイートは、暗号化アルゴリズムのセットです。 TLS/SSL プロトコルの schannel SSP 実装では、暗号スイートのアルゴリズムを使用してキーを作成し、情報を暗号化します。 暗号スイートでは、次のタスクごとに 1 つのアルゴリズムが指定されています。

- キーの交換
- 一括暗号化
- メッセージ認証

AD FS は Schannel.dll を使用して、セキュリティで保護された通信操作を実行します。  現在、AD FS Schannel.dll でサポートされているすべてのプロトコルと暗号スイートがサポートされています。

## <a name="managing-the-tlsssl-protocols-and-cipher-suites"></a>TLS/SSL プロトコルと暗号スイートの管理
> [!IMPORTANT]
> ここでは、レジストリの変更方法を説明する手順について説明します。 ただし、レジストリを正しく変更していない場合、重大な問題が発生する可能性があります。 そのため、手順は確認の上、注意して行ってください。 
> 
> SCHANNEL の既定のセキュリティ設定を変更すると、特定のクライアントとサーバー間の通信が中断または防止される可能性があることに注意してください。  これは、セキュリティで保護された通信が必要で、通信をネゴシエートするプロトコルがない場合に発生します。
> 
> これらの変更を適用する場合は、ファーム内のすべての AD FS サーバーに適用する必要があります。  これらの変更を適用した後、再起動が必要になります。

今日の日と時代には、サーバーのセキュリティ強化と、古いまたは脆弱な暗号スイートの削除が、多くの組織にとって大きな優先事項となってきています。  サーバーをテストし、これらのプロトコルとスイートに関する詳細情報を提供するソフトウェアスイートが用意されています。  準拠した状態を維持するため、またはセキュリティで保護された評価を実現するために、弱いプロトコルや暗号スイートの削除または無効化が必要になりました。  このドキュメントの残りの部分では、特定のプロトコルと暗号スイートを有効または無効にする方法について説明します。

次のレジストリキーは同じ場所にあります: HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols.  Regedit または PowerShell を使用して、これらのプロトコルと暗号スイートを有効または無効にします。

![レジストリの場所](media/Managing-SSL-Protocols-in-AD-FS/registry.png)

## <a name="enable-and-disable-ssl-20"></a>SSL 2.0 を有効または無効にする
SSL 2.0 を有効または無効にするには、次のレジストリキーとその値を使用します。

### <a name="enable-ssl-20"></a>SSL 2.0 を有効にする
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Server]"Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Server]"DisabledByDefault" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Client]"Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Client]"DisabledByDefault" = dword: 00000000 

### <a name="disable-ssl-20"></a>SSL 2.0 を無効にする
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Server]"Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Server]"DisabledByDefault" = dword: 00000001 
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Client]"Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Client]"DisabledByDefault" = dword: 00000001

### <a name="using-powershell-to-disable-ssl-20"></a>PowerShell を使用して SSL 2.0 を無効にする

``` powershell
New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -Force | Out-Null
    
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
            
New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
Write-Host 'SSL 2.0 has been disabled.'
```

## <a name="enable-and-disable-ssl-30"></a>SSL 3.0 を有効または無効にする
SSL 3.0 を有効または無効にするには、次のレジストリキーとその値を使用します。

### <a name="enable-ssl-30"></a>SSL 3.0 の有効化
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Server]"Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Server]"DisabledByDefault" = dword: 00000000 
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Client]"Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Client]"DisabledByDefault" = dword: 00000000 

### <a name="disable-ssl-30"></a>SSL 3.0 の無効化
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Server]"Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Server]"DisabledByDefault" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Client]"Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Client]"DisabledByDefault" = dword: 00000001 

### <a name="using-powershell-to-disable-ssl-30"></a>PowerShell を使用して SSL 3.0 を無効にする

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'SSL 3.0 has been disabled.'
```

## <a name="enable-and-disable-tls-10"></a>TLS 1.0 を有効または無効にする
次のレジストリキーとその値を使用して、TLS 1.0 を有効または無効にします。

> [!IMPORTANT]
> TLS 1.0 を無効にすると、WAP が AD FS の信頼に違反します。  TLS 1.0 を無効にする場合は、アプリケーションに対して強力な認証を有効にする必要があります。  「[強力な認証を有効にする」を](#enabling-strong-authentication-for-net-applications)参照 



### <a name="enable-tls-10"></a>TLS 1.0 を有効にする
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Server]"Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Server]"DisabledByDefault" = dword: 00000000 
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Client]"Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Client]"DisabledByDefault" = dword: 00000000 

### <a name="disable-tls-10"></a>TLS 1.0 の無効化
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Server]"Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Server]"DisabledByDefault" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Client]"Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Client]"DisabledByDefault" = dword: 00000001 

### <a name="using-powershell-to-disable-tls-10"></a>PowerShell を使用した TLS 1.0 の無効化

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.0 has been disabled.'
```


## <a name="enable-and-disable-tls-11"></a>TLS 1.1 を有効または無効にする
次のレジストリキーとその値を使用して、TLS 1.1 を有効または無効にします。

### <a name="enable-tls-11"></a>TLS 1.1 を有効にする
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Server]"Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Server]"DisabledByDefault" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Client]"Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Client]"DisabledByDefault" = dword: 00000000

### <a name="disable-tls-11"></a>TLS 1.1 を無効にする
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Server]"Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Server]"DisabledByDefault" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Client]"Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Client]"DisabledByDefault" = dword: 00000001 

### <a name="using-powershell-to-disable-tls-11"></a>PowerShell を使用した TLS 1.1 の無効化

``` powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.1 has been disabled.'
```

## <a name="enable-and-disable-tls-12"></a>TLS 1.2 を有効または無効にする

次のレジストリキーとその値を使用して、TLS 1.2 を有効または無効にします。

### <a name="enable-tls-12"></a>TLS 1.2 の有効化
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "DisabledByDefault"=dword:00000000 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "DisabledByDefault"=dword:00000000

### <a name="disable-tls-12"></a>TLS 1.2 を無効にする
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server] "DisabledByDefault"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client] "DisabledByDefault"=dword:00000001

### <a name="using-powershell-to-disable-tls-12"></a>PowerShell を使用した TLS 1.2 の無効化

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.2 has been disabled.'
```

## <a name="enable-and-disable-rc4"></a>RC4 の有効化と無効化 

RC4 を有効または無効にするには、次のレジストリキーとその値を使用します。  この暗号スイートのレジストリキーは次の場所にあります。

- HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\

![レジストリの場所](media/Managing-SSL-Protocols-in-AD-FS/cipher.png)



### <a name="enable-rc4"></a>RC4 を有効にする

- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128]"Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128]"Enabled" = dword: 00000001
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128]"Enabled" = dword: 00000001 

### <a name="disable-rc4"></a>RC4 の無効化

- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128]"Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128]"Enabled" = dword: 00000000
- [HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128]"Enabled" = dword: 00000000 

### <a name="using-powershell"></a>PowerShell の使用

```powershell
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
```

## <a name="enabling-or-disabling-additional-cipher-suites"></a>追加の暗号スイートを有効または無効にする

特定の暗号を無効にするには HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Control\Cryptography\Configuration\Local\SSL\00010002 から削除します。 

![レジストリの場所](media/Managing-SSL-Protocols-in-AD-FS/suites.png)

暗号スイートを有効にするには、関数のマルチ文字列値キーに文字列値を追加します。  たとえば、TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P521 を有効にする場合は、文字列に追加します。

サポートされている暗号スイートの完全な一覧については、「 [TLS/SSL (SCHANNEL SSP) の暗号スイート](/windows/win32/secauthn/cipher-suites-in-schannel)」を参照してください。  このドキュメントでは、既定で有効になっているものの、既定ではサポートされていないスイートの一覧を示します。  暗号スイートに優先順位を付けるには、「 [Schannel 暗号スイートの優先順位付け](/windows/win32/secauthn/prioritizing-schannel-cipher-suites)」を参照してください。

## <a name="enabling-strong-authentication-for-net-applications"></a>.NET アプリケーションの強力な認証を有効にする
.NET Framework 3.5/4.0/4.5 .x アプリケーションでは、SchUseStrongCrypto レジストリキーを有効にすることで、既定のプロトコルを TLS 1.2 に切り替えることができます。  このレジストリキーを使用すると、.NET アプリケーションで TLS 1.2 が強制的に使用されます。

> [!IMPORTANT]
> Windows Server 2016 および Windows Server 2012 R2 の AD FS については、.NET Framework 4.0/4.5. x キーを使用する必要があります: HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft \\ 。NETFramework\v4.0.30319


.NET Framework 3.5 では、次のレジストリキーを使用します。

[HKEY_LOCAL_MACHINE \SOFTWARE\Wow6432Node\Microsoft \\ 。NETFramework\v2.0.50727] "SchUseStrongCrypto" = dword: 00000001

.NET Framework 4.0/4.5. x では、次のレジストリキーを使用します: HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft \\ 。NETFramework\v4.0.30319 "SchUseStrongCrypto" = dword: 00000001

![強力な認証](media/Managing-SSL-Protocols-in-AD-FS/strongauth.png)

```powershell
    
    New-ItemProperty -path 'HKLM:\SOFTWARE\Microsoft\.NetFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value '1' -PropertyType 'DWord' -Force | Out-Null
```

## <a name="additional-information"></a>追加情報

- [TLS/SSL (Schannel SSP) の暗号スイート](/windows/win32/secauthn/cipher-suites-in-schannel)
- [Windows 8.1 での TLS 暗号スイート](/windows/win32/secauthn/tls-cipher-suites-in-windows-8-1)
- [Schannel 暗号スイートの優先順位付け](/windows/win32/secauthn/prioritizing-schannel-cipher-suites)
- [暗号とその他の Enigmatic tongues で話す](/archive/blogs/askds/speaking-in-ciphers-and-other-enigmatic-tonguesupdate)
