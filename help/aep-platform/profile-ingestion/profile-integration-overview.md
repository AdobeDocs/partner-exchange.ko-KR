---
title: '[!DNL Platform] 프로필 수집 및 액세스 통합 안내서 개요'
description: ' [!DNL Experience Platform] 프로필 수집 및 액세스 통합에 대해 알아봅니다.'
exl-id: a593511c-dd4c-4437-af73-f44d795cacb8
TQID: https://experienceleague.adobe.com/whnqurJyM4QXl5ikRvez7hpKWRDuU4onzROsUk-WeSI
product_v2:
  - id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: 6698ae880d1ad13a9387cb1ba66b9ba152d1d407
workflow-type: tm+mt
source-wordcount: 492
ht-degree: 1%

---

# 통합 안내서: [!DNL Experience Platform] 프로필 수집 및 액세스

파트너는 이 통합 안내서를 사용하여 Adobe [!DNL Experience Platform]&#x200B;(AEP)에서 수신 및 송신 기능을 빌드하도록 지원해야 합니다. 일괄 처리 수집, 스트리밍 수집 및 통합 프로필 액세스(이그레스)를 위한 API가 있습니다.

개발을 지원하기 위해 Adobe Exchange 팀에서 [Postman 컬렉션](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman)을 만들었습니다. 이 Postman 컬렉션은 통합 안내서 전체에서 참조됩니다.

Postman 컬렉션 설치 및 사용에 대한 자세한 내용은 Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) 페이지에서 확인할 수 있습니다. 또한 [충성도](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) 및 [프로필](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) 데이터의 샘플 데이터 세트가 있습니다.

## 통합 사용 사례 예: 대화형 음성 응답 시스템

통합자의 경우 [!DNL Experience Platform] API는 사용자 인터페이스 전체에서 제공되는 플랫폼의 모든 기능을 제공하지만 지금은 고객 워크플로우 및 자동화된 데이터 흐름을 만들 수 있습니다. 통합자는 데이터 세트의 상태를 정기적으로 확인하고, 새로운 데이터 수집 절차를 설정하고, 고유한 대상 활성화 솔루션을 통합 프로필과 통합합니다.

IVR(Interactive Voice Response) 시스템 및 콜 센터 관리 소프트웨어의 세계를 고려하십시오. 공급업체는 [!DNL Experience Platform] API를 사용하여 고객 콜센터 활동의 내역 정보를 Experience Data Lake에서 수집할 수 있습니다. 데이터를 XDM `ExperienceEvent` 스키마(고객 상호 작용을 표현하는 스키마)로 수집하는 경우 통합 프로필 서비스에 직접 마찰 없이 이러한 상호 작용을 수집할 수 있습니다. 이 경우 `callerId`은(는) 고객의 식별자로 사용됩니다. ID 서비스는 ID 확인을 처리하고 통합 프로필 서비스가 콜센터와의 최근 상호 작용에서 고객 프로필에 데이터 포인트를 추가할 수 있도록 지원합니다.

다음 번에 고객이 콜센터에 전화하면 먼저 IVR에서 응답을 받게 됩니다. 메시지를 개인화하고 발신자에게 맞춘 오퍼를 게재하려면 IVR 시스템이 발신자에 대해 더 많이 이해해야 합니다. 여기에서 통합 프로필과의 API 통합이 제공됩니다. IVR 백엔드는 포인트 조회를 위해 통합 프로필 서비스에 문의할 수 있습니다. 그런 다음 콜 센터 상호 작용에만 적용되는 프로필 속성이나 다른 터치포인트에서의 상호 작용에 대한 속성이 있는 전체 고객 프로필을 참조하십시오. ID 확인 및 통합 프로필을 사용하여 여러 데이터 소스의 데이터를 결합하면 콜 센터와 IVR 공급자가 Adobe [!DNL Experience Platform]에서 지원하는 맞춤 고객 경험을 제공할 수 있습니다.&quot;

## 일반 리소스

* AEP [제품 설명서](https://docs.adobe.com/content/help/ko-KR/experience-platform/landing/documentation/overview.html).
* AEP [확장성](https://www.adobe.com/insights/experience-platform-api-extensibility.html).

## 질문 또는 피드백

[지원 채널](https://adobeexchangeec.zendesk.com/hc/en-us/requests/new)을 통해 모든 질문과 피드백을 제출하세요.
