---
title: RDS クライアント アクセス ライセンスをインストールします。
description: RD クライアントの Cal をインストールする方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 09/20/2016
manager: dongill
ms.openlocfilehash: 2f283b51acc869704a52f09bebc228660cdfbc38
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870573"
---
# <a name="install-rds-client-access-licenses-on-the-remote-desktop-license-server"></a>リモート デスクトップ ライセンス サーバー上の RDS クライアント アクセス ライセンスをインストールします。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

ライセンス サーバーにリモート デスクトップ サービス クライアント アクセス ライセンス (Cal) をインストールするのにには、次の情報を使用します。 Cal がインストールされると、ライセンス サーバーを発行するユーザーに適切なようにします。

リモート デスクトップ ライセンス マネージャを実行していないコンピューターのライセンス サーバーを実行しているコンピューターでインターネットに接続する必要がありますに注意してください。

1. ライセンス サーバー (通常は、最初 RD 接続ブローカー) では、リモート デスクトップ ライセンス マネージャを開きます。
2. ライセンス サーバーを右クリックし、**ライセンスをインストールする**します。
3. クリックして**次**[ようこそ] ページ。
4. RDS Cal を購入したプログラムを選択し、クリックして**次**します。 サービス プロバイダーの場合は選択**サービス プロバイダー ライセンス契約**します。
5. ライセンス プログラムの情報を入力します。 ほとんどの場合、ライセンス コードまたは契約番号では、これになりますが、ライセンス プログラムを使用しているかによって異なります。
6. **[次へ]** をクリックします。
7. 製品バージョン、ライセンスの種類、および、環境内のライセンスの数を選択し、クリックして**次**します。 ライセンス マネージャーは、検証、ライセンスを取得して Microsoft クリアリングハウスにアクセスします。
8.  **[完了]** をクリックして、注文プロセスを完了します。