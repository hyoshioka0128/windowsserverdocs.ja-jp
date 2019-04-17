---
title: "AD FS の SSL または TLS プロトコルおよび暗号スイートを管理します。"
description: "AD FS 2016 についてよく寄せられる質問"
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 23055a1b727e4f1a6b1ccafdea9a410c6021c432
ms.sourcegitcommit: 2782a80a916f8432c030af76e860a72f08481899
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2018
---
# <a name="managing-ssltls-protocols-and-cipher-suites-for-ad-fs"></a>AD FS の SSL または TLS プロトコルおよび暗号スイートを管理します。
次のドキュメントと AD FS で使用されている暗号を無効にして特定の TLS と SSL プロトコルを有効にする方法に関する情報を提供します。

## <a name="tlsssl-schannel-and-cipher-suites-in-ad-fs"></a>TLS と SSL、SChannel、および AD FS での暗号スイート

トランスポート層セキュリティ (TLS) とセキュリティで保護されたソケット レイヤー (SSL) は、通信のセキュリティ保護を提供するプロトコルです。  Active Directory フェデレーション サービスでは、通信にこれらのプロトコルを使用します。  今日のこれらのプロトコルのいくつかのバージョンが存在します。

Schannel は、SSL、TLS および DTLS インターネット標準の認証プロトコルを実装するセキュリティ サポート プロバイダー (SSP) です。 セキュリティ サポート プロバイダー インターフェイス (SSPI) は、認証など、セキュリティ関連の機能を実行する Windows システムで使用される API です。 SSPI は、Schannel SSP を含むいくつかのセキュリティ サポート プロバイダー (Ssp) を共通のインターフェイスとして機能します。

暗号スイートは、暗号アルゴリズムのセットです。 TLS と SSL プロトコルの schannel SSP の実装では、キーを作成し、情報が暗号化の暗号スイートのアルゴリズムを使用します。 暗号スイートは、次のタスクのそれぞれの 1 つのアルゴリズムを指定します。

- キーの交換
- 一括暗号化
- メッセージの認証

AD FS では、Schannel.dll を使用して、セキュリティで保護された通信操作を行います。  現在 AD FS には、すべてのプロトコルおよび Schannel.dll でサポートされている暗号スイートのサポートしています。

## <a name="managing-the-tlsssl-protocols-and-cipher-suites"></a>TLS と SSL プロトコルおよび暗号スイートの管理
> [!IMPORTANT]
> このセクションには、レジストリを変更する方法については、手順が含まれています。 ただし、レジストリを誤って変更する場合に、重大な問題が発生する可能性があります。 そのため、これらの手順を慎重に従うことを確認します。 
> 
> 中断または特定のクライアントとサーバー間の通信を回避するため SCHANNEL の既定のセキュリティ設定を変更している可能性がありますに注意してください。  これは、セキュリティで保護された通信が必要がありとの通信をネゴシエートするプロトコルがない場合に発生するされます。
> 
> これらの変更を適用する場合は、AD FS サーバー ファーム内のすべてに適用する必要があります。  これらの変更を適用した後、再起動が必要です。

[今日日と有効期間、サーバーのセキュリティ強化古いを削除すると脆弱な暗号スイートが、多くの組織の主要な優先順位が高まっています。  ソフトウェアのスイートは利用可能なするは、サーバーをテストし、これらのプロトコルとスイートの詳細情報を提供します。  準拠を維持する、またはセキュリティで保護された評価を実現するために削除または暗号強度の低いプロトコルを無効になりました必要があります。  このドキュメントの残りの部分では、および暗号スイートを有効または特定のプロトコルを無効にする方法のガイダンスを提供します。

次のレジストリ キーに同じ場所にある: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols します。  暗号を有効にする、またはこれらのプロトコルを無効にするには、regedit または PowerShell を使用します。

![レジストリの場所](media/Managing-SSL-Protocols-in-AD-FS/registry.png)

## <a name="enable-and-disable-ssl-20"></a>有効にして、SSL 2.0 を無効にします。
SSL 2.0 を無効にするには、次のレジストリ キーとその値を使用します。

### <a name="enable-ssl-20"></a>SSL 2.0 を有効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server]「有効」= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server]"DisabledByDefault"dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client]「有効」= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client]"DisabledByDefault"dword:00000000 を = 

### <a name="disable-ssl-20"></a>SSL 2.0 を無効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SL 2.0\Server]「有効」dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server]"DisabledByDefault"= dword:00000001 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client]「有効」dword:00000000 を =
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
SSL 3.0 を無効にするには、次のレジストリ キーとその値を使用します。

### <a name="enable-ssl-30"></a>SSL 3.0 を有効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server]「有効」= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server]"DisabledByDefault"dword:00000000 を = 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client]「有効」= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client]"DisabledByDefault"dword:00000000 を = 

### <a name="disable-ssl-30"></a>SSL 3.0 を無効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server]「有効」dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server]"DisabledByDefault"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client]「有効」dword:00000000 を =
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
TLS 1.0 を無効にするには、次のレジストリ キーとその値を使用します。

> [!IMPORTANT]
> TLS 1.0 を無効にすると、AD FS の信頼に、WAP は中断されます。  TLS 1.0 を無効にした場合、アプリケーションの強力な認証を有効にする必要があります。  参照してください[強力な認証を有効にします。](#enabling-strong-authentication-for-net-applications) 



### <a name="enable-tls-10"></a>TLS 1.0 を有効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server]「有効」= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server]"DisabledByDefault"dword:00000000 を = 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client]「有効」= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client]"DisabledByDefault"dword:00000000 を = 

### <a name="disable-tls-10"></a>TLS 1.0 を無効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server]「有効」dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server]"DisabledByDefault"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client]「有効」dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client]"DisabledByDefault"= dword:00000001 

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
TLS 1.1 を無効にするには、次のレジストリ キーとその値を使用します。

### <a name="enable-tls-11"></a>TLS 1.1 を有効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server]「有効」= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server]"DisabledByDefault"dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client]「有効」= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client]"DisabledByDefault"dword:00000000 を =

### <a name="disable-tls-11"></a>TLS 1.1 を無効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server]「有効」dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server]"DisabledByDefault"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client]「有効」dword:00000000 を =
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

TLS 1.2 を無効にするには、次のレジストリ キーとその値を使用します。

### <a name="enable-tls-12"></a>TLS 1.2 を有効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server]「有効」= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server]"DisabledByDefault"dword:00000000 を = 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client]「有効」= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client]"DisabledByDefault"dword:00000000 を =

### <a name="disable-tls-12"></a>TLS 1.2 を無効にします。
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server]「有効」dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server]"DisabledByDefault"= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client]「有効」dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client]"DisabledByDefault"= dword:00000001

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

RC4 を無効にするには、次のレジストリ キーとその値を使用します。  ここでは、この暗号スイートのレジストリ キーください。

- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\

![レジストリの場所](media/Managing-SSL-Protocols-in-AD-FS/cipher.png)



### <a name="enable-rc4"></a>RC4 を有効にします。

- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128]「有効」= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128]「有効」= dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128]「有効」= dword:00000001 

### <a name="disable-rc4"></a>RC4 を無効にします。

- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128]「有効」dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128]「有効」dword:00000000 を =
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128]「有効」dword:00000000 を = 

### <a name="using-powershell"></a>PowerShell を使用します。

```powershell
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
```

## <a name="enabling-or-disabling-additional-cipher-suites"></a>有効にすると、またはその他の暗号スイートを無効にします。

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Cryptography\Configuration\Local\SSL\0010002 からそれらを削除することで特定の特定の暗号を無効にすることができます。 

![レジストリの場所](media/Managing-SSL-Protocols-in-AD-FS/suites.png)

暗号スイートを有効にするには文字列値関数複数行文字列値キーです。  たとえば、TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P521 を有効にする場合、おに追加文字列。

完全な一覧のサポートされている暗号スイートを参照してください[TLS/SSL (Schannel SSP) の暗号スイート](https://msdn.microsoft.com/en-us/library/windows/desktop/aa374757.aspx)します。  このドキュメントでは、既定ではサポートされますが、既定で無効になっているものを有効になっているスイートのテーブルを示します。  暗号スイートでは、優先順位を設定するには、「[Schannel 暗号スイートの優先順位を付ける](https://msdn.microsoft.com/en-us/library/windows/desktop/bb870930.aspx)します。

## <a name="enabling-strong-authentication-for-net-applications"></a>.NET アプリケーションの強力な認証を有効にします。
.NET Framework 3.5/4.0/4.5.x アプリケーションは、SchUseStrongCrypto レジストリ キーを有効にすると、TLS 1.2 を既定のプロトコルを切り替えることができます。  このレジストリ キーは、TLS 1.2 を使用する .NET アプリケーションを強制します。

> [!IMPORTANT]
> Windows Server 2016 および Windows Server 2012 R2 で AD FS 用の .NET Framework 4.0/4.5.x キーを使用する必要があります: HKEY_LOCAL_MACHINE します。NETFramework\v4.0.30319


.NET Framework 3.5 は、次のレジストリ キーを使用します。

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\ します。NETFramework\v2.0.50727]"SchUseStrongCrypto"= dword:00000001

.NET framework 4.0/4.5.x は次のレジストリ キーを使用して: HKEY_LOCAL_MACHINE します。NETFramework\v4.0.30319"SchUseStrongCrypto"= dword:00000001

![強力な認証](media/Managing-SSL-Protocols-in-AD-FS/strongauth.png)

```powershell
    
    New-ItemProperty -path 'HKLM:\SOFTWARE\Microsoft\.NetFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value '1' -PropertyType 'DWord' -Force | Out-Null
```

## <a name="additional-information"></a>追加情報

- [TLS/SSL (Schannel SSP) の暗号スイート](https://msdn.microsoft.com/en-us/library/windows/desktop/aa374757.aspx)
- [Windows 8.1 での TLS 暗号スイート](https://msdn.microsoft.com/en-us/library/windows/desktop/mt767781.aspx)
- [Schannel の暗号スイートの優先度付け](https://msdn.microsoft.com/en-us/library/windows/desktop/bb870930.aspx)
- [暗号およびその他の Enigmatic 語で話しています。](https://blogs.technet.microsoft.com/askds/2015/12/08/speaking-in-ciphers-and-other-enigmatic-tonguesupdate/)
