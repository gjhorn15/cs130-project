Data Source(s)

The dataset was downloaded directly from CORGIS (The Collection of Really Great, Interesting, Situated datasets).

CSV file used:
https://corgis-edu.github.io/corgis/datasets/csv/video_games/video_games.csv

Contains information on video game titles, platforms, genres, publishers, sales, review scores, and release dates.

Data Preparation / Cleaning

Loaded the CSV file using pandas.read_csv().

Checked and confirmed column names, including:

Metadata.Genres, Metadata.Platform, Metrics.Sales,
Metrics.Review Score, Release.Year, etc.

Dropped missing values depending on the specific analysis:

For the Review Score vs Sales analysis:

Removed rows where:

Metrics.Sales was missing

Metrics.Review Score was missing

For the Yearly Release Trend analysis:

Converted Release.Year to numeric format

Dropped rows with missing or invalid years

Converted data types:

Ensured Metrics.Sales was numeric so correlations could be calculated.

Ensured Release.Year was an integer to plot counts accurately.

Flattened string-based genre entries:

Some games list multiple genres separated by commas.

Split each Metadata.Genres string into a list of individual genres.

Aggregated individual genre counts for the bar chart.

Grouped data using groupby for platform-level statistics:

Calculated averages for:

Metrics.Sales

Metrics.Review Score

Assumptions

Missing numeric values represent “unknown," not zero
→ They were dropped from correlation and trend analysis to avoid distortion.

Games with multiple genres contribute 1 count toward each genre
→ This assumes CORGIS treats genres independently rather than selecting a primary one.

Sales are assumed to be global lifetime sales, as the dataset does not specify region or timeframe.

Review scores are assumed to be on a consistent scale (0–10) even though CORGIS does not explicitly state scoring methodology.

Release years are assumed correct even if a game is released alongside a console launch, since the dataset may not track what month the game released.

Platforms listed as the same string are treated as identical
Example: "PlayStation 4" vs "PS4" do not appear in the dataset, but if they did, the analysis assumes they are the same.

Limitations

Dataset does not specify sales region
→ Could be global, U.S. only, or mixed reporting.

No metadata about review source
→ Review Score could come from critics, users, or an average.

Genre field is not standardized
→ Some entries contain combinations like "Action, Adventure"
→ Other entries use single genres like "Action"
→ This can cause inflation in genre counts.

Sales values include unclear units
→ Likely in millions of copies, but CORGIS does not confirm.

Release Year has missing or inconsistent values
→ Some entries had to be dropped to generate plots.

Correlation does not imply causation
→ A high Review Score vs Sales correlation does not mean reviews cause sales.

Platform analysis treats platforms equally, but:

Some platforms have far more games than others.

Some platforms span decades (e.g., PC), while others last only a few years.
