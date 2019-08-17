---
title: CA 証明書と CRL を仮想ディレクトリにコピーする
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: dougkim
ms.topic: article
ms.assetid: a1b5fa23-9cb1-4c32-916f-2d75f48b42c7
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.date: 07/19/2018
ms.openlocfilehash: 9dbe14bec1c39ab5b967276c4faf3e9fc5a9aae3
ms.sourcegitcommit: 0467b8e69de66e3184a42440dd55cccca584ba95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546537"
---
# <a name="copy-the-ca-certificate-and-crl-to-the-virtual-directory"></a>CA 証明書と CRL を仮想ディレクトリにコピーする

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

証明書失効リストとエンタープライズルート CA 証明書を証明機関から Web サーバー上の仮想ディレクトリにコピーし、AD CS が正しく構成されていることを確認するには、次の手順に従います。 以下のコマンドを実行する前に、ディレクトリとサーバーの名前を、実際の展開に適した名前に置き換えてください。  
  
この手順を実行するには、 **Domain Admins**のメンバーである必要があります。  
  
#### <a name="to-copy-the-certificate-revocation-list-from-ca1-to-web1"></a>証明書失効リストを CA1 から WEB1 にコピーするには  
  
1.  CA1 で、管理者として Windows PowerShell を実行し、次のコマンドを使用して CRL を公開します。  
  
    - 「`certutil -crl`」と入力し、Enter キーを押します。  

    - CA1 証明書を Web サーバー上のファイル共有にコピーするには`copy C:\Windows\system32\certsrv\certenroll\*.crt \\WEB1\pki`、「」と入力し、enter キーを押します。  
    
    - 証明書失効リストを Web サーバー上のファイル共有にコピーするには`copy C:\Windows\system32\certsrv\certenroll\*.crl \\WEB1\pki`、「」と入力し、enter キーを押します。  
  
2.  CDP と AIA の拡張機能の場所が正しく構成されて`pkiview.msc`いることを確認するには、「」と入力し、enter キーを押します。 Pkiview Enterprise PKI MMC が開きます。  
  
3.  左側のウィンドウで、CA 名をクリックします。<p>たとえば、CA の名前が CA1 の場合は、 **CA1**をクリックします。 

4. 結果ウィンドウの [状態] 列で、次の値に **[OK]** が表示されていることを確認します。

    - **CA 証明書**
    - **AIA の場所の #1**
    - **CDP の場所の #1**   
  
  
> [!TIP]  
> 項目の**状態**が **[OK]** になっていない場合は、次の手順を実行します。  
> -   Web サーバーで共有を開き、証明書と証明書失効リストファイルが正常に共有にコピーされたことを確認します。 共有に正常にコピーされなかった場合は、正しいファイルソースと共有先を使用してコピーコマンドを変更し、コマンドを再度実行します。  
> -   [CA 拡張] タブで、CDP と AIA の正しい場所を入力したことを確認します。指定した場所に余分なスペースやその他の文字がないことを確認します。  
> -   CRL と CA 証明書を Web サーバー上の正しい場所にコピーしたこと、および場所が CA 上の CDP と AIA の場所に指定した場所と一致していることを確認します。  
> -   CA 証明書と CRL が保存されている仮想フォルダーのアクセス許可が正しく構成されていることを確認します。  
  


