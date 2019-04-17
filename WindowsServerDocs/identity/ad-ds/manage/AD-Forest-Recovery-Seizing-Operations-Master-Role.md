---
title: "AD フォレストの回復 - 操作マスターの役割の強制"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 7e6bb370-f840-4416-b5e2-86b0ba715f4f
ms.technology: identity-adfs
ms.openlocfilehash: 7ca6e3746586feeb3573b1ad6ba02831d1f5addd
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---seizing-an-operations-master-role"></a>AD フォレストの回復 - 操作マスターの役割の強制  

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:

 操作マスターの役割 (フレキシブル シングル マスター操作 (FSMO) の役割とも呼ばれます) を強制するのには、次の手順を使用します。 Ntdsutil.exe、すべての Dc に自動的にインストールされているコマンド ライン ツールを使用することができます。  
  
## <a name="to-seize-an-operations-master-role"></a>操作マスターの役割を強制するのには  
  
1.  コマンド プロンプトで、次のコマンドを入力し、Enter キーを押します。  
  
    ```  
    ntdsutil  
    ```  
  
2.  **Ntdsutil:**求めるし、次のコマンドを入力し、Enter キーを押します。  
  
    ```  
    roles  
    ```  
  
3.  **FSMO メンテナンス:**求めるし、次のコマンドを入力し、Enter キーを押します。  
  
    ```  
    connections  
    ```  
  
4.  **サーバー接続:**求めるし、次のコマンドを入力し、Enter キーを押します。  
  
    ```  
    Connect to server ServerFQDN  
    ```  
  
     ここで*ServerFQDN*は例をこのドメイン コントローラーの完全修飾ドメイン名 (FQDN): **nycdc01.example.com サーバーへの接続**します。  
  
     場合*ServerFQDN*成功しない、DC の NetBIOS 名を使用します。  
  
5.  **サーバー接続:**求めるし、次のコマンドを入力し、Enter キーを押します。  
  
    ```  
    quit  
    ```  
  
6.  によってを強制する役割に、**FSMO メンテナンス:**プロンプトし、次の表で説明するよう、適切なコマンドを入力し、Enter キーを押します。  
  
    |ロール|資格情報|コマンド|  
    |----------|-----------------|-------------|  
    |ドメイン名前付けマスタ|Enterprise Admins|**名前付けマスタを強制します。**|  
    |スキーマ マスタ|Schema Admins|**スキーマ マスターを強制します。**|  
    |インフラストラクチャ マスター**注:**後、インフラストラクチャ マスターの役割を強制移動することがありますエラーが発生した後で Adprep を実行する必要がある場合 /Rodcprep します。 詳細については、「」を参照情報の記事[949257](https://support.microsoft.com/kb/949257)します。|Domain Admins|**インフラストラクチャ マスターを強制します。**|  
    |PDC エミュレータ マスタ|Domain Admins|**Pdc を強制します。**|  
    |RID マスター|Domain Admins|**Rid マスターを強制します。**|  
  
     要求を確認したら、Active Directory または AD DS 役割を転送する試行します。 転送が失敗した場合、いくつかのエラー情報が表示され、発作についての Active Directory または AD DS を実行します。 強制移動が完了したら、ロールと各役割を持っているサーバーのライトウェイト ディレクトリ アクセス プロトコル (LDAP) 名の一覧が表示されます。 実行することも**Netdom Query FSMO**、管理者特権でコマンド プロンプトを現在の役割所有者を確認します。  
  
    > [!NOTE]
    >  このコンピューターが、障害発生前に、の RID マスタ RID マスターの役割を強制移動しようとする場合は、コンピューターは、この役割を受け入れる前に、レプリケーション パートナーと同期しようとします。 ただし、この手順が実行されるため、コンピューターが分離されている場合、これは成功しませんをパートナーとの同期に。 そのため、このコンピューターをパートナーと同期することはできませんに関係なく操作を続行するかどうかを確認する] ダイアログ ボックスが表示されます。 をクリックして**はい**します。  
  
## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
