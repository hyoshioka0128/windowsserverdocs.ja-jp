---
タイトル: bitsadmin キャッシュと setexpirationtime 説明。"の Windows コマンド」のトピック**bitsadmin キャッシュと setexpirationtime** -キャッシュの有効期限を設定します"。
ms.custom: na ms.prod: windows-server-threshold ms.reviewer: na ms.suite: na ms.technology: manage-windows-commands ms.tgt_pltfrm: na ms.topic: article ms.assetid:00ea6e4e-b707-4b31-88dd-b61a78565c8d author: coreyp-at-msft ms.author: coreyp manager: dongill ms.date:10/16/2017 --

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

# <a name="bitsadmin-cache-and-setexpirationtime"></a>bitsadmin キャッシュと setexpirationtime
キャッシュの有効期限を設定します。
## <a name="syntax"></a>構文
```
bitsadmin /Cache /SetExpirationtime secs
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|秒|キャッシュの有効期限が切れるまでの秒数です。|
## <a name="BKMK_examples"></a>例
次の例では、60 秒でキャッシュを期限が切れます。
```
C:\>bitsadmin /Cache / SetExpirationtime 60
```
## <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](command-line-syntax-key.md)
