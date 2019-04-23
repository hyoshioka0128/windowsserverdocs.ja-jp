---
title: CA の証明書と CRL を仮想ディレクトリにコピーします。
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: dougkim
ms.topic: article
ms.assetid: a1b5fa23-9cb1-4c32-916f-2d75f48b42c7
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.date: 07/19/2018
ms.openlocfilehash: 15cc807db805e1be0349ea51119663e515c7e551
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874033"
---
# <a name="copy-the-ca-certificate-and-crl-to-the-virtual-directory"></a>CA の証明書と CRL を仮想ディレクトリにコピーします。

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

AD CS が正しく構成されていることを確認して、証明機関から証明書失効リストとエンタープライズ ルート CA 証明書を Web サーバー上の仮想ディレクトリにコピーするには、この手順を使用することができます。 次のコマンドを実行する前に、展開に適切なものをディレクトリとサーバーの名前を置き換えることを確認します。  
  
この手順を実行する**Domain Admins**します。  
  
#### <a name="to-copy-the-certificate-revocation-list-from-ca1-to-web1"></a>CA1 から WEB1 に証明書失効リストをコピーするには  
  
1.  CA1、管理者は、Windows PowerShell を実行し、次のコマンドで CRL を公開します。  
  
    - 「`certutil -crl`」と入力し、Enter キーを押します。  

    - 証明書の失効リストを Web サーバー上のファイル共有にコピーする入力`copy C:\Windows\system32\certsrv\certenroll\*.crl \\WEB1\pki`、し、ENTER キーを押します。  
  
2.  CDP および AIA 拡張機能の場所が正しく構成されていることを確認するには、次のように入力します。 `pkiview.msc`、し、ENTER キーを押します。 Pkiview、エンタープライズ PKI MMC が開きます。  
  
3.  左側のウィンドウで、CA 名をクリックします。<p>たとえば、CA の名前が corp-CA CA1 である場合は、クリックして**corp-CA CA1**します。 

4. 結果ウィンドウの [状態] 列で、次の値が表示されることを確認します**OK**:

    - **CA 証明書**
    - **AIA の場所 1**
    - **CDP の場所 1**   
  
  
> [!TIP]  
> 場合**状態**任意の項目が **[ok]** 次の操作を行います。  
> -   証明書と証明書失効リスト ファイルを共有にコピーが正常にことを確認する Web サーバー上の共有を開きます。 共有が正常にコピーされていない場合は、正しいファイルのソースとコピー コマンドを変更し、先を共有してコマンドをもう一度実行します。  
> -   CA の 拡張 タブで、CDP と AIA の正しい場所を入力したことを確認します。余分な空白またはその他の文字で指定した場所を確認します。  
> -   Web サーバー上の正しい場所に CRL と CA 証明書をコピーした場所に CA の CDP および AIA の場所の指定した場所と一致することを確認します。  
> -   CA の証明書と CRL が格納されている仮想フォルダーのアクセス許可が正しく構成されていることを確認します。  
  


