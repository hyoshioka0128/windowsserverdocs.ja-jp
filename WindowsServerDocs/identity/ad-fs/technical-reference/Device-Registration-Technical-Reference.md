---
ms.assetid: 69ec592a-5499-4249-8ba0-afa356a8ff75
title: デバイス登録のテクニカル リファレンス
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0956fc959a09a9d00a098203a83091553e917c62
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966774"
---
# <a name="device-registration-technical-reference"></a>デバイス登録のテクニカル リファレンス
デバイス登録サービス \( DRS \) は、windows Server 2012 R2 の Active Directory フェデレーションサービスロールに含まれる新しい windows サービスです。  DRS は、AD FS ファーム内のすべてのフェデレーション サーバーにインストールし、構成する必要があります。  DRS の展開の詳細については、「 [デバイス登録サービスを使用してフェデレーション サーバーを構成する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486831(v=ws.11))」を参照してください。  
  
## <a name="active-directory-objects-created-when-a-device-is-registered"></a>デバイスの登録時に作成される Active Directory オブジェクト  
次の Active Directory オブジェクトは、デバイス登録サービス の一部として作成されます。  
  
### <a name="device-registration-configuration"></a>デバイス登録構成  
デバイス登録構成は、Active Directory フォレストの構成名前付けコンテキストに格納されます \(たとえば、 **cn \= Device Registration CONFIGURATION、cn \= Services、<Configuration \- 名前付け \- コンテキスト>** \) です。 このオブジェクトは、Active Directory フォレストにデバイス登録用のイニシャルが付けられたときに作成されます。  
  
デバイス登録構成には、次の要素が含まれます。  
  
-   **発行者キー**  
  
    登録済みデバイスに関連付けられた X.509 証明書を発行するために使用される、公開キーと秘密キーです。  秘密キーは DKM で保護されます。  
  
-   **デバイス登録サービス構成**  
  
    デバイス登録サービスに関連するポリシーです。  
  
### <a name="registered-devices-container"></a>登録済みデバイス コンテナー  
デバイス オブジェクト コンテナーは、Active Directory フォレスト内のいずれかのドメイン下に作成されます。  このオブジェクト コンテナーには、Active Directory フォレストのすべてのデバイス オブジェクトが格納されます。  
  
既定では、コンテナーは AD FS と同じドメインに作成されます。  \(たとえば、 **CN \= REGISTEREDDEVICES、DC \=<既定の \- 名前付け \- コンテキスト>** \) です。このオブジェクトは、Active Directory フォレストがデバイス登録のために初期化されたときに作成されます。  
  
### <a name="registered-devices"></a>登録済みデバイス  
デバイス オブジェクトは、Active Directory 内の新しい軽量オブジェクトです。  ユーザー、デバイス、および会社の関係を表すために使用されます。  デバイス オブジェクトは、AD FS によって署名された証明書を使用して、物理デバイスを Active Directory 内の論理デバイス オブジェクトに関連付けます。  
  
登録済みデバイスには、次の要素が含まれます。  
  
-   **表示名**  
  
    デバイスのフレンドリ名です。  Windows デバイスの場合、これはコンピューターのホスト名です。  
  
-   **デバイス Id**  
  
    デバイス登録サーバーによって生成される GUID です。  
  
-   **証明書の拇印**  
  
    登録済みデバイスに使用される X.509 証明書の証明書拇印です。  
  
-   **OS の種類**  
  
    デバイスのオペレーティング システムの種類です。  
  
-   **OS バージョン**  
  
    デバイス上のオペレーティング システムのバージョン。  
  
-   **有効**  
  
    デバイスが Active Directory で有効になっているかどうかを示すブール値です。  有効になっているデバイスだけがサービスにアクセスできます。  
  
-   **おおよその最終使用時間**  
  
    リソースへのアクセスにデバイスが使用されたおおよその時間です。  レプリケーション トラフィックを制限するため、この値は 14 日に 1 回だけ更新されます。  
  
-   **登録済み所有者**  
  
    \( \) このデバイスをワークプレースに参加させたユーザーのセキュリティ id SID。  
  
## <a name="ad-fsdrs-server-ssl-certificate-revocation-checking"></a>\/DRS サーバーの SSL 証明書の失効確認の AD FS  
ワークプ レース ジョイン クライアントは、AD FS サーバーの SSL 証明書の有効性をチェックします。  AD FS サーバーの SSL 証明書に証明書失効リストの CRL エンドポイントが含まれている場合 \( \) 、クライアントは、証明書を検証するために指定されたエンドポイントに接続できる必要があります。  
  
テスト環境とテスト証明機関 CA を使用してサーバーの SSL 証明書を発行する場合は、 \( \) CA によって発行されたサーバー証明書に CRL エンドポイントを含めないように選択できます。  そうすると、ワークプ レース ジョイン クライアントが CRL のチェックをバイパスできるようになります。  
  
> [!CAUTION]  
> これを運用システムで行うことは、絶対にお勧めしません。  
  
