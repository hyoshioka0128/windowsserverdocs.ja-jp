---
title: クライアント アクセス ライセンスを管理する
description: MultiPoint Services で Cal を操作する方法について説明します。
ms.custom: na
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 675e089e-d841-401e-bba7-69f3929ef609
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 4d809ab1bf2a18dff537bf63620623d576c0b25d
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949882"
---
# <a name="manage-client-access-licenses"></a>クライアント アクセス ライセンスを管理する
ステーションとして使用される MultiPoint services を実行しているコンピューターを含め、MultiPoint Services システムに接続するすべてのステーションには、ユーザーごとの有効なリモートデスクトップ*クライアントアクセスライセンス (CAL)* が必要です。

ステーション仮想デスクトップを物理ステーションではなく使用している場合は、各ステーション仮想デスクトップに CAL をインストールする必要があります。  
  
1.  MultiPoint Services コンピューターまたはサーバーに接続されている各ステーションのクライアントライセンスを購入します。 Cal の購入の詳細については、リモートデスクトップライセンスに関するドキュメントを参照してください。 

2.  **[スタート]** 画面で、 **[MultiPoint マネージャー]** を開きます。  
  
3.  **[ホーム]** タブをクリックし、 **[クライアントアクセスライセンスの追加]** をクリックします。  CAL ライセンスの管理ツールが開きます。

## <a name="set-the-licensing-mode-manually"></a>ライセンスモードを手動で設定する
適切に構成されていない場合、MultiPoint Services のセットアップでは、猶予期間の期限が切れていることを通知するメッセージが表示されます。 ライセンスモードを設定するには、次の手順に従います。

1. **ローカルグループポリシーエディター** (gpedit.msc) を起動します。

2. 左側のウィンドウで、[**ローカルコンピューター > ポリシー]、[コンピューターの構成-> 管理用テンプレート-> Windows コンポーネント-> リモートデスクトップサービス > リモートデスクトップセッションホスト > ライセンス**] の順に移動します。

3. 右側のウィンドウで、 **[指定されたリモートデスクトップライセンスサーバーを使用する]** を右クリックし、 **[編集]** を選択します。
   - グループポリシーエディター ダイアログで、**有効** を選択します。
   - **[使用するライセンスサーバー]** フィールドにローカルコンピューターの名前を入力します。
   - **[OK]** を選択します。
  
4. 右側のウィンドウで、 **[リモートデスクトップライセンスモードの設定]** を右クリックし、 **[編集]** を選択します。
   - グループポリシーエディター ダイアログで、**有効** を選択します。
   - **ライセンスモード**を [デバイスごと/ユーザーごと] に設定します。
   - **[OK]** を選択します。 

  
## <a name="see-also"></a>関連項目  
[MultiPoint マネージャーを使用したシステム タスクの管理](Manage-System-Tasks-Using-MultiPoint-Manager.md)
