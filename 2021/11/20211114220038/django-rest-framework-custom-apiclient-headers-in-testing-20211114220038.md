---
path: '/2021/11/django-rest-framework-custom-apiclient-headers-in-testing-20211114220038'
title: 'django rest framework custom APIClient headers in testing'
date: '20211114220038'
category: 'django'
tags: ['django rest framework', 'TDD', 'python']
---

# django rest framework custom APIClient headers in testing
Working in DRF has quite a few advantages; however, I found that when testing
with their built-in `APIClient` it needed to have some custom headers.

These headers were for an API-key authorization that I was utilizing instead of
the built-in session/token auth.

**Note:** Because I was doing this on a per-view basis I needed to have some
control over injecting this header.

To append a header to the `APIClient` request we take advantage of the `credentials`
method. I've mocked a quick example below.

Here we can see that I am appending the credentials under a `Authorization` header
that Django Rest Framework will parse from `HTTP_AUTHORIZATION` in the client
headers.

```python

class TestEndpoints():

    endpoint = "api/something/"

    def some_test(self):
        # Arrange
        data = {
            "some_data": 1,
        }

        # Mock
        client = APIClient()
        client.credentials(
            HTTP_AUTHORIZATION=f"Api-Key {my_api_key}",
        )

        # Act
        response = client.get(
            path=self.endpoint,
            data=data,
            format="json",
        )

        # Assert
        assert response.status_code == 200
```

