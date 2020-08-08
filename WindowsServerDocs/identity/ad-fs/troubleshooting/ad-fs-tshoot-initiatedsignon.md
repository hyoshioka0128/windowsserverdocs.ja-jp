---
title: AD FS トラブルシューティング-Idp 開始サインオン
description: このドキュメントでは、AD FS サインオンページのトラブルシューティングを行う方法について説明します。
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.openlocfilehash: 4eb39b697b3dd31dc0a6e3581bdb33437b462197
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969709"
---
# <a name="ad-fs-troubleshooting---idp-initiated-sign-on"></a>AD FS トラブルシューティング-Idp 開始サインオン
[AD FS サインオン] ページを使用して、認証が動作しているかどうかをテストできます。  これを行うには、ページに移動してサインインします。  また、サインインページを使用して、すべての SAML 2.0 証明書利用者が一覧表示されていることを確認することもできます。

## <a name="enable-the-idp-initiated-sign-on-page"></a>Idp によって開始されるサインオンページを有効にする
既定では、Windows 2016 の AD FS では、[サインオン] ページが有効になっていません。  有効にするには、PowerShell コマンド Set-adfsproperties を使用します。  ページを有効にするには、次の手順に従います。

1.  Windows PowerShell を開く
2.  「」 `Get-AdfsProperties` と入力し、enter キーを押します。
3.  **Enableidpinitiatedsignonpage**が false false に設定されていることを確認します。 ![](media/ad-fs-tshoot-initiatedsignon/idp2.png)
4.  PowerShell で、次のように入力します。`Set-AdfsProperties -EnableIdpInitiatedSignonPage $true`
5.  確認メッセージが表示されないため、Set-adfsproperties をもう一度入力し、 **Enableidpinitatedsignonpage**が true に設定されていることを確認します。
![True](media/ad-fs-tshoot-initiatedsignon/idp4.png)

## <a name="test-authentication"></a>認証のテスト
Idp によって開始されるサインオンページで AD FS 認証をテストするには、次の手順に従います。

1.  Web ブラウザーを開き、Idp サインオンページに移動します。  例: https://sts.contoso.com/adfs/ls/idpinitiatedsignon.htm
2.  サインインするように求められます。  資格情報を入力します。
![サインオン](media/ad-fs-tshoot-initiatedsignon/idp5.png)
3.  成功した場合は、サインインする必要があります。


## <a name="test-authentication-using-a-seamless-logon-experience"></a>シームレスなログオンエクスペリエンスを使用して認証をテストする
AD FS サーバーの URL がインターネットオプションのローカルイントラネットゾーンに追加されていることを確認することで、シームレスなログオンエクスペリエンスをテストできます。  次の手順に従います。

1.  Windows 10 クライアントで、[スタート] をクリックし、「インターネットオプション」と入力して、[インターネットオプション] を選択します。
2.   [セキュリティ] タブをクリックし、[ローカルイントラネット] をクリックして、[サイト] ボタンをクリックします。
![連続](media/ad-fs-tshoot-initiatedsignon/idp8.png)
1.  [詳細設定] をクリックします。
2.  Url を入力し、[追加] をクリックします。  [閉じる] をクリックします。
![Url の追加](media/ad-fs-tshoot-initiatedsignon/idp9.png)
1.  [OK] をクリックします。  [OK] をクリックします。  これにより、インターネットオプションが閉じられます。
2.  Web ブラウザーを開き、Idp サインオンページに移動します。  例: https://sts.contoso.com/adfs/ls/idpinitiatedsignon.htm
3.  [サインイン] ボタンをクリックします。  自動的にサインインする必要があります。資格情報の入力は求められません。
![連続](media/ad-fs-tshoot-initiatedsignon/idp6.png)

## <a name="next-steps"></a>次の手順

- [AD FS のトラブルシューティング](ad-fs-tshoot-overview.md)
