---
title: 手順 4. DirectAccess OTP とを確認します。
description: このトピックでは、ガイド Windows Server 2016 での OTP 認証を使用したリモート アクセスの展開の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed49a0a3-1c45-42e5-8f13-cad20c1c1d68
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1ce9fe1327cfad6409d66981e6baadc133fb92a6
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282407"
---
# <a name="step-4-verify-directaccess-with-otp"></a>手順 4. DirectAccess OTP とを確認します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、OTP 展開で、DirectAccess が正しく構成されていることを確認する方法について説明します。
  
### <a name="to-verify-otp-health-on-the-remote-access-server"></a>リモート アクセス サーバーで OTP の正常性を確認するには

1. 開いているリモート アクセス サーバーで、**リモート アクセス管理**コンソール。  

2. **のリモート アクセス サーバー** OTP をサポートするように構成されたリモート アクセス サーバーをクリックします。  

3. クリックして**操作の状況**します。  

4. OTP の状態が緑色のアイコンが表示され、作業は、ことを確認します。  
  
    > [!NOTE]  
    > 正常性ステータスの更新間隔は HKLM\SYSTEM\CCS\Services\Ramgmtsvc\parameters\HealthRefreshTimeout のレジストリ キーから値の合計の最大値になります、**サーバーの利用状況の時間間隔**で設定されている、リモート アクセスの構成。  
  
### <a name="to-verify-access-to-internal-resources-using-otp-authentication"></a>OTP 認証を使用して、内部リソースへのアクセスを確認するには  
  
1.  DirectAccess クライアント コンピューターを企業ネットワークに接続し、実行**gpupdate/force**グループ ポリシーを取得するコマンド プロンプトからです。  
  
2.  クライアント コンピューターを企業ネットワークから切断、外部のネットワークに接続し、内部リソースにアクセスしようとしてください。 内部リソースへのアクセスはありません。  
  
3.  ソフトウェア トークンの場合は、仕入先の手順を使用して、OTP クライアント トークンにアクセスし、現在のトークン コードに注意してください。 ハードウェア トークンを使用する場合、認証のベンダーの指示に従います。  
  
4.  通知領域の **[ネットワーク接続]** アイコンをクリックして、DA メディア マネージャーにアクセスします。  
  
5.  をクリックして、 **DirectAccess 接続**、 をクリック**続行**します。  
  
6.  、前述のトークン コードを入力し、クリックして**OK**します。 認証が完了するまで待ちます。 DirectAccess の職場の接続状態になります**接続**します。  
  
7.  内部リソースにアクセスしようとしてください。 すべての企業リソースにアクセスできます。  
  


