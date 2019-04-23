---
title: Active Directory フェデレーション サービスと証明書キーの仕様のプロパティ情報
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: a5307da5-02ff-4c31-80f0-47cb17a87272
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: db58fcce054f34c4b0a3f6725456badae9fd0468
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879313"
---
# <a name="ad-fs-and-certificate-keyspec-property-information"></a>AD FS と証明書 KeySpec プロパティ情報
キーの仕様 ("KeySpec") は、証明書とキーに関連付けられているプロパティです。 これは、署名、暗号化、またはその両方の証明書に関連付けられている秘密キーを使用できるかどうかを指定します。   

KeySpec 値が正しくない AD FS と Web アプリケーション プロキシのエラーの原因など。


- AD FS イベントのないログに記録 (ただし、36888 と 36874 SChannel イベントが記録される可能性があります) を AD FS または Web アプリケーション プロキシは、SSL や TLS 接続を確立するために失敗
- AD FS または WAP でのログインの失敗は、ページに表示されるエラー メッセージなしでベースの認証ページを形成します。

イベント ログでは、次が表示されます。

    Log Name:      AD FS Tracing/Debug
    Source:        AD FS Tracing
    Date:          2/12/2015 9:03:08 AM
    Event ID:      67
    Task Category: None
    Level:         Error
    Keywords:      ADFSProtocol
    User:          S-1-5-21-3723329422-3858836549-556620232-1580884
    Computer:      ADFS1.contoso.com
    Description:
    Ignore corrupted SSO cookie.

## <a name="what-causes-the-problem"></a>問題を原因します。
KeySpec プロパティでは、Microsoft CryptoAPI (CAPI) から Microsoft レガシ暗号化ストレージ プロバイダー (CSP)、種策さ生成されたキーの使用方法を識別します。

KeySpec @property **1**、または**AT_KEYEXCHANGE**、署名と暗号化に使用できます。  値**2**、または**AT_SIGNATURE**、署名にのみ使用します。

最も一般的な構成の KeySpec ミスが使用して値が 2 のトークン署名証明書以外の証明書。  

証明書のキーを持つは、Cryptography Next Generation (CNG) プロバイダーを使用して生成された場合、キーの仕様の概念がないと KeySpec 値が 0 になります常にします。

以下の有効な KeySpec 値を確認する方法を参照してください。 

### <a name="example"></a>例
従来の CSP の例では、Microsoft Enhanced Cryptographic Provider です。 

Microsoft RSA CSP キー blob 形式か、アルゴリズム識別子を含む**CALG_RSA_KEYX**または**CALG_RSA_SIGN**をそれぞれのいずれかのサービス要求に * * AT_KEYEXCHANGE * * または**する at _署名**キー。
  
RSA キー アルゴリズムの識別子がよう KeySpec 値にマップします。

| プロバイダーがサポートされているアルゴリズム| CAPI 呼び出しの値をキーの仕様 |
| --- | --- |
|CALG_RSA_KEYX:RSA キーの署名と暗号化解除に使用できます。| AT_KEYEXCHANGE (または KeySpec = 1)|
CALG_RSA_SIGN :RSA 署名キーのみ |AT_SIGNATURE (または KeySpec = 2)|

## <a name="keyspec-values-and-associated-meanings"></a>KeySpec 値と関連付けられている意味
次に、さまざまな KeySpec 値の意味を示します。

|Keyspec 値|意味|推奨される AD FS の使用|
| --- | --- | --- |
|0|証明書が CNG 証明書です。|SSL 証明書のみ|
|1|レガシ CAPI (非 CNG) 証明書の署名と暗号化解除キーを使用できます。|    トークン署名、トークンの復号化、サービス通信証明書を SSL|
|2|レガシ CAPI (非 CNG) 証明書の署名にのみ、キーを使用できます。|推奨されません。|

## <a name="how-to-check-the-keyspec-value-for-your-certificates--keys"></a>証明書の KeySpec 値を確認する方法とキー
使用できる証明書の値を表示する、 **certutil**コマンド ライン ツール。  

例を次に: **certutil – v – ストア my**します。  これが証明書情報を画面にダンプされます。

![Keyspec cert](media/AD-FS-and-KeySpec-Property/keyspec1.png)

次の 2 つの CERT_KEY_PROV_INFO_PROP_ID ファイルの場所。


1. **プロバイダーの種類:** これはレガシ暗号化ストレージ プロバイダー (CSP) を使用する証明書またはキー記憶域プロバイダー ベースの新しい証明書 Next Generation (CNG) Api のかどうかを示します。  0 以外の値では、従来のプロバイダーを示します。
2.  **KeySpec:** 以下は、AD FS の証明書の有効な KeySpec 値です。

    レガシ CSP プロバイダー (ProviderType を 0 に等しくない):
    
    |AD FS 証明書の目的|有効な KeySpec 値|
    | --- | --- |
    |サービスの通信|1|
    |トークン暗号化解除|1|
    |トークンの署名|1 と 2|
    |SSL (SSL)|1|

    CNG プロバイダー (プロバイダーの種類 = 0)。
    |AD FS 証明書の目的|有効な KeySpec 値|
    | --- | --- |   
    |SSL (SSL)|0|

## <a name="how-to-change-the-keyspec-for-your-certificate-to-a-supported-value"></a>証明書の keyspec をサポートされている値に変更する方法
KeySpec 値を変更する場合は再生成または再証明機関によって発行される証明書は必要ありません。  次の手順を使用して、証明書ストアに、完全な証明書と秘密キーを PFX ファイルからを再インポートすることは、KeySpec を変更できます。


1. 最初に、確認しができるように構成し直す必要に応じて再インポートした後は、既存の証明書の秘密キーのアクセス許可を記録します。
2. PFX ファイルに秘密キーを含む証明書をエクスポートします。
3. AD FS と WAP サーバーごとに、次の手順を実行します。
    1. 証明書を削除 (AD FS から/WAP サーバー)
    2. 管理者特権の PowerShell コマンド プロンプトを開き、次のコマンドレットの構文を使用して、(これは、すべての AD FS 証明書の目的は) AT_KEYEXCHANGE 値を指定する各 AD FS と WAP サーバー上の PFX ファイルをインポートします。
        1. C:\>certutil – importpfx certfile.pfx AT_KEYEXCHANGE
        2. PFX のパスワードを入力します。
    3. 上記が完了するとは、次を操作します。
        1. 秘密キーのアクセス許可を確認してください。
        2. adfs または wap サービスを再起動します。





