# Security News Collector
보안관제 업무 중 매일 수동으로 확인하던 보안 뉴스를
자동으로 수집하여 엑셀로 정리해주는 도구입니다.

## 왜 만들었는가

보안관제 업무를 하면서 매일 아침 보안 뉴스를 수동으로
확인하는 작업이 반복됐습니다. DDoS, 해킹, 랜섬웨어 등
키워드별로 최신 동향을 파악하는 게 중요한데,
이를 매번 직접 검색하는 건 비효율적이라고 느꼈습니다.

직접 Python으로 자동화 도구를 만들어 해결했습니다.

## 개선 과정

### v1 - 네이버 뉴스 크롤링 (naver_news_crawler.py)
처음에는 Selenium으로 네이버 뉴스를 직접 크롤링하는
방식으로 구현했습니다.

**한계:**
- 네이버 뉴스 HTML 구조 변경 시마다 코드 수정 필요
- 반복적인 크롤링은 보안 정책 위배 가능성 인식
- 유지보수 비용이 지속적으로 발생

### v2 - Google News RSS 활용 (google_news_rss.py)
크롤링 방식의 한계를 인식하고 Google News RSS로 전환했습니다.

**개선점:**
- 공식 RSS 피드를 활용해 보안 정책 이슈 해소
- HTML 구조 변경에 영향받지 않아 유지보수 부담 제거
- 주요 언론사(조선, 중앙, 동아) 필터링 기능 추가
- 한국 시간(KST) 변환 및 시간순 정렬 자동화

## 주요 기능

- 키워드 설정: 기본값(해킹, DDoS, 개인정보) 또는 직접 입력
- 기간 설정: n시간 이내 또는 n일 이내
- 결과 출력: 엑셀 파일로 자동 저장
  - 전체 뉴스 시트
  - 주요 언론사 필터링 시트 (별도 탭)
- 하이퍼링크 자동 삽입으로 원문 바로 접근 가능

## 기술 스택

- Python 3.x
- feedparser: RSS 피드 수집
- BeautifulSoup4 / Selenium: 크롤링 (v1)
- pandas / openpyxl: 엑셀 출력
- pytz: 시간대 변환

## 실행 방법

## 패키지 설치
pip install feedparser pandas openpyxl pytz beautifulsoup4 selenium

## Google RSS 버전 실행 (권장)
python google_news_rss.py

## 실행 후 키워드와 기간을 입력하면 result.xlsx 생성

## 개선 예정 사항

- 스케줄링 적용: 3시간 단위 자동 실행 (cron)
- 이메일 알림 연동
- 키워드 위험도 분류 자동화
