## Features

- [x] Dependency injection with singletons and factories
- [x] Scope system
- [x] Dependency injection with qualifiers
- [x] Module System

## Getting started

### Installation



## Usage

First is necessary to create a class that extends from `Module` and override the `onProvide` method. Inside this method you can use the `provide` method to register your dependencies.

```dart
class NetworkingDiModule extends Module {
  NetworkingDiModule(super.scopedState);

  @override
  void onProvide() {
    provide(() {
      final dio = Dio(
        BaseOptions(
            baseUrl: baseUrl,
            connectTimeout: const Duration(seconds: 5),
            receiveTimeout: const Duration(seconds: 5)),
      );
      dio.interceptors.add(JwtInterceptor(inject()));
      return dio;
    });

    // Services
    provide(() => UserService(inject()));
    provide(() => ProjectService(inject()));
    provide(() => ExpenseService(inject()));
    provide(() => PaymentService(inject()));
    provide(() => LogService(inject()));
  }
}
```

## Additional information

