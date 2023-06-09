# 아이템45. devDependencies 에 typescript 와 @types 추가하기

npm(node package manager) 은 자바스크립트 세상에서 필수적이다. npm 은 자바스크립트 라이브러리 저장소(npm registry)와, 프로젝트가 의존하고 있는 라이브러리들의 버전을 지정하는 방법(`package.json`)을 제공한다.

npm 은 3가지 종류의 의존성을 구분해서 관리하고, 각각의 의존성은 `package.json` 파일 내의 별도의 영역에 들어 있다.

### dependencies

현재 프로젝트를 실행하는데 필수적인 라이브러리들이 포함된다. 프로젝트 런타임에 `lodash` 가 사용된다면 `dependencies` 가 포함되야 한다.

프로젝트를 npm에 공개하여 다른 사용자가 해당 프로젝트를 설치한다면 `dependencies` 에 있는 라이브러리도 함께 설치될 것이다. 이런 현상을 **전이(transitive) 의존성**이라고 한다.

### devDependencies

현재 프로젝트를 개발하고 테스트하는데 필요하지만 런타임에는 필요없는 라이브러리들이 포함된다. 프로젝트를 npm 에 공개하고 다른 사용자가 해당 프로젝트를 설치한다면 `devDependencies` 에 포함된 라이브러리들은 제외된다는 것이 `dependencies` 와 차이점이다.

### peerDependencies

런타임이 필요하지만 의존성을 직접 관리하지 않는 라이브러리들이 포함된다. 버전을 플러그인에서 직접 선택하지 않고, 플러그인이 사용되는 실제 프로젝트에서 선택하도록 만들 때 사용된다.

3 가지 의존성 중에서 `dependencies` 와 `devDependencies` 가 일반적으로 사용된다. 타입스크립트 개발자라면 라이브러리를 추가할 때 어떤 의존성을 사용해야 하는지 알고 있어야 한다. 타입 정보는 런타임에는 존재하지 않기 때문에 타입스크립트 관련 라이브러리는 일반적으로 `devDependencies` 에 속한다.

모든 타입스크립트 프로젝트에서 공통적으로 고려해야 할 의존성 2가지가 있다.

첫 번째는 **타입스크립트 자체 의존성을 고려**해야 한다. 타입스크립트를 시스템 레벨로 설치할 수 있지만 추천하지 않는다. 왜냐하면 팀원들 모두가 항상 같은 버전을 설치한다는 보장이 없고, 프로젝트를 셋업할 때 별도의 단계들이 추가된다. 따라서 시스템 레벨 설치보다는 `devDependencies` 에 넣는 것이 좋다. 프로젝트에 필요한 패키지를 설치할 때(`npm install`) **팀원들 모두 항상 정확한 버전의 타입스크립트를 설치**할 수 있다.

두 번째는 **타입 의존성(`@types`)을 고려**해야 한다. 사용하는 라이브러리에 **타입 선언이 포함되어 있지 않더라도 DefinitelyTyped(타입스크립트 커뮤니티에서 유지보수하고 있는 자바스크립트 라이브러리를 정의한 모음)에서 타입 정보를 얻을 수 있다**. DefinitelyTyped 의 타입 정의들은 npm 레지스트리의  `@types/***` 에 있다. 예를 들면 lodash 의 타입정의는 `@types/lodash` 에 있다.

```
$ npm install lodash
$ npm install --save-dev @types/lodash
```

```json
{
	"dependencies": {
		"lodash": "^8.1.0",
		//...
	},
	"devDependencies": {
		"@types/lodash": "^4.14.0",
		//...
	}
}
```
