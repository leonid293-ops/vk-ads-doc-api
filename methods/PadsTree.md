# PadsTree

> Оригинал: [https://ads.vk.com/doc/api/resource/PadsTree](https://ads.vk.com/doc/api/resource/PadsTree)

---

## /api/v2/pads_trees.json

Ресурс, предоставляющий информацию о деревьях площадок, используемых в таргетинге на места размещений (pads) при создании кампаний. Дерево площадок необходимо для визуализации связи площадок, представленных id в конечных узлах, и физических мест размещений, представленных во внутренних узлах дерева.

Используется объект: [PadsTree](../object/PadsTree)

### GET

Пример запроса:

```HTTP

   GET /api/v2/pads_trees.json
```

Пример ответа:

```HTTP

    {
        "items": [
          {
            "tree": [
              {
                "name": "Desktop",
                "children": [
                  {
                    "name": "MRG",
                    "children": [
                      {
                        "id": 76765
                      },
                      {
                        "id": 76766
                      },
                      {
                        "id": 76767
                      }
                    ]
                  },
                  {
                    "id": 76878
                  }
                ]
              },
              {
                "name": "Mobile",
                "children": [
                  {
                    "name": "MRG",
                    "children": [
                      {
                        "id": 76879
                      },
                      {
                        "id": 76880
                      },
                      {
                        "id": 76881
                      }
                    ]
                  },
                  {
                    "id": 76882
                  }
                ]
              }
            ],
            "id": 393
          },
          {
            "tree": [
              {
                "name": "Desktop",
                "children": [
                  {
                    "name": "MRG",
                    "children": [
                      {
                        "id": 76920
                      },
                      {
                        "id": 76921
                      },
                      {
                        "id": 76922
                      }
                    ]
                  },
                  {
                    "id": 76923
                  }
                ]
              },
              {
                "name": "Mobile",
                "children": [
                  {
                    "name": "MRG",
                    "children": [
                      {
                        "id": 76924
                      },
                      {
                        "id": 76925
                      },
                      {
                        "id": 76926
                      }
                    ]
                  },
                  {
                    "id": 76927
                  }
                ]
              }
            ],
            "id": 396
          },
        ]
   }
```