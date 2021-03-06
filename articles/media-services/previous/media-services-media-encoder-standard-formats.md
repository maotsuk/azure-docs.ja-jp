---
title: Media Encoder Standard の形式とコーデック
description: このトピックでは、Media Encoder Standard の形式とコーデックの概要を示します。
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: f334b1ce-2f56-4968-a019-f0a2b0016d9f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako;anilmur
ms.openlocfilehash: 5e71714f94cf148895585e8de88eaf995f0791fb
ms.sourcegitcommit: e221d1a2e0fb245610a6dd886e7e74c362f06467
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2018
---
# <a name="media-encoder-standard-formats-and-codecs"></a>Media Encoder Standard の形式とコーデック
このドキュメントでは、Media Encoder Standard で使用できる一般的なインポートおよびエクスポート ファイル形式の一覧を示しています。

## <a name="input-containerfile-formats"></a>入力コンテナー/ファイル形式
| ファイル形式 (ファイル拡張子) | サポートされています |
| --- | --- | --- | --- |
| (H.264 および AAC コーデックでの) FLV (.flv) |[はい] |
| MXF    (.mxf) |[はい] |
| GXF    (.gxf) |[はい] |
| MPEG2-PS、MPEG2-TS、3GP (.ts、.ps、.3gp、.3gpp、.mpg) |[はい] |
| Windows Media Video (WMV)/ASF (.wmv、.asf) |[はい] |
| AVI (非圧縮 8-bit/10-bit) (.avi) |[はい] |
| MP4 (.mp4、.m4a、.m4v)/ISMV (.isma、.ismv) |[はい] |
| [Microsoft Digital Video Recording (DVR-MS)](https://msdn.microsoft.com/library/windows/desktop/dd692984) (.dvr-ms) |[はい] |
| Matroska/WebM (.mkv) |[はい] |
| WAVE/WAV (.wav) |[はい] |
| QuickTime (.mov) |[はい] |

> [!NOTE]
> 上に記載したのは、ごく一般的なファイル拡張子の一覧です。 Media Encoder Standard は他にもさまざまな拡張子をサポートしています (例: .m2ts、.mpeg2video、.qt)。 ファイルをエンコードしようとしたときに、ファイル形式がサポートされていないことに関するエラー メッセージが表示された場合は、[こちら](https://feedback.azure.com/forums/169396-media-services/category/144411-encoding-and-processing/)からフィードバックをお寄せください。
> 
> 

### <a name="audio-formats-in-input-containers"></a>入力コンテナーのオーディオ形式
Media Encoder Standard の入力コンテナーは次のオーディオ形式に対応しています。

* オーディオ トラックにインターリーブ ステレオまたは 5.1 サンプルが含まれる MXF、GXF、QuickTime ファイル

or

* オーディオが個別 PCM トラックとして送信されるが、(ステレオまたは 5.1 への) チャネル マッピングをファイル メタデータから推測できる MXF、GXF、QuickTime ファイル

明示的/ユーザー指定のチャネル マッピングが近い将来にサポートされる予定です。

## <a name="input-video-codecs"></a>入力ビデオ コーデック
| 入力ビデオ コーデック | サポートされています |
| --- | --- | --- | --- |
| AVC 8-bit/10-bit、最大 4:2:2 (AVCIntra を含む) |8 ビット 4:2:0 および 4:2:2 |
| Avid DNxHD (MXF) |[はい] |
| DVCPro/DVCProHD (MXF) |[はい] |
| デジタル ビデオ (DV) (AVI ファイルで) |[はい] |
| JPEG 2000 |[はい] |
| MPEG-2 (XDCAM、XDCAM HD、XDCAM IMX、CableLabs®、D10 など、最大 422 プロファイルおよびハイ レベル) |最大 422 プロファイル |
| MPEG-1 |[はい] |
| VC-1/WMV9 |[はい] |
| Canopus HQ/HQX |いいえ  |
| MPEG-4 Part 2 |[はい] |
| [Theora](https://en.wikipedia.org/wiki/Theora) |[はい] |
| YUV420 非圧縮または中間 |[はい] |
| Apple ProRes 422 |[はい] |
| Apple ProRes 422 LT |[はい] |
| Apple ProRes 422 HQ |[はい] |
| Apple ProRes プロキシ |[はい] |
| Apple ProRes 4444 |[はい] |
| Apple ProRes 4444 XQ |[はい] |

## <a name="input-audio-codecs"></a>入力オーディオ コーデック
| 入力オーディオ コーデック | サポートされています |
| --- | --- | --- | --- |
| AAC (AAC-LC、AAC-HE、AAC-HEv2。最大 5.1) |[はい] |
| MPEG Layer 2 |[はい] |
| MP3 (MPEG-1 Audio Layer 3) |[はい] |
| Windows Media オーディオ |[はい] |
| WAV/PCM |[はい] |
| [FLAC](https://en.wikipedia.org/wiki/FLAC)</a> |[はい] |
| [Opus](http://go.microsoft.com/fwlink/?LinkId=822667) |[はい] |
| [Vorbis](https://en.wikipedia.org/wiki/Vorbis)</a> |[はい] |
| AMR (アダプティブ マルチ レート) |[はい] |
| AES (SMPTE 331M および 302M、AES3-2003) |いいえ  |
| Dolby® E |いいえ  |
| Dolby® Digital (AC3) |いいえ  |
| Dolby® Digital Plus (E-AC3) |いいえ  |

## <a name="output-formats-and-codecs"></a>出力形式とコーデック
次の表では、エクスポートでサポートされるコーデックおよびファイル形式の一覧を示します。

| ファイル形式 | ビデオ コーデック | オーディオ コーデック |
| --- | --- | --- |
| MP4  <br/><br/>(マルチビットレートの MP4 コンテナーを含む) |H.264 (High、Main、Baseline Profile) |AAC-LC、HE-AAC v1、HE-AAC v2 |
| MPEG2-TS |H.264 (High、Main、Baseline Profile) |AAC-LC、HE-AAC v1、HE-AAC v2 |

## <a name="media-services-learning-paths"></a>Media Services のラーニング パス
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>フィードバックの提供
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="see-also"></a>関連項目
[Azure Media Services を使用してオンデマンド コンテンツをエンコードする](media-services-encode-asset.md)

[メディア エンコーダー スタンダードを使用したエンコード方法](media-services-dotnet-encode-with-media-encoder-standard.md)

