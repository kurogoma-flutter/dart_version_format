## dart_version_format
アプリバージョンを比較するメソッド

https://qiita.com/kurogoma939/items/87628b735b10fbccb34a


### コード
```dart
void main() {
  
  String version = '8.1';
  String version2 = '12.20.11';
  
  int appVersion = formatVersionNumber(version);
  int deviceVersion = formatVersionNumber(version2);
  
  print('appVersion $appVersion'); // appVersion 80100
  print('deviceVersion $deviceVersion'); // deviceVersion 122011
  
  final result = compareVersionNumber(baseVersion: '8.0', targetVersion:'8.1');
  print(result);
}

/// ピリオド区切りなどの数字を整数6桁に変換する
int formatVersionNumber(String version) {
  // 集計用変数
  String tempValue = '';
  // ピリオドで分割する
  final List<String> versionNumbers = version.split('.');
  // 配列の個数で識別
  // ex.) version 15 => '150000' => 150000
  if (versionNumbers.length == 1) {
    tempValue = versionNumbers.first.padRight(6, '0');
  }

  // ex.) version 8.5 => '080500' => 800500
  if (versionNumbers.length == 2) {
    versionNumbers.asMap().forEach((int index, String value) {
      tempValue += value.padLeft(2, '0');
    });
    tempValue = tempValue.padRight(6, '0');
  }

  // ex.) version 1.0.1 => '010001' => 10001
  if (versionNumbers.length == 3) {
    versionNumbers.asMap().forEach((int index, String value) {
      tempValue += value.padLeft(2, '0');
    });
  }

  return int.parse(tempValue);
}

/// フォーマット関数を使って実際比較に使うメソッド
bool compareVersionNumber({
  required String baseVersion,
  required String targetVersion,
}) {
  return formatVersionNumber(targetVersion) >=
      formatVersionNumber(baseVersion);
}
```
