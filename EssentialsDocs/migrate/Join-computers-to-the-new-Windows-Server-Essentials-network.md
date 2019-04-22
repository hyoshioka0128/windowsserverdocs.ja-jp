---
title: 新しい Windows Server Essentials network1 にコンピューターを参加させる
description: Windows Server Essentials を使用する方法について説明します
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822643"
---
# <a name="join-computers-to-the-new-windows-server-essentials-network1"></a>新しい Windows Server Essentials network1 にコンピューターを参加させる

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

##  <a name="BKMK_JoinComputers"></a>   
 移行プロセスの次の手順では、クライアント コンピューターを新しい Windows Server Essentials ネットワークに参加させるし、グループ ポリシー設定を更新します。  
  
### <a name="domain-joined-client-computers"></a>ドメインに参加しているクライアント コンピューター  
 参照**http://***先 servername***/connect**と場合、新しいコンピューターと同じように、Windows Server コネクタ ソフトウェアをインストールします。 インストール プロセスは、クライアント コンピューターがドメインに参加する場合でも参加しない場合でも同じです。  
  
> [!NOTE]
>  Windows Server コネクタ ソフトウェアは、Windows XP または Windows Vista を実行しているコンピューターはサポートしていません。 既にドメインに参加している Windows XP または Windows Vista を実行しているコンピューターがある場合は、この手順を省略できます。  
  
### <a name="non-domain-joined-client-computers"></a>ドメインに参加していないクライアント コンピューター  
 参照**http://***先 servername***/connect**と場合、新しいコンピューターと同じように、Windows Server コネクタ ソフトウェアをインストールします。 インストール プロセスは、クライアント コンピューターがドメインに参加しているかどうかにかかわらず同じです。  
  
> [!NOTE]
>  Windows Server コネクタ ソフトウェアは、Windows XP または Windows Vista を実行しているコンピューターはサポートしていません。 既にドメインに参加している Windows XP または Windows Vista を実行しているコンピューターがある場合は、この手順を省略できます。  
  
### <a name="ensure-that-group-policy-has-updated"></a>グループ ポリシーが更新されたことを確認する  
  
> [!NOTE]
>  これはオプションの手順であり、移行元サーバーがフォルダー リダイレクトなどのカスタム グループ ポリシーの設定で構成されていた場合にのみ必要です。  
  
 移行元サーバーと移行先サーバーがまだオンラインの間に、グループ ポリシーの設定が移行先サーバーからクライアント コンピューターにレプリケートされたことを確認する必要があります。 各クライアント コンピューターで次の手順を実行します。  
  
1.  コマンド プロンプト ウィンドウを開きます。  
  
2.  コマンド プロンプトで「 **GPRESULT /R**」と入力し、Enter キーを押します。  
  
3.  グループ ポリシーの適用 セクションの結果の出力を確認してください: ことなど、移行先サーバーの一覧を確認して**DestinationSrv.Domain.local**します。 次に、例を示します。  
  
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
  
4.  移行先サーバーが一覧に表示されない場合、コマンド プロンプトで「**gpupdate /force**」と入力して Enter キーを押し、グループ ポリシーの設定を更新します。 その後、前の手順を再度実行します。  
  
5.  移行先サーバーがまだ表示されない場合は、グループ ポリシーの設定またはこの特定のクライアント コンピューターへのポリシーの適用にエラーがある可能性があります。 移行先サーバーが表示されない場合は、次の手順を実行してください。  
  
    1.  **[スタート]** ボタンをクリックし、**[ファイル名を指定して実行]** をクリックし、「 **rsop.msc** 」 (ポリシーの結果セット) と入力して、Enter キーを押します。  
  
    2.  ノードに表示されるまでに X 印が付いたツリーを展開します。  
  
    3.  ノードを右クリックし、**[エラーの表示]** をクリックして、一覧のコンピューターでグループ ポリシーの設定が失敗する理由についての情報を確認します。
