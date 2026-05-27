========================================================================
                          STOCKSTORY PROJECT
========================================================================

StockStory is an end-to-end financial data engineering and visualization 
application. It parses raw stock market historical CSV files using a custom 
ANTLR4 translator, processes the data into semantic financial "stories" 
using Python/Pandas, and visualizes market trends, trading signals, and 
portfolio risk metrics via a Streamlit web application.

------------------------------------------------------------------------
1. PROJECT ARCHITECTURE & FILE STRUCTURE
------------------------------------------------------------------------

StockStory/
│
├── Stock.g4              # ANTLR4 Grammar file defining lexer & parser rules
├── Main.java             # Java driver: Runs ANTLR parser, outputs records.json
│
├── main.py               # CLI entry point to trigger Python semantic processing
├── app.py                # Streamlit Web App dashboard entry point
│
├── src/
│   └── DataProcessor.py  # Pandas engine: Calculates SMA crossover, returns, 
│                         # risk/volatility, and normalized performance
├── ChartBuilder.py       # Plotly visualization components for the frontend
└── requirements.txt      # Python dependencies (Pandas, Plotly, Streamlit)

------------------------------------------------------------------------
2. PIPELINE WORKFLOW & EXECUTION
------------------------------------------------------------------------

STAGE 1: Parsing & Translation (Java + ANTLR4)
  1. Compile the ANTLR grammar:
     antlr4 Stock.g4 -javac-compile
  2. Compile and run the Java driver to convert a stock CSV to JSON:
     javac Main.java
     java Main <path_to_input.csv> <path_to_output.json>
     (e.g., java Main AAPL.csv AAPL_records.json)

STAGE 2: Semantic Data Engineering (Python + Pandas)
  1. Install dependencies:
     pip install -r requirements.txt
  2. Process the raw JSON records into financial metrics (Saved as CSV):
     python main.py <path_to_json_file> [output_directory]
     (e.g., python main.py AAPL_records.json outputs)

STAGE 3: Dashboard Visualization (Streamlit + Plotly)
  1. Launch the interactive web server:
     streamlit run app.py
  2. Features: Candle stick price actions, SMA 20/50 trend crossovers, 
     rolling volatility risk assessments, and multi-ticker asset comparisons.

------------------------------------------------------------------------
3. FINANCIAL STORIES METRICS IMPLEMENTED
------------------------------------------------------------------------
* Trend Following: 20-Day vs 50-Day Simple Moving Average (SMA) crossovers.
* Risk Assessment: Day-over-day percentage returns and 20-day rolling 
  standard deviation (volatility).
* Relative Performance: Baseline index normalization to 100 for historical 
  asset comparison.
========================================================================
