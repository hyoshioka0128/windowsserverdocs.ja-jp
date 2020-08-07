---
title: 手順 3. 展開を確認する
description: このトピックは、「Windows Server 2016 で DirectAccess クライアントをリモート管理する」ガイドの一部です。
manager: brianlic
ms.topic: article
ms.assetid: 6a78a078-d2e7-4cbd-b8d5-20cfb6d1524b
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 7e8b7e037c0c98c62daf9abdf743ae4c1153f054
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950847"
---
# <a name="step-3-verify-the-deployment"></a>手順 3. 展開を確認する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、DirectAccess クライアントのリモート管理の展開が正しく構成されていることを確認する方法について説明します。

### <a name="to-verify-proper-deployment"></a>適切な展開を検証するには

1.  DirectAccess クライアントコンピューターを企業ネットワークに接続し、グループポリシーオブジェクトを取得します。

2.  クライアントコンピューターで、通知領域の [**ネットワーク接続**] アイコンをクリックして、DirectAccess メディアマネージャーにアクセスします。

3.  [ **DirectAccess 接続**] をクリックすると、状態が**ローカルに接続**されていることがわかります。

4.  企業ネットワークからコンピューターを削除し、パブリックネットワークに接続します。

5.  コマンドプロンプトで、「 **nltest/dsgetdc: [完全修飾ドメイン名]**」と入力します。 このコマンドは、クライアントが企業ネットワークにアクセスできることを確認します。 ドメインコントローラにアクセスできない場合、次のエラーメッセージが表示され、ドメインが存在しないことを示すレポートが表示されます: ERROR_NO_SUCH_DOMAIN。



