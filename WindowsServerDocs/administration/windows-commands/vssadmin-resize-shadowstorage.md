---
title: Vssadmin resize shadowstorage
description: Vssadmin resize shadowstorage コマンドの説明です。
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 03/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8cd3b5e5629e41702126fb42b815931ff0aea6fa
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830025"
---
# <a name="vssadmin-resize-shadowstorage"></a>Vssadmin resize shadowstorage

>適用対象: Windows 10、Windows 8.1、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008

シャドウコピーの記憶域に使用できる記憶域の最大容量のサイズを変更します。

シャドウコピー記憶域に使用できる記憶域の最小容量は、 **Mindiffgram**のレジストリ値を使用して指定できます。 詳細については、「 [Mindiffgram](https://docs.microsoft.com/windows/win32/backup/registry-keys-for-backup-and-restore#mindiffareafilesize)」を参照してください。

> [!WARNING]
> 記憶域の関連付けのサイズを変更すると、シャドウコピーが消失する可能性があります。

## <a name="syntax"></a>構文

```cmd
vssadmin resize shadowstorage /for=<ForVolumeSpec> /on=<OnVolumeSpec> [/maxsize=<MaxSizeSpec>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---|---|
`/for=<ForVolumeSpec>`  | ストレージ領域の最大サイズを変更するボリュームを指定します。
`/on=<OnVolumeSpec>` | 記憶域ボリュームを指定します。
`[/maxsize=<MaxSizeSpec>]` |  シャドウコピーの格納に使用できる領域の最大サイズを指定します。 /Maxsize に値が指定されていない場合、使用できるストレージ領域の量に制限はありません。  <br> <br> MaxSizeSpec 値は 1 MB 以上である必要があり、KB、MB、GB、TB、PB、EB のいずれかの単位で表す必要があります。 単位が指定されていない場合、MaxSizeSpec は既定でバイトを使用します。

## <a name="examples"></a>例

```cmd
vssadmin Resize ShadowStorage /For=C: /On=D: /MaxSize=900MB
vssadmin Resize ShadowStorage /For=C: /On=D: /MaxSize=UNBOUNDED
vssadmin Resize ShadowStorage /For=C: /On=C: /MaxSize=20%
```

## <a name="additional-references"></a>その他の参照情報

* [コマンドライン構文のキー](https://docs.microsoft.com/windows-server/administration/windows-commands/command-line-syntax-key)
* [Vssadmin](vssadmin.md)
