---
title: ドメイン ベースの名前空間を Windows Server 2008 モードに移行する
description: この記事では、ドメイン ベースの名前空間を Windows Server 2008 モードに移行する方法について説明します。
ms.date: 6/5/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e2624e53d306dd198525b0abe8adf96fe6060bc1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847863"
---
# <a name="migrate-a-domain-based-namespace-to-windows-server-2008-mode"></a>ドメイン ベースの名前空間を Windows Server 2008 モードに移行する

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

ドメイン ベースの名前空間の Windows Server 2008 モードには、アクセス ベースの列挙とスケーラビリティの向上のサポートが含まれています。

## <a name="to-migrate-a-domain-based-namespace-to-windows-server-2008-mode"></a>ドメイン ベースの名前空間を Windows Server 2008 モードに移行するには

ドメイン ベースの名前空間を Windows 2000 Server モードから Windows Server 2008 モードに移行するには、名前空間をファイルにエクスポートして名前空間を削除し、Windows Server 2008 モードで再作成してから名前空間設定をインポートする必要があります。 この場合、次の手順を実行します。

1.  コマンド プロンプト ウィンドウを開き、名前空間をファイルにエクスポートするには、次のコマンドを入力、 \\ \\*ドメイン*\\*名前空間*の名前を指定します適切なドメイン、および名前空間と*パス\\filename*エクスポート ファイルのパスとファイルの名前を指定します。
     ```
     Dfsutil root export \\domain\namespace path\filename.xml 
     ```
2.  パスを書き留めます ( \\ \\ *server* \\*共有*) の各名前空間サーバー。 Dfsutil は名前空間サーバーをインポートできないため、再作成された名前空間に名前空間サーバーを手動で追加する必要があります。
3.  DFS 管理で、名前空間を右クリックして **[削除]** をクリックするか、コマンド プロンプトに次のコマンドを入力します。 <br /> 場所\\ \\*ドメイン*\\*名前空間*適切なドメインと名前空間の名前を指定します。
     ```
     Dfsutil root remove \\domain\namespace
     ```
4.  DFS 管理では、同じ名前の名前空間を再作成しますが、Windows Server 2008 モードを使うか、コマンド プロンプトに次のコマンドを入力します。 <br /> \\\\*server*\\*名前空間*適切なサーバーと共有の名前空間のルートの名前を指定します。
     ```
     Dfsutil root adddom \\server\namespace v2
     ```
5.  エクスポート ファイルから名前空間をインポートするには、コマンド プロンプトで次のコマンドを入力します。 <br /> \\\\*ドメイン*\\*名前空間*適切なドメインと名前空間の名前を指定し、*パス\\filename*インポートするファイルのパスとファイルの名前を指定します。
     ```
     Dfsutil root import merge path\filename.xml \\domain\namespace
     ```

    > [!NOTE]
    > 大きい名前空間のインポートに必要な時間を最小限に抑えるため、名前空間サーバーのローカルで **Dfsutil** ルート インポート コマンドを実行します。
6.  DFS 管理で名前空間を右クリックして **[名前空間サーバーを追加]** をクリックするか、コマンド プロンプトで次のコマンドを入力して、残りの名前空間サーバーをすべて再作成された名前空間に追加します。 <br /> \\\\*server*\\*共有*適切なサーバーと共有の名前空間のルートの名前を指定します。
     ```
     Dfsutil target add \\server\share 
     ```

    > [!NOTE]
    > 名前空間サーバーは名前空間をインポートする前に追加できますが、名前空間サーバーとして追加された後に名前空間全体をすぐにダウンロードするのではなく、名前空間サーバーが名前空間のメタデータを増加的にダウンロードすることになります。

## <a name="see-also"></a>関連項目
-   [DFS 名前空間を展開します。](deploying-dfs-namespaces.md)
-   [Namespace の種類を選択します。](choose-a-namespace-type.md)