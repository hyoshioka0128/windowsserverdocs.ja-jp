---
ms.assetid: 81c55015-82e5-4ba1-b15e-cc7b49af28fc
title: ファイルサーバーに関する情報の保持を実装するシナリオ
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 2f6b55d8a98a0f4fb0c286e16d752a18e61dce1a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861105"
---
# <a name="scenario-implement-retention-of-information-on-file-servers"></a>Scenario: Implement Retention of Information on File Servers

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

保持期間とは、ドキュメントの有効期限が切れるまでに保存される時間の長さです。 組織によって、保持期間が異なる場合があります。 フォルダー内のファイルを、短い保持期間のファイル、中間の保持期間のファイル、または長い保持期間のファイルとして分類し、それぞれの期間に対して期限を割り当てることができます。 訴訟ホールドにすることでファイルを無期限に保持することもできます。  
  
## <a name="scenario-description"></a><a name="BKMK_OVER"></a>シナリオの説明  
ファイル分類インフラストラクチャおよびファイル サーバー リソース マネージャーは、ファイル管理タスクおよびファイル分類を使用して一連のファイルに保持期間を適用します。 フォルダーに保持期間を割り当てた後にファイル管理タスクを使用することで、割り当てられた保持期間をいつまで適用するかを構成できます。 フォルダー内のファイルの有効期限が切れそうになると、ファイルの所有者は電子メールによる通知を受信します。 ファイルを訴訟ホールドとして分類し、ファイル管理タスクでファイルの有効期限が切れないように設定できます。  
  
「[ファイル サーバーでの情報の保持の計画](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)」に、保持の構成に関する計画情報があります。  
  
「 [ &#40;ファイルサーバーへの情報の保持の実装&#41;](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md)」の手順に従って、訴訟ホールドのためにファイルを分類し、保有期間を構成するための手順を確認できます。  
  
> [!NOTE]  
> このシナリオでは、訴訟ホールドのためにドキュメントを手動で分類する方法のみが説明されています。 ただし、Windows Server 2012 では、訴訟ホールドのためにドキュメントを自動的に分類することができます。 これを行う 1 つの方法として、訴訟ホールド下のユーザー アカウントのリストに対してファイル所有者を比較する Windows PowerShell 分類子を作成する方法があります。 ファイル所有者がユーザー アカウント リストの一部である場合、ファイルは訴訟ホールドとして分類されます。  
  
## <a name="in-this-scenario"></a>このシナリオの内容  
このシナリオは、ダイナミック アクセス制御のシナリオの一部です。 ダイナミック アクセス制御の追加情報については、次のトピックを参照してください。  
  
-   [動的 Access Control: シナリオの概要](Dynamic-Access-Control--Scenario-Overview.md)  
  
## <a name="features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>このシナリオに含まれる機能  
次の表で、このシナリオに含まれる機能を紹介すると共に、それをシナリオに活かす方法について説明します。  
  
|機能|このシナリオのサポート方法|  
|-----------|---------------------------------|  
|[ファイルサーバーリソースマネージャーの概要](https://technet.microsoft.com/library/hh831701.aspx)|ファイル分類インフラストラクチャは、ファイル サーバー リソース マネージャーに含まれている機能です。|  
|[ファイル サービスおよび記憶域サービスの概要](https://technet.microsoft.com/library/hh831487.aspx)|ファイル サーバー リソース マネージャーは、ファイル サービスのサーバーの役割に付属している機能です。|  
  
  


