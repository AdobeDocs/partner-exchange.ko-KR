---
title: 실시간 가져오기
description: 실시간으로 AEP으로 데이터를 가져오는 방법을 알아봅니다.
exl-id: 0b6215a9-1160-49ae-8aa5-302b47357200
TQID: https://experienceleague.adobe.com/GvWcwNPjQdmdKSUkwvJ2EpoCKJHGvf5c1Kn4dwWRVi8
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
source-git-commit: 6698ae880d1ad13a9387cb1ba66b9ba152d1d407
workflow-type: tm+mt
source-wordcount: 642
ht-degree: 4%

---

# AEP에 데이터 스트리밍

Adobe [!DNL Experience Platform]을(를) 사용하면 프로필 및 경험 이벤트를 거의 실시간으로 스트리밍하고 사용할 수 있습니다. 스트리밍을 통해 AEP으로 전송되는 모든 데이터는 데이터 레이크에서 유지됩니다. 데이터는 API를 통해 또는 Adobe Launch를 사용하여 기존 데이터 세트 또는 완전히 새로운 데이터 세트로 스트리밍할 수 있습니다.

이 문서에서는 다음 내용을 다룹니다.

* XDM 개별 프로필로 스트리밍
* XDM ExperienceEvent로 스트리밍
* AEP을 사용하여 Launch 확장 스트리밍

[Postman 컬렉션](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman)은(는) 연결된 번호별 호출을 사용하여 문서 전체에서 참조됩니다. Postman 컬렉션 설치 및 사용에 대한 자세한 내용은 Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) 페이지에서 확인할 수 있습니다. 또한 [충성도](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) 및 [프로필](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) 데이터의 샘플 데이터 세트가 있습니다.

## 전제 조건

* [플랫폼에 인증](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html).
* 위에 연결된 인증 자습서에서 필수 헤더에 대한 값을 수집합니다.

## 스트리밍 연결 만들기

AEP으로 스트리밍하려면 먼저 스트리밍 연결을 만들어야 합니다. 스트리밍 연결에는 스트리밍 데이터 원본 및 [!DNL Experience Data Model]&#x200B;(XDM) 스키마에 속하는 레코드를 전송하는지 여부와 같은 특성이 포함되어 있습니다. 스트리밍 연결을 만들면 AEP으로 데이터를 스트리밍하는 데 사용하는 고유한 URL이 제공됩니다.

API를 통해 스트리밍 연결을 만드는 방법에 대한 지침은 [여기](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/create-streaming-connection.html)로, UI를 통해 스트리밍 연결을 만드는 방법은 [여기](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/create-streaming-connection-ui.html)로 이동하십시오.

```json
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }
```

응답:

```json
 {
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

향후 스트리밍 수집 호출을 위해 위의 응답에 제공된 ID를 저장해야 합니다(Postman 컬렉션은 이 ID를 CONNECTION_ID 환경 변수에 저장합니다).

## AEP에 프로필 데이터 스트리밍

이 섹션의 경우 Postman 호출 폴더를 사용하십시오. 3: 실시간 가져오기, 3a: 프로필 데이터에 대한 실시간 가져오기.

스트리밍 프로필 데이터에 대한 응답이 포함된 자세한 JSON 요청은 [여기](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/streaming-record-data.html)에 설명되어 있습니다.

단계:

1. XDM 개별 프로필 스키마 만들기
1. XDM 개별 프로필에 대한 기본 ID 설명자 설정(기본 키)
1. XDM 개별 프로필 레코드에 대한 데이터 세트 만들기
1. 스트리밍 수집 API를 호출하여 XDM 개별 프로필 레코드 만들기
1. 새로 생성된 프로필 검색

## AEP에 경험 이벤트 스트리밍

이 섹션의 경우 Postman 호출 폴더를 사용하십시오. 3: 실시간 가져오기, 3b: 프로필 데이터에 대한 실시간 가져오기.

스트리밍 경험 데이터에 대한 응답이 포함된 자세한 JSON 요청은 [여기](https://docs.adobe.com/content/help/en/experience-platform/ingestion/tutorials/streaming-time-series-data.html)에 설명되어 있습니다.

단계:

1. XDM ExperienceEvent 스키마 만들기
1. XDM ExperienceEvent(기본 키)에 대한 기본 ID 설명자 설정
1. XDM ExperienceEvents에 대한 데이터 세트 만들기
1. 스트리밍 수집 API를 호출하여 XDM ExperienceEvent를 만듭니다
1. 새로 생성된 이벤트 검색

## Experience Platform 태그를 사용하여 AEP으로 스트리밍

Adobe [!DNL Experience Platform] Launch 확장은 Launch를 통해 AEP으로 스트리밍하는 방법을 제공합니다. 자세한 내용은 [이 안내서](https://docs.adobe.com/content/help/ko/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)를 참조하세요.

## 참조 문서

* [데이터 수집 API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#/acpdr/swagger-specs)
* [스트리밍 수집 개요](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/streaming_ingest_overview.md)
* [스트리밍 수집 개발자 안내서](https://www.adobe.io/apis/experienceplatform/home/data-ingestion/data-ingestion-services.html#!api-specification/markdown/narrative/technical_overview/streaming_ingest/getting_started_with_platform_streaming_ingestion.md)
* [AEP Launch 확장 사용](https://docs.adobe.com/content/help/ko/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html)
