# Group project

*Data Wrangling through Analytics with Python* · ESMT Berlin, MAAI 2027

The group project is worth 30% of the module grade. It has three parts.

| part | weight | when |
|---|---|---|
| Checkpoint | 5% | due Monday 16 November at 09:00 |

| Presentation | 10% | in class on Thursday 19 November |
| Code | 15% | due Friday 20 November at 18:00 |

## The task

In class we have been getting Kiezkaffee's data into shape, one source at a time. In the project you'll do the same with data of your own.

In your group, choose a question that you would like to answer with data. Find at least three sources that you need to answer it. Then
write the code that downloads them, cleans them and combines them into one table. Check that table before you use it to answer your
question.

Most of the marks are for how you get, clean, combine and check the data. The analysis at the end can be simple, and one good chart with a
clear sentence is enough.

Friday's class covers APIs, and Tuesday's class covers combining and checking tables. You can start now by choosing your question and
looking at sources.

## Your sources

[`SOURCES.md`](SOURCES.md) has a list of sources that work well for the project. You can also use sources of your own.

Whatever you choose, your sources need to meet these requirements.

- You need at least three sources, and they must come from at least two different organisations.
- At least one source must be an API where you need parameters, pages or a key. At least one source must be something else, such as a
  file to download or a table on a web page.
- Your code should download every source itself. If a source can only be downloaded by hand, you may include one such file. Put it in
  `data/raw/` and say in your README where and when you downloaded it.
- Respect the sites you take data from. Send a `User-Agent` that says who you are, and read a site's `robots.txt` and terms of use
  before you take data from its pages. Save what you download so that you only ask for it once.
- Never commit an API key to your repository.
- Don't use personal data about people who could be identified, such as profiles, reviews with names or social media accounts.
  Aggregated figures are fine.
- Keep your raw data under about 100 MB. The whole project should run in under 15 minutes in a Codespace when nothing has been
  downloaded yet.
- Don't use Kiezkaffee's data. Don't build your project around a dataset that has already been cleaned for you, such as a Kaggle file.

## Checkpoint (5%)

The checkpoint is due on Monday 16 November at 09:00. It is a short proposal. Push these two files to your group's repository.

- `PROPOSAL.md`, filled in with your question, your sources and how you plan to join them.
- `notebooks/00_first_look.ipynb`, with code that gets a first sample from each source and shows it. It doesn't need to be clean yet.

The assessment includes the following.

- The question is clear and can be answered from the data.
- The sources fit the question and meet the requirements above.
- The proposal says how the sources will be joined.
- The first-look notebook gets a sample from every source.

## Presentation (10%)

The presentations are in class on Thursday 19 November. Each group has 10 minutes to present, followed by 5 minutes of questions, and
everyone in the group should speak. Your presentation should cover the following.

1. Your question, and why it matters.
2. Your sources and how you got and combined them, shown in one diagram.
3. The hardest data problem you met and how you solved it. Show the data before and after.
4. How you checked your final table, and what you found.
5. Your answer, as one chart and one sentence.

The assessment includes these five things, timekeeping and how you answer questions.

## Code (15%)

The code is due on Friday 20 November at 18:00. Your repository will be marked as it is at the deadline. It will be opened in a
fresh Codespace, and its notebooks will be run in order.

The assessment includes the following.

- The notebooks run in order from start to finish when nothing has been downloaded yet.
- Every source is downloaded by code, through a session with retries and a timeout. Each download is recorded in a download log.
- The raw data is left untouched. Each source is cleaned into a table with clear column names and the right types and units, and the
  changes are recorded in the cleaning log.
- The sources are combined on keys that have been checked, and every merge uses `validate=`.
- The final table is checked with rules written in code, and any corrections are recorded with reasons.
- The result is saved as Parquet or SQLite, and a data dictionary describes its columns.
- The README gives the question and the answer.

## Working in your group

Each group has one repository, which is created when you accept the group assignment. Everyone in the group should commit to it, and the
commit history will be checked. Everyone should also be able to explain all of the project at the presentation.

Use AI tools responsibly, acknowledging use as per ESMT guidelines.

Post questions on the Canvas discussion board, or ask in the breaks.

### Collaborating with Git

- Commit often. Each commit in the Codespace goes to GitHub straight away.
- Commit your work before you stop for the day.
- If a sync shows a conflict, open the file. Fix the cell and delete the lines of `<<<<<<<`, `=======` and `>>>>>>>`. Then press `+`
  beside the file in the Source Control panel and click the green Continue button.
