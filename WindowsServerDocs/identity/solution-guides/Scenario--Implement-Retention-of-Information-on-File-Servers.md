---
ms.assetid: 81c55015-82e5-4ba1-b15e-cc7b49af28fc
title: ファイル サーバー上の情報のシナリオ実装の保有期間
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 59fd7f0a0a4d9ed8f5cec57b17be21e1aa4cd592
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880253"
---
# <a name="scenario-implement-retention-of-information-on-file-servers"></a>シナリオ:ファイル サーバーでの情報の保持を実装する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

保持期間とは、ドキュメントの有効期限が切れるまでに保存される時間の長さです。 組織によって、保持期間が異なる場合があります。 フォルダー内のファイルを、短い保持期間のファイル、中間の保持期間のファイル、または長い保持期間のファイルとして分類し、それぞれの期間に対して期限を割り当てることができます。 訴訟ホールドにすることでファイルを無期限に保持することもできます。  
  
## <a name="BKMK_OVER"></a>シナリオの説明  
ファイル分類インフラストラクチャおよびファイル サーバー リソース マネージャーは、ファイル管理タスクおよびファイル分類を使用して一連のファイルに保持期間を適用します。 フォルダーに保持期間を割り当てた後にファイル管理タスクを使用することで、割り当てられた保持期間をいつまで適用するかを構成できます。 フォルダー内のファイルの有効期限が切れそうになると、ファイルの所有者は電子メールによる通知を受信します。 ファイルを訴訟ホールドとして分類し、ファイル管理タスクでファイルの有効期限が切れないように設定できます。  
  
「 [Plan for Retention of Information on File Servers](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)」に、保持の構成に関する計画情報があります。  
  
訴訟ホールド用にファイルを分類および保持期間を構成するための手順を見つけることができます[展開を実装する保有期間のサーバー上の情報ファイル&#40;デモンストレーション手順&#41;](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md)します。  
  
> [!NOTE]  
> このシナリオでは、訴訟ホールドのためにドキュメントを手動で分類する方法のみが説明されています。 ただし、訴訟ホールド用のドキュメントを自動的に分類する Windows Server 2012 で可能です。 これを行う 1 つの方法として、訴訟ホールド下のユーザー アカウントのリストに対してファイル所有者を比較する Windows PowerShell 分類子を作成する方法があります。 ファイル所有者がユーザー アカウント リストの一部である場合、ファイルは訴訟ホールドとして分類されます。  
  
## <a name="in-this-scenario"></a>このシナリオの内容  
このシナリオは、ダイナミック アクセス制御のシナリオの一部です。 ダイナミック アクセス制御の追加情報については、次のトピックを参照してください。  
  
-   [ダイナミック アクセス制御:シナリオの概要](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="BKMK_NEW"></a>このシナリオに含まれる機能  
次の表で、このシナリオに含まれる機能を紹介すると共に、それをシナリオに活かす方法について説明します。  
  
|機能|このシナリオのサポート方法|  
|-----------|---------------------------------|  
|[ファイル サーバー リソース マネージャーの概要](https://technet.microsoft.com/library/hh831701.aspx)|ファイル分類インフラストラクチャは、ファイル サーバー リソース マネージャーに含まれている機能です。|  
|[ファイル サービスおよび記憶域サービスの概要](https://technet.microsoft.com/library/hh831487.aspx)|ファイル サーバー リソース マネージャーは、ファイル サービスのサーバーの役割に付属している機能です。|  
  
  


