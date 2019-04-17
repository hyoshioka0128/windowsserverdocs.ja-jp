---
title: "トランスポート層セキュリティ (TLS) の管理します。"
description: "Windows Server のセキュリティ"
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
ms.date: 06/05/2017
ms.openlocfilehash: e26d1f833dbb7219251947f1cb3cb09def958aea
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="manage-transport-layer-security-tls"></a>トランスポート層セキュリティ (TLS) の管理します。

## <a name="configuring-tls-cipher-suite-order"></a>構成 TLS 暗号の順位

異なるバージョンの Windows では、別の TLS 暗号スイートおよび優先順位をサポートします。 参照してください[TLS/SSL (Schannel SSP) の暗号スイート](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)の異なるバージョンの Windows で Microsoft の Schannel プロバイダーでサポートされている既定の順序です。

> [!NOTE] 
> 一覧を変更することもできます。CNG 関数を使用して暗号スイート、のを参照してください。[Schannel 暗号スイートの優先順位を付ける](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx)詳細についてはします。

TLS 暗号スイートの順序の変更は、再起動後に有効になります。 まで再起動またはシャット ダウン、既存の順序は有効になります。

> [!WARNING] 
> 既定の優先順位の順序のレジストリ設定を更新して、サポートされていない、サービシングの更新プログラムをリセットすることがあります。 

### <a name="configuring-tls-cipher-suite-order-by-using-group-policy"></a>グループ ポリシーを使用して TLS 暗号の順位を構成します。

SSL 暗号スイートの順序のグループ ポリシー設定を使用して、既定 TLS 暗号スイート順を構成することができます。

1.  移動するグループ ポリシーから管理コンソール、**コンピューターの構成** > **管理用テンプレート** > **ネットワーク** > **SSL 構成設定**します。
2.  をダブルクリック**SSL 暗号の順位**、クリックして、**有効**オプションです。
3.  右クリック**SSL 暗号**ボックスし、**すべて選択**、ポップアップ メニューからです。

    ![グループ ポリシー設定](../media/Transport-Layer-Security-protocol/ssl-cipher-suite-order-gp-setting.png)

4.  選択したテキストを右クリックして選択**コピー**、ポップアップ メニューからです。
5.  Notepad.exe と、新しい暗号スイート順] 一覧で更新プログラムなどのテキスト エディターにテキストを貼り付けます。

    > [!NOTE]
    > TLS 暗号スイートの順序の一覧は、厳密なコンマ区切り形式でなければなりません。 各暗号スイートの文字列が右側にあるは、コンマ (,) で終了します。 

    > さらに、暗号スイートの一覧は、1,023 文字に制限されます。

6.  [一覧の置換、**SSL 暗号**更新された順序付きリストを使用します。
7.  をクリックして**OK**または**適用**します。

### <a name="configuring-tls-cipher-suite-order-by-using-mdm"></a>MDM を使用して TLS 暗号の順位を構成します。

Windows 10 ポリシー CSP では、TLS 暗号スイートの構成がサポートされます。 参照してください[暗号化/TLSCipherSuites](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/policy-configuration-service-provider#cryptography-tlsciphersuites)詳細についてはします。

### <a name="configuring-tls-cipher-suite-order-by-using-tls-powershell-cmdlets"></a>TLS の PowerShell コマンドレットを使用して TLS 暗号の順位を構成します。

TLS PowerShell モジュールには、TLS 暗号スイートの順序付きリストを取得して、暗号スイートを無効にすると、暗号スイートを有効にするとがサポートしています。 参照してください[TLS モジュール](https://technet.microsoft.com/itpro/powershell/windows/tls/tls)詳細についてはします。

## <a name="configuring-tls-ecc-curve-order"></a>TLS ECC 曲線順序を構成します。 

Windows 10 と Windows Server 2016 以降では、ECC 曲線順序構成できます、暗号の順位の独立しました。 TLS は暗号の順位一覧は、楕円曲線サフィックスを持つ場合、有効にするは新しい楕円曲線優先順位に従って、によって上書きされます。 これには、グループ ポリシー オブジェクトを使用して暗号スイートのと同じ順序で異なるバージョンの Windows を構成する組織ができるようにします。

> [!NOTE]
> Windows 10 より前の曲線優先順位を決定する楕円曲線暗号スイートの文字列の末尾されました。

### <a name="managing-windows-ecc-curves-using-certutil"></a>CertUtil を使用して Windows ECC カーブを管理します。

Windows 10 および Windows Server 2016 以降では、Windows、楕円曲線パラメーター管理でもコマンド ライン ユーティリティ certuil.exe します。 楕円曲線パラメーターは、bcryptprimitives.dll に格納されます。 Certutil.exe を使用すると、管理者は追加し、それぞれ曲線パラメーターと、Windows の間を削除します。 Certutil.exe は、レジストリ内に安全に曲線パラメーターを格納します。 曲線に関連付けられている名前によって曲線パラメーターを使用して Windows を開始できます。    

#### <a name="displaying-registered-curves"></a>登録済みカーブを表示します。

曲線は現在のコンピューターの登録の一覧を表示するのにには、次の certutil.exe コマンドを使用します。

```powershell
certutil.exe –displayEccCurve
```

![Certutil 表示カーブ](../media/Transport-Layer-Security-protocol/certutil-display-curves.png)

*図 1 Certutil.exe を出力カーブを登録済みの一覧を表示します。*

#### <a name="adding-a-new-curve"></a>新しいカーブを追加します。

組織は、作成し、その他の信頼されたエンティティの研究曲線パラメーターを使用できます。  
Windows でこれらの新しいカーブを使用する管理者は、曲線を追加する必要があります。  
現在のコンピューターに曲線を追加するのにには、次の certutil.exe コマンドを使用します。

```powershell
Certutil —addEccCurue curveName curveParameters [curveOID] [curveType]
```

- **CurveName**引数がカーブ パラメーターが追加されましたがカーブの名前を表します。
- **CurveParameters**引数を追加する曲線のパラメーターを含む証明書のファイル名を表します。
- **CurveOid**引数を追加する (省略可能) 曲線パラメーターの OID を含む証明書のファイル名を表します。
- **CurveType**引数から名前付きの曲線の 10 進数の値を表す、[EC という名前の曲線レジストリ](http://www.iana.org/assignments/tls-parameters/tls-parameters.xhtml#tls-parameters-8)(省略可能)。

![Certutil カーブを追加します。](../media/Transport-Layer-Security-protocol/certutil-add-curves.png)

*図 2 は、certutil.exe を使用して曲線を追加します。*

#### <a name="removing-a-previously-added-curve"></a>以前に追加したカーブを削除します。

管理者は、certutil.exe の次のコマンドを使用して、以前に追加したカーブを削除できます。

```powershell
Certutil.exe –deleteEccCurve curveName
```

Windows では、管理者がコンピューターから曲線を削除した後、名前付き曲線を使用できません。

## <a name="managing-windows-ecc-curves-using-group-policy"></a>グループ ポリシーを使用して Windows ECC カーブを管理します。

組織では、enterprise、ドメインに参加しているグループ ポリシーとグループ ポリシーの基本設定のレジストリの拡張機能を使用してコンピューターに曲線パラメーターを配布できます。  
曲線を配布するためのプロセスは次のとおりです。

1.  Windows 10 および Windows Server 2016 を使用して**certutil.exe** Windows に登録されている新しい名前付き曲線を追加します。
2.  同じコンピューターからグループ ポリシー管理コンソール (GPMC) を開き、新しいグループ ポリシー オブジェクトを作成、編集します。
3.  移動**コンピューターの構成 |基本設定 |Windows の設定 |レジストリ**します。  右クリック**レジストリ**します。 マウスをポイント**新規**選択**コレクション項目**します。 曲線の名前と一致するコレクション項目の名前を変更します。 下にあるレジストリ キーごとに 1 つのレジストリ コレクション項目を作成します*HKEY_LOCAL_MACHINE\CurrentControlSet\Control\Cryptography\ECCParameters*します。
4.  新しいを追加することで、新しく作成したグループ ポリシー基本設定のレジストリ コレクションを構成する**レジストリ項目**下にある各レジストリ値が表示されている*HKEY_LOCAL_MACHINE\CurrentControlSet\Control\Cryptography\ECCParameters\ [curveName]*します。
5.  新しい名前付き曲線を受け取る必要のある Windows 10 および Windows Server 2016 のコンピューターにグループ ポリシー レジストリ コレクション項目を含むグループ ポリシー オブジェクトを展開します。

    ![GPP カーブを配布します。](../media/Transport-Layer-Security-protocol/gpp-distribute-curves.png)

    *図 3 を使用してグループ ポリシーの基本設定カーブを配布するには*

## <a name="managing-tls-ecc-order"></a>TLS ECC 注文を管理します。

Windows 10 および Windows Server 2016 以降では、ECC 曲線順序のグループ ポリシー設定を使用する既定 TLS ECC 曲線順序を構成します。 汎用 ECC し、この設定を組織を使用して独自信頼されるという名前のカーブ (TLS で使用するためには、承認されて) オペレーティング システムに追加できカーブを将来の TLS ハンドシェイクで使用されることを確認する曲線優先順位のグループ ポリシー設定をという名前を追加できます。 新規曲線優先度の一覧を次の再起動のポリシー設定を受信した後でアクティブになります。     

![GPP カーブを配布します。](../media/Transport-Layer-Security-protocol/gp-managing-tls-curve-priority-order.png)

*グループ ポリシーを使用して、図 4 管理 TLS 曲線の優先順位*


