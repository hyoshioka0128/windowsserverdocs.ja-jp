---
title: レプリケーション要求を受け入れるようにレプリカサーバーを構成する必要がある
description: このベストプラクティスアナライザー規則によって報告された問題を解決するための手順を示します。
manager: dongill
ms.author: kathydav
ms.topic: article
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 027b9df0bad5e37e0a6e2f2d9c44dde1a3e79127
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960745"
---
# <a name="a-replica-server-must-be-configured-to-accept-replication-requests"></a>レプリケーション要求を受け入れるようにレプリカサーバーを構成する必要がある

>適用先:Windows Server 2016

ベスト プラクティスおよびスキャンの詳細については、「[ベスト プラクティス アナライザー スキャンの実行とスキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|エラー|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題
*このコンピューターは Hyper-v レプリカサーバーとして指定されていますが、プライマリサーバーからの入力方向のレプリケーションデータを受け入れるように構成されていません。*

## <a name="impact"></a>影響
*このサーバーは、プライマリサーバーからのレプリケーショントラフィックを受け付けることができません。*

## <a name="resolution"></a>解決方法
*Hyper-v マネージャーを使用して、このレプリカサーバーがレプリケーションデータを受け入れるプライマリサーバーを指定します。*

#### <a name="create-authorization-entries-using-hyper-v-manager"></a>HYPER-V マネージャーを使用して承認エントリを作成します。

1.  Hyper-V マネージャーを開きます。 (サーバーマネージャーから、[**ツール**  >  ] をクリックします。**Hyper-v マネージャー**)

2.  ホストの一覧から、目的のホストを右クリックし、[Hyper-v の**設定**] をクリックします。

3.  ナビゲーションウィンドウで、[**レプリケーションの構成**] をクリックします。

4.  [**承認と記憶域**] で、[**指定したサーバーからレプリケーションを許可する**] をクリックします。

5.  サーバーの一覧の下にある [**追加**] をクリックします。

6.  [**承認エントリの追加**] で、次のようにします。

    -   最初のサーバーの完全修飾名を入力します。

    -   そのサーバーのファイルのみを格納する専用の場所を指定します。

7.  **[OK]** をクリックします。

8.  各プライマリサーバーに対してこの手順を繰り返します。

9. もう一度 [ **OK** ] をクリックして終了し、ウィンドウを閉じます。

### <a name="create-authorization-entries-using-windows-powershell"></a>Windows PowerShell を使用して承認エントリを作成する

1.  Windows PowerShell を開きます。 (デスクトップから [スタート] をクリックし、「 **Windows PowerShell**」と入力を開始します)。

2.  右クリック **Windows PowerShell** ] をクリック **管理者として実行**します。

3.  次のようなコマンドを実行して、を置き換えます。

    -   サーバーの完全修飾ドメイン名を使用した server01.domain01.contoso.com のプライマリサーバー名。

    -   D:\ReplicaVMStorage の場所を指定します。

    -   既定という名前の信頼グループが作成されている場合は、そのグループの名前。 それ以外の場合は、既定値を使用します。

```
New-VMReplicationAuthorizationEntry server01.domain01.contoso.com D:\ReplicaVMStorage DEFAULT
```



