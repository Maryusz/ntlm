# NTLM

A library for NTLM authentication in Dart/Flutter.

## Installing

Add the dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  ntlm: ^1.0.2
```

## Example

```dart
import 'package:ntlm/ntlm.dart';

main() {
  NTLMClient client = new NTLMClient(
    domain: "",
    workstation: "LAPTOP",
    username: "User208",
    password: "password",
  );

  client.get("https://example.com/").then((res) {
    print(res.body);
  });
}
```

You can also pre-hash the password and use those results instead:

```dart
String lmPassword = lmHash("password");
String ntPassword = ntHash("password");

NTLMClient client = new NTLMClient(
  domain: "",
  workstation: "LAPTOP",
  username: "User208",
  lmPassword: lmPassword,
  ntPassword: ntPassword,
);
```

## Flutter Web Support

For cross-origin requests, make sure your server includes the following header in responses:

```
Access-Control-Expose-Headers: WWW-Authenticate
```

This allows the package to view NTLM messages sent by the server.

## Acknowledgements

Created from templates made available by Stagehand under a BSD-style
[license](https://github.com/dart-lang/stagehand/blob/master/LICENSE).

The DES code is a port of
[Bouncy Castle's DES Engine](https://github.com/bcgit/bc-java/blob/master/core/src/main/java/org/bouncycastle/crypto/engines/DESEngine.java).

Most of the NTLM response creation code is a port of [SamDecrock/node-http-ntlm](https://github.com/SamDecrock/node-http-ntlm)
which itself is a port of [mullender/python-ntlm](https://github.com/mullender/python-ntlm).

Password hashing functions for the type 3 message are ports of the Java code on
[this](http://davenport.sourceforge.net/ntlm.html#appendixD) page.