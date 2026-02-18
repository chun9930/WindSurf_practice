# TODO 웹 애플리케이션 설계 문서

## 1. 아키텍처 설계

### 1.1 전체 시스템 아키텍처

<div align="center">
<svg width="900" height="400" viewBox="0 0 900 400" xmlns="http://www.w3.org/2000/svg">
  <!-- 프론트엔드 -->
  <rect x="20" y="100" width="200" height="200" rx="10" fill="#3b82f6" stroke="#1e40af" stroke-width="2"/>
  <text x="120" y="130" text-anchor="middle" fill="white" font-size="16" font-weight="bold">프론트엔드</text>
  <text x="120" y="150" text-anchor="middle" fill="white" font-size="14">(React)</text>
  
  <!-- 프론트엔드 상세 -->
  <rect x="35" y="170" width="170" height="25" rx="5" fill="#60a5fa"/>
  <text x="120" y="188" text-anchor="middle" fill="white" font-size="12">UI/UX 컴포넌트</text>
  
  <rect x="35" y="200" width="170" height="25" rx="5" fill="#60a5fa"/>
  <text x="120" y="218" text-anchor="middle" fill="white" font-size="12">상태 관리 (Zustand)</text>
  
  <rect x="35" y="230" width="170" height="25" rx="5" fill="#60a5fa"/>
  <text x="120" y="248" text-anchor="middle" fill="white" font-size="12">로컬 스토리지</text>
  
  <rect x="35" y="260" width="170" height="25" rx="5" fill="#60a5fa"/>
  <text x="120" y="278" text-anchor="middle" fill="white" font-size="12">Tailwind CSS</text>
  
  <!-- 백엔드 -->
  <rect x="350" y="100" width="200" height="200" rx="10" fill="#10b981" stroke="#047857" stroke-width="2"/>
  <text x="450" y="130" text-anchor="middle" fill="white" font-size="16" font-weight="bold">백엔드 API</text>
  <text x="450" y="150" text-anchor="middle" fill="white" font-size="14">(Node.js/TypeScript)</text>
  
  <!-- 백엔드 상세 -->
  <rect x="365" y="170" width="170" height="25" rx="5" fill="#34d399"/>
  <text x="450" y="188" text-anchor="middle" fill="white" font-size="12">비즈니스 로직</text>
  
  <rect x="365" y="200" width="170" height="25" rx="5" fill="#34d399"/>
  <text x="450" y="218" text-anchor="middle" fill="white" font-size="12">API 엔드포인트</text>
  
  <rect x="365" y="230" width="170" height="25" rx="5" fill="#34d399"/>
  <text x="450" y="248" text-anchor="middle" fill="white" font-size="12">인증 처리</text>
  
  <rect x="365" y="260" width="170" height="25" rx="5" fill="#34d399"/>
  <text x="450" y="278" text-anchor="middle" fill="white" font-size="12">데이터 검증</text>
  
  <!-- 데이터베이스 -->
  <rect x="680" y="100" width="200" height="200" rx="10" fill="#f59e0b" stroke="#d97706" stroke-width="2"/>
  <text x="780" y="130" text-anchor="middle" fill="white" font-size="16" font-weight="bold">데이터베이스</text>
  <text x="780" y="150" text-anchor="middle" fill="white" font-size="14">(DynamoDB)</text>
  
  <!-- 데이터베이스 상세 -->
  <rect x="695" y="170" width="170" height="25" rx="5" fill="#fbbf24"/>
  <text x="780" y="188" text-anchor="middle" fill="white" font-size="12">TODO 데이터</text>
  
  <rect x="695" y="200" width="170" height="25" rx="5" fill="#fbbf24"/>
  <text x="780" y="218" text-anchor="middle" fill="white" font-size="12">사용자 데이터</text>
  
  <rect x="695" y="230" width="170" height="25" rx="5" fill="#fbbf24"/>
  <text x="780" y="248" text-anchor="middle" fill="white" font-size="12">인덱스 관리</text>
  
  <rect x="695" y="260" width="170" height="25" rx="5" fill="#fbbf24"/>
  <text x="780" y="278" text-anchor="middle" fill="white" font-size="12">백업/복구</text>
  
  <!-- 화살표 -->
  <defs>
    <marker id="arrowhead" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
      <polygon points="0 0, 10 3.5, 0 7" fill="#333"/>
    </marker>
  </defs>
  
  <!-- 프론트엔드 -> 백엔드 -->
  <line x1="220" y1="200" x2="350" y2="200" stroke="#333" stroke-width="2" marker-end="url(#arrowhead)"/>
  <text x="285" y="190" text-anchor="middle" font-size="12" fill="#333">HTTP/REST API</text>
  
  <!-- 백엔드 -> 데이터베이스 -->
  <line x1="550" y1="200" x2="680" y2="200" stroke="#333" stroke-width="2" marker-end="url(#arrowhead)"/>
  <text x="615" y="190" text-anchor="middle" font-size="12" fill="#333">AWS SDK</text>
  
  <!-- 제목 -->
  <text x="450" y="40" text-anchor="middle" font-size="20" font-weight="bold" fill="#1f2937">TODO 웹 애플리케이션 시스템 아키텍처</text>
  
  <!-- AWS 인프라 레이블 -->
  <rect x="320" y="330" width="260" height="40" rx="5" fill="#f3f4f6" stroke="#9ca3af" stroke-width="1" stroke-dasharray="5,5"/>
  <text x="450" y="355" text-anchor="middle" font-size="14" fill="#6b7280">AWS 서버리스 인프라</text>
</svg>
</div>

### 1.2 개발 단계별 아키텍처
**1단계 (프론트엔드 전용):**
- React + 로컬 스토리지로 독립 실행
- localStorage를 통한 데이터 영속성

**2단계 (백엔드 연동):**
- AWS 서버리스 아키텍처로 확장
- API Gateway + Lambda + DynamoDB 연동

## 2. 프론트엔드 설계

### 2.1 컴포넌트 구조
```
src/
├── components/
│   ├── common/
│   │   ├── Button/
│   │   ├── Input/
│   │   └── Modal/
│   ├── todo/
│   │   ├── TodoForm/
│   │   ├── TodoItem/
│   │   ├── TodoList/
│   │   └── TodoFilter/
│   └── layout/
│       ├── Header/
│       └── Layout/
├── hooks/
│   ├── useTodos.ts
│   ├── useLocalStorage.ts
│   └── useTheme.ts
├── store/
│   ├── todoStore.ts
│   └── themeStore.ts
├── types/
│   └── todo.ts
├── utils/
│   └── todoUtils.ts
└── styles/
    └── globals.css
```

### 2.2 상태 관리 설계
**Zustand를 사용한 상태 관리:**

```typescript
// store/todoStore.ts
interface Todo {
  id: string;
  title: string;
  priority: 'low' | 'medium' | 'high';
  status: 'pending' | 'completed';
  createdAt: string;
  updatedAt: string;
}

interface TodoStore {
  todos: Todo[];
  filter: 'all' | 'pending' | 'completed';
  sortBy: 'date' | 'priority';
  
  // Actions
  addTodo: (todo: Omit<Todo, 'id' | 'createdAt' | 'updatedAt'>) => void;
  updateTodo: (id: string, updates: Partial<Todo>) => void;
  deleteTodo: (id: string) => void;
  toggleTodo: (id: string) => void;
  setFilter: (filter: string) => void;
  setSortBy: (sortBy: string) => void;
}
```

### 2.3 데이터 흐름
```
사용자 액션 → 컴포넌트 → Zustand Store → localStorage → UI 업데이트
```

## 3. 백엔드 설계

### 3.1 API 엔드포인트 설계
```
POST   /api/todos          # TODO 생성
GET    /api/todos          # TODO 목록 조회
GET    /api/todos/:id      # 특정 TODO 조회
PUT    /api/todos/:id      # TODO 수정
DELETE /api/todos/:id      # TODO 삭제
```

### 3.2 DynamoDB 테이블 설계
```json
{
  "TableName": "Todos",
  "KeySchema": [
    {
      "AttributeName": "userId",
      "KeyType": "HASH"
    },
    {
      "AttributeName": "todoId",
      "KeyType": "RANGE"
    }
  ],
  "AttributeDefinitions": [
    {
      "AttributeName": "userId",
      "AttributeType": "S"
    },
    {
      "AttributeName": "todoId",
      "AttributeType": "S"
    },
    {
      "AttributeName": "status",
      "AttributeType": "S"
    },
    {
      "AttributeName": "priority",
      "AttributeType": "S"
    }
  ],
  "GlobalSecondaryIndexes": [
    {
      "IndexName": "StatusIndex",
      "KeySchema": [
        {
          "AttributeName": "userId",
          "KeyType": "HASH"
        },
        {
          "AttributeName": "status",
          "KeyType": "RANGE"
        }
      ],
      "Projection": {
        "ProjectionType": "ALL"
      }
    }
  ]
}
```

### 3.3 리퀘스트 처리 시퀀스 다이어그램

#### TODO 생성 시퀀스

<div align="center">
<svg width="800" height="600" viewBox="0 0 800 600" xmlns="http://www.w3.org/2000/svg">
  <!-- 액터 -->
  <rect x="20" y="40" width="80" height="40" rx="5" fill="#3b82f6" stroke="#1e40af" stroke-width="2"/>
  <text x="60" y="65" text-anchor="middle" fill="white" font-size="12" font-weight="bold">사용자</text>
  
  <rect x="140" y="40" width="80" height="40" rx="5" fill="#10b981" stroke="#047857" stroke-width="2"/>
  <text x="180" y="65" text-anchor="middle" fill="white" font-size="12" font-weight="bold">React UI</text>
  
  <rect x="260" y="40" width="80" height="40" rx="5" fill="#8b5cf6" stroke="#6d28d9" stroke-width="2"/>
  <text x="300" y="65" text-anchor="middle" fill="white" font-size="12" font-weight="bold">Zustand</text>
  
  <rect x="380" y="40" width="80" height="40" rx="5" fill="#f59e0b" stroke="#d97706" stroke-width="2"/>
  <text x="420" y="65" text-anchor="middle" fill="white" font-size="12" font-weight="bold">API</text>
  
  <rect x="500" y="40" width="80" height="40" rx="5" fill="#ef4444" stroke="#dc2626" stroke-width="2"/>
  <text x="540" y="65" text-anchor="middle" fill="white" font-size="12" font-weight="bold">Lambda</text>
  
  <rect x="620" y="40" width="80" height="40" rx="5" fill="#06b6d4" stroke="#0891b2" stroke-width="2"/>
  <text x="660" y="65" text-anchor="middle" fill="white" font-size="12" font-weight="bold">DynamoDB</text>
  
  <!-- 생명선 -->
  <line x1="60" y1="80" x2="60" y2="560" stroke="#333" stroke-width="1" stroke-dasharray="5,5"/>
  <line x1="180" y1="80" x2="180" y2="560" stroke="#333" stroke-width="1" stroke-dasharray="5,5"/>
  <line x1="300" y1="80" x2="300" y2="560" stroke="#333" stroke-width="1" stroke-dasharray="5,5"/>
  <line x1="420" y1="80" x2="420" y2="560" stroke="#333" stroke-width="1" stroke-dasharray="5,5"/>
  <line x1="540" y1="80" x2="540" y2="560" stroke="#333" stroke-width="1" stroke-dasharray="5,5"/>
  <line x1="660" y1="80" x2="660" y2="560" stroke="#333" stroke-width="1" stroke-dasharray="5,5"/>
  
  <!-- 화살표 정의 -->
  <defs>
    <marker id="arrow" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
      <polygon points="0 0, 10 3.5, 0 7" fill="#333"/>
    </marker>
  </defs>
  
  <!-- 1. 사용자 입력 -->
  <line x1="60" y1="120" x2="180" y2="120" stroke="#333" stroke-width="2" marker-end="url(#arrow)"/>
  <text x="120" y="110" text-anchor="middle" font-size="11" fill="#333">TODO 입력</text>
  
  <!-- 2. UI에서 상태 관리로 -->
  <line x1="180" y1="160" x2="300" y2="160" stroke="#333" stroke-width="2" marker-end="url(#arrow)"/>
  <text x="240" y="150" text-anchor="middle" font-size="11" fill="#333">addTodo()</text>
  
  <!-- 3. 상태 관리에서 API 호출 -->
  <line x1="300" y1="200" x2="420" y2="200" stroke="#333" stroke-width="2" marker-end="url(#arrow)"/>
  <text x="360" y="190" text-anchor="middle" font-size="11" fill="#333">POST /api/todos</text>
  
  <!-- 4. API에서 Lambda로 -->
  <line x1="420" y1="240" x2="540" y2="240" stroke="#333" stroke-width="2" marker-end="url(#arrow)"/>
  <text x="480" y="230" text-anchor="middle" font-size="11" fill="#333">요청 전달</text>
  
  <!-- 5. Lambda에서 DynamoDB로 -->
  <line x1="540" y1="280" x2="660" y2="280" stroke="#333" stroke-width="2" marker-end="url(#arrow)"/>
  <text x="600" y="270" text-anchor="middle" font-size="11" fill="#333">PutItem</text>
  
  <!-- 6. 응답 반환 -->
  <line x1="660" y1="320" x2="540" y2="320" stroke="#333" stroke-width="2" stroke-dasharray="3,3" marker-end="url(#arrow)"/>
  <text x="600" y="310" text-anchor="middle" font-size="11" fill="#333">성공 응답</text>
  
  <!-- 7. Lambda에서 API로 -->
  <line x1="540" y1="360" x2="420" y2="360" stroke="#333" stroke-width="2" stroke-dasharray="3,3" marker-end="url(#arrow)"/>
  <text x="480" y="350" text-anchor="middle" font-size="11" fill="#333">201 Created</text>
  
  <!-- 8. API에서 상태 관리로 -->
  <line x1="420" y1="400" x2="300" y2="400" stroke="#333" stroke-width="2" stroke-dasharray="3,3" marker-end="url(#arrow)"/>
  <text x="360" y="390" text-anchor="middle" font-size="11" fill="#333">TODO 데이터</text>
  
  <!-- 9. 상태 관리에서 UI로 -->
  <line x1="300" y1="440" x2="180" y2="440" stroke="#333" stroke-width="2" stroke-dasharray="3,3" marker-end="url(#arrow)"/>
  <text x="240" y="430" text-anchor="middle" font-size="11" fill="#333">상태 업데이트</text>
  
  <!-- 10. UI에서 사용자로 -->
  <line x1="180" y1="480" x2="60" y2="480" stroke="#333" stroke-width="2" stroke-dasharray="3,3" marker-end="url(#arrow)"/>
  <text x="120" y="470" text-anchor="middle" font-size="11" fill="#333">화면 업데이트</text>
  
  <!-- 제목 -->
  <text x="400" y="20" text-anchor="middle" font-size="16" font-weight="bold" fill="#1f2937">TODO 생성 시퀀스 다이어그램</text>
</svg>
</div>

#### TODO 목록 조회 시퀀스

<div align="center">
<svg width="800" height="500" viewBox="0 0 800 500" xmlns="http://www.w3.org/2000/svg">
  <!-- 액터 -->
  <rect x="20" y="40" width="80" height="40" rx="5" fill="#3b82f6" stroke="#1e40af" stroke-width="2"/>
  <text x="60" y="65" text-anchor="middle" fill="white" font-size="12" font-weight="bold">사용자</text>
  
  <rect x="140" y="40" width="80" height="40" rx="5" fill="#10b981" stroke="#047857" stroke-width="2"/>
  <text x="180" y="65" text-anchor="middle" fill="white" font-size="12" font-weight="bold">React UI</text>
  
  <rect x="260" y="40" width="80" height="40" rx="5" fill="#8b5cf6" stroke="#6d28d9" stroke-width="2"/>
  <text x="300" y="65" text-anchor="middle" fill="white" font-size="12" font-weight="bold">Zustand</text>
  
  <rect x="380" y="40" width="80" height="40" rx="5" fill="#f59e0b" stroke="#d97706" stroke-width="2"/>
  <text x="420" y="65" text-anchor="middle" fill="white" font-size="12" font-weight="bold">API</text>
  
  <rect x="500" y="40" width="80" height="40" rx="5" fill="#ef4444" stroke="#dc2626" stroke-width="2"/>
  <text x="540" y="65" text-anchor="middle" fill="white" font-size="12" font-weight="bold">Lambda</text>
  
  <rect x="620" y="40" width="80" height="40" rx="5" fill="#06b6d4" stroke="#0891b2" stroke-width="2"/>
  <text x="660" y="65" text-anchor="middle" fill="white" font-size="12" font-weight="bold">DynamoDB</text>
  
  <!-- 생명선 -->
  <line x1="60" y1="80" x2="60" y2="460" stroke="#333" stroke-width="1" stroke-dasharray="5,5"/>
  <line x1="180" y1="80" x2="180" y2="460" stroke="#333" stroke-width="1" stroke-dasharray="5,5"/>
  <line x1="300" y1="80" x2="300" y2="460" stroke="#333" stroke-width="1" stroke-dasharray="5,5"/>
  <line x1="420" y1="80" x2="420" y2="460" stroke="#333" stroke-width="1" stroke-dasharray="5,5"/>
  <line x1="540" y1="80" x2="540" y2="460" stroke="#333" stroke-width="1" stroke-dasharray="5,5"/>
  <line x1="660" y1="80" x2="660" y2="460" stroke="#333" stroke-width="1" stroke-dasharray="5,5"/>
  
  <!-- 화살표 정의 -->
  <defs>
    <marker id="arrow" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
      <polygon points="0 0, 10 3.5, 0 7" fill="#333"/>
    </marker>
  </defs>
  
  <!-- 1. 페이지 로드 -->
  <line x1="60" y1="120" x2="180" y2="120" stroke="#333" stroke-width="2" marker-end="url(#arrow)"/>
  <text x="120" y="110" text-anchor="middle" font-size="11" fill="#333">페이지 접속</text>
  
  <!-- 2. UI에서 상태 관리로 -->
  <line x1="180" y1="160" x2="300" y2="160" stroke="#333" stroke-width="2" marker-end="url(#arrow)"/>
  <text x="240" y="150" text-anchor="middle" font-size="11" fill="#333">fetchTodos()</text>
  
  <!-- 3. 상태 관리에서 API 호출 -->
  <line x1="300" y1="200" x2="420" y2="200" stroke="#333" stroke-width="2" marker-end="url(#arrow)"/>
  <text x="360" y="190" text-anchor="middle" font-size="11" fill="#333">GET /api/todos</text>
  
  <!-- 4. API에서 Lambda로 -->
  <line x1="420" y1="240" x2="540" y2="240" stroke="#333" stroke-width="2" marker-end="url(#arrow)"/>
  <text x="480" y="230" text-anchor="middle" font-size="11" fill="#333">조회 요청</text>
  
  <!-- 5. Lambda에서 DynamoDB로 -->
  <line x1="540" y1="280" x2="660" y2="280" stroke="#333" stroke-width="2" marker-end="url(#arrow)"/>
  <text x="600" y="270" text-anchor="middle" font-size="11" fill="#333">Query</text>
  
  <!-- 6. 응답 반환 -->
  <line x1="660" y1="320" x2="540" y2="320" stroke="#333" stroke-width="2" stroke-dasharray="3,3" marker-end="url(#arrow)"/>
  <text x="600" y="310" text-anchor="middle" font-size="11" fill="#333">TODO 목록</text>
  
  <!-- 7. Lambda에서 API로 -->
  <line x1="540" y1="360" x2="420" y2="360" stroke="#333" stroke-width="2" stroke-dasharray="3,3" marker-end="url(#arrow)"/>
  <text x="480" y="350" text-anchor="middle" font-size="11" fill="#333">200 OK</text>
  
  <!-- 8. API에서 상태 관리로 -->
  <line x1="420" y1="400" x2="300" y2="400" stroke="#333" stroke-width="2" stroke-dasharray="3,3" marker-end="url(#arrow)"/>
  <text x="360" y="390" text-anchor="middle" font-size="11" fill="#333">데이터 저장</text>
  
  <!-- 9. 상태 관리에서 UI로 -->
  <line x1="300" y1="440" x2="180" y2="440" stroke="#333" stroke-width="2" stroke-dasharray="3,3" marker-end="url(#arrow)"/>
  <text x="240" y="430" text-anchor="middle" font-size="11" fill="#333">렌더링</text>
  
  <!-- 제목 -->
  <text x="400" y="20" text-anchor="middle" font-size="16" font-weight="bold" fill="#1f2937">TODO 목록 조회 시퀀스 다이어그램</text>
</svg>
</div>

## 4. UI/UX 설계

### 4.1 화면 구성

#### 모바일 뷰 와이어프레임

<div align="center">
<svg width="400" height="800" viewBox="0 0 400 800" xmlns="http://www.w3.org/2000/svg">
  <!-- 모바일 프레임 -->
  <rect x="10" y="10" width="380" height="780" rx="20" fill="#f8fafc" stroke="#e2e8f0" stroke-width="2"/>
  
  <!-- 상단바 -->
  <rect x="10" y="10" width="380" height="80" rx="20" fill="#1e293b"/>
  <text x="200" y="55" text-anchor="middle" fill="white" font-size="18" font-weight="bold">TODO 앱</text>
  <circle cx="350" cy="50" r="15" fill="#475569"/>
  <text x="350" y="55" text-anchor="middle" fill="white" font-size="12">🌙</text>
  
  <!-- TODO 입력 폼 -->
  <rect x="30" y="110" width="340" height="120" rx="10" fill="white" stroke="#e2e8f0" stroke-width="1"/>
  <text x="50" y="135" font-size="14" fill="#64748b">새로운 TODO 추가</text>
  <rect x="50" y="145" width="300" height="35" rx="5" fill="#f1f5f9" stroke="#cbd5e1" stroke-width="1"/>
  <text x="65" y="167" font-size="12" fill="#94a3b8">제목을 입력하세요...</text>
  <rect x="50" y="185" width="100" height="30" rx="5" fill="#3b82f6"/>
  <text x="100" y="203" text-anchor="middle" fill="white" font-size="12">추가</text>
  <rect x="250" y="185" width="100" height="30" rx="5" fill="#f59e0b"/>
  <text x="300" y="203" text-anchor="middle" fill="white" font-size="12">높음</text>
  
  <!-- 필터 탭 -->
  <rect x="30" y="250" width="340" height="50" rx="10" fill="#f8fafc" stroke="#e2e8f0" stroke-width="1"/>
  <rect x="50" y="265" width="80" height="20" rx="10" fill="#3b82f6"/>
  <text x="90" y="278" text-anchor="middle" fill="white" font-size="11">전체</text>
  <rect x="140" y="265" width="80" height="20" rx="10" fill="#e2e8f0"/>
  <text x="180" y="278" text-anchor="middle" fill="#64748b" font-size="11">미완료</text>
  <rect x="230" y="265" width="80" height="20" rx="10" fill="#e2e8f0"/>
  <text x="270" y="278" text-anchor="middle" fill="#64748b" font-size="11">완료</text>
  
  <!-- TODO 아이템 1 -->
  <rect x="30" y="320" width="340" height="80" rx="10" fill="white" stroke="#e2e8f0" stroke-width="1"/>
  <rect x="50" y="340" width="20" height="20" rx="3" fill="#e2e8f0" stroke="#94a3b8" stroke-width="1"/>
  <text x="85" y="355" font-size="14" fill="#1e293b">프로젝트 문서 작성</text>
  <rect x="50" y="365" width="50" height="20" rx="10" fill="#ef4444"/>
  <text x="75" y="378" text-anchor="middle" fill="white" font-size="10">높음</text>
  <text x="320" y="378" text-anchor="end" fill="#94a3b8" font-size="10">2시간 전</text>
  
  <!-- TODO 아이템 2 -->
  <rect x="30" y="420" width="340" height="80" rx="10" fill="white" stroke="#e2e8f0" stroke-width="1"/>
  <rect x="50" y="440" width="20" height="20" rx="3" fill="#3b82f6" stroke="#1e40af" stroke-width="1"/>
  <path d="M55 450 L58 453 L65 445" stroke="white" stroke-width="2" fill="none"/>
  <text x="85" y="455" font-size="14" fill="#94a3b8" text-decoration="line-through">이메일 확인</text>
  <rect x="50" y="465" width="50" height="20" rx="10" fill="#f59e0b"/>
  <text x="75" y="478" text-anchor="middle" fill="white" font-size="10">중간</text>
  <text x="320" y="478" text-anchor="end" fill="#94a3b8" font-size="10">어제</text>
  
  <!-- TODO 아이템 3 -->
  <rect x="30" y="520" width="340" height="80" rx="10" fill="white" stroke="#e2e8f0" stroke-width="1"/>
  <rect x="50" y="540" width="20" height="20" rx="3" fill="#e2e8f0" stroke="#94a3b8" stroke-width="1"/>
  <text x="85" y="555" font-size="14" fill="#1e293b">팀 미팅 준비</text>
  <rect x="50" y="565" width="50" height="20" rx="10" fill="#10b981"/>
  <text x="75" y="578" text-anchor="middle" fill="white" font-size="10">낮음</text>
  <text x="320" y="578" text-anchor="end" fill="#94a3b8" font-size="10">3일 전</text>
  
  <!-- 하단 네비게이션 -->
  <rect x="10" y="720" width="380" height="70" rx="0 0 20 20" fill="#f8fafc" stroke="#e2e8f0" stroke-width="1"/>
  <circle cx="100" cy="755" r="20" fill="#e2e8f0"/>
  <text x="100" y="760" text-anchor="middle" fill="#64748b" font-size="16">📝</text>
  <circle cx="200" cy="755" r="20" fill="#3b82f6"/>
  <text x="200" y="760" text-anchor="middle" fill="white" font-size="16">✓</text>
  <circle cx="300" cy="755" r="20" fill="#e2e8f0"/>
  <text x="300" y="760" text-anchor="middle" fill="#64748b" font-size="16">⚙️</text>
  
  <text x="200" y="30" text-anchor="middle" font-size="16" font-weight="bold" fill="#1e293b">모바일 뷰 (375px)</text>
</svg>
</div>

#### 데스크톱 뷰 와이어프레임

<div align="center">
<svg width="1200" height="800" viewBox="0 0 1200 800" xmlns="http://www.w3.org/2000/svg">
  <!-- 데스크톱 프레임 -->
  <rect x="10" y="10" width="1180" height="780" rx="10" fill="#f8fafc" stroke="#e2e8f0" stroke-width="2"/>
  
  <!-- 헤더 -->
  <rect x="10" y="10" width="1180" height="80" rx="10" fill="#1e293b"/>
  <text x="50" y="55" font-size="24" font-weight="bold" fill="white">TODO 애플리케이션</text>
  <circle cx="1130" cy="50" r="20" fill="#475569"/>
  <text x="1130" y="56" text-anchor="middle" fill="white" font-size="16">🌙</text>
  
  <!-- 사이드바 -->
  <rect x="10" y="90" width="250" height="700" rx="0 0 0 10" fill="#f1f5f9" stroke="#e2e8f0" stroke-width="1"/>
  
  <!-- 사이드바 내용 -->
  <text x="30" y="120" font-size="16" font-weight="bold" fill="#1e293b">메뉴</text>
  <rect x="20" y="140" width="230" height="40" rx="5" fill="#3b82f6"/>
  <text x="135" y="165" text-anchor="middle" fill="white" font-size="14">📝 전체 TODO</text>
  
  <rect x="20" y="190" width="230" height="40" rx="5" fill="#f8fafc"/>
  <text x="135" y="215" text-anchor="middle" fill="#64748b" font-size="14">📊 대시보드</text>
  
  <rect x="20" y="240" width="230" height="40" rx="5" fill="#f8fafc"/>
  <text x="135" y="265" text-anchor="middle" fill="#64748b" font-size="14">📈 통계</text>
  
  <!-- 통계 카드 -->
  <rect x="30" y="320" width="210" height="100" rx="10" fill="white" stroke="#e2e8f0" stroke-width="1"/>
  <text x="50" y="345" font-size="14" font-weight="bold" fill="#1e293b">오늘의 할일</text>
  <text x="50" y="370" font-size="24" font-weight="bold" fill="#3b82f6">12</text>
  <text x="50" y="395" font-size="12" fill="#64748b">5개 완료</text>
  
  <rect x="30" y="440" width="210" height="100" rx="10" fill="white" stroke="#e2e8f0" stroke-width="1"/>
  <text x="50" y="465" font-size="14" font-weight="bold" fill="#1e293b">이번 주</text>
  <text x="50" y="490" font-size="24" font-weight="bold" fill="#10b981">28</text>
  <text x="50" y="515" font-size="12" fill="#64748b">18개 완료</text>
  
  <!-- 메인 콘텐츠 -->
  <rect x="270" y="90" width="920" height="700" fill="white"/>
  
  <!-- TODO 입력 영역 -->
  <rect x="290" y="110" width="880" height="100" rx="10" fill="#f8fafc" stroke="#e2e8f0" stroke-width="1"/>
  <text x="310" y="135" font-size="16" font-weight="bold" fill="#1e293b">새로운 TODO 추가</text>
  <rect x="310" y="150" width="400" height="40" rx="5" fill="#f1f5f9" stroke="#cbd5e1" stroke-width="1"/>
  <text x="325" y="175" font-size="14" fill="#94a3b8">제목을 입력하세요...</text>
  <rect x="720" y="150" width="100" height="40" rx="5" fill="#f59e0b"/>
  <text x="770" y="175" text-anchor="middle" fill="white" font-size="14">중간</text>
  <rect x="830" y="150" width="80" height="40" rx="5" fill="#3b82f6"/>
  <text x="870" y="175" text-anchor="middle" fill="white" font-size="14">추가</text>
  
  <!-- 필터 및 정렬 -->
  <rect x="290" y="230" width="880" height="60" rx="10" fill="#f8fafc" stroke="#e2e8f0" stroke-width="1"/>
  <rect x="310" y="245" width="80" height="30" rx="15" fill="#3b82f6"/>
  <text x="350" y="264" text-anchor="middle" fill="white" font-size="12">전체</text>
  <rect x="400" y="245" width="80" height="30" rx="15" fill="#e2e8f0"/>
  <text x="440" y="264" text-anchor="middle" fill="#64748b" font-size="12">미완료</text>
  <rect x="490" y="245" width="80" height="30" rx="15" fill="#e2e8f0"/>
  <text x="530" y="264" text-anchor="middle" fill="#64748b" font-size="12">완료</text>
  
  <text x="700" y="264" font-size="12" fill="#64748b">정렬:</text>
  <rect x="740" y="245" width="100" height="30" rx="5" fill="#f1f5f9" stroke="#cbd5e1" stroke-width="1"/>
  <text x="790" y="264" text-anchor="middle" fill="#64748b" font-size="12">최신순</text>
  
  <!-- TODO 목록 -->
  <text x="290" y="320" font-size="18" font-weight="bold" fill="#1e293b">TODO 목록</text>
  
  <!-- TODO 아이템 1 -->
  <rect x="290" y="340" width="880" height="80" rx="10" fill="white" stroke="#e2e8f0" stroke-width="1"/>
  <rect x="310" y="360" width="25" height="25" rx="5" fill="#e2e8f0" stroke="#94a3b8" stroke-width="1"/>
  <text x="350" y="378" font-size="16" fill="#1e293b">프로젝트 문서 작성 - 기술 명세서 및 API 설계</text>
  <rect x="310" y="390" width="60" height="20" rx="10" fill="#ef4444"/>
  <text x="340" y="403" text-anchor="middle" fill="white" font-size="11">높음</text>
  <text x="1130" y="378" text-anchor="end" fill="#94a3b8" font-size="12">2시간 전</text>
  <text x="1130" y="403" text-anchor="end" fill="#94a3b8" font-size="11">수정 | 삭제</text>
  
  <!-- TODO 아이템 2 -->
  <rect x="290" y="440" width="880" height="80" rx="10" fill="white" stroke="#e2e8f0" stroke-width="1"/>
  <rect x="310" y="460" width="25" height="25" rx="5" fill="#3b82f6" stroke="#1e40af" stroke-width="1"/>
  <path d="M317 472 L321 476 L330 467" stroke="white" stroke-width="3" fill="none"/>
  <text x="350" y="478" font-size="16" fill="#94a3b8" text-decoration="line-through">이메일 확인 및 회신</text>
  <rect x="310" y="490" width="60" height="20" rx="10" fill="#f59e0b"/>
  <text x="340" y="503" text-anchor="middle" fill="white" font-size="11">중간</text>
  <text x="1130" y="478" text-anchor="end" fill="#94a3b8" font-size="12">어제</text>
  <text x="1130" y="503" text-anchor="end" fill="#94a3b8" font-size="11">수정 | 삭제</text>
  
  <!-- TODO 아이템 3 -->
  <rect x="290" y="540" width="880" height="80" rx="10" fill="white" stroke="#e2e8f0" stroke-width="1"/>
  <rect x="310" y="560" width="25" height="25" rx="5" fill="#e2e8f0" stroke="#94a3b8" stroke-width="1"/>
  <text x="350" y="578" font-size="16" fill="#1e293b">팀 미팅 준비 - 주간 계획 발표 자료</text>
  <rect x="310" y="590" width="60" height="20" rx="10" fill="#10b981"/>
  <text x="340" y="603" text-anchor="middle" fill="white" font-size="11">낮음</text>
  <text x="1130" y="578" text-anchor="end" fill="#94a3b8" font-size="12">3일 전</text>
  <text x="1130" y="603" text-anchor="end" fill="#94a3b8" font-size="11">수정 | 삭제</text>
  
  <!-- TODO 아이템 4 -->
  <rect x="290" y="640" width="880" height="80" rx="10" fill="white" stroke="#e2e8f0" stroke-width="1"/>
  <rect x="310" y="660" width="25" height="25" rx="5" fill="#e2e8f0" stroke="#94a3b8" stroke-width="1"/>
  <text x="350" y="678" font-size="16" fill="#1e293b">코드 리뷰 - PR #123 검토 및 피드백</text>
  <rect x="310" y="690" width="60" height="20" rx="10" fill="#ef4444"/>
  <text x="340" y="703" text-anchor="middle" fill="white" font-size="11">높음</text>
  <text x="1130" y="678" text-anchor="end" fill="#94a3b8" font-size="12">5일 전</text>
  <text x="1130" y="703" text-anchor="end" fill="#94a3b8" font-size="11">수정 | 삭제</text>
  
  <text x="600" y="30" text-anchor="middle" font-size="16" font-weight="bold" fill="#1e293b">데스크톱 뷰 (1200px)</text>
</svg>
</div>

### 4.2 반응형 디자인
- **모바일 (320px-768px):** 단일 컬럼, 카드 형태
- **태블릿 (768px-1024px):** 2단계 레이아웃
- **데스크톱 (1024px+):** 최적화된 레이아웃

### 4.3 테마 설계
```css
/* 라이트 모드 */
:root {
  --bg-primary: #ffffff;
  --bg-secondary: #f3f4f6;
  --text-primary: #111827;
  --text-secondary: #6b7280;
  --border-color: #e5e7eb;
  --accent-color: #3b82f6;
}

/* 다크 모드 */
[data-theme="dark"] {
  --bg-primary: #1f2937;
  --bg-secondary: #111827;
  --text-primary: #f9fafb;
  --text-secondary: #9ca3af;
  --border-color: #374151;
  --accent-color: #60a5fa;
}
```

## 5. 테스트 전략

### 5.1 TDD 접근 방식
1. **레드 그린:** 실패하는 테스트 작성
2. **그린:** 최소한의 코드로 테스트 통과
3. **리팩토링:** 코드 개선

### 5.2 테스트 구조
```
src/
├── __tests__/
│   ├── components/
│   │   ├── TodoItem.test.tsx
│   │   ├── TodoForm.test.tsx
│   │   └── TodoList.test.tsx
│   ├── hooks/
│   │   ├── useTodos.test.ts
│   │   └── useLocalStorage.test.ts
│   ├── store/
│   │   └── todoStore.test.ts
│   └── utils/
│       └── todoUtils.test.ts
```

### 5.3 테스트 케이스 예시
```typescript
// __tests__/hooks/useTodos.test.ts
describe('useTodos', () => {
  test('새로운 TODO를 추가해야 함', () => {
    // Given
    const initialTodos = [];
    
    // When
    const result = addTodo(initialTodos, {
      title: '새로운 할일',
      priority: 'medium',
      status: 'pending'
    });
    
    // Then
    expect(result).toHaveLength(1);
    expect(result[0].title).toBe('새로운 할일');
  });
});
```

## 6. 배포 전략

### 6.1 프론트엔드 배포
- **플랫폼:** GitHub Pages
- **CI/CD:** GitHub Actions
- **빌드 도구:** Vite

### 6.2 백엔드 배포
- **인프라:** AWS 서버리스
- **API Gateway:** REST API 엔드포인트
- **Lambda:** Node.js TypeScript 런타임
- **DynamoDB:** NoSQL 데이터베이스

## 7. 개발 계획

### 7.1 1단계: 기본 기능 (프론트엔드 전용)
- [ ] React 프로젝트 설정
- [ ] 기본 컴포넌트 구조
- [ ] Zustand 상태 관리
- [ ] localStorage 연동
- [ ] 기본 CRUD 기능
- [ ] 반응형 UI

### 7.2 2단계: UI/UX 개선
- [ ] 테마 기능 (라이트/다크 모드)
- [ ] 필터링 및 정렬
- [ ] 애니메이션 효과
- [ ] 접근성 개선

### 7.3 3단계: 백엔드 연동
- [ ] AWS 서버리스 설정
- [ ] API 엔드포인트 구현
- [ ] DynamoDB 연동
- [ ] 인증 기능 (Cognito)

## 8. 기술적 의사결정

### 8.1 선택한 기술 스택 이유
- **React:** 컴포넌트 기반 아키텍처, 생태계
- **Zustand:** 간단한 상태 관리, TypeScript 지원
- **Tailwind CSS:** 유틸리티 우선, 빠른 개발
- **Vite:** 빠른 빌드 속도, 현대적인 개발 경험
- **AWS 서버리스:** 확장성, 비용 효율성

### 8.2 대안 기술 고려사항
- **상태 관리:** Redux Toolkit 대신 Zustand 선택 (단순성)
- **UI 프레임워크:** Material-UI 대신 Tailwind CSS 선택 (유연성)
- **데이터베이스:** MongoDB 대신 DynamoDB 선택 (서버리스 통합)

이 설계 문서는 개발 과정에서 지속적으로 업데이트됩니다.


