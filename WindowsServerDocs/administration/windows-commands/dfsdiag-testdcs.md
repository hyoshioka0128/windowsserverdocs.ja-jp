---
title: Dfsdiag TestDCs
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: abb915ab-23eb-45d7-9a2e-b6b9a5756a70
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 62956ae65d2311939ac0db6a4b86950f21dba407
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836603"
---
# <a name="dfsdiag-testdcs"></a>Dfsdiag TestDCs

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したドメイン内の各ドメイン コント ローラーで、次のテストを実行することによって、ドメイン コント ローラーの構成を確認します。  
  
-   検証が行われます分散ファイル システム\(DFS\) Namespace サービスが実行されていると、スタートアップの種類が自動に設定します。  
  
-   サイトのサポートを確認します\-NETLOGON と SYSvol の紹介コストがかかります。  
  
-   ホスト名と IP アドレスでは、サイトの関連付けの整合性を確認します。  
  
  
  
## <a name="syntax"></a>構文  
  
```  
dfsdiag /TestDCs [/Domain:<Domain name>]  
```  
  
### <a name="parameters"></a>パラメーター  
  
|パラメーター|説明|  
|-------|--------|  
|\/ドメイン:<Domain name>|確認するドメイン。|  
  
## <a name="remarks"></a>注釈  
\/ドメインは、省略可能なパラメーターです。 既定値は、ローカル ドメインに参加しているローカル ホストです。  
  
## <a name="BKMK_Examples"></a>例  
Contoso.com ドメインのドメイン コント ローラーの構成を確認するには、次のように入力します。  
  
```  
dfsdiag /TestDCs /Domain:Contoso.com  
```  
  
## <a name="additional-references"></a>その他の参照  
  
-   [コマンドライン構文キー](command-line-syntax-key.md)  
  
-   [dfsdiag](dfsdiag.md)  
  

