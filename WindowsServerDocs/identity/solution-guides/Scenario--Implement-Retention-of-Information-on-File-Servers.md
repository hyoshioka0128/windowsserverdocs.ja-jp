---
ms.assetid: 81c55015-82e5-4ba1-b15e-cc7b49af28fc
title: "ファイル サーバー上の情報のシナリオの実装保有期間"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 59fd7f0a0a4d9ed8f5cec57b17be21e1aa4cd592
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="scenario-implement-retention-of-information-on-file-servers"></a>シナリオ: ファイル サーバー上の情報の保持を実装します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

保有期間がドキュメントをする必要があります時間期限が切れるまでに保存します。 組織によっては、保有期間が異なるできます。 短い、中、または長い保持期間を持つものとしてフォルダーにファイルを分類し、それぞれの期間の期限を割り当てることができます。 訴訟ホールド上に配置して、ファイルを無期限に保持することがあります。  
  
## <a name="BKMK_OVER"></a>シナリオの説明  
ファイル分類インフラストラクチャおよびファイル サーバー リソース マネージャーは、一連のファイルの保存期間を適用するのにファイル管理タスクおよびファイル分類を使用します。 フォルダーの保持期間を割り当てたし、最後に、割り当てられた保持期間は、どのくらいの期間を構成するファイル管理タスクを使用できます。 フォルダー内のファイルが切れそうになると、ファイルの所有者は電子メールによる通知を受信します。 また、できるように、ファイル管理タスクがファイル有効期限はありません、訴訟ホールドにすると、ファイルを分類できます。  
  
ご覧の保有期間の構成に関する計画情報[情報の保有期間のファイル サーバーの計画](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)します。  
  
訴訟ホールドのためのファイルを分類しての保有期間を構成するための手順を見つけることができます[展開を実装する保有期間の情報には、ファイル サーバー (&) #40; デモンストレーション手順 & #41 です。](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md).  
  
> [!NOTE]  
> このシナリオでは、訴訟ホールドのためのドキュメントを手動で分類する方法についてのみ説明します。 ただし、訴訟ホールドのためにドキュメントを自動的に分類する Windows Server 2012 でです。 これを行う方法の 1 つでは、訴訟ホールド下にあるユーザー アカウントの一覧をファイル所有者を比較する Windows PowerShell 分類子を作成します。 ファイルの所有者がユーザー アカウントの一覧の一部である場合は、ファイルが訴訟ホールドとして分類されます。  
  
## <a name="in-this-scenario"></a>このシナリオでは  
このシナリオは、ダイナミック アクセス制御シナリオの一部です。 ダイナミック アクセス制御についての詳細についてを参照してください。  
  
-   [ダイナミック アクセス制御: シナリオの概要](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="BKMK_NEW"></a>このシナリオでは含まれている機能  
次の表は、このシナリオの一部である機能の一覧し、活かす方法について説明します。  
  
|機能|このシナリオをサポートする方法|  
|-----------|---------------------------------|  
|[ファイル サーバー リソース マネージャーの概要](https://technet.microsoft.com/library/hh831701.aspx)|ファイル分類インフラストラクチャは、ファイル サーバー リソース マネージャーに含まれている機能です。|  
|[ファイル サービスおよび記憶域サービスの概要](https://technet.microsoft.com/library/hh831487.aspx)|ファイル サーバー リソース マネージャーは、ファイル サービス サーバーの役割に含まれている機能です。|  
  
  


