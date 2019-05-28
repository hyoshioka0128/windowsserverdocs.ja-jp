---
ms.assetid: 4b71b212-7e5b-4fad-81ee-75b3d1f27869
title: AD FS での証明書認証のための代替ホスト名バインドのサポート
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3e3d1e5d86afbef2fdabd211047f513d31a40300
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190322"
---
# <a name="ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication"></a>AD FS での証明書認証のための代替ホスト名バインドのサポート

多くのネットワークのローカル ファイアウォール ポリシーは、非標準ポート 49443 などを通じてトラフィックを許可可能性があります。 これは、Windows Server 2016 での AD FS の前に AD FS で証明書認証を実行しようとするときで、問題になりました。 同じホスト上のデバイスの認証とユーザー証明書認証ごとに異なるバインドができなかったためにです。 既定のポート 443 では、デバイスの証明書を受信はバインドされ、同じチャネルで複数のバインドをサポートするために変更することはできません。 結果は、スマート カード認証が機能しないと、ユーザーが実際に変更点を示す値が存在しないためにの変更点の認識していなかったことでした。  
  
Windows Server 2016 での AD FS とこれを実現することができます。
  
Windows Server 2016 での AD FS でこれが変更されました。 2 つのモードでサポートされています、最初は、別のポート (443、49443) で同じホスト (adfs.contoso.com など) を使用します。 2 つ目は、同じポート (443) を持つ別のホスト (adfs.contoso.com および certauth.adfs.contoso.com) を使用しました。 これには、「certauth. < adfs サービス名 >」代替サブジェクト名としてをサポートする SSL 証明書が必要です。 これは、または PowerShell を使用して後でファームの作成時に実行できます。  
  
## <a name="how-to-configure-alternate-host-name-binding-for-certificate-authentication"></a>証明書の認証の代替ホスト名バインドを構成する方法  
証明書の認証の代替ホスト名バインドを追加することが 2 つの方法はあります。 最初は、上記で説明した 2 つ目のメソッドを使用してセットアップが自動的に行われます、証明書にサブジェクト代替名 (SAN) が含まれる場合は、Windows Server 2016 での AD FS と新しい AD FS ファームを設定するときです。 (Sts.contoso.com と同じポートを持つ certauth.sts.contoso.com 2 つの異なるホストを自動的にセットアップには。 証明書に SAN が含まれていないと、証明書のサブジェクト代替名が certauth.* をサポートしていないことを示す警告が表示されます。 次のスクリーン ショットを参照してください。 1 つ目は、証明書が、SAN、2 つ目ではありませんでしたが、証明書を示しています。 インストールを示しています。  
  
![代替ホスト名バインド](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_1.png)  
  
![代替ホスト名バインド](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_2.png)  
  
同様に、Windows Server 2016 での AD FS をデプロイした後は、PowerShell コマンドレットを使用することができます。セット AdfsAlternateTlsClientBinding します。
  
```powershell
Set-AdfsAlternateTlsClientBinding -Member DC1.contoso.com -Thumbprint '<thumbprint of cert>'
```

メッセージが表示されたら、確認するには、[はい] をクリックします。  そのことにあります。

![代替ホスト名バインド](media/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication/ADFS_CA_3.png)

## <a name="additional-references"></a>その他の参照情報

* [AD FS と WAP で Windows Server 2016 で SSL 証明書の管理](../operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)
