---
title: 手順 3. 展開を確認する
description: このトピックは、「Windows Server 2016 で DirectAccess クライアントをリモート管理する」ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a78a078-d2e7-4cbd-b8d5-20cfb6d1524b
ms.author: lizross
author: eross-msft
ms.openlocfilehash: e1a8d3208acb0e0ce891e517492916357b9fbfcc
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314355"
---
# <a name="step-3-verify-the-deployment"></a>手順 3. 展開を確認する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、DirectAccess クライアントのリモート管理の展開が正しく構成されていることを確認する方法について説明します。  
  
### <a name="to-verify-proper-deployment"></a>適切な展開を検証するには  
  
1.  DirectAccess クライアントコンピューターを企業ネットワークに接続し、グループポリシーオブジェクトを取得します。  
  
2.  クライアントコンピューターで、通知領域の **[ネットワーク接続]** アイコンをクリックして、DirectAccess メディアマネージャーにアクセスします。  
  
3.  **[DirectAccess 接続]** をクリックすると、状態が**ローカルに接続**されていることがわかります。  
  
4.  企業ネットワークからコンピューターを削除し、パブリックネットワークに接続します。  
  
5.  コマンドプロンプトで、「 **nltest/dsgetdc: [完全修飾ドメイン名]** 」と入力します。 このコマンドは、クライアントが企業ネットワークにアクセスできることを確認します。 ドメインコントローラにアクセスできない場合、次のエラーメッセージが表示され、ドメインが存在しないことを示すレポートが表示されます: ERROR_NO_SUCH_DOMAIN。  
  


