# React Native

## React와 비교한 React Native의 특징
- 웹에서 쓰던 HTML 태그를 사용하지 않고, React Native에서 제공되는 컴포넌트를 사용함.
  - React와의 차이
    - React에서는 `<span>`, `<div>` 등등의 HTML 태그를 사용하지만,
    - React Native에서는 `<View>`, `<Text>`, `<Pressable>` 등등을 사용해야 한다.
  - React Native의 컴포넌트는 빌드 타임에 각 플랫폼에 해당하는 네이티브 UI 구성 요소로 변환된다.
    - 예를 들어, React Native의 `<View>` 컴포넌트는, iOS에서는 `UIView`, Android에서는 `ViewGroup`로 변환됨.
    - 근거: https://reactnative.dev/docs/intro-react-native-components#core-components
- JavaScript 객체 기반의 StyleSheet으로 스타일링.
  - React와의 차이
    - React에서는 CSS나 SCSS, styled-components같은 CSS-in-JS 등등으로 모든 CSS 속성을 지원하는 스타일링이 가능하지만,
    - React Native에서는 스타일링이 JavaScript 객체 기반의 StyleSheet으로 이루어진다.
      - View 컴포넌트에 가능한 스타일링(`ViewStyle`)과, Text 컴포넌트에 가능한 스타일링(`TextStyle`)이 따로 있다.
      - 스타일링 객체 배열로 여러가지 특징의 스타일링을 혼합할 수 있다. 이 때, 중복되는 속성은 가장 뒤에 있는 엘리먼트 객체의 것을 따른다.
- 플랫폼에 따라 배포 방식과 동작 등등이 상이함.
  - 배포 방식
    - iOS는 빌드된 앱을 App Store Connect를 통해 배포하며, Android는 빌드된 앱을 Google Play Store를 통해 배포한다.
    - iOS 앱을 배포하려면 Apple Developer Program에 가입하여야 하며(연간 99 USD), Android 앱을 배포하려면 Google Play Console에서 개발자 계정을 만들어야 한다(일회성 25 USD).
    - iOS 앱 테스트는 빌드된 앱을 TestFlight에 올려 테스트할 수 있고, Android 앱 테스트는 apk 파일로 빌드하여 내부 공유 또는 aab 파일로 빌드하여 비공개 테스트 트랙에 올려 테스트할 수 있다.
    - 빌드 후 바로 웹으로 올릴 수 있는 React와 달리, React Native는 빌드 후 배포하려면 빌드된 앱을 스토어에 제출하여 심사를 거쳐야 한다.
  - 동작
    - iOS와 Android는 UI 디자인 가이드라인과 하드웨어 동작 방식이 다르기 때문에, 같은 JavaScript 코드이더라도 동작 결과가 플랫폼에 따라 상이할 수 있다.
    - 이 때, `Platform.OS === '<OS 이름>' ? ... : ...` 등등의 코드를 삽입하여 플랫폼에 따라 로직을 나눌 수 있다.
- 실행 환경
  - React는 웹 브라우저의 JavaScript 엔진(에를 들어 V8 엔진)에서 작동한다.
  - React Native는 JavaScript 계층과 네이티브 계층이 있는데, JavaScript 계층은 Hermes 엔진이 JavaScript 코드를 작동시키고, 실제 UI는 네이티브 계층에서 작동한다.
    - JavaScript 계층과 네이티브 계층 간 통신은, New Architecture 이전까진 Bridge를 통한 JSON 직렬화를 통해 이루어졌지만, New Architecture 이후 Turbo Module / Fabric / Codegen 등등의 모듈을 통해 서로 직접 참조하는 방식으로 이루어진다.
