---
title: AD フォレストの回復-操作マスターの役割の強制
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 7e6bb370-f840-4416-b5e2-86b0ba715f4f
ms.technology: identity-adds
ms.openlocfilehash: 672dc119845acbe9cf38f82c793bd377d31db3b2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390276"
---
# <a name="ad-forest-recovery---seizing-an-operations-master-role"></a>AD フォレストの回復-操作マスターの役割の強制  

>適用先:Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

操作マスターの役割 (フレキシブルシングルマスター操作 (FSMO) の役割とも呼ばれます) を強制するには、次の手順に従います。 すべての Dc に自動的にインストールされるコマンドラインツールである Ntdsutil.exe を使用できます。  
  
## <a name="to-seize-an-operations-master-role"></a>操作マスタの役割を強制実行するには  
  
1. コマンド プロンプトで、次のコマンドを入力して Enter キーを押します。  

   ```  
   ntdsutil  
   ```  

2. **Ntdsutil:** プロンプトで、次のコマンドを入力し、enter キーを押します。  

   ```  
   roles  
   ```  

3. FSMO の**メンテナンス:** プロンプトで、次のコマンドを入力し、enter キーを押します。  

   ```  
   connections  
   ```  

4. **サーバー接続:** プロンプトで、次のコマンドを入力し、enter キーを押します。  

   ```  
   Connect to server ServerFQDN  
   ```  

   ここで、 *Serverfqdn*はこの DC の完全修飾ドメイン名 (FQDN) です。たとえば、 **server nycdc01.example.com に接続**します。  

   *Serverfqdn*が成功しない場合は、DC の NetBIOS 名を使用します。  

5. **サーバー接続:** プロンプトで、次のコマンドを入力し、enter キーを押します。  

   ```  
   quit  
   ```  

6. 強制移動するロールに応じて、**次の表**の説明に従って、適切なコマンドを入力し、enter キーを押します。  
  
|ロール|資格情報|コマンド|  
|----------|-----------------|-------------|  
|ドメイン名前付けマスタ|Enterprise Admins|**名前付けマスタの強制移動**|  
|スキーママスタ|Schema Admins|**スキーママスタの強制移動**|  
|インフラストラクチャマスタの**メモ:** インフラストラクチャマスターの役割を強制終了した後、Adprep/Rodcprep. を実行する必要がある場合は、後でエラーが発生することがあります。 詳細については、サポート技術情報の記事[949257](https://support.microsoft.com/kb/949257)を参照してください。|Domain Admins|**インフラストラクチャマスターの強制**|  
|PDC エミュレーターマスター|Domain Admins|**Pdc を強制する**|  
|RID マスター|Domain Admins|**マスターの強制移動**|  

要求を確認すると、Active Directory または AD DS によってロールの転送が試行されます。 転送が失敗すると、いくつかのエラー情報が表示され、Active Directory または AD DS が強制実行を続行します。 強制が完了すると、ロールの一覧と、各ロールを現在保持しているサーバーのライトウェイトディレクトリアクセスプロトコル (LDAP) 名が表示されます。 また、管理者特権でのコマンドプロンプトで**Netdom QUERY FSMO**を実行して、現在のロールの所有者を確認することもできます。  
  
> [!NOTE]
> エラーが発生する前にこのコンピュータが RID マスタではない場合、RID マスタの役割を強制移動しようとすると、コンピュータはこの役割を受け入れる前に、レプリケーションパートナーと同期しようとします。 ただし、この手順はコンピューターが分離されている場合に実行されるため、パートナーとの同期は成功しません。 このため、このコンピューターがパートナーと同期できないにもかかわらず、操作を続行するかどうかを確認するダイアログボックスが表示されます。 **[はい]** をクリックします。  
  
## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
