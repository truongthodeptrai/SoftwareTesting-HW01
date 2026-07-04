## Weekly report
- Group ID: 08
- Project Name: T8 Database Testing
- Date range: 2026/06/29-2026/07/04

## Task Completed This Week
Nguyễn Chí Đức - 23127172
- Task 1 - Deep study (about the tools our group using aka DbUnit, Tonic.ai and Database Rider) and hands-on practice

Nguyễn Phan Hùng Linh - 23127081
- Task 1 - Deep study (about the tools our group using aka DbUnit, Tonic.ai and Database Rider) and hands-on practice
- Task 2 - Run an end-to-end scenario in eshop (which is importing csv files on Admin)

Evidence:
- "Đức - Linh - Thọ: tìm hiểu 3 công cụ trên, luyện tập sử dụng và chạy 1 tình huống end-to-end trên eshop"

## AI Usage Declaration
In this week, our group uses AI tools for instructions of downloading and setting up DbUnit, Database Rider; creating databases by using Tonic.ai.
Not only that, AI tools are also used for corrections around the EShop test scenarios, suggesting formats of reports and writing small parts reports to make it look professional.

## Tasks planned for next week
- Continue on running scenarios on EShop
- Doing User-guide + demo recording

## Issues
- Linh:
One important issue was found during human review.

At first, the report described 3 bugs, but the Maven command appeared to pass:

```bash
mvn test
```

The human reviewer noticed that this was confusing and pointed out that the
bugs should be found by DbUnit and Database Rider style tests, not only by the
helper JavaScript files or written explanation.

After that review, the AI changed the Java EShop scenario test so that it
asserts the correct expected behavior:

- Invalid CSV rows should cause the whole import to rollback.
- Negative prices should not be saved.
- Normal users should not access admin import APIs.
- Tonic Fabricate data should be tested through the same Java scenario.

After the correction, the simple command:

```bash
mvn test
```

still passes because it only runs the hello-world tool installation tests.

The real EShop scenario command:

```bash
mvn test -q -Deshop.e2e=true \
  -Deshop.baseUrl=http://localhost:3000 \
  -Deshop.backendContainer=eshop-sut-backend-1 \
  -Dtest=EshopCsvImportScenarioTest
```

now fails while the EShop bugs still exist. This is the correct result for a
bug-finding test.

Another issue was that some early Tonic-related files were not needed anymore.
The human reviewer asked for unused files to be removed, so the report was
updated to focus on the final CSV data and the final screenshot evidence.

- Đức:

| Issue | Cause | Resolution |
| --- | --- | --- |
| `Non-parseable POM ... in epilog non whitespace content is not allowed` | Extra Markdown content was accidentally copied into `pom.xml` after `</project>` | Removed the extra content so `pom.xml` only contains valid Maven XML |
| Missing dataset file | `EshopDbUnitTest.java` expected `src/test/resources/datasets/initial-dataset.xml` | Created `initial-dataset.xml` |
| Maven could not write to `~/.m2/repository` in sandbox | Sandbox permission restriction | Re-ran Maven with approved elevated permission |
