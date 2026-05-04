---
title: 통합 프로필 액세스
description: API를 사용하여 통합 프로필에 액세스합니다.
exl-id: c9d2fa2d-9ffe-4e66-996f-ad930bee22c6
TQID: https://experienceleague.adobe.com/ECndsmKpnN3No-PYL0kq0lktWuDK4Z6lFb99i82dK7k
product_v2: id: d0a3eab4-7b10-4d96-a71e-6c0f8e7b7c87
topic_v2: id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 6698ae880d1ad13a9387cb1ba66b9ba152d1d407
workflow-type: tm+mt
source-wordcount: 797
ht-degree: 0%

---

# 프로필 API를 사용하여 통합 프로필에 액세스

Adobe [!DNL Experience Platform]은(는) 고객 프로필에 실시간으로 액세스할 수 있습니다. [[!DNL Experience Platform] 실시간 고객 프로필 API](https://adobe.ly/2TtDHWr)는 이러한 프로필과 상호 작용하도록 설계되었습니다. 프로필 API를 사용하여 실시간 고객 프로필 데이터에 액세스하는 방법은 이 [자습서](https://docs.adobe.com/content/help/en/experience-platform/profile/api/getting-started.html)를 참조하십시오.

이 문서는 위에 연결된 자습서를 실질적으로 참조합니다.

[Postman 컬렉션](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman)은(는) 연결된 번호별 호출을 사용하여 문서 전체에서 참조됩니다. Postman 컬렉션 설치 및 사용에 대한 자세한 내용은 Github [README](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/README.md) 페이지에서 확인할 수 있습니다. 또한 [충성도](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20events.json) 및 [프로필](https://github.com/Adobe-Marketing-Cloud/exchange-aep-profile-integration-postman/blob/master/AEP%20loyalty%20profiles.json) 데이터의 샘플 데이터 세트가 있습니다.

이 섹션의 경우 Postman 폴더 5: 프로필 조회, 5a: 실시간 조회 프로필 데이터 또는 5b: 실시간 조회 이벤트 데이터를 사용합니다.

## API 사용

다음 섹션은 Experience Platform 인증에 도움이 됩니다. API 경로, 헤더 정보 등에 대해 알아봅니다.

### [!DNL Platform] 인증

아래 호출을 수행하기 전에 [이](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html) 인증 자습서를 참조하십시오.

### API 경로

실시간 고객 프로필 API에 필요한 플랫폼 게이트웨이 URL: `https://platform.adobe.io/`

API의 기본 경로는 `/data/core/ups/access/entities`입니다.

전체 경로의 예: `https://platform.adobe.io/data/core/ups/access/entities`

### 헤더 정보

헤더에는 다음이 포함되어야 합니다.

* Authorization
* x-gw-ims-org-id - console.adobe.io를 통해 획득
* x-api-key - console.adobe.io를 통해 가져오기
* x-sandbox-name - Adobe 통합 관리자에서 가져옴
* Content-Type: application/json

헤더에 대해 설명된 자세한 내용은 [자습서](https://adobe.ly/2PTHuKv)를 참조하십시오.

## ID를 사용하여 실시간 고객 프로필에 액세스

프로필 API를 사용하면 GET 요청을 통해 ID를 사용하여 프로필에 액세스할 수 있습니다. 아래 섹션은 이 [안내서](https://docs.adobe.com/content/help/en/experience-platform/profile/api/entities.html)를 따릅니다.

### ID를 사용하여 프로필 데이터 액세스

API는 ID를 사용하여 프로필 정보에 액세스할 수 있도록 합니다. 이 작업은 매개 변수 및 엔티티 ID 네임스페이스 중 하나로 엔티티 ID를 사용하는 /access/entities에 GET 요청을 통해 수행됩니다. 참고: 50개의 레코드를 반환하는 요청은 422 HTTP 상태와 &quot;관련 ID가 너무 많습니다&quot;라는 메시지만 전달하며 더 많은 매개 변수로 검색을 좁혀야 합니다.

요청:

다음 요청은 ID를 사용하여 고객의 이메일과 이름을 검색합니다.

```
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답:

```
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    }
}
```

### ID 목록으로 프로필 액세스

API는 /access/entities 끝점에 대한 POST 요청을 사용하고 페이로드에 ID를 제공하여 ID 목록을 사용하여 프로필에 액세스할 수 있도록 합니다. 이러한 ID는 ID 값(entityId)과 ID 네임스페이스(entityIdNS)로 구성됩니다.

요청:
다음 요청은 ID 목록으로 여러 고객의 이름과 이메일 주소를 검색합니다.

```
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema":{
        "name":"_xdm.context.profile"
    },
    "fields":["identities","person.name","workEmail"],
    "identities":[
        {
            "entityId":"89149270342662559642753730269986316601",
            "entityIdNS":{
                "code":"ECID"
            }
        },
        {
            "entityId":"89149270342662559642753730269986316900",
            "entityIdNS":{
                "code":"ECID"
            }
        },
        {
            "entityId":"89149270342662559642753730269986316602",
            "entityIdNS":{
                "code":"ECID"
            }
        }
    ]
}'
```

응답:
성공적인 응답은 요청 본문에 지정된 엔티티의 요청된 필드를 반환합니다.

```
{
    "A29cgveD5y64ezlhxjUXNzcm": {
        "entityId": "A29cgveD5y64ezlhxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "05DD23564EC4607F0A490D44",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316603",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316700",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316701",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    },
    "A29cgveD5y64e2RixjUXNzcm": {
        "entityId": "A29cgveD5y64e2RixjUXNzcm",
        "sources": [
            ""
        ],
        "entity": {},
        "lastModifiedAt": "1970-01-01T00:00:00Z"
    },
    "A29cgveD5y64ezphxjUXNzcm": {
        "entityId": "A29cgveD5y64ezphxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-27T23:25:52Z"
    }
}
```

## 시계열 이벤트

파트너는 /access/entities 끝점에 대한 GET 요청을 통해 연결된 프로필 엔티티의 ID로 시계열 이벤트에 액세스할 수 있습니다.

### ID별로 프로필에 대한 시계열 이벤트에 액세스

시계열 이벤트는 /access/entities 끝점에 대한 GET 요청을 통해 연결된 프로필 엔티티의 ID에 의해 액세스됩니다. 이 ID는 ID 값(entityId)과 ID 네임스페이스(entityIdNS)로 구성됩니다.

요청:
다음 요청은 ID별로 프로필 엔터티를 찾고 엔터티와 연결된 모든**시계열 이벤트에 대한 속성 endUserID, 웹 및 채널**&#x200B;의 값을 검색합니다.

```
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답:

성공적인 응답은 요청 매개 변수에 지정된 시계열 이벤트 및 관련 필드의 페이지가 매겨진 목록을 반환합니다.

```
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236036",
        "count": 1,
        "next": "c8d11988-6b56-4571-a123-b6ce74236037"
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": 1531260476000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:49:02Z"
        }
    ],
    "_links": {
        "next": {
            "href": "/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1"
        }
    }
}
```

### 프로필의 시계열 이벤트에 대한 페이지 매김

시계열 이벤트를 검색할 때 결과에 페이지가 매겨집니다. 후속 결과 페이지가 있는 경우 응답의 &amp;lowbar;page.next 매개 변수에 ID가 포함됩니다. 또한 응답의 &amp;lowbar;links.next.href 매개 변수는 후속 페이지 검색을 위한 요청 URI를 제공합니다.

요청:

다음 요청은 _links.next.href URI를 요청 경로로 사용하여 결과의 다음 페이지를 검색합니다.

```
curl -X GET \

  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

응답:

성공적인 응답은 다음 결과 페이지를 반환합니다. 이 예에서는 &amp;lowbar;page.next 및 &amp;lowbar;links.next.href의 빈 문자열 값으로 표시되는 대로 후속 결과 페이지가 없는 응답을 보여 줍니다.

```
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236037",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236037",
            "timestamp": 1531260477000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:50:01Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## 참조 문서

* [실시간 고객 프로필 API](https://adobe.ly/2TtDHWr)
* [프로필 API 튜토리얼을 사용하여 실시간 고객 프로필 데이터에 액세스](https://docs.adobe.com/content/help/en/experience-platform/profile/api/getting-started.html)
* [[!DNL Experience Platform] 인증 안내서](https://docs.adobe.com/content/help/en/experience-platform/tutorials/authentication.html)
