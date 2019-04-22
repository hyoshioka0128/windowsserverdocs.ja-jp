---
title: AD フォレストの回復 - GC の追加
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: 156a4a64d9c3bb8261bd603b72ae11b81ff1d152
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825633"
---
# <a name="ad-forest-recovery---adding-the-gc"></a>AD フォレストの回復 - GC の追加

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

次の手順を使用すると、DC をグローバル カタログを追加できます。  
  
## <a name="to-add-the-global-catalog"></a>グローバル カタログに追加するには  
  
1. クリックして**開始**、 をポイント**すべてのプログラム**、 をポイント**管理ツール**、順にクリックします**Active Directory サイトとサービス**します。  
2. コンソール ツリーで、展開、**サイト**コンテナー、およびターゲット サーバーを含む適切なサイトを選択します。  
3. 展開、**サーバー**コンテナー、グローバル カタログを追加する DC のサーバー オブジェクトを展開します。  
4. 右クリックして**NTDS 設定**、 をクリックし、**プロパティ**します。  
5. 選択、**グローバル カタログ**チェック ボックスをオンします。  
![GC を追加します。](media/AD-Forest-Recovery-Add-GC/addgc1.png)

## <a name="to-add-the-global-catalog-using-repadmin"></a>Repadmin を使用してグローバル カタログに追加するには  

- 管理者特権でコマンド プロンプトを開きます次のコマンドを入力し、ENTER キーを押します。  

   ```  
   repadmin.exe /options DC_NAME +IS_GC  
   ```  

以下は、ルート ドメインの DC をグローバル カタログを追加するプロセスを高速化する方法です。  

- 理想的には、ルート ドメインの DC には、ルート以外のドメインで復元された Dc のレプリケーション パートナーがあります。 そうである場合は、対応する知識整合性チェッカー (KCC) が作成することを確認**repsFrom**ソース DC とルート DC でパーティションのオブジェクト。 これを確認するにを実行して、 **repadmin/showreps/v**コマンド。 

- 存在する場合ありません**repsFrom**オブジェクトの作成、構成パーティションについて、このオブジェクトを作成します。 これにより、ルート ドメインの DC を判断できます非ルート ドメインでは、どの Dc が削除されました。 これは、次のコマンドで行うことができます。  

   ```
   repadmin /add ConfigurationNamingContext DestinationDomainController SourceDomainControllerCNAME  
   ```

   ```
   repadmin /options DSA -Disable_NTDSCONN_XLATE  
   ```

   形式、 *SourceDomainControllerCNAME*は。  

   ```
  
   sourceDCGuid._msdcs.root domain  
   ```

   Repadmin などのコマンドの追加、contoso.com ドメインの構成パーティションがある可能性があります。  

   ```
   repadmin /add cn=configuration,DC=contoso,DC=com DC01 937ef930-7356-43c8-88dc-8baaaa781cf6._msdcs.dDSP17A22.contoso.com  
   ```

- 場合、 **repsFrom**オブジェクトが存在する、次のようにルート以外のドメインの DC にルート ドメインの DC を同期しようとしています。  

   ```
   Repadmin /sync DomainNamingContext DestinationDomainController SourceDomainControllerGUID  
   ```

   場所*DestinationDomainController*ルート ドメインの dc と*SourceDomainController*非ルート ドメインで、復元された DC が。 

- ルート ドメインの DNS サーバーは、ソース DC のエイリアス (CNAME) リソース レコードが必要です。 親 DNS ゾーンが、子ゾーンでの適切なドメイン コント ローラー (バックアップから復元された Dc) (ネーム サーバー (NS) とホスト (A) リソース レコード) の委任のリソース レコードには含まれていることを確認します。 
- ルート ドメインの DC がルート以外のドメインで正しいキー配布センター (KDC) への接続を確認します。 コマンド プロンプトで、これをテストするには、次のコマンドを入力し、ENTER キーを押します。  

   ```
   nltest /dsgetdc:nonroot domain name /KDC /Force  
   ```

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)  
