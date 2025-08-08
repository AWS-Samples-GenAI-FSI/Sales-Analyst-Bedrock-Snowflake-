# GenAI Sales Analyst
*(Powered by Amazon Bedrock and Snowflake)*

A Streamlit application that uses Amazon Bedrock, LangGraph, and FAISS to analyze sales data using natural language queries.

## Features

- Natural language to SQL query conversion using Amazon Bedrock
- LangGraph workflow for structured analysis
- FAISS vector store for semantic search
- LangFuse monitoring integration
- Structured workflow with error handling
- Persistent metadata caching

## Project Structure

```
genai-sales-analyst/
├── .gitignore
├── README.md
├── app.py                    # Main Streamlit app
├── setup.py                  # Setup script
├── requirements.txt
└── src/
    ├── __init__.py
    ├── prompts/              # Prompt management
    │   ├── __init__.py
    │   ├── prompt_template.py
    │   └── prompts.yaml      # Structured prompts
    ├── graph/                # LangGraph components
    │   ├── __init__.py
    │   └── workflow.py       # Workflow definitions
    ├── vector_store/         # FAISS integration
    │   ├── __init__.py
    │   └── faiss_manager.py
    ├── monitoring/           # Monitoring integration
    │   ├── __init__.py
    │   └── langfuse_monitor.py
    ├── bedrock/              # Amazon Bedrock integration
    │   ├── __init__.py
    │   └── bedrock_helper.py
    └── utils/                # Utility functions
        ├── __init__.py
        ├── helpers.py
        ├── setup_utils.py
        └── snowflake_connector.py
```

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/AWS-Samples-GenAI-FSI/genai-sales-analyst.git
   cd genai-sales-analyst
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Update credentials** in `src/utils/snowflake_connector.py`
   ```python
   user = "<insert username here>"
   password = "<insert password here>"
   account = "<insert account identifier here>"
   ```

## Usage

### 1. Setup Credentials
Update your credentials in `src/utils/snowflake_connector.py`:
```python
user = "your_username"
password = "your_password" 
account = "your_account_identifier"
warehouse = "your_warehouse"
role = "your_role"
```

### 2. Configure AWS (Optional)
Set up AWS credentials for Bedrock access:
```bash
aws configure
# OR set environment variables
export AWS_ACCESS_KEY_ID=your_key
export AWS_SECRET_ACCESS_KEY=your_secret
export AWS_REGION=us-east-1
```

### 3. Run the Application
```bash
streamlit run app.py
```

### 4. Automatic Database Setup
On first run, the app will automatically:
- ✅ Connect to your Snowflake account
- 🔄 Check if Northwind sample database exists
- 📥 Download Northwind sample data if needed
- 🏗️ Create `SALES_ANALYST` database and `NORTHWIND` schema
- 📊 Load complete sample dataset (8 tables with sales data)
- 🚀 Ready to query!

### 5. Ask Questions
Use natural language to query your data:

**Example Questions:**
- "What are the top 5 customers by order value?"
- "Show me the schema of the CUSTOMERS table"
- "Count the number of orders by country"
- "What's the distribution of order priorities?"
- "What's the average order value by customer?"
- "Which products are most popular?"

### 6. View Results
The app provides:
- 🤖 **AI-generated SQL** queries
- 📋 **Query results** in table format
- 📈 **Analysis and insights** from the data
- 🔄 **Workflow steps** showing the AI reasoning process
- 📚 **Query history** for reference

### 7. Database Structure
After setup, you'll have access to:
- **CUSTOMERS** - Customer information
- **ORDERS** - Order headers
- **ORDER_DETAILS** - Order line items
- **PRODUCTS** - Product catalog
- **CATEGORIES** - Product categories
- **SUPPLIERS** - Supplier information
- **EMPLOYEES** - Employee data
- **SHIPPERS** - Shipping companies

## How It Works

### AI-Powered Workflow
The application uses **LangGraph** and **Amazon Bedrock** to create an intelligent analysis workflow:

1. 🧠 **Understand Query**: AI analyzes your natural language question
2. 🔍 **Retrieve Context**: Finds relevant table/column metadata using FAISS vector search
3. 💻 **Generate SQL**: Creates optimized SQL query using context
4. ⚡ **Execute Query**: Runs SQL against your Snowflake database
5. 📊 **Analyze Results**: Provides business insights and explanations

### Key Features
- **Natural Language to SQL**: No SQL knowledge required
- **Intelligent Context**: Understands your database schema automatically
- **Error Recovery**: Handles and recovers from query errors
- **Performance Monitoring**: Tracks AI interactions with LangFuse
- **Persistent Caching**: Speeds up repeated queries

## Monitoring (Optional)

**LangFuse Integration** provides:
- 📊 AI interaction tracking
- 🔄 Workflow step monitoring  
- 🚨 Error logging and analysis
- ⚡ Performance metrics

To enable, update your credentials in the connector file or set environment variables.