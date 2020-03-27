---
title: Windows PowerShell で役割ベースのアクセス制御を管理する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f13f78e-0114-4e41-9a28-82a4feccecfc
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a5cd347b849948052f4f7caa7fa8a863808e8c26
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309532"
---
# <a name="manage-role-based-access-control-with-windows-powershell"></a>Windows PowerShell で役割ベースのアクセス制御を管理する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Windows PowerShell を使用してロールベースのアクセス制御を管理するために IPAM を使用する方法について説明します。  
  
>[!NOTE]
>IPAM Windows PowerShell コマンドリファレンスについては、 [Windows powershell の IpamServer コマンドレット](https://docs.microsoft.com/powershell/module/ipamserver/?view=win10-ps)を参照してください。  
  
新しい Windows PowerShell IPAM コマンドを使用すると、DNS および DHCP オブジェクトのアクセススコープを取得したり、変更したりできます。 次の表は、各 IPAM オブジェクトに対して使用する正しいコマンドを示しています。  
  
|IPAM オブジェクト|コマンド|説明|  
|---------------|-----------|---------------|  
|DNS サーバー|IpamDnsServer|このコマンドレットは、IPAM 内の DNS サーバーオブジェクトを返します。|  
|DNS ゾーン|IpamDnsZone|このコマンドレットは、IPAM 内の DNS ゾーンオブジェクトを返します。|  
|DNS リソースレコード|IpamResourceRecord|このコマンドレットは、IPAM 内の DNS リソースレコードオブジェクトを返します。|  
|DNS 条件付きフォワーダー|IpamDnsConditionalForwarder|このコマンドレットは、IPAM 内の DNS 条件付きフォワーダーオブジェクトを返します。|  
|DHCP サーバー|IpamDhcpServer|このコマンドレットは、IPAM 内の DHCP サーバーオブジェクトを返します。|  
|DHCP スーパースコープ|IpamDhcpSuperscope|このコマンドレットは、IPAM 内の DHCP スーパースコープオブジェクトを返します。|  
|DHCP スコープ|IpamDhcpScope|このコマンドレットは、IPAM 内の DHCP スコープオブジェクトを返します。|  
  
次のコマンド出力例では、`Get-IpamDnsZone` コマンドレットは**Dublin.contoso.com** DNS ゾーンを取得します。  
  
```  
PS C:\Users\Administrator.CONTOSO> Get-IpamDnsZone -ZoneType Forward -ZoneName dublin.contoso.com  
  
ZoneName             : dublin.contoso.com  
ZoneType             : Forward  
AccessScopePath      : \Global\Dublin  
IsSigned             : False  
DynamicUpdateStatus  : None  
ScavengeStaleRecords : False  
```  
  
## <a name="setting-access-scopes-on-ipam-objects"></a>IPAM オブジェクトでのアクセススコープの設定  
IPAM オブジェクトにアクセススコープを設定するには、`Set-IpamAccessScope` コマンドを使用します。 このコマンドを使用すると、オブジェクトの特定の値にアクセススコープを設定したり、オブジェクトが親オブジェクトからアクセススコープを継承するように設定したりできます。 このコマンドを使用して構成できるオブジェクトを次に示します。  
  
-   DHCP スコープ  
  
-   DHCP サーバー  
  
-   DHCP スーパースコープ  
  
-   DNS 条件付きフォワーダー  
  
-   DNS リソースレコード  
  
-   DNS サーバー  
  
-   DNS ゾーン  
  
-   IP アドレス ブロック  
  
-   IP Address Range  
  
-   IP アドレス空間  
  
-   IP アドレスサブネット  
  
`Set-IpamAccessScope` コマンドの構文を次に示します。  
  
```  
NAME  
    Set-IpamAccessScope  
  
SYNTAX  
    Set-IpamAccessScope [-IpamRange] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDnsServer] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDhcpServer] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDhcpSuperscope] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDhcpScope] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDnsConditionalForwarder] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDnsResourceRecord] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamDnsZone] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamAddressSpace] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  
    [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamSubnet] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]  
  
    Set-IpamAccessScope [-IpamBlock] -InputObject <ciminstance[]> [-AccessScopePath <string>] [-IsInheritedAccessScope] [-PassThru] [-CimSession <CimSession[]>] [-ThrottleLimit <int>] [-AsJob] [-WhatIf] [-Confirm]  [<CommonParameters>]  
```  
  
次の例では、DNS ゾーン**dublin.contoso.com**のアクセススコープが**ダブリン**から**ヨーロッパ**に変更されています。  
  
```  
PS C:\Users\Administrator.CONTOSO> Get-IpamDnsZone -ZoneType Forward -ZoneName dublin.contoso.com  
  
ZoneName             : dublin.contoso.com  
ZoneType             : Forward  
AccessScopePath      : \Global\Dublin  
IsSigned             : False  
DynamicUpdateStatus  : None  
ScavengeStaleRecords : False  
  
PS C:\Users\Administrator.CONTOSO> $a = Get-IpamDnsZone -ZoneType Forward -ZoneName dublin.contoso.com  
PS C:\Users\Administrator.CONTOSO> Set-IpamAccessScope -IpamDnsZone -InputObject $a -AccessScopePath \Global\Europe -PassThru  
  
ZoneName             : dublin.contoso.com  
ZoneType             : Forward  
AccessScopePath      : \Global\Europe  
IsSigned             : False  
DynamicUpdateStatus  : None  
ScavengeStaleRecords : False  
```  
  


