# 📰 뉴스 

이 프로젝트는 Vue.js를 사용하여 작성된 뉴스 웹 애플리케이션입니다. 사용자는 다양한 카테고리의 뉴스를 탐색하고 조회할 수 있습니다. Vue의 컴포넌트 기반 구조와 반응형 데이터 바인딩을 활용하여 사용자 인터페이스를 개선했습니다.

![project_main](https://example.com/project_image.png) <!-- 여기에 프로젝트 관련 이미지를 추가할 수 있어요. -->

## 🔗 사이트 URL

- [뉴스 웹 앱 바로가기](https://example.com) <!-- 실제 URL로 변경 -->

## 📑 개요

1. **주제**
   - 사용자가 다양한 카테고리의 뉴스를 쉽게 접할 수 있는 웹 애플리케이션
2. **목표**
   - 뉴스 카테고리 선택 및 관련 뉴스를 표시하고, 사용자가 더 많은 정보를 쉽게 얻을 수 있도록 하는 것
3. **개발 환경**
   - Vue.js, HTML, CSS, Axios
4. **기간 및 인원**
   - 2024.10.01 ~ 2024.10.30 (2일), 1인

## 🙌 담당 직무

|    이름    |                   GitHub                    |     직무     |
| :--------: | :-----------------------------------------: | :----------: |
| **허다영** | **[my-github](https://github.com/my-github)** |   **개발**   |

## 💡 주요 기능

### 1. 뉴스 카테고리 탐색
- 사용자는 '전체', '정치', '경제', '사회', '문화', '세계' 등의 카테고리를 선택하여 뉴스를 필터링할 수 있습니다.
- 각 버튼의 활성화 상태는 Vue의 반응형 데이터 바인딩을 통해 자동으로 업데이트됩니다.

```javascript
<button @click="news2('politics')" :class="{ active: activeCategory === 'politics' }">정치</button>
```

### 2. 뉴스 데이터 가져오기
- Axios를 사용하여 API로부터 뉴스 데이터를 가져오고, Vue의 created 라이프사이클 훅에서 기본적으로 전체 뉴스를 로드합니다.
- API 호출 시 에러 처리를 통해 사용자에게 오류 메시지를 출력합니다.

```javascript
created() {
    this.newsko(); // 기본적으로 전체 뉴스 로드
}
```
### 3. 뉴스 상세 보기
- 사용자가 뉴스 항목의 요약을 클릭하면, 
더 많은 내용을 확인할 수 있도록 요약 부분이 토글됩니다.
showMore 플래그를 사용하여 각 뉴스 항목의 상세 정보 표시를 제어합니다.

```javascript

<button class="more" @click="toggleSummary(handle)">
    <img :src="'/more.svg'" />
</button>
```

### 4. 스크롤 맨 위 버튼
- 사용자가 페이지를 스크롤할 때, 특정 위치에서 "맨 위로" 버튼이 나타나며 클릭 시 부드럽게 스크롤됩니다.
- 이 기능은 Vue의 상태 관리와 `이벤트 리스너`를 활용하여 구현되었습니다.
```javascript
mounted() {
    window.addEventListener('scroll', this.handleScroll);
},
beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll);
}
```

## 🐱‍💻 사용 훅

### 1. `created()`
 -설명: 컴포넌트가 인스턴스화된 후, 즉 DOM에 추가되기 전에 호출됩니다. 데이터 초기화 및 API 호출에 적합합니다.
사용 예시: 뉴스 데이터를 초기 로드하는 데 사용됩니다.
```javascript
created() {
    this.newsko(); // 기본적으로 전체 뉴스 로드
}
```
### 2. `mounted()`
 - 설명: 컴포넌트가 DOM에 추가된 후 호출됩니다. DOM 조작이나 외부 라이브러리와의 통합에 유용합니다.
사용 예시: 스크롤 이벤트 리스너를 추가하는 데 사용됩니다.
```javascript
mounted() {
    window.addEventListener('scroll', this.handleScroll);
}
```
### 3. `beforeUnmount()`

- 설명: 컴포넌트가 DOM에서 제거되기 전에 호출됩니다. 메모리 누수를 방지하기 위해 이벤트 리스너를 정리하는 데 유용합니다.
- 사용 예시: 추가한 스크롤 이벤트 리스너를 제거합니다.
```javascript
beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll);
}
```
### 4. `methods`
 - 설명: 컴포넌트의 메서드를 정의하는 부분입니다. 사용자 상호작용에 반응하여 호출되는 함수들을 포함합니다.
 - 사용 예시: 뉴스 카테고리를 변경하거나, 
 뉴스 요약을 토글하는 등의 메서드가 포함됩니다.
```javascript
methods: {
    async newsko() {
        this.activeCategory = ""; // 전체 카테고리 활성화
        try {
            const api = await axios.get(`https://server-woad-theta.vercel.app/news/ko`);
            this.data = api.data.data.map((handle) => ({
                ...handle,
                showMore: false,
            }));
        } catch (error) {
            console.error("Error fetching news:", error);
        }
    },
    toggleSummary(handle) {
        handle.showMore = !handle.showMore; // 요약 표시 토글
    },
}
```

## 💥 트러블 슈팅
데이터 로드 문제

API 호출 시 데이터가 로드되지 않는 이슈 발생.
해결 방안

API URL을 확인하고 CORS 문제를 해결하기 위해 서버 설정을 조정했습니다.
UI 반응성 문제

카테고리 버튼 클릭 시 UI가 즉시 업데이트되지 않는 이슈 발생.
해결 방안

Vue의 반응형 데이터 구조를 활용하여 상태 업데이트 시 UI가 자동으로 리렌더링되도록 수정했습니다.