---
title: tracerpt
description: Windows コマンドに関するトピックでは、イベントトレースログ、パフォーマンスモニターによって生成されるログファイル、およびリアルタイムのイベントトレースプロバイダーを解析します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cb9eaf86-0ef6-4197-b6c8-9cca8a1d723c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 17bed5b1cb084392ed3169ca963ce03c1ee2b0d2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832685"
---
# <a name="tracerpt"></a>tracerpt

**Tracerpt**コマンドを使用すると、イベントトレースログ、パフォーマンスモニターによって生成されるログファイル、およびリアルタイムのイベントトレースプロバイダーを解析できます。 ダンプファイル、レポートファイル、およびレポートスキーマが生成されます。

**Tracerpt**の使用方法の例については、「[例](#BKMK_EXAMPLES)」を参照してください。

## <a name="syntax"></a>構文

```
tracerpt <[-l] <value [value [...]]>|-rt <session_name [session_name [...]]>> [options]
```

## <a name="options"></a>オプション

|              オプションフラグ               |                                                                    説明                                                                    |
|----------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
|                   -?                   |                                                         状況依存のヘルプを表示します。                                                          |
|          -config \<ファイル名 >           |                                                 コマンドオプションを含む設定ファイルを読み込みます。                                                  |
|                   -y                   |                                                  確認を求めずにすべての質問に対して [はい] を回答します。                                                   |
|            -f \<XML\|HTML >             |                                                                  レポート形式。                                                                   |
|         -\<CSV\|.EVTX\|XML >          |                                                         ダンプ形式、既定値は XML です。                                                          |
|            -df \<ファイル名 >             |                                            Microsoft 固有のカウント/レポートスキーマファイルを作成します。                                            |
|            -int \<ファイル名 >            |                                            解釈されたイベント構造体を、指定したファイルにダンプします。                                            |
|                  -rts                  |                        イベントトレースヘッダーに生のタイムスタンプを報告します。 使用できるのは-o、not report、-summary だけです。                         |
|            -tmf \<ファイル名 >            |                                                  トレースメッセージ形式の定義ファイルを指定します。                                                  |
|              -tp \<値 >              |                            TMF ファイルの検索パスを指定します。 セミコロン (;) で区切られた複数のパスを使用できます。                            |
|              -i \<値 >               | プロバイダーイメージのパスを指定します。 一致する PDB は、シンボルサーバーに配置されます。 複数のパスを使用して、セミコロン (;) で区切ることができます。 |
|             -pdb \<値 >              |                             シンボルサーバーのパスを指定します。 複数のパスを使用して、セミコロン (;) で区切ることができます。                             |
|                  -gmt                  |                                              WPP ペイロードのタイムスタンプをグリニッジ標準時に変換します。                                               |
|              -rl \<値 >              |                                               1 ~ 5 のシステムレポートレベルを定義します。 既定値は 1 です。                                               |
|          -summary [ファイル名]           |                                  概要レポートのテキストファイルを生成します。 ファイル名が指定されていない場合は、summary.txt です。                                   |
|             -o [ファイル名]              |                                      テキスト出力ファイルを生成します。 指定されていない場合のファイル名はダンプファイルです。                                      |
|           -レポート [ファイル名]           |                                  テキスト出力レポートファイルを生成します。 ファイル名が指定されていない場合、ワークロード .xml です。                                   |
|                  -lr                   |                        制限の緩い値を指定します。 これは、events スキーマに一致しないイベントに対して最適な作業を行います。                         |
|           -export [ファイル名]           |                                  イベントスキーマエクスポートファイルを生成します。 指定されていない場合、ファイル名は schema. man です。                                   |
|       [-l] \<値 [...]]>        |                                                   処理するイベントトレースログファイルを指定します。                                                    |
| -rt \<session_name [session_name [...]]> |                                                リアルタイムイベントトレースセッションのデータソースを指定します。                                                |

## <a name="examples"></a><a name=BKMK_EXAMPLES></a>例

- この例では、 **logfile1**と**logfile2**という2つのイベントログに基づいてレポートを作成し、ダンプファイル**logdump** .xml を xml 形式で作成します。  
  ```
  tracerpt logfile1.etl logfile2.etl -o logdump.xml -of XML
  ```  
- この例では、イベントログの**ログ**ファイルに基づいてレポートを作成し、ダンプファイル**LOGDMP .xml**を xml 形式で作成します。また、スキーマに含まれていないイベントを特定するのに最適な方法を使用して、概要レポートファイル**logdmp .txt**を生成し、レポートファイル**logrpt .xml**を生成します。  
  ```
  tracerpt logfile.etl -o logdmp.xml -of XML -lr -summary logdmp.txt -report logrpt.xml
  ```  
- この例では、 **logfile1**と**logfile2**という2つのイベントログを使用して、既定のファイル名を持つダンプファイルとレポートファイルを生成します。  
  ```
  tracerpt logfile1.etl logfile2.etl -o -report
  ```  
- この例では、イベントログ**logfile**とパフォーマンスログ**counterfile**を使用して、レポートファイル**Logrpt .XML**および Microsoft 固有の xml スキーマファイル**スキーマ**を生成します。  
  ```
  tracerpt logfile.etl counterfile.blg -report logrpt.xml -df schema.xml
  ```  
- この例では、リアルタイムイベントトレースセッション NT カーネルロガーを読み取り、CSV 形式でダンプファイル**logfile**を生成します。  
  ```
  tracerpt -rt NT Kernel Logger -o logfile.csv -of CSV
  ```
