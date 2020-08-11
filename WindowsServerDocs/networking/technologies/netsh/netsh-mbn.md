---
title: モバイル ブロードバンド ネットワーク (MBN) 用の netsh コマンド
description: netsh mbn を使用して、モバイル ブロードバンドの設定とパラメーターを照会および構成します。
ms.topic: article
author: apdutta
ms.date: 02/20/2020
ms.openlocfilehash: 50c0bbf441e3109189117cbfd8df9ee597712bcd
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953988"
---
# <a name="netsh-mbn-commands"></a>netsh mbn コマンド


**netsh mbn** を使用して、モバイル ブロードバンドの設定とパラメーターを照会および構成します。

> [!TIP]
> netsh mbn コマンドのヘルプを表示するには、次を使用します
>
> &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;netsh mbn /?

使用できる netsh mbn コマンドは次のとおりです。

- [add](#add)
- [connect](#connect)
- [delete](#delete)
- [disconnect](#disconnect)
- [diagnose](#diagnose)
- [dump](#dump)
- [help](#help)
- [set](#set)
- [show](#show)

## <a name="add"></a>追加

テーブルに構成項目を追加します。

使用できる netsh mbn add コマンドは次のとおりです。

- [dmprofile](#dmprofile)
- [profile](#profile)

### <a name="dmprofile"></a>dmprofile

プロファイル データ ストアに DM 構成プロファイルを追加します。

**構文**

```powershell
add dmprofile [interface=]<string> [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |
| **name**      | プロファイル XML ファイルの名前。 プロファイル データを含む XML ファイルの名前です。     | 必須 |


**例**

```powershell
add dmprofile interface="Cellular" name="Profile1.xml"
```


### <a name="profile"></a>プロファイル

プロファイル データ ストアにネットワーク プロファイルを追加します。

**構文**

```powershell
add profile [interface=]<string> [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |
| **name**      | プロファイル XML ファイルの名前。 プロファイル データを含む XML ファイルの名前です。     | 必須 |


**例**

```powershell
add profile interface="Cellular" name="Profile1.xml"
```


## <a name="connect"></a>connect

モバイル ブロードバンド ネットワークに接続します。

**構文**

```powershell
connect [interface=]<string> [connmode=]tmp|name [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |
| **connmode**  | 接続パラメーターの提供方法を指定します。 接続を要求するには、プロファイル XML を使用するか、以前に "netsh mbn add profile" コマンドを使用してモバイル ブロードバンド プロファイル データ ストアに格納したプロファイル XML のプロファイル名を使用します。 前者の場合、パラメーター connmode には値として "tmp" を指定する必要があります。 一方、後者の場合は、"name" を指定します                                       | 必須 |
| **name**      | プロファイル XML ファイルの名前。 プロファイル データを含む XML ファイルの名前です。     | 必須 |


**例**

```powershell
connect interface="Cellular" connmode=tmp name=d:\profile.xml
connect interface="Cellular" connmode=name name=MyProfileName
```


## <a name="delete"></a>delete

テーブルから構成項目を削除します。

使用できる netsh mbn delete コマンドは次のとおりです。

- [dmprofile](#dmprofile)
- [profile](#profile)

### <a name="dmprofile"></a>dmprofile

プロファイル データ ストアから DM 構成プロファイルを削除します。

**構文**

```powershell
delete dmprofile [interface=]<string> [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |
| **name**      | プロファイル XML ファイルの名前。 プロファイル データを含む XML ファイルの名前です。     | 必須 |

**例**

```powershell
delete dmprofile interface="Cellular" name="myProfileName"
```

### <a name="profile"></a>プロファイル

プロファイル データ ストアからネットワーク プロファイルを削除します。

**構文**

```powershell
delete profile [interface=]<string> [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |
| **name**      | プロファイル XML ファイルの名前。 プロファイル データを含む XML ファイルの名前です。     | 必須 |


**例**

```powershell
delete profile interface="Cellular" name="myProfileName"
```

## <a name="diagnose"></a>diagnose

携帯ネットワークの基本的な問題の診断を実行します。

**構文**

```powershell
diagnose [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
diagnose interface="Cellular"
```


## <a name="disconnect"></a>切断

モバイル ブロードバンド ネットワークから切断します。

**構文**

```powershell
disconnect [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
disconnect interface="Cellular"
```


## <a name="dump"></a>dump

構成スクリプトを表示します。

現在の構成を含むスクリプトを作成します。  ファイルに保存されている場合は、このスクリプトを使用して変更された構成設定を復元できます。

**構文**

```powershell
dump
```

## <a name="help"></a>ヘルプ

コマンドの一覧を表示します。

**構文**

```powershell
help
```

## <a name="set"></a>set

構成情報を設定します。

使用できる netsh mbn set コマンドは次のとおりです。

- [acstate](#acstate)
- [dataenablement](#dataenablement)
- [dataroamcontrol](#dataroamcontrol)
- [enterpriseapnparams](#enterpriseapnparams)
- [highestconncategory](#highestconncategory)
- [powerstate](#powerstate)
- [profileparameter](#profileparameter)
- [slotmapping](#slotmapping)
- [tracing](#tracing)

### <a name="acstate"></a>acstate

特定のインターフェイスに対してモバイル ブロードバンド データの自動接続の状態を設定します。

**構文**

```powershell
set acstate [interface=]<string> [state=]autooff|autoon|manualoff|manualon
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |
| **name**      | 設定する自動接続の状態。 次のいずれかの値です。<br>autooff:自動接続トークン オフ。<br>autoon:自動接続トークン オン。<br>manualoff:手動接続トークン オフ。<br>manualon:手動接続トークン オン。 | 必須 |


**例**

```powershell
set acstate interface="Cellular" state=autoon
```


### <a name="dataenablement"></a>dataenablement

特定のプロファイル セットおよびインターフェイスに対してモバイル ブロードバンド データをオンまたはオフにします。

**構文**

```powershell
set dataenablement [interface=]<string> [profileset=]internet|mms|all [mode=]yes|no
```

**Parameters**

|                |                                                                                               |          |
|----------------|-----------------------------------------------------------------------------------------------|----------|
| **interface**  | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |
| **profileset** | プロファイル セットの名前。                                                                      | 必須 |
| **mode**       | 次のいずれかの値です。<br>yes:対象のプロファイル セットを有効にします。<br>no:対象のプロファイル セットを無効にします。| 必須 |


**例**

```powershell
set dataenablement interface="Cellular" profileset=mms mode=yes
```


### <a name="dataroamcontrol"></a>dataroamcontrol

特定のプロファイル セットおよびインターフェイスに対してモバイル ブロードバンド データのローミング制御の状態を設定します。

**構文**

```powershell
set dataroamcontrol [interface=]<string> [profileset=]internet|mms|all [state=]none|partner|all
```

**Parameters**

|                |                                                                                               |          |
|----------------|-----------------------------------------------------------------------------------------------|----------|
| **interface**  | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |
| **profileset** | プロファイル セットの名前。                                                                      | 必須 |
| **mode**       | 次のいずれかの値です。<br>none:ホーム キャリアのみ。<br>partner:ホームおよびパートナー キャリアのみ。<br>all:ホーム、パートナー、およびローミング キャリア。| 必須 |


**例**

```powershell
set dataroamcontrol interface="Cellular" profileset=mms mode=partner
```


### <a name="enterpriseapnparams"></a>enterpriseapnparams

特定のインターフェイスについてモバイル ブロードバンド データの enterpriseAPN パラメーターを設定します。

**構文**

```powershell
set enterpriseapnparams [interface=]<string> [allowusercontrol=]yes|no|nc [allowuserview=]yes|no|nc [profileaction=]add|delete|modify|nc
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |
| **allowusercontrol** | 次のいずれかの値です。<br>yes: エンド ユーザーに enterpriseAPN の制御を許可します。<br>no: エンド ユーザーに enterpriseAPN の制御を許可しません。<br>nc: 変更なし。 | 必須 |
| **allowuserview** |次のいずれかの値です。<br>yes: エンド ユーザーに enterpriseAPN の表示を許可します。<br>no: エンド ユーザーに enterpriseAPN の表示を許可しません。<br>nc: 変更なし。 | 必須 |
| **profileaction** | 次のいずれかの値です。<br>add: enterpriseAPN プロファイルの追加だけを行います。<br>delete: enterpriseAPN プロファイルの削除だけを行います。<br>modify: enterpriseAPN プロファイルの変更だけを行います。<br>nc: 変更なし。 | 必須 |


**例**

```powershell
set enterpriseapnparams interface="Cellular" profileset=mms mode=yes
```


### <a name="highestconncategory"></a>highestconncategory

特定のインターフェイスについてモバイル ブロードバンド データの最高の接続カテゴリを設定します。

**構文**

```powershell
set highestconncategory [interface=]<string> [highestcc=]admim|user|operator|device
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |
| **highestcc** | 次のいずれかの値です。<br>admin: 管理者がプロビジョニングしたプロファイル。<br>user: ユーザーがプロビジョニングしたプロファイル。<br>operator: オペレーターがプロビジョニングしたプロファイル。<br>device: デバイスがプロビジョニングしたプロファイル。 | 必須 |


**例**

```powershell
set highestconncategory interface="Cellular" highestcc=operator
```


### <a name="powerstate"></a>powerstate

特定のインターフェイスに対してモバイル ブロードバンド無線をオンまたはオフにします。

**構文**

```powershell
set powerstate [interface=]<string> [state=]on|off
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |
| **state**      | 次のいずれかの値です。<br>on: 無線トランシーバーの電源をオンにします。<br>off: 無線トランシーバーの電源をオフにします。 | 必須 |


**例**

```powershell
set powerstate interface="Cellular" state=on
```


### <a name="profileparameter"></a>profileparameter

モバイル ブロードバンド ネットワーク プロファイルにパラメーターを設定します。

**構文**

```powershell
set profileparameter [name=]<string> [[interface=]<string>] [[cost]=default|unrestricted|fixed|variable]
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **name**      | 変更するプロファイルの名前。 インターフェイスを指定した場合は、そのインターフェイスのプロファイルのみが変更されます。 | 必須 |
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | オプション |
| **cost**      | プロファイルに関連付けられたコスト。                                                             | オプション |


**注釈**

インターフェイス名とコストのうち少なくとも 1 つのパラメーターを指定する必要があります。


**例**

```powershell
set profileparameter name="profile 1" cost=default
```


### <a name="slotmapping"></a>slotmapping

特定のインターフェイスに対してモバイル ブロードバンド モデムのスロットのマッピングを設定します。

**構文**

```powershell
set slotmapping [interface=]<string> [slotindex=]<integer>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |
| **slotindex** | 設定するスロット インデックス。                                                                         | 必須 |


**例**

```powershell
set slotmapping interface="Cellular" slotindex=1
```


### <a name="tracing"></a>tracing

トレースを有効または無効にします。

**構文**

```powershell
set tracing [mode=]yes|no
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **mode**      | 次のいずれかの値です。<br>yes:モバイル ブロードバンドのトレースを有効にします。<br>no:モバイル ブロードバンドのトレースを無効にします。     | 必須 |


**例**

```powershell
set tracing mode=yes
```

## <a name="show"></a>show

モバイル ブロードバンド ネットワークの情報を表示します。

使用できる netsh mbn set コマンドは次のとおりです。

- [acstate](#acstate)
- [capability](#capability)
- [connection](#connection)
- [dataenablement](#dataenablement)
- [dataroamcontrol](#dataroamcontrol)
- [dmprofiles](#dmprofiles)
- [enterpriseapnparams](#enterpriseapnparams)
- [highestconncategory](#highestconncategory)
- [homeprovider](#homeprovider)
- [interfaces](#interfaces)
- [netlteattachinfo](#netlteattachinfo)
- [pin](#pin)
- [pinlist](#pinlist)
- [preferredproviders](#preferredproviders)
- [profiles](#profiles)
- [profilestate](#profilestate)
- [provisionedcontexts](#provisionedcontexts)
- [purpose](#purpose)
- [radio](#radio)
- [readyinfo](#readyinfo)
- [signal](#signal)
- [slotmapping](#slotmapping)
- [slotstatus](#slotstatus)
- [smsconfig](#smsconfig)
- [tracing](#tracing)
- [visibleproviders](#visibleproviders)

### <a name="acstate"></a>acstate

特定のインターフェイスについてモバイル ブロードバンド データの自動接続の状態を表示します。

**構文**

```powershell
show acstate [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show acstate interface="Cellular"
```


### <a name="capability"></a>機能

特定のインターフェイスについてインターフェイスの機能の情報を表示します。

**構文**

```powershell
show capability [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show capability interface="Cellular"
```


### <a name="connection"></a>connection

特定のインターフェイスについて現在の接続の情報を表示します。

**構文**

```powershell
show connection [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show connection interface="Cellular"
```


### <a name="dataenablement"></a>dataenablement

特定のインターフェイスについてモバイル ブロードバンド データの有効化の状態を設定します。

**構文**

```powershell
show dataenablement [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show dataenablement interface="Cellular"
```


### <a name="dataroamcontrol"></a>dataroamcontrol

特定のインターフェイスについてモバイル ブロードバンド データのローミング制御の状態を表示します。

**構文**

```powershell
show dataroamcontrol [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show dataroamcontrol interface="Cellular"
```


### <a name="dmprofiles"></a>dmprofiles

システムで構成されている DM 構成プロファイルの一覧を表示します。

**構文**

```powershell
show dmprofiles [[name=]<string>] [[interface=]<string>]
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **name**      | 表示するプロファイルの名前。                                                               | オプション |
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | オプション |

**注釈**

プロファイル データを表示するか、システムのプロファイルを一覧表示します。

プロファイル名を指定すると、そのプロファイルの内容が表示されます。 それ以外の場合は、インターフェイスのプロファイルが一覧表示されます。

インターフェイス名を指定すると、指定したインターフェイス上の指定したプロファイルのみが一覧表示されます。 それ以外の場合は、最初に一致したプロファイルが表示されます。

**例**

```powershell
show dmprofiles name="profile 1" interface="Cellular"
show dmprofiles name="profile 2"
show dmprofiles
```


### <a name="enterpriseapnparams"></a>enterpriseapnparams

特定のインターフェイスについてモバイル ブロードバンド データの enterpriseAPN パラメーターを表示します。

**構文**

```powershell
show enterpriseapnparams [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show enterpriseapnparams interface="Cellular"
```


### <a name="highestconncategory"></a>highestconncategory

特定のインターフェイスについてモバイル ブロードバンド データの最高の接続カテゴリを表示します。

**構文**

```powershell
show highestconncategory [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show highestconncategory interface="Cellular"
```


### <a name="homeprovider"></a>homeprovider

特定のインターフェイスについてホーム プロバイダーの情報を表示します。

**構文**

```powershell
show homeprovider [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show homeprovider interface="Cellular"
```


### <a name="interfaces"></a>interfaces

システム上のモバイル ブロードバンド インターフェイスの一覧を表示します。 このコマンドにパラメーターはありません。

**構文**

```powershell
show interfaces
```


### <a name="netlteattachinfo"></a>netlteattachinfo

特定のインターフェイスについてモバイル ブロードバンド ネットワークの LTE アタッチ情報を表示します。

**構文**

```powershell
show netlteattachinfo [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show netlteattachinfo interface="Cellular"
```

### <a name="pin"></a>pin

特定のインターフェイスについて PIN の情報を表示します。

**構文**

```powershell
show pin [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show pin interface="Cellular"
```


### <a name="pinlist"></a>pinlist

特定のインターフェイスについて PIN 一覧情報を表示します。

**構文**

```powershell
show pinlist [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show pinlist interface="Cellular"
```


### <a name="preferredproviders"></a>preferredproviders

特定のインターフェイスについて優先プロバイダーの一覧を表示します。

**構文**

```powershell
show preferredproviders [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show preferredproviders interface="Cellular"
```


### <a name="profiles"></a>profiles

システムで構成されているプロファイルの一覧を表示します。

**構文**

```powershell
show profiles [[name=]<string>] [[interface=]<string>] [[purpose=]<string>]
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **name**      | 表示するプロファイルの名前。                                                               | オプション |
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | オプション |
| **purpose**   | 目的 | オプション |

**注釈**

プロファイル名を指定すると、そのプロファイルの内容が表示されます。 それ以外の場合は、インターフェイスのプロファイルが一覧表示されます。

インターフェイス名を指定すると、指定したインターフェイス上の指定したプロファイルのみが一覧表示されます。 それ以外の場合は、最初に一致したプロファイルが表示されます。

目的を指定した場合は、目的の GUID が一致するプロファイルのみが表示されます。  それ以外の場合、プロファイルは目的によってフィルター処理されません。  文字列には、中かっこで囲んだ GUID、または internet、supl、mms、ims、allhost のいずれかの文字列を指定できます。

**例**

```powershell
show profiles interface="Cellular" purpose="{00000000-0000-0000-0000-000000000000}"
show profiles name="profile 1" interface="Cellular"
show profiles name="profile 2"
show profiles
```

### <a name="profilestate"></a>profilestate

特定のインターフェイスについてモバイル ブロードバンド プロファイルの状態を表示します。

**構文**

```powershell
show profilestate [interface=]<string> [name=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |
| **name**      | プロファイルの名前。 これは、状態を表示するプロファイルの名前です。            | 必須 |

**例**

```powershell
show profilestate interface="Cellular" name="myProfileName"
```

### <a name="provisionedcontexts"></a>provisionedcontexts

特定のインターフェイスについてプロビジョニングされたコンテキストの情報を表示します。

**構文**

```powershell
show provisionedcontexts [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show provisionedcontexts interface="Cellular"
```


### <a name="purpose"></a>purpose

デバイスのプロファイルをフィルター処理するために使用できる目的グループの GUID を表示します。 このコマンドにパラメーターはありません。

**構文**

```powershell
show purpose
```


### <a name="radio"></a>radio

特定のインターフェイスについて無線の状態の情報を表示します。

**構文**

```powershell
show radio [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show radio interface="Cellular"
```


### <a name="readyinfo"></a>readyinfo

特定のインターフェイスについて準備状態の情報を表示します。

**構文**

```powershell
show readyinfo [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show readyinfo interface="Cellular"
```


### <a name="signal"></a>signal

特定のインターフェイスについてシグナルの情報を表示します。

**構文**

```powershell
show signal [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show signal interface="Cellular"
```


### <a name="slotmapping"></a>slotmapping

特定のインターフェイスについてモバイル ブロードバンド モデムのスロットのマッピングを表示します。

**構文**

```powershell
show slotmapping [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show slotmapping interface="Cellular"
```


### <a name="slotstatus"></a>slotstatus

特定のインターフェイスについてモバイル ブロードバンド モデムのスロットの状態を表示します。

**構文**

```powershell
show slotstatus [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show slotstatus interface="Cellular"
```


### <a name="smsconfig"></a>smsconfig

特定のインターフェイスについて SMS 構成の情報を表示します。

**構文**

```powershell
show smsconfig [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show smsconfig interface="Cellular"
```


### <a name="tracing"></a>tracing

モバイル ブロードバンド トレースが有効か無効かを示します。

**構文**

```powershell
show tracing
```


### <a name="visibleproviders"></a>visibleproviders

特定のインターフェイスの表示可能なプロバイダーの一覧を表示します。

**構文**

```powershell
show visibleproviders [interface=]<string>
```

**Parameters**

|               |                                                                                               |          |
|---------------|-----------------------------------------------------------------------------------------------|----------|
| **interface** | インターフェイス名。 これは、"netsh mbn show interface" コマンドによって表示されるインターフェイス名の 1 つです。 | 必須 |


**例**

```powershell
show visibleproviders interface="Cellular"
```
