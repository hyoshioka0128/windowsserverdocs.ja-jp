---
title: トランスポート層セキュリティ (TLS) の管理します。
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-tls-ssl
ms.tgt_pltfrm: na
ms.topic: article
author: justinha
ms.author: justinha
manager: brianlic-msft
ms.date: 05/16/2018
ms.openlocfilehash: 872647f09898bf8ae08ee69f28b717d28abf7c78
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447306"
---
# <a name="manage-transport-layer-security-tls"></a>トランスポート層セキュリティ (TLS) の管理します。

>適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows 10

## <a name="configuring-tls-cipher-suite-order"></a>TLS 暗号スイートの構成の順序

Windows バージョンでは、さまざまな TLS 暗号スイートと優先順位をサポートします。 参照してください[in TLS/SSL (Schannel SSP) 暗号スイート](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)のさまざまな Windows バージョンで、Microsoft の Schannel プロバイダーでサポートされている既定の順序。

> [!NOTE] 
> リストを変更することもできます。 CNG 関数を使用して暗号スイート、のを参照してください。 [Schannel 暗号スイートの優先順位を付ける](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx)詳細についてはします。

TLS 暗号スイートの順序の変更は、次の起動時に有効になります。 再起動またはシャット ダウン、までは、既存の注文が有効になります。

> [!WARNING] 
> 既定の優先順位の順序のレジストリ設定の更新はサポートされていませんし、サービス更新プログラムをリセットすることがあります。 

### <a name="configuring-tls-cipher-suite-order-by-using-group-policy"></a>グループ ポリシーを使用して TLS 暗号の順位を構成します。

SSL Cipher Suite Order のグループ ポリシー設定を使用すると、既定の TLS 暗号スイート順序を構成します。

1. 移動し、グループ ポリシー管理コンソールから**コンピューターの構成** > **管理用テンプレート** > **ネットワーク** >  **SSL 構成設定**します。
2. ダブルクリック**SSL 暗号の順位**、 をクリックし、**有効**オプション。
3. 右クリックして**SSL 暗号**ボックスを選択します**すべて選択**ポップアップ メニューから。

   ![グループ ポリシー設定](../media/Transport-Layer-Security-protocol/ssl-cipher-suite-order-gp-setting.png)

4. 選択したテキストを右クリックして**コピー**ポップアップ メニューから。
5. テキストを notepad.exe と暗号スイートの新しい順序リストでの更新プログラムなどのテキスト エディターに貼り付けます。

   > [!NOTE]
   > TLS 暗号スイートの注文リストは、厳密なコンマ区切り形式でなければなりません。 各暗号スイートの文字列の右側に、コンマ (,) で終了します。 
   > 
   > さらに、暗号スイートの一覧は、1,023 文字に制限されます。

6. リストを置き換える、 **SSL 暗号**で更新された順序付きリスト。
7. **[OK]** または **[適用]** をクリックします。

### <a name="configuring-tls-cipher-suite-order-by-using-mdm"></a>MDM を使用して TLS 暗号の順位を構成します。

Windows 10 ポリシー CSP では、TLS 暗号の構成をサポートします。 参照してください[暗号化/TLSCipherSuites](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/policy-configuration-service-provider#cryptography-tlsciphersuites)詳細についてはします。

### <a name="configuring-tls-cipher-suite-order-by-using-tls-powershell-cmdlets"></a>TLS の PowerShell コマンドレットを使用して TLS 暗号の順位を構成します。

TLS PowerShell モジュールでは、TLS 暗号スイートの順序付きリストを取得する、暗号スイートでは、無効にして暗号スイートを有効化をサポートします。 参照してください[TLS モジュール](https://technet.microsoft.com/itpro/powershell/windows/tls/tls)詳細についてはします。

## <a name="configuring-tls-ecc-curve-order"></a>TLS ECC 曲線の順序を構成します。 

Windows 10 および Windows Server 2016 以降、ECC 曲線の順序構成できます暗号スイートの順序に関係なく。 TLS は暗号スイートの順序が楕円曲線のサフィックスの一覧場合、有効にするは、新しい楕円曲線優先順位によってオーバーライドされます。 これは、グループ ポリシー オブジェクトを使用して、暗号スイートと同じ順序で異なるバージョンの Windows を構成する組織です。

> [!NOTE]
> Windows 10 では、前に暗号スイートの文字列には楕円曲線の曲線の優先順位を決定が付加されます。

### <a name="managing-windows-ecc-curves-using-certutil"></a>CertUtil を使用して Windows ECC 曲線を管理します。

Windows 10 および Windows Server 2016 以降、Windows は、コマンド ライン ユーティリティ certutil.exe による楕円曲線パラメーターの管理を提供します。 楕円曲線パラメーターは、bcryptprimitives.dll に格納されます。 Certutil.exe を使用して、管理者は追加し、Windows との間の曲線パラメーターをそれぞれ削除します。 Certutil.exe は、レジストリの曲線パラメーターを安全に保存します。 曲線パラメーターを使用して、曲線に関連付けられている名前で Windows を開始できます。    

#### <a name="displaying-registered-curves"></a>登録済みの曲線を表示します。

現在のコンピューターの登録の曲線の一覧を表示するのにには、次の certutil.exe コマンドを使用します。

```powershell
certutil.exe –displayEccCurve
```

![Certutil 表示曲線](../media/Transport-Layer-Security-protocol/certutil-display-curves.png)

*登録済みの曲線の一覧を表示する出力を図 1 Certutil.exe します。*

#### <a name="adding-a-new-curve"></a>新しい曲線を追加します。

組織では、作成でき、他の信頼されたエンティティによって調査曲線パラメーターを使用することができます。  
管理者は Windows でこれらの新しい曲線が使用するには、曲線を追加する必要があります。  
現在のコンピューターに曲線を追加するのにには、certutil.exe の次のコマンドを使用します。

```powershell
Certutil —addEccCurue curveName curveParameters [curveOID] [curveType]
```

- **CurveName**引数を曲線パラメーターが追加された曲線の名前を表します。
- **CurveParameters**引数を追加する曲線のパラメーターを含む証明書のファイル名を表します。
- **CurveOid**引数 (省略可能) を追加する曲線のパラメーターの OID を含む証明書のファイル名を表します。
- **CurveType**引数が 10 進数値から名前付き曲線を表す、 [EC 名前付き曲線レジストリ](http://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml#tls-parameters-8)(省略可能)。

![Certutil 曲線を追加します。](../media/Transport-Layer-Security-protocol/certutil-add-curves.png)

*図 2 は、certutil.exe を使用して曲線を追加します。*

#### <a name="removing-a-previously-added-curve"></a>以前に追加された曲線を削除します。

管理者は、certutil.exe の次のコマンドを使用して以前に追加された曲線を削除できます。

```powershell
Certutil.exe –deleteEccCurve curveName
```

Windows では、管理者がコンピューターから、曲線を削除した後、名前付き曲線を使用できません。

## <a name="managing-windows-ecc-curves-using-group-policy"></a>グループ ポリシーを使用して Windows ECC 曲線を管理します。

組織では、enterprise、ドメインに参加しているコンピューターのグループ ポリシーとグループ ポリシー基本設定のレジストリ拡張機能を使用する曲線パラメーターを配布できます。  
曲線を配布するためのプロセスは次のとおりです。

1.  Windows 10 および Windows Server 2016 では、次のように使用します。 **certutil.exe** Windows に新しい登録済みの名前付き曲線を追加します。
2.  、同じコンピューターからグループ ポリシー管理コンソール (GPMC) を開き、新しいグループ ポリシー オブジェクトを作成および編集します。
3.  移動します**コンピューターの構成 |基本設定 |Windows の設定 |レジストリ**します。  右クリックして**レジストリ**します。 ポインターを合わせる**新規**選択**コレクション アイテム**します。 曲線の名前と一致するコレクション項目の名前を変更します。 下のレジストリ キーごとに 1 つのレジストリのコレクション アイテムを作成します*HKEY_LOCAL_MACHINE\CurrentControlSet\Control\Cryptography\ECCParameters*します。
4.  新しく作成されたグループ ポリシー基本設定のレジストリ コレクションを追加して構成**レジストリ項目**各レジストリ値の下の*HKEY_LOCAL_MACHINE\CurrentControlSet\Control\Cryptography\ECCParameters\[curveName]* します。
5.  新しい名前付き曲線を受け取る必要のある Windows 10 および Windows Server 2016 のコンピューターにグループ ポリシー レジストリのコレクション アイテムを含むグループ ポリシー オブジェクトを展開します。

    ![GPP は曲線を配布します。](../media/Transport-Layer-Security-protocol/gpp-distribute-curves.png)

    *図 3 Using Group Policy Preferences: 曲線を配布するには*

## <a name="managing-tls-ecc-order"></a>TLS ECC 順序を管理します。

以降では、Windows 10 および Windows Server 2016 は、ECC 曲線の順序のグループ ポリシー設定を使用する既定の TLS ECC 曲線の順序を構成します。 ジェネリック ECC し、この設定、組織を使用する独自信頼を名前付き曲線 (TLS で使用するためには、承認されて) いるオペレーティング システムに追加および将来 TLS で使用されていることを確認するには、曲線の優先順位グループ ポリシー設定をその名前付き曲線を追加できます。ハンドシェイクです。 曲線の優先度リストの新しいポリシー設定を受信した後、次回の起動時にアクティブになります。     

![GPP は曲線を配布します。](../media/Transport-Layer-Security-protocol/gp-managing-tls-curve-priority-order.png)

*グループ ポリシーを使用して、図 4 管理 TLS 曲線の優先順位*


