---
ms.assetid: 2a5d5271-6ac6-4c1b-b4ef-9b568932a55a
title: Active Directory ドメインのスキーマの更新
description: ドメイン コント ローラーを昇格させるときに、adprep/domainprep によって実行されるドメインのスキーマの更新
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 10/29/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 20598431b9c2376051247fd7ba14e33af00968cc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812323"
---
# <a name="domain-wide-schema-updates"></a>ドメインのスキーマの更新

>適用先:Windows Server

次の一連の理解し、Windows Server で adprep/domainprep が実行されるスキーマの更新の準備に役立つ変更を確認できます。

Windows Server 2012 以降では、Adprep コマンドを AD DS のインストール中に必要に応じて自動的に実行します。 AD DS のインストール前とは別に、実行することもできます。 詳細については、「 [Adprep.exe の実行](https://technet.microsoft.com/library/dd464018(v=ws.10).aspx)」を参照してください。

アクセス制御エントリ (ACE) の文字列を解釈する方法の詳細については、次を参照してください。 [ACE 文字列](https://msdn.microsoft.com/library/aa374928(VS.85).aspx)します。 セキュリティ ID (SID) の文字列を解釈する方法の詳細については、次を参照してください。 [SID 文字列](https://msdn.microsoft.com/library/aa379602(VS.85).aspx)します。

## <a name="windows-server-semi-annual-channel-domain-wide-updates"></a>Windows Server (半期チャネル):ドメイン全体の更新

によって実行される操作の実行後**domainprep** Windows Server 2016 (操作 89) 完了するで、**リビジョン**cn 属性 ActiveDirectoryUpdate、CN = DomainUpdates、CN = System, DC = =フォレスト ルート ドメインのオブジェクトに設定されている**16**します。

|操作の数と GUID|説明|アクセス許可|
|------------------------------|---------------|--------------|---------------|
|**操作 89**: {A0C238BA-9E30-4EE6-80A6-43F731E9A5CD}|エンタープライズのキーの管理者にフル コントロールを許可する ACE を削除し、msdsKeyCredentialLink 属性だけ経由で企業キー管理者のフル コントロールを許可するように ACE を追加します。|(A; の削除します。CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;Enterprise Key Admins) <br /> <br />(OA; の追加します。CI;RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063; です。Enterprise Key Admins)|

## <a name="windows-server-2016-domain-wide-updates"></a>Windows Server 2016 の場合:ドメイン全体の更新

によって実行される操作の実行後**domainprep** Windows Server 2016 (operations 82 88) 完了するで、**リビジョン**cn 属性 ActiveDirectoryUpdate、CN = DomainUpdates、CN を = = システム、DC = オブジェクトに設定されている**15**します。

|操作の数と GUID|説明|属性|アクセス許可|
|------------------------------|---------------|--------------|---------------|
|**操作 82**: {83C53DA7-427E-47A4-A07A-A324598B88F7}|CN を作成するドメインのルートにあるキー コンテナーを =|-objectClass: コンテナー<br />説明。キー資格情報オブジェクトの既定のコンテナー<br />-ShowInAdvancedViewOnly:TRUE|(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;EA)<br />(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;DA)<br />(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)<br />(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;DD)<br />(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;ED)|
|**操作 83**: {C81FC9CC-0130-4FD1-B272-634D74818133}|フル コントロールの追加の許可 ace を CN ="domain\Key Admins"のキー コンテナーと"rootdomain\Enterprise Key Admins"。|なし|(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;キーの管理者)<br />(A;CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;Enterprise Key Admins)|
|**操作 84**: {E5F9E791-D96D-4FC9-93C9-D53E1DC439BA}|CN を指す otherWellKnownObjects 属性を変更するキー コンテナーを = です。|-otherWellKnownObjects:B:32:683A24E2E8164BD3AF86AC3C2CF3F981:CN=Keys,%ws|なし|
|**操作 85**: {e6d5fd00-385d-4e65-b02d-9da3493ed850}|ドメイン NC"domain\Key 管理者"を許可するように変更し、"rootdomain\Enterprise Key Admins"msds KeyCredentialLink 属性を変更します。 |なし|(OA;CI;RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063; です。キーの管理者)<br />(OA;CI;RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063; です。エンタープライズ Key Admins の非ルート ドメインが、ルート ドメインで解決できない-527 SID を持つ偽のドメインの相対 ACE が発生しました)|
|**操作 86**: {3a6b3fbf-3168-4312-a10d-dd5b3393952d}|DS-検証-書き込み-コンピューターの自動車の所有者と self の許可|なし|(OA;CIIO;SW;9b026da6-0d3c-465c-8bee-5199d7165cba;bf967a86-0de6-11d0-a285-00aa003049e2;PS)<br />(OA;CIIO;SW;9b026da6-0d3c-465c-8bee-5199d7165cba;bf967a86-0de6-11d0-a285-00aa003049e2;CO)|
|**操作 87**: {7F950403-0AB3-47F9-9730-5D7B0269F9BD}|正しくないドメインの相対 Enterprise Key Admins グループにフル コントロールを許可する ACE を削除し、エンタープライズ Key Admins グループにフル コントロールを許可するように ACE を追加します。 |なし|(A; の削除します。CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;Enterprise Key Admins)<br /> <br />(A; を追加します。CI;RPWPCRLCLOCCDCRCWDWOSDDTSW;;Enterprise Key Admins)|
|**Operation 88**: {434bb40d-dbc9-4fe7-81d4-d57229f7b080}|ドメイン NC のオブジェクトの"msDS ExpirePasswordsOnSmartCardOnlyAccounts"を追加し、既定値を FALSE に設定|なし|なし|

Enterprise Key Admins および Key Admins グループは、Windows Server 2016 ドメイン コント ローラーは昇格され、PDC エミュレーター FSMO ロールを引き継ぎ後のみ作成します。

## <a name="windows-server-2012-r2-domain-wide-updates"></a>Windows Server 2012 R2ドメイン全体の更新

によって操作が実行されないが**domainprep**コマンドが完了すると、Windows Server 2012 R2 で、**リビジョン**cn 属性 ActiveDirectoryUpdate、CN = DomainUpdates、CN を = = システムDC = オブジェクトに設定されている**10**します。

## <a name="windows-server-2012-domain-wide-updates"></a>Windows Server 2012:ドメイン全体の更新

によって実行される操作の実行後**domainprep** Windows Server 2012 (78、79、80、および 81 の操作)、完全な**リビジョン**cn 属性 ActiveDirectoryUpdate、CN を = = DomainUpdates、CN = System, DC = オブジェクトに設定されている**9**します。

|操作の数と GUID|説明|属性|アクセス許可|
|------------------------------|---------------|--------------|---------------|
|**Operation 78**: {c3c927a6-cc1d-47c0-966b-be8f9b63d991}|新しいオブジェクト CN を作成、ドメイン パーティションで TPM デバイスを = です。|オブジェクト クラス: msTPM InformationObjectsContainer|なし|
|**操作 79**: {54afcfb9-637a-4251-9f47-4d50e7021211}|TPM サービスのアクセス制御エントリを作成します。|なし|(OA;CIIO;WP;ea1b7b93-5e48-46d5-bc6c-4df4fda78a35;bf967a86-0de6-11d0-a285-00aa003049e2;PS)|
|**操作 80**: {f4728883-84dd-483c-9897-274f2ebcf11e}|"複製 DC"ための拡張権利の付与**Cloneable Domain Controllers**グループ|なし|(OA;CR; 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e; です。*ドメイン SID*-522)|
|**操作 81**: {ff4f9d27-7157-4cb0-80a9-5d6f2b14c8ff}|すべてのオブジェクトに対する ms-DS-Allowed-To-Act-On-Behalf-Of-Other-Identity Self プリンシパルに付与します。|なし|(OA;CIOI;RPWP; 3f78c3e5-f79a-46bd-a0b8-9d18116ddc79; です。PS)|
