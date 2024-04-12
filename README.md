#  젤다 왕눈 사당 공략 챗봇 [전체 PPT 보기](https://www.canva.com/design/DAF8EBkzvo8/fcg11cMhcLjIM5PuifXmIg/edit)

### 01. 한국 게임 산업 매출 추이: 최근 10년 동안 꾸준히 증가
<img width="435" alt="Screenshot 2024-04-12 at 2 06 04 PM" src="https://github.com/jiapn123/zelda-guide-gpt/assets/155503641/7f7c8547-7a8c-447a-9035-de208ea59801">

### 02. 데이터 크롤링([ZELDA DUNGEON](https://www.zeldadungeon.net/wiki/Category:Tears_of_the_Kingdom_Sky_Shrines))
Output:
- langchain_doc.csv (사당별 공략 본문)
- sql_db.csv (사당별 상세정보: 위치/적/아이템/재료/선행 조건/보상/유형/기술/주민/관련내용/깊이/대응물/Y 좌표/퀘스트)

### 03. Langchain React Agent 3까지 도구 기능 구현
- csv retrieval : 공략 가이드
- SQL chain: 위치,좌표,동영상 가이드등 검색
- search API: 사당외 게임 정보 제공 
<img width="629" alt="Screenshot 2024-04-12 at 2 18 49 PM" src="https://github.com/jiapn123/zelda-guide-gpt/assets/155503641/153a6596-692e-4bd9-9644-925046c0a349">


```python
tools = [
    Tool(
        name="zelda shiren guidebook",
        func=zelda_guide.invoke,
        description="useful for answering questions about a guide to unlocking a Shiren in Zelda Tears of the Kingdom game. Input should be a fully formed question."
    ),
    Tool(
        name="summary table",
        func=db_chain.run,
        description="""useful for when you need to grab the user-requested information of a Shiren. 
        The database has 16 columns, including the information of coordinators, youtube_link, Location, Enemies, Items, Materials, Prerequisite, Rewards, Type, Skills, Inhabitants, Related, Depths Counterpart, Coordinates_y and Quests about a Shiren.
        If any of the words mentioned in the user input, please make sure to search in the database first
        """),
    Tool(
        name="search",
        func=search.invoke,
        description="useful for when you need to answer other questions about the Zelda Tears of the Kingdom game rather than a shiren-related question"
    )
]
```

### 04.결과 평가
<img width="1001" alt="Screenshot 2024-04-12 at 2 38 25 PM" src="https://github.com/jiapn123/zelda-guide-gpt/assets/155503641/1fc2bbc2-dca9-4c78-9cd4-48ce05378933">


