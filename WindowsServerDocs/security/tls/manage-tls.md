---
title: トランスポート層セキュリティ (TLS) を管理する
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
author: justinha
ms.author: justinha
manager: brianlic-msft
ms.date: 05/16/2018
ms.openlocfilehash: a4ac1ea5b0648dbb80f103c146ad3df23fc04ab7
ms.sourcegitcommit: 06ae7c34c648538e15c4d9fe330668e7df32fbba
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2020
ms.locfileid: "78371396"
---
# <a name="manage-transport-layer-security-tls"></a>トランスポート層セキュリティ (TLS) を管理する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows 10

## <a name="configuring-tls-cipher-suite-order"></a>TLS 暗号スイートの順序の構成

Windows のバージョンによって、さまざまな TLS 暗号スイートと優先順位がサポートされます。 さまざまな Windows バージョンの Microsoft Schannel プロバイダーでサポートされている既定の順序については、「 [TLS/SSL (SCHANNEL SSP) の暗号スイート](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)」を参照してください。

> [!NOTE] 
> CNG 関数を使用して暗号スイートの一覧を変更することもできます。詳細については、「 [Schannel Cipher suite の優先順位付け](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx)」を参照してください。

TLS 暗号スイートの順序の変更は、次回の起動時に有効になります。 再起動またはシャットダウンまでは、既存の順序が有効になります。

> [!WARNING] 
> 既定の優先順位順序のレジストリ設定の更新はサポートされていないため、サービス更新プログラムによってリセットされる可能性があります。 

### <a name="configuring-tls-cipher-suite-order-by-using-group-policy"></a>グループポリシーを使用した TLS 暗号スイートの順序の構成

SSL 暗号スイートの順序グループポリシー設定を使用して、既定の TLS 暗号スイートの順序を構成できます。

1. グループポリシー管理コンソールから、コンピューターの**構成** > **管理用テンプレート** > **ネットワーク** > **SSL 構成設定** にアクセスします。
2. **[SSL 暗号スイートの順序]** をダブルクリックし、 **[有効]** オプションをクリックします。
3. **[SSL 暗号スイート]** を右クリックし、ポップアップメニューから **[すべて選択]** を選択します。

   ![グループ ポリシー設定](../media/Transport-Layer-Security-protocol/ssl-cipher-suite-order-gp-setting.png)

4. 選択したテキストを右クリックし、ポップアップメニューから **[コピー]** を選択します。
5. テキストを notepad.exe などのテキストエディターに貼り付け、新しい暗号スイートの順序の一覧を使用して更新します。

   > [!NOTE]
   > TLS 暗号スイートの順序一覧は、厳密なコンマ区切り形式である必要があります。 各暗号スイート文字列は、右側のコンマ (,) で終わります。 
   > 
   > また、暗号スイートの一覧は、1023文字までに制限されています。

6. **SSL 暗号スイート**の一覧を更新された順序付きリストに置き換えます。
7. **[OK]** または **[適用]** をクリックします。

### <a name="configuring-tls-cipher-suite-order-by-using-mdm"></a>MDM を使用した TLS 暗号スイートの順序の構成

Windows 10 ポリシー CSP は、TLS 暗号スイートの構成をサポートしています。 詳細については[、「Cryptography/TLSCipherSuites](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/policy-configuration-service-provider#cryptography-tlsciphersuites) 」を参照してください。

### <a name="configuring-tls-cipher-suite-order-by-using-tls-powershell-cmdlets"></a>Tls PowerShell コマンドレットを使用した TLS 暗号スイートの順序の構成

TLS PowerShell モジュールでは、TLS 暗号スイートの順序付きリストの取得、暗号スイートの無効化、および暗号スイートの有効化をサポートしています。 詳細については、「 [TLS モジュール](https://technet.microsoft.com/itpro/powershell/windows/tls/tls)」を参照してください。

## <a name="configuring-tls-ecc-curve-order"></a>TLS ECC 曲線の順序の構成 

Windows 10 & Windows Server 2016 以降では、ECC 曲線の順序は、暗号スイートの順序とは別に構成できます。 TLS 暗号スイートの順序リストに楕円曲線サフィックスがある場合は、新しい楕円曲線の優先順位 (有効な場合) によってオーバーライドされます。 これにより、組織はグループポリシーオブジェクトを使用して、同じ暗号スイートの順序で異なるバージョンの Windows を構成することができます。

> [!NOTE]
> Windows 10 より前では、曲線の優先順位を決定するために、暗号スイート文字列が楕円曲線と共に追加されました。

### <a name="managing-windows-ecc-curves-using-certutil"></a>CertUtil を使用した Windows ECC 曲線の管理

Windows 10 および windows Server 2016 以降では、コマンドラインユーティリティ certutil を使用して、楕円曲線パラメーターを管理できます。 楕円曲線パラメーターは、bcryptprimitives dll に格納されます。 Certutil を使用すると、管理者はそれぞれ Windows との間で曲線パラメーターを追加および削除できます。 Certutil は、曲線パラメーターをレジストリに安全に格納します。 曲線に関連付けられている名前によって、曲線パラメーターの使用を開始できます。    

#### <a name="displaying-registered-curves"></a>登録された曲線の表示

次の certutil コマンドを使用して、現在のコンピューターに登録されている曲線の一覧を表示します。

```powershell
certutil.exe –displayEccCurve
```

![Certutil の表示曲線](../media/Transport-Layer-Security-protocol/certutil-display-curves.png)

*図 1 Certutil 出力して、登録されている曲線の一覧を表示します。*

#### <a name="adding-a-new-curve"></a>新しい曲線の追加

組織は、他の信頼されたエンティティによって調査された曲線パラメーターを作成して使用できます。  
Windows でこれらの新しい曲線を使用する場合、管理者は曲線を追加する必要があります。  
次の certutil コマンドを使用して、現在のコンピューターに曲線を追加します。

```powershell
Certutil —addEccCurue curveName curveParameters [curveOID] [curveType]
```

- **Curの ame**引数は、曲線パラメーターが追加された曲線の名前を表します。
- **Curveparameters**引数は、追加する曲線のパラメーターを含む証明書のファイル名を表します。
- **Curveoid**引数は、追加する曲線パラメーターの OID を含む証明書のファイル名を表します (省略可能)。
- **Curvetype**引数は、 [EC 名前付き曲線レジストリ](http://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml#tls-parameters-8)からの名前付き曲線の10進値を表します (省略可能)。

![Certutil 曲線の追加](../media/Transport-Layer-Security-protocol/certutil-add-curves.png)

*図 2 certutil を使用して曲線を追加する*

#### <a name="removing-a-previously-added-curve"></a>以前に追加した曲線の削除

管理者は、次の certutil コマンドを使用して、以前に追加された曲線を削除できます。

```powershell
Certutil.exe –deleteEccCurve curveName
```

管理者がコンピューターから曲線を削除した後、Windows で名前付き曲線を使用することはできません。

## <a name="managing-windows-ecc-curves-using-group-policy"></a>グループポリシーを使用した Windows ECC 曲線の管理

組織は、グループポリシーとグループポリシー設定のレジストリ拡張を使用して、企業、ドメインに参加しているコンピューター、およびユーザー設定のレジストリ拡張を使用して、曲線パラメーターを配布できます。  
曲線を分散するプロセスは次のとおりです。

1.  Windows 10 および Windows Server 2016 では、 **certutil**を使用して、登録されている新しい名前付き曲線を windows に追加します。
2.  同じコンピューターから、グループポリシー管理コンソール (GPMC) を開き、新しいグループポリシーオブジェクトを作成して編集します。
3.  [コンピューターの構成] に移動します。 **基本設定 |Windows の設定 |レジストリ**。  **[レジストリ]** を右クリックします。 **[新規]** をポイントし、 **[コレクションアイテム]** を選択します。 曲線の名前に一致するように、コレクションアイテムの名前を変更します。 *HKEY_LOCAL_MACHINE \currentcontrolset\control\cryptography\eccparameters*の下にあるレジストリキーごとに1つのレジストリコレクション項目を作成します。
4.  *HKEY_LOCAL_MACHINE \currentcontrolset\control\cryptography\eccparameters\[Curベンダー名]* の下に一覧表示されている各レジストリ値に新しい**レジストリ項目**を追加して、新しく作成されたグループポリシー基本設定レジストリコレクションを構成します。
5.  グループポリシーレジストリコレクション項目を含むグループポリシーオブジェクトを、新しい名前付き曲線を受け取る必要がある Windows 10 および Windows Server 2016 コンピューターに展開します。

    ![GPP 分散曲線](../media/Transport-Layer-Security-protocol/gpp-distribute-curves.png)

    *図3曲線を配布するためのグループポリシーの設定の使用*

## <a name="managing-tls-ecc-order"></a>TLS ECC の順序を管理する

Windows 10 および Windows Server 2016 以降では、ECC 曲線の順序のグループポリシー設定を使用して、既定の TLS ECC 曲線の順序を構成できます。 この設定を使用すると、組織は、信頼された独自の名前付き曲線 (TLS で使用することが承認されている) をオペレーティングシステムに追加し、これらの名前付き曲線を曲線の優先順位グループポリシー設定に追加して、将来の TLS で使用されるようにすることができます。ハンドシェイク. 新しい曲線の優先順位の一覧は、ポリシー設定の受信後、次回の再起動時にアクティブになります。     

![GPP 分散曲線](../media/Transport-Layer-Security-protocol/gp-managing-tls-curve-priority-order.png)

*図4グループポリシーを使用した TLS 曲線の優先順位の管理*


