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
        - 사용자의 권한을 부여하거나 빼앗을 때 사용.

<br />

❗**↓↓↓ SQL 명령어는 단순 개념 정리가 아닌 예시 위주의 복습 정리입니다.**

❗**↓↓↓ 질의의 마지막은 세미콜론(;)을 사용하며 하위 설명에선 편의상 제외합니다.**
- **SQL 명령어**
    - SELECT
        - 요구하는 데이터를 가져옵니다. 
            ```sql
            SELECT  coulumn_name            -- SELECT DISTINCT는 중복 제거 출력
            FROM    table_references        
            WHERE   height > 150 AND Conuntry = 'KOREA'
               AND  Money BETWEEN 1000 and 2000
               AND  Pet IN ('cat', 'dog')
            GROUP BY
            HAVING
            ORDER BY - city_population DESC    -- ASC 오름 차순(default), DESC 내림 차순
            LIMIT 10       -- 결과에 대한 상위 10개만 출력
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