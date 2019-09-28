---
ms.assetid: 4b71b212-7e5b-4fad-81ee-75b3d1f27869
title: AD FS での証明書認証のための代替ホスト名バインドのサポート
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: be522f4dd990a920e910950c1bf2564d795bf9fa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358587"
---
# <a name="ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication"></a>AD FS での証明書認証のための代替ホスト名バインドのサポート

多くのネットワークでは、ローカルファイアウォールポリシーは、49443のような非標準ポート経由のトラフィックを許可しない可能性があります。 これは、Windows Server 2016 で AD FS 前に AD FS で証明書認証を実行しようとしたときに問題になりました。 これは、同じホストで、デバイス認証とユーザー証明書認証に対して異なるバインドを持つことができなかったためです。 既定のポート443はデバイス証明書の受信にバインドされており、同じチャネルで複数のバインドをサポートするように変更することはできません。 結果として、スマートカード認証が機能しなくなり、実際に何が起こったかがわかりません。  
  
Windows Server 2016 の AD FS を使用すると、これを実現できます。
  
Windows Server 2016 の AD FS では、これが変更されました。 2つのモードがサポートされるようになりました。最初のモードでは、異なるポート (443、49443) を持つ同じホスト (つまり adfs.contoso.com) が使用されます。 2番目のホスト (adfs.contoso.com と certauth.adfs.contoso.com) が同じポート (443) で使用されています。 これには、"certauth. < adfs-service-name >" を代替サブジェクト名としてサポートするための SSL 証明書が必要です。 これは、ファームの作成時または後で PowerShell を使用して行うことができます。  
  
## <a name="how-to-configure-alternate-host-name-binding-for-certificate-authentication"></a>証明書認証用の代替ホスト名バインドを構成する方法  
証明書認証用の代替ホスト名のバインドを追加する方法は2つあります。 1つ目は、Windows Server 2016 用の AD FS を持つ新しい AD FS ファームを設定する場合です。証明書にサブジェクト代替名 (SAN) が含まれている場合は、前述の2番目の方法を使用するように自動的にセットアップされます。 つまり、2つの異なるホスト (sts.contoso.com と certauth.sts.contoso.com が同じポートで自動的に設定されます。 証明書に SAN が含まれていない場合は、証明書のサブジェクトの別名が certauth. * をサポートしていないことを示す警告が表示されます。 以下のスクリーンショットを参照してください。 最初の例では、証明書に SAN があり、2番目の証明書にはなかった証明書が表示されています。  
  
![代替ホスト名のバインド](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_1.png)  
  
![代替ホスト名のバインド](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_2.png)  
  
同様に、Windows Server 2016 で AD FS が展開されたら、PowerShell コマンドレットを使用できます。AdfsAlternateTlsClientBinding。
  
```powershell
Set-AdfsAlternateTlsClientBinding -Member DC1.contoso.com -Thumbprint '<thumbprint of cert>'
```

メッセージが表示されたら、[はい] をクリックして確定します。  そうですね。

![代替ホスト名のバインド](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_3.png)

## <a name="additional-references"></a>その他の参照情報

* [Windows Server 2016 での AD FS と WAP での SSL 証明書の管理](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)
