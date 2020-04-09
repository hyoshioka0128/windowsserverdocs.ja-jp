---
ms.assetid: 2a5d5271-6ac6-4c1b-b4ef-9b568932a55a
title: ドメイン全体でのスキーマの更新の Active Directory
description: ドメインコントローラーを昇格するときに adprep/domainprep によって実行されるドメイン全体のスキーマの更新
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 10/29/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 3b82958471e5292f202aa338aee7f4f5863459af
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80825215"
---
# <a name="domain-wide-schema-updates"></a>ドメイン全体でのスキーマの更新

>適用対象: Windows Server

Windows Server で adprep/domainprep によって実行されるスキーマの更新について理解し、準備するために、次の一連の変更を確認することができます。

Windows Server 2012 以降では、Adprep コマンドは、AD DS のインストール時に必要に応じて自動的に実行されます。 また、AD DS のインストールの前に個別に実行することもできます。 詳細については、「 [Adprep.exe の実行](https://technet.microsoft.com/library/dd464018(v=ws.10).aspx)」を参照してください。

アクセス制御エントリ (ACE) 文字列を解釈する方法の詳細については、「 [ace 文字列](https://msdn.microsoft.com/library/aa374928(VS.85).aspx)」を参照してください。 セキュリティ ID (SID) 文字列を解釈する方法の詳細については、「 [sid 文字列](https://msdn.microsoft.com/library/aa379602(VS.85).aspx)」を参照してください。

## <a name="windows-server-semi-annual-channel-domain-wide-updates"></a>Windows Server (半期チャネル): ドメイン全体の更新

Windows Server 2016 (operation 89) で**domainprep**によって実行された操作が完了すると、Cn = ACTIVEDIRECTORYUPDATE, Cn = domainupdates, Cn = SYSTEM, DC = ForestRootDomain オブジェクトの**revision**属性が**16**に設定されます。

|操作番号と GUID|説明|アクセス許可|
|------------------------------|---------------|--------------|---------------|
|**操作 89**: {A0C238BA-9E30-4EE6-80A6-43F731E9A5CD}|エンタープライズキー管理者へのフルコントロールを許可する ACE を削除し、msdsKeyCredentialLink 属性のみに対して、エンタープライズキー管理者のフルコントロールを許可する ACE を追加します。|Delete (A;項目RPWPCRLCLOCCDCRCWDWOSDDTSW;;;エンタープライズキー管理者) <br /> <br />Add (OA;項目5b47d60f-6090-40b2-9f37-2a4de88f3063;;エンタープライズキー管理者)|

## <a name="windows-server-2016-domain-wide-updates"></a>Windows Server 2016: ドメイン全体の更新プログラム

Windows Server 2016 (operations 82-88) で**domainprep**によって実行された操作が完了すると、Cn = ACTIVEDIRECTORYUPDATE, Cn = domainupdates, Cn = SYSTEM, DC = ForestRootDomain オブジェクトの**revision**属性が**15**に設定されます。

|操作番号と GUID|説明|属性|アクセス許可|
|------------------------------|---------------|--------------|---------------|
|**操作 82**: {83c53da747 27E4-7a4a07a324598b88 f7}|ドメインのルートに CN = Keys コンテナーを作成します|-objectClass: container<br />-description: キー資格情報オブジェクトの既定のコンテナー<br />-ShowInAdvancedViewOnly: TRUE|ある項目RPWPCRLCLOCCDCRCWDWOSDDTSW;;;A<br />ある項目RPWPCRLCLOCCDCRCWDWOSDDTSW;;;Dある<br />ある項目RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY<br />ある項目RPWPCRLCLOCCDCRCWDWOSDDTSW;;;DA<br />ある項目RPWPCRLCLOCCDCRCWDWOSDDTSW;;;プロンプト|
|**操作 83**: {C81FC9CC-0130-4FD1-B272-634D74818133}|[フルコントロールの追加] には、"会社キー管理者" および "root" エンタープライズキー管理者 "の CN = Keys コンテナーへの ace を許可します。|N/A|ある項目RPWPCRLCLOCCDCRCWDWOSDDTSW;;;キー管理者)<br />ある項目RPWPCRLCLOCCDCRCWDWOSDDTSW;;;エンタープライズキー管理者)|
|**操作 84**: {E5F9E791-D96D-4FC9-93C9-D53E1DC439BA}|OtherWellKnownObjects 属性を、CN = Keys コンテナーを指すように変更します。|-otherWellKnownObjects: B:32: 683A24E2E8164BD3AF86AC3C2CF3F981: CN = Keys,% ws|N/A|
|**操作 85**: {e6d5fd00-385d-4e65-b02d-9da3493ed850}|ドメイン NC を変更して、"ドメイン \ キー管理者" と "rootドメイン \ キー管理者" を許可して、KeyCredentialLink 属性を変更します。 |N/A|OA項目5b47d60f-6090-40b2-9f37-2a4de88f3063;;キー管理者)<br />OA項目5b47d60f-6090-40b2-9f37-2a4de88f3063;;ルートドメインのエンタープライズキー管理者は、ルートドメイン以外では、非解決可能な-527 SID を持つ偽のドメイン相対 ACE が生成されるようになりました。|
|**操作 86**: {3a6b3fbf-3168-4312-a10d-dd5b3393952d}|DS で検証されたコンピューター車を作成者の所有者と自己に付与する|N/A|OACIIO; SW; 9b026da6-0d3c-465c-8bee-5199d7165cba; bf967a86-0de6-11d0-a285-00aa003049e2; PS)<br />OACIIO; SW; 9b026da6-0d3c-465c-8bee-5199d7165cba; bf967a86-0de6-11d0-a285-00aa003049e2; CO)|
|**操作 87**: {7F950403-0AB3-47F9-9730-5D7B0269F9BD}|正しくないドメイン相対 Enterprise Key Admins グループに対してフルコントロールを許可する ACE を削除し、Enterprise Key Admins グループにフルコントロールを許可する ACE を追加します。 |N/A|Delete (A;項目RPWPCRLCLOCCDCRCWDWOSDDTSW;;;エンタープライズキー管理者)<br /> <br />(A; を追加します。項目RPWPCRLCLOCCDCRCWDWOSDDTSW;;;エンタープライズキー管理者)|
|**操作 88**: {434bb40d-dbc9-4fe7-81d4-d57229f7b080}|ドメイン NC オブジェクトに "ExpirePasswordsOnSmartCardOnlyAccounts" を追加し、既定値を FALSE に設定します。|N/A|N/A|

Enterprise Key Admins グループと Key Admins グループが作成されるのは、Windows Server 2016 ドメインコントローラーを昇格し、PDC エミュレーター FSMO の役割を引き継ぎた後のみです。

## <a name="windows-server-2012-r2-domain-wide-updates"></a>Windows Server 2012 R2: ドメイン全体の更新プログラム

Windows Server 2012 R2 では、 **domainprep**によって操作は実行されませんが、コマンドの完了後、Cn = ACTIVEDIRECTORYUPDATE, Cn = domainupdates, Cn = SYSTEM, DC = ForestRootDomain オブジェクトの**revision**属性は**10**に設定されます。

## <a name="windows-server-2012-domain-wide-updates"></a>Windows Server 2012: ドメイン全体の更新プログラム

Windows Server 2012 (operations 78、79、80、および 81) で**domainprep**によって実行された操作が完了すると、Cn = ACTIVEDIRECTORYUPDATE, Cn = domainupdates, Cn = SYSTEM, DC = ForestRootDomain オブジェクトの**revision**属性が**9**に設定されます。

|操作番号と GUID|説明|属性|アクセス許可|
|------------------------------|---------------|--------------|---------------|
|**操作 78**: {c3c927a6-cc1d-47c0-966b-be8f9b63d991}|新しいオブジェクト CN = TPM デバイスをドメインパーティションに作成します。|オブジェクトクラス: msTPM|N/A|
|**操作 79**: {54afcfb9-637a-4251-9f47-4d50e7021211}|TPM サービスのアクセス制御エントリが作成されました。|N/A|OACIIO。WP、ea1b7b93-5e48-46d5-bc6c-4df4fda78a35、bf967a86-0de6-11d0-a285-00aa003049e2、PS)|
|**操作 80**: {f4728883-84dd-483c-9897-274f2ebcf11e}|"複製 DC" を、複製可能**ドメインコントローラー**グループに付与します|N/A|(OA;;CR; 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e;;*ドメイン SID*-522)|
|**操作 81**: {ff4f9d27-7157-4cb0-80a9-5d6f2b14c8ff}|すべてのオブジェクトに対して、その他の Id を使用することをプリンシパルに許可します。|N/A|OACIOI;3f78c3e5-f79a-46bd-a0b8-9d18116ddc79;;PS|
