---
title: Dfsdiag TestReferral
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 877c60dc-e993-4bd5-87dd-e892e3f98a1a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cd1b87befa8a9cfda5ea27a4ce5a5105ea1a1009
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848023"
---
# <a name="dfsdiag-testreferral"></a>Dfsdiag TestReferral

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

分散ファイル システムを確認します。 \(DFS\) 、次のテストを実行することで参照します。  
  
-   引数を指定せず、DFSpath パラメーターを使用する場合、このコマンドは、参照一覧に、信頼されたドメインすべてが含まれているを検証します。  
  
-   ドメインを指定すると、コマンドは、ドメイン コント ローラーの正常性チェックを実行します\(dfsdiag \/testdcs\)サイトの関連付けと、ローカル ホストのドメイン キャッシュしてテストします。  
  
-   ドメインを指定する場合と\\SYSvol または\\NETLOGON の 同じ正常性を実行するだけでなく、ドメインを指定すると、コマンドがチェックされるときを To Live の時間をチェック\(TTL\) SYSvol、または NETLOGON の紹介900 秒間の既定値に一致します。  
  
-   同じ正常性を実行するだけでなく、名前空間のルートを指定すると、コマンドが DFS 構成のチェックを実行するドメインを指定するときに確認します\(dfsdiag \/TestDFSConfig\)と名前空間の整合性の確認\(dfsdiag \/TestDFSIntegrity\)します。  
  
-   DFS フォルダーを指定すると\(リンク\)、コマンドにフォルダー ターゲットのサイトの構成が検証される間、名前空間のルートを指定する場合に同じ正常性がチェックを実行するだけでなく\(dfsdiag \/testsites\)し、ローカル ホストのサイトの関連付けを検証します。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
dfsdiag /TestReferral /DFSpath:<DFS path for getting referrals> [/Full]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|\/DFSpath:<path for getting referrals>|この DFS パスには、次のいずれかを指定できます。<br /><br />-   \(空白\):信頼されたドメインをテストします。<br />-   \\\\ドメイン:ドメイン コント ローラーの参照。<br />-   \\\\ドメイン\\SYSvol:SYSvol の参照。<br />-   \\\\ドメイン\\NETLOGON:NETLOGON の参照。<br />-   \\\\<Domain or server>\\<Namespace Root>:Namespace のルートの紹介。<br />-   \\\\<Domain or server>\\<Namespace root>\\<DFS folder>:DFS フォルダー\(リンク\)紹介します。|  
|\/完全です|ドメインとルートの参照にのみ適用されます。 レジストリと active directory ドメイン サービス間でサイトの関連付け情報の整合性を検証\(AD DS\)します。|  
  
## <a name="BKMK_Examples"></a>例  
TBD を入力します。  
  
```  
dfsdiag /TestReferral /DFSpath:\\Contoso.com\MyNamespace  
```  
  
TBD を入力します。  
  
```  
dfsdiag /TestReferral /DFSpath:  
```  
  
## <a name="additional-references"></a>その他の参照  
  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
  

