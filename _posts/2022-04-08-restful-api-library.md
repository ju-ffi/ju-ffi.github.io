---
layout: post
author: Ju Heesong
tags: [restfulapi, project, portfolio]
---

# Restful API를 활용한 디지털 라이브러리 프로그램

본 프로그램은 실험을 통해 수집한 데이터를 서버에 저장하고 모니터링하며 데이터 관리 기능을 수행하는 web기반의 디지털라이브러리 프로그램으로 Flutter를 활용하여 구현하였다.


## 주요기능

- 실험데이터 DB관리 기능
- 각 실험 물질별 데이터 특징 및 구조도 명시
- 데이터별로 그래프 시각화

사용방법:

1. 서버에서 동작하고 있으며, web 주소로 접근 가능
2. 첫 web 실행 화면에 각 실험 물질이 카드형식으로 나타남
3. 물질 카드를 클릭하면 해당 물질에 대한 상세 내용 확인 가능
4. Data Info는 해당 물질의 화학적 특성으로 서버에서 get한 데이터이며, 오른쪽 상단의 연필모양 아이콘으로 수정 가능
5. Data File은 서버에 업로드된 데이터 목록을 나타내며, 오른쪽 상단 + 아이콘을 클릭하여 서버에 파일을 추가 업로드 및 쓰레기통 아이콘으로 서버에서 삭제 가능
6. Ion Mobility Spectrometry는 각 물질 데이터를 그래프로 시각화한 것으로 Data File에서 원하는 파일을 클릭했을 때 실시간으로 확인 가능


## 구현 및 코드 설명
(본 코드는 프로젝트 유출금지로 일부의 코드만 변형 및 기재하였습니다.)

- web 실행화면

1. 카드형식으로 물질의 이미지와 함께 정보를 나타냈으며 드래그를 이용해 원하는 물질 목록 확인
 - flutter의 ScrollBehavior를 활용, web 프로그램이므로 touch와 mouse에 반응하도록 설정

![theme logo](http://ju-ffi.github.io/assets/images/favicon/P1실행화면.PNG)

Now some code:

```javascript
class MyCustomScrollBehavior extends MaterialScrollBehavior {

  // Override behavior methods and getters like dragDevices
  @override
  Set<PointerDeviceKind> get dragDevices => {
        PointerDeviceKind.touch,
        PointerDeviceKind.mouse,
      };
}
```

- 각 물질별 DB화면
1.원하는 물질의 카드를 클릭하면 나오는 화면으로 해당 물질에 대한 상세 내용 확인 가능
 
 화면 구성:
 - 물질 이미지 및 특징
 - Data Info : 물질의 화학적 특징
 - Ion Mobility Spectrometry : 실험 데이터 그래프 시각화
 - Data File : 실험 데이터 서버 업로드 및 파일 목록

![theme logo](http://ju-ffi.github.io/assets/images/favicon/p1물질별화면.PNG)



- Data Info
1.해당 물질의 화학적 특징, 서버에서 데이터 get
 - Future와 Flutter의 http 라이브러리를 활용하여 서버에 있는 데이터를 get하고 화면에 데이터를 구현
 
![theme logo](http://ju-ffi.github.io/assets/images/favicon/p1DataInfo.PNG)

Now some code:

```javascript
Future<DataInfo> getDataInfo(String comm, String typeid) async {
  //print('1. get data');
  final response =
      await http.get(Uri.parse(address + comm + 'data_id=' + id));
  item = response.body;
  if (response.statusCode == 200) {
    return Data.fromJson(jsonDecode(response.body));
  } else {
    throw Exception('Failed to load album');
  }
}
```

 2. Edit 화면에서는 사용자가 이용하기 쉽게 기존값을 나타내고, 수정하는 형태로 구현.
 
![theme logo](http://ju-ffi.github.io/assets/images/favicon/p1datainfoedit.PNG)

Now some code:

```javascript

OutlinedButton(
 onPressed: () {
   return _showUploadDialog();
  },
  child: Icon(Icons.edit))
  ...
Future<DataInfo> ChangeDataInfo(
    String id, String dataid, List postData) async {
      final http.Response response = await http.post(
          Uri.parse(address + 'change_data'),
            body: <String, String>{ 
            ...
            });

```

- Ion Mobility Spectrometry

1. 해당 물질의 데이터 시각화
 - 파일 목록을 선택했을 때 서버에서 파일의 path 주소를 읽고, json과 csv 파일 형식에 맞게 값을 decode하여 그래프로 나타낼 수 있도록 구현
 - json 파일의 경우, 데이터의 용량이 커서 읽어오는데 한계가 있으므로 raw 파일이 아닌 preview 파일이 나타나도록 설정

![theme logo](http://ju-ffi.github.io/assets/images/favicon/p1graph.PNG)

Now some code:
```javascript
Future<Data> readJson(String path, {bool fromAsset = false}) async {
  var tagsJson;
  if (fromAsset) {
    String response = await rootBundle.loadString(path);
    tagsJson = json.decode(response);
  } else {
  
//11/24
//http로 파일 path에서 json읽는 법으로 변경
//tagsJson에 get한 데이터를 넣어줘야 함.

    var response =
        await http.get(Uri.parse(path)); // path include the string of JSON

    if (response.statusCode == 200) {
      return tagsJson = Data.fromJson(jsonDecode(response.body));
    }
  }

  return Data.fromJson(tagsJson);
}
```

- Data File

1. 서버에 업로드된 데이터 목록을 나타내며, 오른쪽 상단 + 아이콘을 클릭하여 서버에 파일을 추가 업로드 및 쓰레기통 아이콘으로 서버에서 삭제 가능

![theme logo](http://ju-ffi.github.io/assets/images/favicon/p1datafile.PNG)

Now some code:
 ```javascript
 Future<List<DataFileList>> getImsFilelist(String comm, id) async {
  //print(address + comm + 'data_id=' + id);
  final response =
      await http.get(Uri.parse(address + comm + 'data_id=' + id));
      
  //print("receive data list");
  if (response.statusCode == 200) {
    return parseFileInfo(response.body);
  } else {
    //print(response.body);
    throw Exception('Failed to load album');
  }
}
...
FutureBuilder<List<DataFileList>>(
            future: getFilelist(
                "data_file_list?", data.id),
            builder: (context, snapshot) {
              if (snapshot.hasData) {
              ...
              }
             }
            )
 ```

 2. 서버에 데이터 파일 업로드
 - 파일 업로드는 http 라이브러리가 아닌 dio 라이브러리를 사용
 - dio라이브러리는 http와 다르게 header , body 등 생성해줄 필요가 없이 formMap을 통하여 항목에 맞게 정도를 mapping할 수 있는 장점 때문
 - 또한, 부가 기능으로 onSendProgress가 있어서 파일 업로드 현황을 확인 가능
![theme logo](http://ju-ffi.github.io/assets/images/favicon/p1uploadrawfile.PNG)

Now some code:
 ```javascript
 ...
   var dio = Dio();
      var formData = FormData.fromMap({
        'data_id': dataId,
        'file': await MultipartFile.fromBytes(filename: fileName)
      });

      response = dio.post(
        url,
        data: formData,
        onSendProgress: (count, total) =>
            print("uploading... ${(count * 100 / total).toStringAsFixed(2)}%"),
      );
    }

    return response;
    ...
```
