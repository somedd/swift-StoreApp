# - Step1 (상품 목록)

## 요구사항
- 스토리보드 ViewController에 TableView를 추가하고 Safe 영역에 가득 채우도록 frame을 설정한다.
- 테이블뷰에 새로운 프로토타입 Cell을 추가하고, Custom 스타일로 지정하고 다음과 같이 디자인한다.
- main.json 데이터 경로 => http://public.codesquad.kr/jk/storeapp/main.json
- 위 파일을 다운로드해서 프로젝트에 복사하고 JSONDecoder를 활용해서 내부에 Array<StoreItem> 타입으로 변환하는 DataSource에서 사용할 모델 객체를 만든다.
	- subscript로 배열에 index로 접근하면 StoreItem 구조체를 반환한다.
	- StoreItem은 Decodable 프로토콜을 채택하고, main.json에 있는 키와 값을 매핑해서 속성으로 갖도록 구현한다.
- UITableViewDataSource 프로토콜 구현 부분에서 cell을 위에서 만든 DataSource 모델 객체에 접근해서 테이블뷰를 표시한다.

## 실행화면
![screemsh_step1](./img/Step1.png)

# - Step2 ( AutoLayout 적용 )

## 요구사항
- 스토리보드 ViewController에 Cell을 Content View를 기준으로 하위 뷰들에 오토레이아웃을 적용한다.
	- 메뉴 이미지 뷰는 top, bottom, lead 제약을 주고 width 제약을 넣는다. height와 width 비율은 1:1로 aspectRatio를 맞춘다.
	- 타이틀 제목은 메뉴 이미지보다 10pt 우측에 lead 제약을 주고, top, tail 제약을 주고, height 제약을 준다.
	- 상세 설명도 top 제약만 타이틀 제목보다 4pt 띄우고, 나머지는 타이틀에 맞춘다.
	- 메뉴 가격도 width 제약을 넣고, 나머지는 타이틀과 마찬가지로 제약을 준다.
	- 이벤트 배지는 최소width 제약만 주고 글자 내용에 맞추고, 없을 경우 감춘다.

## 실행화면
![screemsh_step2](./img/Step2.png)

## Priority & isActive
 - 우선순위, Priority는 UILayoutPriority로 설정할 수 있으며 1에서 1000까지의 값을 갖는다.
 - Required는 1000, DefaultHigh는 750, DefaultLow는 250의 기본값을 갖는다.
  	- 세 가지 우선순위로 제약조건이 걸려있는 경우 1000이 가장 높은 영향력을 가지며, 1000이 없어진 경우 750, 750이 없어진 경우 250, 순차적으로 연결된다.
 - Constraint의 isActive를 true/false로 변경하면 해당 값을 활성화/비활성화할 수 있다. 단, 이때 해당 Constraint가 weak으로 연결되면 ARC 문제로 해제될 경우가 있으므로 Strong으로 연결해야 한다.

# - Step3 ( Custom Section 헤더 적용 )
## 요구사항
- 다음 2개 파일을 다운로드해서 프로젝트에 복사하고 JSONDecoder를 활용해서 모델 객체를 기존 main과 함께 섹션(section)을 구분할 수 있도록 개선한다.
	- soup.json 데이터 경로 => http://public.codesquad.kr/jk/storeapp/soup.json
	- side.json 데이터 경로 => http://public.codesquad.kr/jk/storeapp/side.json

- 스토리보드 ViewController에 Cell에 Section Header로 사용할 Custom Cell을 추가한다.
	- 총 섹션은 3개로 구분해서 헤더에 다음과 같이 표시한다.
	- main => 메인반찬 / 한그릇 뚝딱 메인 요리
	- soup => 국.찌게 / 김이 모락모락 국.찌게
	- side => 밑반찬 / 언제 먹어도 든든한 밑반찬

## 실행화면
![screemsh_step3](./img/Step3.png)
