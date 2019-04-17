---
title: 役割ベースの管理アクセスを Windows PowerShell での制御
description: このトピックでは、Windows Server 2016 での IP アドレス管理 (IPAM) の管理ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4f13f78e-0114-4e41-9a28-82a4feccecfc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: df6fa423a4ec891f1ad3faefad6c6054519542c4
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="manage-role-based-access-control-with-windows-powershell"></a>役割ベースの管理アクセスを Windows PowerShell での制御

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、IPAM を使用して Windows PowerShell で役割ベースのアクセス制御を管理するのに方法について説明します。  
  
>[!NOTE]
>IPAM の Windows PowerShell コマンドのリファレンスを参照してください。 [Windows PowerShell の IP アドレス管理 (IPAM) サーバー コマンドレット](https://technet.microsoft.com/library/jj553807.aspx)します。  
  
新しい Windows PowerShell の IPAM のコマンドは、取得し、DNS および DHCP のオブジェクトのアクセス スコープを変更する機能を提供します。 次の表は、IPAM オブジェクトごとに使用する正しいコマンドを示しています。  
  
|IPAM オブジェクト|コマンド|説明|  
|---------------|-----------|---------------|  
|DNS サーバー|Get IpamDnsServer|このコマンドレットは、IPAM の DNS サーバー オブジェクトを返します|  
|DNS ゾーン|Get IpamDnsZone|このコマンドレットは、IPAM の DNS ゾーンのオブジェクトを返します|  
|DNS リソース レコード|Get IpamResourceRecord|このコマンドレットは、IPAM の DNS リソース レコード オブジェクトを返します|  
|DNS 条件付きフォワーダ|Get IpamDnsConditionalForwarder|このコマンドレットは、IPAM では、DNS 条件付きフォワーダのオブジェクトを返します|  
|DHCP サーバー|Get IpamDhcpServer|このコマンドレットは、IPAM で DHCP サーバー オブジェクトを返します|  
|DHCP スーパースコープ|Get IpamDhcpSuperscope|このコマンドレットは、IPAM で DHCP スーパースコープ オブジェクトを返します|  
|DHCP スコープ|Get IpamDhcpScope|このコマンドレットは、IPAM で DHCP スコープのオブジェクトを返します|  
  
次のコマンドの出力の例で、`Get-IpamDnsZone`コマンドレットを取得、 **dublin.contoso.com** DNS ゾーンです。  
  
```  
PS C:\Users\Administrator.CONTOSO> Get-IpamDnsZone -ZoneType Forward -ZoneName dublin.contoso.com  
  
ZoneName             : dublin.contoso.com  
ZoneType             : Forward  
AccessScopePath      : \Global\Dublin  
IsSigned             : False  
DynamicUpdateStatus  : None  
ScavengeStaleRecords : False  
```  
  
## <a name="setting-access-scopes-on-ipam-objects"></a>IPAM のオブジェクトに対するアクセス スコープの設定  
IPAM のオブジェクトに対するアクセス スコープを設定するにを使用して、`Set-IpamAccessScope`コマンド。 使用して、親オブジェクトからアクセス スコープを継承するオブジェクトまたはオブジェクトの特定の値にアクセス スコープを設定するには、このコマンドを使用することができます。 このコマンドを使用して構成可能なオブジェクトを次に示します。  
  
-   DHCP スコープ  
  
-   DHCP サーバー  
  
-   DHCP スーパースコープ  
  
-   DNS 条件付きフォワーダ  
  
-   DNS リソース レコード  
  
-   DNS サーバー  
  
-   DNS ゾーン  
  
-   IP アドレス ブロック  
  
-   IP アドレスの範囲  
  
-   IP アドレス空間  
  
-   IP アドレス サブネット  
  
構文を次に示します、`Set-IpamAccessScope`コマンド。  
  
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
  
次の例では、DNS ゾーンのアクセス スコープで**dublin.contoso.com**がから変更された**Dublin**に**ヨーロッパ**します。  
  
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
  


