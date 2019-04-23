---
title: 操作マスターの役割を強制する場合の AD フォレストの回復
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 7e6bb370-f840-4416-b5e2-86b0ba715f4f
ms.technology: identity-adds
ms.openlocfilehash: 1994d49652ee9eb10f6afc73cf5b4630b4718e77
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858463"
---
# <a name="ad-forest-recovery---seizing-an-operations-master-role"></a>操作マスターの役割を強制する場合の AD フォレストの回復  

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

操作マスターの役割 (フレキシブル シングル マスター操作 (FSMO) ロールとも呼ばれます) を強制するのには、次の手順を使用します。 Ntdsutil.exe、すべての Dc に自動的にインストールされているコマンド ライン ツールを使用することができます。  
  
## <a name="to-seize-an-operations-master-role"></a>操作マスターの役割を強制するのには  
  
1. コマンド プロンプトで、次のコマンドを入力して Enter キーを押します。  

   ```  
   ntdsutil  
   ```  

2. **Ntdsutil:** と表示されたら、次のコマンドを入力し、ENTER キーを押します。  

   ```  
   roles  
   ```  

3. **FSMO メンテナンス:** と表示されたら、次のコマンドを入力し、ENTER キーを押します。  

   ```  
   connections  
   ```  

4. **サーバー接続:** と表示されたら、次のコマンドを入力し、ENTER キーを押します。  

   ```  
   Connect to server ServerFQDN  
   ```  

   場所*ServerFQDN*は、この DC の完全修飾ドメイン名 (FQDN) をたとえば: **nycdc01.example.com のサーバーに接続する**します。  

   場合*ServerFQDN*いない成功しますが、ドメイン コント ローラーの NetBIOS 名を使用しません。  

5. **サーバー接続:** と表示されたら、次のコマンドを入力し、ENTER キーを押します。  

   ```  
   quit  
   ```  

6. 強制移動すると、ロールに応じてで、 **FSMO メンテナンス:** と表示されたら、次の表に示すように、適切なコマンドを入力し、ENTER キーを押します。  
  
|ロール|資格情報|コマンド|  
|----------|-----------------|-------------|  
|ドメイン名前付けマスタ|Enterprise Admins|**名前付けマスタを強制します。**|  
|スキーマ マスター|Schema Admins|**スキーマ マスターを強制します。**|  
|インフラストラクチャ マスタ**に注意してください。** インフラストラクチャ マスターの役割を強制した後、Adprep/Rodcprep を実行する必要がある場合後でエラーを受信する可能性があります。 詳細については、サポート技術情報の記事を参照してください[949257](https://support.microsoft.com/kb/949257)します。|Domain Admins|**インフラストラクチャ マスターを強制します。**|  
|PDC エミュレーター マスター|Domain Admins|**Pdc を強制します。**|  
|RID マスター|Domain Admins|**Rid マスターを強制します。**|  

要求を確認したら、Active Directory または AD DS 役割を転送する試みます。 転送が失敗したときに、いくつかのエラー情報が表示されたら、Active Directory または AD DS が強制を実行します。 強制が完了した後、ロールと各ロールを現在保持しているサーバーのライトウェイト ディレクトリ アクセス プロトコル (LDAP) の名前の一覧が表示されます。 実行することも**Netdom Query FSMO**を現在の役割所有者を確認します。 管理者特権のコマンド プロンプトでします。  
  
> [!NOTE]
> このコンピューターは、障害発生前に、RID マスターでした。 RID マスターの役割を強制しようとした場合は、コンピューターは、このロールを受け入れる前にレプリケーション パートナーと同期しようとします。 ただし、コンピューターが分離されたときにこの手順を実行しているために、パートナーとの同期に成功にとはしません。 そのため、パートナーと同期することはできません、このコンピューターに関係なく操作を続行するかどうかを確認するダイアログ ボックスが表示されます。 **[はい]** をクリックします。  
  
## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
