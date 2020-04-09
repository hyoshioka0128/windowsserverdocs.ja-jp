---
title: クライアント アクセス ライセンスを管理する
description: MultiPoint Services で Cal を操作する方法について説明します。
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 675e089e-d841-401e-bba7-69f3929ef609
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 2981f22b2b85d90f4102c3a0b67e25901cb12395
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853545"
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
   - [ **OK]** を選択
  
4. 右側のウィンドウで、 **[リモートデスクトップライセンスモードの設定]** を右クリックし、 **[編集]** を選択します。
   - グループポリシーエディター ダイアログで、**有効** を選択します。
   - **ライセンスモード**を [デバイスごと/ユーザーごと] に設定します。
   - [ **OK]** を選択 

  
## <a name="see-also"></a>参照  
[MultiPoint マネージャーを使用したシステム タスクの管理](Manage-System-Tasks-Using-MultiPoint-Manager.md)
