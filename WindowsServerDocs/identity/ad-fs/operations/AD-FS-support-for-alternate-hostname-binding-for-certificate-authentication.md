---
ms.assetid: 4b71b212-7e5b-4fad-81ee-75b3d1f27869
title: "AD FS の証明書認証用の代替ホスト名バインドのサポートします。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 553ff059693c7b0c0e6f0364d82c1adbca661097
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication"></a>AD FS の証明書認証用の代替ホスト名バインドのサポートします。

>Windows Server 2016 の適用対象:

多くのネットワークでローカルのファイアウォール ポリシー可能性があります通過を許可しないトラフィック非標準ポート 49443 のようにします。 Windows Server 2016 での AD FS の前に AD FS と証明書の認証を実行しようとするとき、問題になりました。 これは、同じホスト上のデバイス認証とユーザー証明書の認証に別のバインドがない可能性があるためです。 既定のポート 443 では、デバイスの証明書を受け取るバインドされ、同じチャネルで複数のバインドをサポートするために変更することはできません。 結果は、スマート カード認証が機能しないと、ユーザーが実際に発生した内容を示す値がないために何が起こったかわからないことでした。  
  
Windows Server 2016 での AD FS でこれを実現することができます。
  
Windows Server 2016 での AD FS でこれが変更されました。 2 つのモードをサポートするようになりました最初は別のポート (443、49443) と同じホスト (つまり adfs.contoso.com) を使用します。 2 つ目は、同じポート (443) と共に別のホスト (adfs.contoso.com と certauth.adfs.contoso.com) を使用します。 これにより、"certauth"です。 < ad fs サービス名 >、代わりのサブジェクト名としてサポートするために SSL 証明書が必要です。 これは、または PowerShell を使用して後でファームの作成時に実行できます。  
  
## <a name="how-to-configure-alternate-host-name-binding-for-certificate-authentication"></a>証明書の認証の代替ホスト名バインドを構成する方法  
次の 2 つの方法が証明書の認証の代替ホスト名バインドを追加することができます。 最初は、上記 2 つ目の方法を使用してセットアップが自動的に行われます、証明書にサブジェクトの別名 (SAN) が含まれる場合、Windows Server 2016 での AD FS と新しい AD FS ファームをセットアップするときにです。 次の 2 つの異なるホスト (sts.contoso.com と同じポートで certauth.sts.contoso.com を自動的にセットアップ、つまり。 証明書に SAN が含まれていない場合は、証明書のサブジェクトの別名が certauth.* をサポートしていないことを通知する警告が表示されます。 以下のスクリーン ショットを参照してください。 最初の 1 つは、ここで、証明書、SAN があり、2 つ目はない証明書を示しています、インストールを示しています。  
  
![代替ホスト名バインド](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_1.png)  
  
![代替ホスト名バインド](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_2.png)  
  
同様に、Windows Server 2016 での AD FS の展開後は、PowerShell コマンドレットを使用できます: セット AdfsAlternateTlsClientBinding します。
  
```powershell
Set-AdfsAlternateTlsClientBinding -Member DC1.contoso.com -Thumbprint '<thumbprint of cert>'
```

メッセージが表示されたら、ことを確認するには、[はい] をクリックします。  それをする必要があります。

![代替ホスト名バインド](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_3.png)

## <a name="additional-references"></a>その他の参照

* [AD FS と WAP Windows Server 2016 での SSL 証明書の管理](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)
