# Database
- [SQL](#sql)

<br />

## SQL
- **SQL의 종류**
    - DDL : Data Definition Language `CREATE, DROP, ALTER`
        - 데이터 정의 언어
        - 데이터베이스, 테이블, 뷰, 인덱스 등의 데이터베이스 개체 생성/삭제/변경
        - DDL은 트랜잭션을 발생시키지 않습니다.
        - ROLLBACK, COMMIT 사용 불가능
    - DML : Data Manipulation Language `SELECT, INSERT, UPDATE, DELETE`
        - 데이터 조작 언어
        - 데이터를 조작(선택, 삽입, 수정, 삭제)
        - DML 구문이 사용되는 대상은 테이블의 행
        - 사용 전에 테이블이 정의되어 있어야 합니다.
        - 트랜잭션이 발생하는 SQL도 DML에 속합니다.
        - ❗데이터를 변경(입력/수정/삭제)할 때 실제 테이블에 완전히 적용하지 않고, 임시로 적용시키는 것
        - ❗취소 가능.
    - DCL : Data Control Language `GRANT, REVOKE`
        - 데이터 제어 언어
        - 사용자에게  권한을 부여하거나 빼앗을 때 사용.

<br />

❗**↓↓↓ SQL 명령어는 단순 개념 정리가 아닌 예시 위주의 복습 정리입니다.**

❗**↓↓↓ 질의의 마지막은 세미콜론(;)을 사용하며 하위 설명에선 편의상 생략될 수 있습니다.**
- **SQL 명령어**
    - SELECT
        - 요구하는 데이터를 가져옵니다. 
            ```sql
            SELECT  coulumn_name            -- SELECT DISTINCT는 중복 제거 출력
            FROM    table_references        
            WHERE   height > 150 AND Conuntry = 'KOREA'
               AND  price BETWEEN 1000 and 2000
               AND  Pet IN ('cat', 'dog')
            GROUP BY country_code       -- 데이터를 묶어줍니다. 상세내용 아래 기타.
            HAVING
            ORDER BY - city_population DESC    -- ASC 오름 차순(default), DESC 내림 차순
            LIMIT 10;       -- 결과에 대한 상위 10개만 출력
            ```
    - JOIN
        - 여러 테이블에서 가져온 레코드를 조합하여 하나의 테이블이나 결과 집합으로 출력합니다.
            ```sql
            SELECT *
            FROM city
            
            -- city와 country, country_language테이블을 ON 뒤의 조건에 맞게 합칩니다.
            JOIN country ON city.CountryCode = country.Code 
            JOIN country_language ON city.CountryCode = country_language.Code;
            ```
    
    - 기타
        - \* : 모든 데이터 
        - LIKE : 데이터의 부분 일치``
            ```sql
            SELECT *
            WHERE CountryCode LIKE 'KO_'
            ----------------------------
            LIKE '%TEL'     -- TEL로 시작하는 모든 데이터 
            LIKE 'TEL%'     -- TEL로 끝나는 모든 데이터
            LIKE '%TEL%'    -- TEL이 들어가는 모든 데이터
            ```
        - Sub Query
            ```sql
            SELECT *
            FROM city
            WHERE CountryCode = (   SELECT CountryCode      -- 동일하게 매핑
                                    FROM city
                                    WHERE city_name = 'Seoul'    )
            -- 하위 질의의 결과가 KOR 이라고 가정하면
            -- CountryCode가 KOR인 city의 데이터를 모두 보여줍니다.
            ---------------------------------------------------------------
            WHERE CountryCode > ANY ( Sub Query ) 
            -- 서브 쿼리에 해당하는 것에 1개라도 해당하면 출력합니다.
            -- ANY는 SOME과 같습니다.
            -- ALL은 서브 쿼리 출력의 모든 것(최대값)을 포함하는 데이터를 출력합니다.
            ```
        - GROUP BY
            ```sql
            AS를 사용하여 별칭 부여가 가능합니다. 효율적인 데이터 그룹화가 가능합니다.
            
            ❗집계 함수와 같이 사용. 
            AVG() - 평균, MIN() - 최소, MAX() - 최대, 
            COUNT() - 행의 개수, COUNT(DISTINCT) - 중복 제외된 행의 개수,
            STDEV() - 표준 편차, VARIANCE() - 분산
            
            SELECT CountryCode, MAX(city_population) AS 'Population'
            FROM city
            GROUP BY CountryCode                 -- HAVING으로 상세 조건 가능.
            HAVING MAX(city_population) > 1000;  -- 반드시 GROUP BY 다음에 나와야 합니다.
            
            SELECT CountryCode, city_name, SUM(city_population)
            FROM city
            GROUP BY CountryCode, city_name WITH ROLLUP; 
            -- WITH ROLLUP으로 중간 합계를 보여주는 행(들)을 추가합니다.
            ```
        - LENGTH - 문자열의 길이 반환
            ```sql
            SELECT LENGTH('Hello')      -- 5 반환
            ```
        - CONCAT - 문자열 결합
            ```sql
            SELECT CONCAT('He', 'llo'),         -- Hello 반환
                   CONCAT('H', NULL, 'ello')    -- 하나라도 NULL이면 NULL 반환
            ```
        - LOCATE - 문자열이 처음 등장하는 위치 반환, 인덱스는 1부터, 존재하지 않으면 0 반환.
            ```sql
            SELECT LOCATE('abc', 'aaabc'),      -- 3 반환
                   LOCATE('abc', 'abab')        -- 0 반환
            ```
        - LEFT, RIGHT - 한 방향에서 지정된 개수만큼의 문자 반환
            ```sql
            SELECT LEFT('abcdefg', 2),          -- ab 반환
                   RIGHT('abcdefg', 2)          -- fg 반환
            ```
        - UPPER(), LOWER() - 대, 소문자로 변환
            ```sql
            SELECT UPPER('aBc'),                -- ABC 반환
                   LOWER('aBc')                 -- abc 반환
            ```
        - REPLACE
            ```sql
            SELECT REPLACE('MSSQL', 'MS', 'My') -- MySQL 반환
            ```
        - TRIM
            ```sql
            
            ```
        