---
title: ダッシュボード、リモート Web アクセス、スタートパッドにブランドを追加する
description: ダッシュボード、リモート Web アクセス、スタートパッドの各画面にブランド資料を追加する方法について説明します。
ms.date: 04/10/2014
ms.prod: windows-server
ms.topic: article
ms.assetid: 166262f8-b2a5-4b1c-a4a7-a141e1c54f10
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 056c7264fc90adbf115c3c6587081a449240a98a
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471087"
---
# <a name="add-branding-to-the-dashboard-remote-web-access-and-launchpad"></a>ダッシュボード、リモート Web アクセス、スタート パッドへのブランドの追加

> 適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

レジストリにエントリを追加することによって、多くのブランド追加を実行できます。 オペレーティングシステムのレジストリ内のすべてのブランド化エントリは、にあり `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OEM` ます。

共同ブランド化を行うには、Windows Server Essentials のロゴの幅が**170 ピクセル**以上である必要があります。これにより、正しい縦横比が**96 DPI**で維持されます。

## <a name="to-add-branding-by-changing-the-registry"></a>レジストリを変更することでブランドを追加するには

1. サーバーで、カーソルを画面の右上隅に移動して、[**検索**] をクリックします。

2. 検索ボックスに「**regedit**」と入力して、[**Regedit**] アプリケーションをクリックします。

3. ナビゲーション ウィンドウで、[**HKEY_LOCAL_MACHINE**]、[**SOFTWARE**]、[**Microsoft**]、[**Windows Server**] の順に展開します。 **OEM**キーが存在しない場合は、次のように作成できます。

    1. [**Windows Server**] を右クリックし、[**新規**] をクリックし、[**キー**] をクリックします。

    2. キーの名前に「**OEM**」と入力します。

4. Optionalロゴのエントリを作成する場合は、ロゴの言語バージョンを区別するために異なるキーを作成できます。 たとえば、英語バージョンのロゴとドイツ語バージョンのロゴを所有する場合、en-us キーと de-de キーを作成できます。 ロゴ ファイルはすべて同じフォルダーに保存されるため、ロゴ イメージ ファイルのインスタンスに、言語ごとに一意の名前を指定する必要があります。 たとえば、DashboardLogo_en.png と DashboardLogo_de.png という名前のファイルを作成します。

5. [ **OEM** ] を右クリックするか、適切な言語キーを右クリックして [**新規作成**] をクリックし、[**文字列値**] をクリックします。

6. 文字列の名前を入力し、Enter キーを押します。 文字列名とデータ値の詳細については、この記事の「**レジストリの文字列と値**」を参照してください。

7. 文字列の名前を入力し、Enter キーを押します。 文字列名とデータ値の詳細については、この記事の「**レジストリの文字列と値**」を参照してください。

8. 新しい文字列を右クリックして、[**変更**] をクリックします。

9. 文字列名に関連する表から値を入力し、[**OK**] をクリックします。

10. ロゴイメージまたは追加されたリンクのエントリを作成する場合は、ファイルをにコピーし `%programFiles%\Windows Server\Bin\OEM` ます。 OEM ディレクトリが存在しない場合は、ディレクトリを作成します。

11. お客様がサーバーの所有権を取得した後にリモート Web アクセスに変更を加える場合は、次の方法でリモート Web アクセスを有効にする必要があります。

    1. ダッシュボードで、[**設定**] をクリックし、[**Anywhere Access**] タブをクリックします。

    2. **Anywhere access**が有効になっている場合は、[**構成**] をクリックし、[anywhere access の**設定**] ウィザードの [**有効にする anywhere access の機能を選択**します] ページで [リモート Web アクセスチェックボックスをオフにします。

    3. **[構成]** をクリックします。

### <a name="registry-strings-and-values"></a>レジストリの文字列と値

次の表は、使用可能な文字列名とデータ値に関する情報を示しています。

| ブランド化の場所 | 説明 | 文字列名 | データ値 |
|--|--|--|--|
| ダッシュボードのロゴ | ロゴのイメージをダッシュボードに追加します。 ダッシュボードのロゴは .png 形式にし、幅 350 ピクセル、高さ 38 ピクセルを超えないようにする必要があります。<p>**重要:** ダッシュボードをロゴと共同ブランド化するには、OPK DVD に収録されているアートワークタイルを編集し、適切な空白の要件に従って、会社のロゴをイメージに追加する必要があります。 | DashboardLogo | ロゴイメージファイルの名前を入力します。 |
| DashboardClientLogo | ダッシュボードクライアントのサインイン画面にロゴイメージを追加します。 | DashboardClientLogo | ロゴイメージファイルの名前を入力します。 |
| Web サイトの背景画像 | リモート Web アクセスサインインページに表示される背景イメージを変更します。 一般的な解像度では、次のように表示されます。<ul><li>**1024x768 ピクセル**-この解像度は、サインインページを正確に塗りつぶします。</li><li>**800 x 600 ピクセル**-この解像度では、イメージがページ上に中央に表示され、黒い境界線が表示されます。</li><li>**1280 x 20 ピクセル**-この解像度はイメージを中心にします。 1024x720 を超えるピクセルは表示されません。 | LogonBackground | 背景画像ファイルの名前を入力します。 |
| Web サイトのタイトル | リモート Web アクセスサイトのタイトルを Windows Server Essentials から指定されたタイトルに置き換えます。 | WebsiteName | 新しいリモート Web アクセスサイトのタイトルを入力します。 |
| Web サイトのロゴ | リモート Web アクセス サイトの既定のロゴを変更します。 予想されるロゴ サイズは 32 × 32 ピクセルです。 ロゴがこの値より小さいか大きい場合は、これらの寸法に合わせて拡大または縮小されます。 | WebsiteLogo | ロゴ画像ファイルの名前を入力します |
| 追加された Web サイトのロゴ | パートナーのロゴは、リモート Web アクセスサイトに表示される Microsoft ロゴのすぐ下に表示されます。 予想されるロゴ サイズは高さ 200 ピクセル、幅 50 ピクセルです。 ロゴがこれより大きい場合、元の縦横比を保持した状態でサイズに合わせて縮小されます。 ロゴがこれより小さい場合は、200 x 50 ピクセルのスペースの中央に配置され、サイズも縦横比も変更されません。 | OEMLogo | ロゴイメージファイルの名前を入力します。 |
| Web サイトのホームページとサインインページのリンク | リモート Web アクセスサイトのサインインページとホームページへのリンクを追加します。 リンク情報を含む XML ファイルは、フォルダーに配置する必要があり `%programFiles%\Windows Server\Bin\OEM` ます。 | LinksXML | 要素とその説明の一覧については、表「LinksXML 要素」を参照してください。 |
| スタート パッドのロゴ | ロゴのイメージをスタート パッドに追加します。 スタート パッドのロゴは .png 形式にし、高さ 64 ピクセルを超えないようにする必要があります。 | LaunchpadLogo | ロゴイメージファイルの名前を入力します。 |

#### <a name="xml-linking-format"></a>XML リンク形式

Web サイトの**ホーム**ページとサインインページのリンクは、次のように書式設定する必要があります。

```xml
<OemLinks>
    <LogonLinks>
        <Link Name=LogonLinkName>
        <Text>LogonLinkDescription</Text>
        <Url>LogonLinkURL</Url>
        <Icon>LinkIcon</Icon>
        </Link>
    </LogonLinks>

    <HomepageLinks>
        <Link Name=HomepageLinkName>
        <Text>HomepageLinkDescription</Text>
        <Url>HomepageLinkURL</Url>
        <Icon>HomepageLinkIcon</Icon>
        </Link>
    </HomepageLinks>
</OemLinks>
```

### <a name="linksxml-elements"></a>LinksXML 要素

| LinksXML 要素 | 説明 |
|--|--|
| LogonLinks | サインインリンクの親エントリ。 |
| リンク名 | サインインのリンク名。 |
| Text | サインインページのリンクとして表示されるテキスト。 |
| URL | サインインページリンクに解決される URL。 |
| ［アイコン］ | サインインリンクのアイコンファイルの名前。 このファイルは、.xml ファイルと同じフォルダー場所に存在する必要があります。 アイコンイメージは、16 x 16 ピクセルで、.png 形式である必要があります。 アイコンを指定しない場合は、既定のリンクアイコンイメージが使用されます。 |
| HomepageLinks | **ホーム**ページの親エントリ。 |
| リンク名 | **ホーム**ページのリンク名。 |
| Text | **ホーム**ページのリンクとして表示されるテキスト。 |
| URL | **ホーム**ページのリンクに解決される URL。 |
| ［アイコン］ | **ホーム**ページのリンクのアイコンファイルの名前。 このファイルは、.xml ファイルと同じフォルダー場所に存在する必要があります。 アイコンイメージは、16 x 16 ピクセルで、.png 形式である必要があります。 アイコンを指定しない場合は、既定の**ホーム**ページリンクアイコンの画像が使用されます。 |

## <a name="additional-references"></a>その他のリファレンス

- [イメージの作成とカスタマイズ](Creating-and-Customizing-the-Image.md)

- [追加のカスタマイズ](Additional-Customizations.md)

- [イメージの展開の準備](Preparing-the-Image-for-Deployment.md)

- [カスタマー エクスペリエンスのテスト](Testing-the-Customer-Experience.md)