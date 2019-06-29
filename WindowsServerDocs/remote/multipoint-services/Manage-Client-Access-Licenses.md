---
title: クライアント アクセス ライセンスを管理する
description: MultiPoint Services での Cal を使用する方法について説明します
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 42b943ed5e0066f1f810efaba9e65a529ac25f00
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469347"
---
# <a name="manage-client-access-licenses"></a>クライアント アクセス ライセンスを管理する
すべてのステーションが MultiPoint Services ステーションとして使用されているを実行しているコンピューターを含め、MultiPoint Services システムに接続するには、ユーザーごとの有効なリモート デスクトップをいる必要があります*クライアント アクセス ライセンス (CAL)* します。

ステーションの仮想デスクトップ ステーションが物理的ではなくを使用している場合は、各ステーションの仮想デスクトップの CAL をインストールする必要があります。  
  
1.  MultiPoint Services コンピューターまたはサーバーに接続されている各ステーションのクライアント ライセンスを購入します。 Cal の購入方法の詳細については、リモート デスクトップ ライセンスに関するドキュメントを参照してください。 

2.  **開始** 画面で、開いている**MultiPoint マネージャー**します。  
  
3.  をクリックして、**ホーム**タブをクリックし、をクリックし、**クライアント アクセス ライセンスを追加**します。  これにより、CAL ライセンスの管理ツールが開きます。

# <a name="set-the-licensing-mode-manually"></a>ライセンス モードを手動で設定します。
場合は正しく構成されているこの MultiPoint Services のセットアップは、猶予期間の有効期限切れに関する通知を求められます。 ライセンス モードを設定する次の手順に従います。

1. 起動**ローカル グループ ポリシー エディター** (gpedit.msc)。

2. 左側のウィンドウに移動します**ローカル コンピューター ポリシー] の [コンピュータの構成 - > 管理用テンプレート Windows]-> [コンポーネント] メニューの [リモート デスクトップ サービス - > リモート デスクトップ セッション ホストがライセンスを ->** 。

3. 右側のウィンドウで右クリックして **、指定したリモート デスクトップ ライセンス サーバーを使用して、** 選択**編集**:
   - グループ ポリシー エディター] ダイアログ ボックス [**有効**
   - ローカル コンピューター名を入力、**ライセンス サーバーを使用する**フィールド。
   - 選択**OK**
  
4. 右側のウィンドウで右クリックして**リモート デスクトップ ライセンス モードを設定**選択**編集**
   - グループ ポリシー エディター] ダイアログ ボックス [**有効**
   - 設定、**ライセンス モード**を各デバイス/ユーザーごと
   - 選択**OK** 

  
## <a name="see-also"></a>関連項目  
[MultiPoint マネージャーを使用したシステム タスクの管理](Manage-System-Tasks-Using-MultiPoint-Manager.md)
