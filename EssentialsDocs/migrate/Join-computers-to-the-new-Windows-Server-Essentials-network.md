---
title: "新しい Windows Server Essentials network1 にコンピューターを参加させる"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d94de050-3300-4323-a5ea-c824cb9cecc9
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c6abc11ba2ce8a9f1d32c6a884db6332586de78b
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="join-computers-to-the-new-windows-server-essentials-network1"></a>新しい Windows Server Essentials network1 にコンピューターを参加させる

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

##  <a name="BKMK_JoinComputers"></a>   
 移行プロセスの次の手順では、クライアント コンピューターを新しい Windows Server Essentials ネットワークに参加し、グループ ポリシー設定を更新します。  
  
### <a name="domain-joined-client-computers"></a>ドメインに参加しているクライアント コンピューター  
 参照**http://***移行先サーバー名***/connect**して場合、新しいコンピューターと同じように、Windows Server コネクタ ソフトウェアをインストールします。 インストール プロセスは、ドメインに参加しているか、ドメインに参加しているクライアント コンピューターの同じです。  
  
> [!NOTE]
>  Windows Server コネクタ ソフトウェアは、Windows XP または Windows Vista を実行しているコンピューターをサポートしていません。 既にドメインに参加している Windows XP または Windows Vista を実行しているコンピューターがある場合は、この手順をスキップすることができます。  
  
### <a name="non-domain-joined-client-computers"></a>ドメインに参加していないクライアント コンピューター  
 参照**http://***移行先サーバー名***/connect**して場合、新しいコンピューターと同じように、Windows Server コネクタ ソフトウェアをインストールします。 インストール プロセスは、ドメインに参加または非ドメインに参加しているクライアント コンピューターに同じです。  
  
> [!NOTE]
>  Windows Server コネクタ ソフトウェアは、Windows XP または Windows Vista を実行しているコンピューターをサポートしていません。 既にドメインに参加している Windows XP または Windows Vista を実行しているコンピューターがある場合は、この手順をスキップすることができます。  
  
### <a name="ensure-that-group-policy-has-updated"></a>グループ ポリシーが更新されることを確認します。  
  
> [!NOTE]
>  これは、オプションの手順とのみが、移行元サーバーがフォルダー リダイレクトなどのカスタムのグループ ポリシー設定で構成されているかどうかに必要なです。  
  
 移行元サーバーと移行先サーバーがまだオンライン、中に行う必要がありますをグループ ポリシーの設定がクライアント コンピューターに移行先サーバーからレプリケートします。 各クライアント コンピューターで、次の手順を実行します。  
  
1.  コマンド プロンプト ウィンドウを開きます。  
  
2.  コマンド プロンプトで、次のように入力します。**GPRESULT/R**、し、Enter キーを押します。  
  
3.  結果の出力からグループ ポリシーの適用] セクションで確認: など、移行先サーバーが一覧表示することを確認および**DestinationSrv.Domain.local**します。 例えば：  
  
    ```  
    USER SETTINGS  
    --------------  
        CN=User,OU=Users,DC=DOMAIN,DC=Local  
        Last time Group Policy was applied: 1/24/2011 at 1:26:27 PM  
        Group Policy was applied from:      DestinationSrv.Domain.local  
        Group Policy slow link threshold:   500 kbps  
        Domain Name:                        Domain  
        Domain Type:                        Windows 2008  
  
    ```  
  
4.  移行先サーバーが表示されない場合、コマンド プロンプトで入力**gpupdate/force**、し、Enter キーを押して、グループ ポリシー設定を更新します。 前の手順をもう一度実行します。  
  
5.  移行先サーバーが表示されない場合または可能性があります、グループ ポリシー設定のエラーでこの特定のクライアント コンピューターに適用するエラー。 移行先サーバーが表示されない場合は、次の手順を実行します。  
  
    1.  をクリックして**開始**、] をクリックして**実行**、種類**rsop.msc** (ポリシーの結果セット)、し、Enter キーを押します。  
  
    2.  ノードに移動するまでに x 印が付いたツリーを展開します。  
  
    3.  ノードを右クリックし、をクリックして**表示エラー**理由についての情報は、グループ ポリシー設定が表示されているコンピューターで失敗しています。
