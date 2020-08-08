---
title: Active Directory フェデレーションサービス (AD FS) と証明書キー指定のプロパティ情報
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.assetid: a5307da5-02ff-4c31-80f0-47cb17a87272
ms.author: billmath
ms.openlocfilehash: a78f989230450bcf59f86add66bdcfe91fa23c77
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938120"
---
# <a name="ad-fs-and-certificate-keyspec-property-information"></a>AD FS と certificate KeySpec のプロパティ情報
キー指定 ("KeySpec") は、証明書とキーに関連付けられているプロパティです。 証明書に関連付けられた秘密キーを署名、暗号化、またはその両方に使用できるかどうかを指定します。

KeySpec 値が正しくないと、次のような AD FS と Web アプリケーションプロキシエラーが発生する可能性があります。


- AD FS または Web アプリケーションプロキシへの SSL/TLS 接続を確立できませんでした。 AD FS イベントは記録されません (ただし、SChannel 36888 および36874イベントはログに記録される可能性があります)。
- ページにエラーメッセージが表示されず、AD FS または WAP のフォームベースの認証ページでログインできませんでした。

イベントログに次のように表示される場合があります。

```
Log Name:   AD FS Tracing/Debug
Source: AD FS Tracing
Date:   2/12/2015 9:03:08 AM
Event ID:   67
Task Category: None
Level:  Error
Keywords:   ADFSProtocol
User:   S-1-5-21-3723329422-3858836549-556620232-1580884
Computer:   ADFS1.contoso.com
Description:
Ignore corrupted SSO cookie.
```

## <a name="what-causes-the-problem"></a>問題の原因
KeySpec プロパティは、microsoft CryptoAPI (CAPI) によって生成または取得されたキーを Microsoft レガシ暗号化ストレージプロバイダー (CSP) から使用できるようにする方法を指定します。

KeySpec 値**1**または**AT_KEYEXCHANGE**は、署名と暗号化に使用できます。  値**2**、または**AT_SIGNATURE**は、署名にのみ使用されます。

最も一般的な KeySpec mis 構成では、トークン署名証明書以外の証明書に対して値2を使用します。

Cryptography Next Generation (CNG) プロバイダーを使用してキーが生成された証明書の場合、キー指定の概念はなく、KeySpec 値は常に0になります。

次の「有効な KeySpec 値を確認する方法」を参照してください。

### <a name="example"></a>例
従来の CSP の例として、Microsoft Enhanced Cryptographic Provider があります。

Microsoft RSA CSP キー blob 形式には、 <strong>AT_KEYEXCHANGE * * または * * AT_SIGNATURE</strong>キーの要求を処理するために、それぞれ**CALG_RSA_KEYX**または**CALG_RSA_SIGN**のいずれかのアルゴリズム識別子が含まれています。

RSA キーアルゴリズム識別子は、次のように KeySpec 値にマップされます。

| プロバイダーでサポートされているアルゴリズム| CAPI 呼び出しのキー指定値 |
| --- | --- |
|CALG_RSA_KEYX: 署名と復号化に使用できる RSA キー| AT_KEYEXCHANGE (または KeySpec = 1)|
CALG_RSA_SIGN: RSA 署名のみのキー |AT_SIGNATURE (または KeySpec = 2)|

## <a name="keyspec-values-and-associated-meanings"></a>KeySpec 値と関連する意味
さまざまな KeySpec 値の意味を次に示します。

|Keyspec 値|と|推奨 AD FS 使用|
| --- | --- | --- |
|0|証明書が CNG 証明書である|SSL 証明書のみ|
|1|従来の CAPI (CNG) 以外の証明書の場合、キーを署名と復号化に使用できます。|    SSL、トークン署名、トークン暗号化解除、サービス通信証明書|
|2|従来の CAPI (CNG) 以外の証明書の場合、キーは署名にのみ使用できます。|推奨されません|

## <a name="how-to-check-the-keyspec-value-for-your-certificates--keys"></a>証明書/キーの KeySpec 値を確認する方法
証明書の値を表示するには、 **certutil**コマンドラインツールを使用します。

次に例を示します。 **certutil – v – store my**.  これにより、証明書の情報が画面にダンプされます。

![Keyspec cert](media/AD-FS-and-KeySpec-Property/keyspec1.png)

[CERT_KEY_PROV_INFO_PROP_ID] で、次の2つの項目を探します。


1. **Providertype:** 証明書で、新しい Certificate Next GENERATION (CNG) api に基づく従来の暗号化ストレージプロバイダー (CSP) またはキー記憶域プロバイダーを使用するかどうかを示します。  0以外の値は、レガシプロバイダーを示します。
2. **KeySpec:** AD FS 証明書の有効な KeySpec 値を次に示します。

   レガシ CSP プロバイダー (ProviderType が0に等しくない):

   |AD FS 証明書の目的|有効な KeySpec 値|
   | --- | --- |
   |サービス通信|1|
   |トークンの復号化|1|
   |トークンの署名|1 と 2|
   |SSL|1|

   CNG プロバイダー (ProviderType = 0):

   |AD FS 証明書の目的|有効な KeySpec 値|
   | --- | --- |
   |SSL|0|

## <a name="how-to-change-the-keyspec-for-your-certificate-to-a-supported-value"></a>証明書の keyspec をサポートされている値に変更する方法
KeySpec 値を変更しても、証明機関によって証明書が再生成または再発行される必要はありません。  KeySpec を変更するには、次の手順を使用して、完全な証明書と秘密キーを PFX ファイルから証明書ストアに再インポートします。


1. まず、既存の証明書の秘密キーのアクセス許可を確認して記録し、再インポート後に必要に応じて再構成できるようにします。
2. 秘密キーを含む証明書を PFX ファイルにエクスポートします。
3. AD FS と WAP サーバーごとに次の手順を実行します。
    1. (AD FS/WAP サーバーから) 証明書を削除します。
    2. 管理者特権の PowerShell コマンドプロンプトを開き、次のコマンドレット構文を使用して、各 AD FS および WAP サーバーで PFX ファイルをインポートします。このとき、AT_KEYEXCHANGE の値 (すべての AD FS 証明書の目的で機能します) を指定します。
        1. C: \> certutil – importpfx certfile .pfx AT_KEYEXCHANGE
        2. PFX パスワードを入力してください
    3. 上記の手順を完了したら、次の手順を実行します。
        1. 秘密キーのアクセス許可を確認する
        2. adfs または wap サービスを再起動する





