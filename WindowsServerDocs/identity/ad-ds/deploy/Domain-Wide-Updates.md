---
ms.assetid: 2a5d5271-6ac6-4c1b-b4ef-9b568932a55a
title: "Active Directory ドメインのスキーマの更新"
description: "Adprep によって実行されるドメインのスキーマ更新 /domainprep ドメイン コントローラーに昇格させるとき"
author: MicrosoftGuyJFlo
ms.author: joflore
manager: femila
ms.date: 07/14/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 59efb7c854b7f3693776bf9a1a371f98c2206d60
ms.sourcegitcommit: 79c1359232bece2e5c3ee5507f1e4bf19b44f487
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2018
---
# <a name="domain-wide-schema-updates"></a>ドメインのスキーマの更新

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

次の概要し、adprep によって実行される、スキーマの更新の準備のための変更のセットを確認する /domainprep Windows Server でします。 

Windows Server 2012 以降では、Adprep コマンドを AD DS のインストール中に、必要に応じて自動的に実行します。 AD DS のインストールを前もってお客様とは別に、実行することもできます。 For more information, see [Running Adprep.exe](https://technet.microsoft.com/library/dd464018(v=ws.10).aspx).

For more information about how to interpret the access control entry (ACE) strings, see [ACE strings](https://msdn.microsoft.com/library/aa374928(VS.85).aspx). For more information about how to interpret the security ID (SID) strings, see [SID strings](https://msdn.microsoft.com/library/aa379602(VS.85).aspx).

## <a name="windows-server-semi-annual-channel-domain-wide-updates"></a>ドメイン全体の更新の Windows Server (半期チャネル)。

後で実行される操作**domainprep** Windows Server 2016 (操作 89) 完了するで、**リビジョン**CN の属性 ActiveDirectoryUpdate、CN = DomainUpdates、CN = System, DC = = されています。オブジェクトに設定されている**16**します。

|操作の数と GUID|説明|アクセス許可|
|------------------------------|---------------|--------------|---------------|
|**操作 89**: {A0C238BA-9E30-4EE6-80A6-43F731E9A5CD}|エンタープライズ キー管理者にフル コントロールを許可する ACE を削除し、エンタープライズ キー Admins を完全に制御 msdsKeyCredentialLink 属性だけを付与する ACE を追加します。|(A; の削除します。CI です。RPWPCRLCLOCCDCRCWDWOSDDTSW;;Enterprise キー Admins) <br /> <br />追加する (OA です。CI です。RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063;Enterprise キー Admins)|

## <a name="windows-server-2016-domain-wide-updates"></a>ドメイン全体の更新の Windows Server 2016 の場合。

後で実行される操作**domainprep** Windows Server 2016 (operations 82 88) 完了するで、**リビジョン**CN の属性 ActiveDirectoryUpdate、CN = DomainUpdates、CN = System, DC = = にオブジェクトが設定されている**15**します。

|操作の数と GUID|説明|属性|アクセス許可|
|------------------------------|---------------|--------------|---------------|
|**操作 82**: {83C53DA7-427E-47A4-A07A-A324598B88F7}|CN を作成するドメインのルートにあるキー コンテナー =|-objectClass: コンテナー<br />-説明: キーの資格情報オブジェクトの既定のコンテナー<br />-ShowInAdvancedViewOnly: TRUE|(A;CI です。RPWPCRLCLOCCDCRCWDWOSDDTSW;;EA)<br />(A;CI です。RPWPCRLCLOCCDCRCWDWOSDDTSW;; DA)<br />(A;CI です。RPWPCRLCLOCCDCRCWDWOSDDTSW;;SY)<br />(A;CI です。RPWPCRLCLOCCDCRCWDWOSDDTSW;; DD)<br />(A;CI です。RPWPCRLCLOCCDCRCWDWOSDDTSW;;ED)|
|**操作 83**: {C81FC9CC-0130-4FD1-B272-634D74818133}|フル コントロールを追加する CN ace を許可する ="domain\Key Admins"のキー コンテナと"rootdomain\Enterprise キー Admins"します。|該当なし|(A;CI です。RPWPCRLCLOCCDCRCWDWOSDDTSW;;キー Admins)<br />(A;CI です。RPWPCRLCLOCCDCRCWDWOSDDTSW;;Enterprise キー Admins)|
|**操作 84**: {E5F9E791-D96D-4FC9-93C9-D53E1DC439BA}|CN を指す otherWellKnownObjects 属性を変更キー コンテナー = します。|-otherWellKnownObjects: B:32:683A24E2E8164BD3AF86AC3C2CF3F981:CN = キー、%ws|該当なし|
|**操作 85**: {e6d5fd00-385d-4e65-b02d-9da3493ed850}|ドメイン NC を"domain\Key Admins"の許可を変更し、"rootdomain\Enterprise キー Admins"msds KeyCredentialLink 属性を変更します。 |該当なし|(OA です。CI です。RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063;キー Admins)<br />(OA です。CI です。RPWP; 5b47d60f-6090-40b2-9f37-2a4de88f3063;[ルート ドメインが、非ルート ドメイン内の Enterprise キー Admins の非解決可能な-527 SID を持つ偽のドメインとの相対 ACE の原因として考え)|
|**操作 86**: {3a6b3fbf-3168-4312-a10d-dd5b3393952d}|作成者の所有者と自己 DS 検証-書き込み-コンピューターの車を与える|該当なし|(OA です。CIIO;SW;9b026da6-0d3c-465c-8bee-5199d7165cba;bf967a86-0de6-11d0-a285-00aa003049e2;PS)<br />(OA です。CIIO;SW;9b026da6-0d3c-465c-8bee-5199d7165cba;bf967a86-0de6-11d0-a285-00aa003049e2;CO)|
|**操作 87**: {7F950403-0AB3-47F9-9730-5D7B0269F9BD}|正しくないドメインとの相対 Enterprise キー Admins グループにフル コントロールを付与する ACE を削除し、エンタープライズ キー Admins グループにフル コントロールを付与する ACE を追加します。 |該当なし|(A; の削除します。CI です。RPWPCRLCLOCCDCRCWDWOSDDTSW;;Enterprise キー Admins)<br /> <br />(A; を追加します。CI です。RPWPCRLCLOCCDCRCWDWOSDDTSW;;Enterprise キー Admins)|
|**操作 88**: {434bb40d-dbc9-4fe7-81d4-d57229f7b080}|ドメイン NC のオブジェクトの"msDS ExpirePasswordsOnSmartCardOnlyAccounts"を追加し、既定値を FALSE に設定|該当なし|該当なし|

エンタープライズ キー Admins とキー Admins グループは、Windows Server 2016 ドメイン コントローラーの昇格し、PDC エミュレーター FSMO 役割を引き継ぐのみ作成します。

## <a name="windows-server-2012-r2-domain-wide-updates"></a>ドメイン全体の更新の Windows Server 2012 R2 の場合。

によって処理は行われませんが**domainprep**コマンドが完了したら、Windows Server 2012 R2 で、**リビジョン**CN の属性 ActiveDirectoryUpdate、CN = DomainUpdates、CN = System, DC = = にオブジェクトが設定されている**10**します。

## <a name="windows-server-2012-domain-wide-updates"></a>Windows Server 2012: ドメイン全体の更新

によって実行される操作の後に**domainprep** Windows Server 2012 (operations 78、79、80、および 81) 完了すると、**リビジョン**CN の属性 ActiveDirectoryUpdate、CN = DomainUpdates、CN = System, DC = = にオブジェクトが設定されている**9**します。

|操作の数と GUID|説明|属性|アクセス許可|
|------------------------------|---------------|--------------|---------------|
|**操作 78**: {c3c927a6-cc1d-47c0-966b-be8f9b63d991}|新しいオブジェクトの CN を作成するドメイン パーティションに TPM デバイスを = します。|オブジェクトのクラス: msTPM InformationObjectsContainer|該当なし|
|**操作 79**: {54afcfb9-637a-4251-9f47-4d50e7021211}|TPM サービス用のアクセス制御エントリを作成します。|該当なし|(OA です。CIIO です。WP;ea1b7b93-5e48-46d5-bc6c-4df4fda78a35;bf967a86-0de6-11d0-a285-00aa003049e2;PS)|
|**操作 80**: {f4728883-84dd-483c-9897-274f2ebcf11e}|"複製 DC"ための拡張権利を付与**Cloneable Domain Controllers**グループ|該当なし|(OA;CR; 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e;*ドメイン SID*-522)|
|**操作 81**: {ff4f9d27-7157-4cb0-80a9-5d6f2b14c8ff}|すべてのオブジェクトに対する Self プリンシパルに MS-DS-Allowed-To-Act-On-Behalf-Of-Other-Identity を許可します。|該当なし|(OA です。CIOI です。RPWP; 3f78c3e5-f79a-46bd-a0b8-9d18116ddc79;PS)。|
