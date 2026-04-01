# AuditPixelCheck

> Оригинал: [https://ads.vk.com/doc/api/resource/AuditPixelCheck](https://ads.vk.com/doc/api/resource/AuditPixelCheck)

---

## /api/v3/audit_pixel.json

Ресурс, позволяющий проверить валидность пикселя и узнать о том, какие пиксели можно сгенерировать на его основе

### POST

Пример запроса:

```HTTP

   POST /api/v3/audit_pixel.json?fields=audit_pixel,generated_audit_pixels

    {
        "audit_pixel": "https://top-fwz1.mail.ru/tracker?id=2930776;e=RG%3A/trg-pixel-2812993-1507041739095",
    }
```

Пример ответа:

```HTTP

    {
        "audit_pixel": "https://top-fwz1.mail.ru/tracker?id=2930776;e=RG%3A/trg-pixel-2812993-1507041739095",
        "generated_audit_pixels": [
            {
                "audit_pixel": "https://top-fwz1.mail.ru/tracker?id=2930776;e=RG%3A/trg-pixel-2812993-1507041739095&role=impression",
                "role": "impression"
            },
            {
                "audit_pixel": "https://top-fwz1.mail.ru/tracker?id=2930776;e=RG%3A/trg-pixel-2812993-1507041739095&role=playheadReachedValue50",
                "role": "playheadReachedValue50"
            }
        ]
    }
```

Возвращаемые коды статуса:

- 200 - Пиксель валиден.
- 400 - Ошибка валидации.

Пример ответа в случае ошибки валидации переданного пискселя:

```HTTP

    {
        "error": {
            "code": "validation_failed",
            "message": "Validation failed",
            "fields": {
                "audit_pixel": {
                    "code": "invalid_audit_pixel",
                    "message": "Audit pixel is invalid"
                }
            }
        }
    }
```

Пример ответа в случае передачи некорректного значения пикселя:

```HTTP

    {
        "error": {
            "code": "validation_failed",
            "message": "Validation failed",
            "fields": {
                "audit_pixel": {
                    "code": "bad_value",
                    "message": "Bad value",
                    "expected": "URL"
                }
            }
        }
    }
```

Пример ответа в случае передачи параметров в некорректном виде:

```HTTP

    {
        "error": {
            "code": "validation_failed",
            "message": "Validation failed",
            "fields": {
                "code": "object_required",
                "message": "Resource data must be an object",
            }
        }
    }
```

Пример ответа в случае ошибки на стороне сервера:

```HTTP

    {
        "error": {
            "message": "Remote service error"
            "code": "audit_pixel_service_error"
        }
    }
```