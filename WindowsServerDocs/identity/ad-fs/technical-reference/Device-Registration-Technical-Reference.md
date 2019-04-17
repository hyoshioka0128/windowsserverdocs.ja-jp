---
ms.assetid: 69ec592a-5499-4249-8ba0-afa356a8ff75
title: "デバイス登録のテクニカル リファレンス"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fac6437e9b6c3893064769a8279c2cf96cbc47d6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
>適用対象: Windows Server 2016、Windows Server 2012 R2

# <a name="device-registration-technical-reference"></a>デバイス登録のテクニカル リファレンス
デバイス登録サービス \(DRS\) とは、Windows Server 2012 R2 で Active Directory フェデレーション サービス役割に含まれている新しい Windows サービスです。  DRS をインストールして、すべての AD FS ファームにフェデレーション サーバーに構成されている必要があります。  DRS の展開方法の詳細については、次を参照してください。[デバイス登録サービスによるフェデレーション サーバーを構成する](https://technet.microsoft.com/library/dn486831.aspx)します。  
  
## <a name="active-directory-objects-created-when-a-device-is-registered"></a>Active Directory オブジェクトをデバイスの登録時に作成  
デバイス登録サービスの一部として、次の Active Directory オブジェクトが作成されます。  
  
### <a name="device-registration-configuration"></a>デバイス登録の構成  
デバイス登録構成は、Active Directory フォレストの構成名前付けコンテキストに格納されます。 \ (たとえば、**CN\ = Device Registration Configuration, CN\ = Services, < コンテキスト依存 naming\ configuration \ >**\)。 このオブジェクトは、デバイス登録のため、Active Directory フォレストのイニシャルが付けられたときに作成されます。  
  
デバイス登録構成には、次の要素が含まれています。  
  
-   **発行者キー**  
  
    登録済みデバイスに関連付けられている、公開キーと秘密キー X.509 証明書を発行するために使用します。  秘密キーは DKM で保護します。  
  
-   **デバイス登録サービスの構成**  
  
    デバイス登録サービスに関連するポリシーです。  
  
### <a name="registered-devices-container"></a>登録済みデバイス コンテナー  
デバイス オブジェクト コンテナーは、Active Directory フォレスト内のドメインの下にあるいずれかでが作成されます。  このオブジェクト コンテナーは、すべての Active Directory フォレストにデバイス オブジェクトが含まれます。  
  
既定では、AD FS と同じドメイン内のコンテナーが作成されます。  \ (たとえば、**CN\ = RegisteredDevices、DC\ = < コンテキスト依存 naming\ default\ >**\)。このオブジェクトは、デバイス登録のため、Active Directory フォレストのイニシャルが付けられたときに作成されます。  
  
### <a name="registered-devices"></a>登録済みデバイス  
デバイス オブジェクトは、Active Directory で新しい、光の重み付けオブジェクトです。  間の関係を表すために使用されます。ユーザー、デバイス、および会社。  デバイス オブジェクトでは、AD FS によって署名された証明書を使用して、物理デバイスを Active Directory 内の論理デバイス オブジェクトを関連付けます。  
  
登録済みデバイスには、次の要素が含まれています。  
  
-   **表示名**  
  
    デバイスのフレンドリ名。  Windows デバイスでは、これは、コンピューターのホスト名です。  
  
-   **デバイス Id**  
  
    デバイスの登録サーバーによって生成される GUID です。  
  
-   **証明書の拇印**  
  
    登録されたデバイスで使用される X.509 証明書の証明書の拇印。  
  
-   **OS の種類**  
  
    デバイスのオペレーティング システムの種類。  
  
-   **OS のバージョン**  
  
    デバイス上のオペレーティング システムのバージョン。  
  
-   **有効になっています。**  
  
    Active Directory にデバイスが有効になっているかどうかを示すブール値。  サービスへのアクセスには、有効になっているデバイスのみが許可されています。  
  
-   **おおよその最終使用時間**  
  
    リソースにアクセスするデバイスが使用されたおおよその時間。  レプリケーション トラフィックを制限するには、これに 14 日に 1 回は更新のみされます。  
  
-   **登録済み所有者**  
  
    このデバイスを職場に参加しているユーザーのセキュリティ ID \(SID\) します。  
  
## <a name="ad-fsdrs-server-ssl-certificate-revocation-checking"></a>AD FS\/DRS サーバーの SSL 証明書失効の確認  
ワークプ レース ジョイン クライアントでは、AD FS サーバーの SSL 証明書の有効性を確認します。  AD FS サーバーの SSL 証明書には、証明書失効リスト \(CRL\) エンドポイントが含まれている場合、クライアントは、証明書の検証を指定されたエンドポイントに到達できる必要があります。  
  
テスト環境とテスト証明書機関を使用しているかどうか、CA によって発行されたサーバー証明書の CRL のエンドポイントを含めないようにすることもできますし、サーバーに SSL 証明書を発行する \(CA\) します。  これを行うと、CRL チェックをバイパスするワークプ レース ジョイン クライアントが許可されます。  
  
> [!CAUTION]  
> 運用システムに推奨されることはありません。  
  

