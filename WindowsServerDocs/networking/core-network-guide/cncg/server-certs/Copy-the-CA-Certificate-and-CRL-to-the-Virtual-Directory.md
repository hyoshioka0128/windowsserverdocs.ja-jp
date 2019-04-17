---
title: CA 証明書と CRL を仮想ディレクトリにコピーします。
description: このトピックの「802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部である
manager: brianlic
ms.topic: article
ms.assetid: a1b5fa23-9cb1-4c32-916f-2d75f48b42c7
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e37bfce7f8cf33fd7fcb5e6227d783c28bd29d35
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="copy-the-ca-certificate-and-crl-to-the-virtual-directory"></a>CA 証明書と CRL を仮想ディレクトリにコピーします。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

AD CS が正しく構成されていることを確認して、証明機関から証明書失効リストとエンタープライズ ルート CA 証明書を Web サーバー上の仮想ディレクトリにコピーするには、この手順を使用することができます。 以下のコマンドを実行するには、する前に、ディレクトリとサーバー名を展開に適切なものを置き換えることを確認します。  
  
この手順を実行するには、メンバーである**Domain Admins**します。  
  
#### <a name="to-copy-the-certificate-revocation-list-from-ca1-to-web1"></a>CA1 から WEB1 に証明書失効リストをコピーするには  
  
1.  CA1、[を管理者として Windows PowerShell を実行し、し、次のコマンドを使用して CRL を公開します。  
  
    - 種類`certutil -crl`、し、ENTER キーを押します。  
  
    - CA 証明書を Web サーバー上のファイル共有にコピーするに次のように入力します。 `copy C:\Windows\system32\certsrv\certenroll\*.crt \\WEB1\pki`、し、ENTER キーを押します。  
    - 証明書失効リストを Web サーバー上のファイル共有にコピーするに次のように入力します。 `copy C:\Windows\system32\certsrv\certenroll\*.crl \\WEB1\pki`、し、ENTER キーを押します。  
  
2. AD CS を再起動して、次のように入力します。 `Restart-Service certsvc`、し、ENTER キーを押します。  
  
2.  CDP および AIA 拡張機能の場所が正しく構成されていることを確認するには、次のように入力します。 `pkiview.msc`、し、ENTER キーを押します。 Pkiview、エンタープライズ PKI MMC が開きます。  
  
3.  CA の名前をクリックします。 たとえば、CA の名前が corp-CA CA1 である場合は、クリックして**corp-CA CA1**します。 詳細ウィンドウで、いることを確認、**ステータス**の値、 **CA 証明書**、 **AIA の場所 1**と**CDP の場所 1**はすべて**OK**します。  
  
次の図は、[ok] のすべての項目の状態を pkiview 結果ペインを示しています。  
  
![adcs_pkiviewmedia/adcs_pkiview.png)  
  
> [!IMPORTANT]  
> 場合**ステータス**いずれかの項目が**OK**、次の操作します。  
> -   証明書と証明書失効リストのファイルが正常にコピーされて、共有することを確認するように Web サーバー上の共有を開きます。 共有にそれらが正常にコピーされていない場合は、適切なファイルのソースと、コピー コマンドを変更し、先を共有するコマンドをもう一度実行します。  
> -   余分なスペースなし、または指定した場所にその他の文字があることを確認する CA の拡張機能] タブで CDP および AIA の正しい場所を入力したことを確認します。  
> -   Web サーバー上の正しい場所に CRL と CA 証明書をコピーした場所に CA の CDP および AIA の場所の指定した場所と一致することを確認します。  
> -   CA 証明書と CRL が格納されている仮想フォルダのアクセス許可が正しく構成されていることを確認します。  
  


