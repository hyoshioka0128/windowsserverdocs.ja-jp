---
title: "AD フォレストの回復 - GC を追加します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: 3749fd99737f61c55871f613b9feaa21090d3bae
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---adding-the-gc"></a>AD フォレストの回復 - GC を追加します。 

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:

 DC にグローバル カタログを追加するのにには、次の手順を使用します。  
  
## <a name="to-add-the-global-catalog"></a>グローバル カタログに追加するには  
  
1.  をクリックして**開始**、] をポイント**すべてのプログラム**、] をポイント**管理ツール**、] をクリックし、 **Active Directory サイトとサービス**します。  
2.  コンソール ツリーで、展開、**サイト**コンテナー、およびターゲット サーバーが含まれている適切なサイトを選択します。  
3.  展開、**サーバー**コンテナー、グローバル カタログを追加する DC のサーバー オブジェクトを展開します。  
4.  右クリック**NTDS 設定**、] をクリックし、**プロパティ**します。  
5.  選択、**グローバル カタログ**チェック ボックスをオンします。  
![GC を追加します。](media/AD-Forest-Recovery-Add-GC/addgc1.png)
  
## <a name="to-add-the-global-catalog-using-repadmin"></a>Repadmin を使用してグローバル カタログに追加するには  
  
1.  管理者特権でコマンド プロンプトを開き、次のコマンドを入力し、Enter キーを押します。  
  
    ```  
    repadmin.exe /options DC_NAME +IS_GC  
    ```  
  
 ルート ドメインの DC にグローバル カタログを追加するプロセスを高速化する方法を次に示します。  
  
-   理想的には、ルート ドメインの DC では、非ルート ドメインに復元された Dc のレプリケーション パートナーをする必要があります。 場合は、対応する、知識整合性チェッカー (KCC) が作成することを確認**repsFrom**ソース DC とルート DC にパーティションのオブジェクトです。 これを確認するにを実行して、 **repadmin/showreps/v**コマンド。  
  
-   場合があるない**repsFrom**オブジェクトの作成、構成パーティションについて、このオブジェクトを作成します。 これにより、ルート ドメインの DC を決定できます非ルート ドメインにあるどの Dc が削除されました。 次のコマンドを使用して、これを行うことができます。  
  
    ```  
    repadmin /add ConfigurationNamingContext DestinationDomainController SourceDomainControllerCNAME  
    ```  
  
    ```  
    repadmin /options DSA -Disable_NTDSCONN_XLATE  
    ```  
  
     形式、 *SourceDomainControllerCNAME*は。  
  
    ```  
  
    sourceDCGuid._msdcs.root domain  
    ```  
  
     Repadmin など]、[コマンドを追加、contoso.com ドメインの構成パーティションがある可能性があります。  
  
    ```  
    repadmin /add cn=configuration,DC=contoso,DC=com DC01 937ef930-7356-43c8-88dc-8baaaa781cf6._msdcs.dDSP17A22.contoso.com  
    ```  
  
-   場合、 **repsFrom**オブジェクトが存在、次のように非ルート ドメインの DC とルート ドメインの DC を同期しようとします。  
  
    ```  
    Repadmin /sync DomainNamingContext DestinationDomainController SourceDomainControllerGUID  
    ```  
  
     ここで*DestinationDomainController*ルート ドメインのドメイン コント ローラーと*SourceDomainController*非ルート ドメインの復元されたドメイン コント ローラーします。  
  
-   ルート ドメインの DNS サーバーは、ソース DC のエイリアス (CNAME) リソース レコードが必要です。 親 DNS ゾーンが含まれている委任リソース レコード (ネーム サーバー (NS) とホスト (A) リソース レコード)、正しい dc (バックアップから復元された Dc) で、子ゾーンを確認します。  
  
-   ルート ドメインの DC が非ルート ドメインの適切なキー配布センター (KDC) に連絡していることを確認します。 コマンド プロンプトで、これをテストするには、次のコマンドを入力し、し、ENTER キーを押します。  
  
    ```  
    nltest /dsgetdc:nonroot domain name /KDC /Force  
    ```  
## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)  
